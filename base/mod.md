# Go Modules
在 Go Modules 出现前项目开发需要依赖 $GOPATH 来解决库依赖的问题。在 Go Modules 后摆脱掉 $GOPATH ,并且更清晰的来管理库依赖。

# go mod 命令
用法:

        go mod <command> [arguments]

可选的 command 值:

        init        //把当前目录初始化为 Modules
        download    //下载依赖库到本地目录（$GOPATH/pkg/mod）
        vendor      //将所需的依赖库从 $GOPATH/pkg/mod/ 下复制到 项目根目录/vendor/ 下。使用 vendor 后所有依赖库必须放在这个文件夹中不会去再查找 $GOPATH/pkg/mod 目录，所以不推荐
        tidy        //移除未使用的依赖库并下载缺失的依赖库

# 创建 Modules 项目(ersut.top/test)
创建一个空文件夹,在这个文件夹下执行 `go mod init ersut.top/test`,执行后会生成 go.mod 文件，具体内容：
```
module ersut.top/test

go 1.15
```

# go.mod 文件支持的语句
### module
`module ersut.top/test`
指定包的名字，引用时则是 ersut.top/test/xxx
### require
```
require (
	github.com/sirupsen/logrus v1.4.2
)
```
指定依赖库,每次添加新的依赖库后需在项目目录下执行`go mod download`或`go mod tidy`来获取依赖库的源码
### exclude
忽略依赖库，还未涉及到
### replace
替换依赖库，还未涉及到