[中文](https://github.com/gvcgo/gobuilder/blob/main/docs/README_CN.md) | [En](https://github.com/gvcgo/gobuilder)
### What's gobuilder?

Gobuilder is a tool for building Go binaries. It is similar to the Go tool, but it supports building multiple binaries at once and supports custom build configurations without creating any script.

### Features

- Builds binaries for any platform from go source code.
- Cross-compilation for CGO using **xgo**. (optional)
- Packs binaries with **UPX**. (optional)
- Obfuscate binaries with **garble** for windows. (optional)
- Sign windows exe with **osslsigncode**. (optional)
- Zip binaries automatically.
- Builds binaries at anywhere in a go project.
- Remembers the build operations forever.
- No script is needed.
- Keep source code tidy. A dir named **build** is created, all the related files are restored in **build**. 

**Note**: You can install **upx** and **go compiler** using [VMR](https://github.com/gvcgo/version-manager). **osslsigncode** needs manuall compilation. **garble** and **xgo** can be installed using **go install xxx**.
**xgo docker image** is available at **ghcr.io/crazy-max/xgo** or **crazymax/xgo**.


### How to use?

- Install

```bash
go install github.com/gvcgo/gobuilder/cmd/gber@v0.1.5
```

- Usage

```bash
gber build <your-go-build-flags-and-args>
```

**Note**: If you need to inject variables when building go source code, "$" should be replaced with "#".
```bash
# original
gber build -ldflags "-X main.GitTag=$(git describe --abbrev=0 --tags) -X main.GitHash=$(git show -s --format=%H)  -s -w" ./cmd/vmr/

# replaced
gber build -ldflags "-X main.GitTag=#(git describe --abbrev=0 --tags) -X main.GitHash=#(git show -s --format=%H)  -s -w" ./cmd/vmr
```

### Dependencies

- [go compiler](https://go.dev/dl/) (required)
- [garble](https://github.com/burrowers/garble) (optional)
- [osslsigncode](https://github.com/mtrojnar/osslsigncode) (optional)
- [upx](https://github.com/upx/upx) (optional)
- [xgo](https://github.com/crazy-max/xgo) (optional)
