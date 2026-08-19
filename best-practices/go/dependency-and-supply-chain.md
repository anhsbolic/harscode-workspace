# dependency-and-supply-chain.md

**Location:** `go/dependency-and-supply-chain.md`

**Principle**
Without automated CI/CD dependency scanning, this discipline has to be manual and consistent: run a vulnerability scanner (`govulncheck` or equivalent) before any commit that adds or changes a dependency, verify module integrity (`go mod verify`), pin dependency versions explicitly, and review the changelog/source before adding a new package — especially one with access to the filesystem, network, or sensitive data.

**Bad**
```bash
go get github.com/some/package@latest   # no review, no explicit version pin
git commit -am "add package"            # no vulnerability scan before commit
```

**Good**
```bash
govulncheck ./...                        # before any commit that changes dependencies
go get github.com/some/package@v1.2.3    # explicit version, not @latest
go mod verify
# review the new package's changelog/source, especially if it needs network/filesystem access
git commit -am "add package v1.2.3, govulncheck clean"
```

**Checklist**
- [ ] `govulncheck` (or equivalent) runs before any commit that changes a dependency
- [ ] Dependency versions are pinned explicitly, not floating/`@latest`
- [ ] New packages are reviewed at the source before being added, especially ones needing sensitive access
- [ ] `go mod verify` runs periodically, not just once during initial setup