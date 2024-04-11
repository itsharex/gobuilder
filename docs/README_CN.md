### 何为gobuilder？

gobuilder是一个用于编译go项目的工具。它功能上与go build类似，但是做了增强。能够同时编译到不同平台和架构，也不需要单独写脚本。

### 功能特点

- 同时编译到go build支持的任何一个或者多个平台；
- 使用UPX对binary进行压缩(可选)；
- 自动对binary进行zip压缩打包(可选)；
- 在go项目下的任何文件夹中，都可以一键编译该项目；
- 记住编译参数，后续任何时间再编译时，无需要输入任何参数；
- 无需编写任何脚本；

### 如何使用？

- 安装

```bash
go install github.com/gvcgo/gobuilder/cmd/gber@latest
```

- 使用方法

```bash
gber build <your-go-build-flags-and-args>
```

**注意**: 如果你需要在编译时动态地注入一些变量，也许你需要将"$"符号替换为"#"符号，以此避免$()中的命令立即执行，gber会自动识别这类替换。例如：

```bash
# original
gber build -ldflags "-X main.GitTag=$(git describe --abbrev=0 --tags) -X main.GitHash=$(git show -s --format=%H)  -s -w" ./cmd/vmr/

# replaced
gber build -ldflags "-X main.GitTag=#(git describe --abbrev=0 --tags) -X main.GitHash=#(git show -s --format=%H)  -s -w" ./cmd/vmr
```