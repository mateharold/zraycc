
### Windows (PowerShell)

```powershell
$env:CGO_ENABLED=0
go build -o xray.exe -trimpath -buildvcs=false -ldflags="-s -w -buildid=" -v ./main
```

### Linux / macOS

```bash
CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -ldflags="-s -w -buildid=" -v ./main
```

### Reproducible Releases

Make sure that you are using the same Go version, and remember to set the git commit id (7 bytes):

```bash
CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid=" -v ./main
```

For Android:

```bash
GOOS=android GOARCH=arm64 CGO_ENABLED=1 CC=/path/to/aarch64-linux-android24-clang go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid= -checklinkname=0" -v ./main
GOOS=android GOARCH=amd64 CGO_ENABLED=1 CC=/path/to/x86_64-linux-android24-clang go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid= -checklinkname=0" -v ./main
```
