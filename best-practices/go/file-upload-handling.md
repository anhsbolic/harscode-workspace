# file-upload-handling.md

**Location:** `go/file-upload-handling.md`

**Principle**
The client-supplied `Content-Type` header must not be trusted as-is to determine file type — a client can send any header regardless of the file's actual content. File type validation must sniff the file's magic bytes. Cap multipart form size at the server before the body is fully read, and stream large files to their destination storage (rather than buffering the whole thing into memory) to avoid resource exhaustion from large uploads.

**Bad**
```go
file, header, _ := r.FormFile("upload")
if header.Header.Get("Content-Type") != "image/png" {
    return errors.New("invalid file type") // trusts the client header as-is
}
data, _ := io.ReadAll(file) // entire file buffered into memory
uploadToStorage(data)
```

**Good**
```go
r.Body = http.MaxBytesReader(w, r.Body, maxUploadSize) // server-side size cap
file, _, err := r.FormFile("upload")
if err != nil { return err }
defer file.Close()

buf := make([]byte, 512)
n, _ := file.Read(buf)
contentType := http.DetectContentType(buf[:n]) // magic-byte sniff, not the header
if !allowedTypes[contentType] {
    return errors.New("invalid file type")
}
file.Seek(0, io.SeekStart)
streamToStorage(file) // streaming, not a full ReadAll
```

**Checklist**
- [ ] File type is validated from magic bytes (`http.DetectContentType` or equivalent), not the raw `Content-Type` header
- [ ] Maximum upload size is capped before the body is fully read (`MaxBytesReader` or equivalent)
- [ ] Large files are streamed to destination storage, not fully buffered into memory
- [ ] The resulting stored filename is sanitized/regenerated, not taken directly from the client-supplied name as a path