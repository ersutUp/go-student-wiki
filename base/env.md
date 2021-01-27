# Go环境变量

Go开发环境依赖部分系统的环境变量，这些变量需要手动设置，在安装Go之前需要先设置好他们。如果是windows系统使用msi安装文件安装可以省去环境变量的配置，因为他已经自动配置了部分环境变量。

## $GOROOT(必须手动配置)
表示Go的安装位置，windows的mis文件安装默认位置为 C:/GO；linux中可安装到 /usr/local/go

## $GOPATH(必须手动配置)
依赖库的存储位置（默认位置是$HOME/go）,例如：引用web框架 beego 库，则将其检出到 $GOPATH/src/github.com/beego/beego/v2@v2.0.0,如果使用了模块化则是 $GOPATH/pkg/mod 中。

Go模块化问世前人们在开发时需要将项目的根目录配置到 $GOPATH 中,多个路径使用 ';' 隔开

### $GOPATH目录的结构
- $GOPATH/bin	:编译后生成的可执行文件,为了执行方便可将整个目录添加至 $PATH 环境变量中
- $GOPATH/pkg	:包文件（**这块还不太明白**）
- $GOPATH/src	:存放源代码

## $GOBIN（一般使用默认值）
依赖库或者项目的可执行文件存放目录，默认值为 $GOPATH/bin,如果$GOPATH未设置那么默认值为$HOME/go/bin

示例: 

- go install 后会生成可执行文件会放在 $GOBIN 目录下
- go get xxxx 
	- 从远程下载需要用到的包
	- 执行 go install

## $GOOS 和 $GOARCH（交叉编译时临时使用）
$GOOS为目标机器的操作系统

$GOARCH为目标机器的处理器架构

$GOOS和$GOARCH的有效组合有：

|$GOOS|$GOARCH|
|:-:|:-:|
|aix|ppc64|
|android|386|
|android|amd64|
|android|arm|
|android|arm64|
|darwin|amd64|
|darwin|arm64|
|dragonfly|amd64|
|freebsd|386|
|freebsd|amd64|
|freebsd|arm|
|illumos|amd64|
|js|wasm|
|linux|386|
|linux|amd64|
|linux|arm|
|linux|arm64|
|linux|ppc64|
|linux|ppc64le|
|linux|mips|
|linux|mipsle|
|linux|mips64|
|linux|mips64le|
|linux|riscv64|
|linux|s390x|
|netbsd|386|
|netbsd|amd64|
|netbsd|arm|
|openbsd|386|
|openbsd|amd64|
|openbsd|arm|
|openbsd|arm64|
|plan9|386|
|plan9|amd64|
|plan9|arm|
|solaris|amd64|
|windows|386|
|windows|amd64|

## $GOHOSTOS 和 $GOHOSTARCH（一般使用默认值）
$GOHOSTOS为本地机器的操作系统

$GOHOSTARCH为本地机器的处理器架构

$GOHOSTOS和$GOHOSTARCH的有效组合与$GOOS和$GOARCH一致,设置的值必须与本地系统兼容。

## 交叉编译
在一个平台上就能生成可以在另一个平台运行的二进制程序，例如，我们可以64位的Windows操作系统开发环境上，生成可以在64位Linux操作系统上运行的二进制程序。

示例：假设当前平台为64位的windows操作系统生成64位Linux操作系统上运行的二进制程序,命令如下
```
set GOOS=linux
set GOARCH=arm64
go build
```
### 交叉编译时处理器架构的特殊相关环境变量
- $GO386：适用于386架构
- $GOARM：适用于arm架构
- $GOMIPS：适用于mips和mipsle架构
- $GOMIPS64：适用于mips和mipsle架构
- $GOPPC64：适用于pcc64和pcc64le架构
- $GOWASM：适用于wasm架构

## Go环境变量相关命令
```
//查看Go所有的环境变量
go env
//查看Go某个环境变量的值
go env GOOS
//修改Go环境变量的值
go env -w GOPROXY=https://goproxy.io,direct
```