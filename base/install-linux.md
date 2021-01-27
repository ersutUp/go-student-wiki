# linux下安装GO环境
示例环境：centos7
Go版本：1.15.7
## 环境变量配置

1. 设置永久变量修改`/etc/profile`文件
2. 配置GO的根目录为`/usr/local/go`
```
echo 'GOROOT=/usr/local/go' >> /etc/profile
```
3. 配置GO的依赖库目录为`$HOME/go`
```
echo 'GOPATH=$HOME/go' >> /etc/profile
```
4. 配置go相关命令在全局都可用
```
echo 'PATH=$PATH:$GOROOT/bin' >> /etc/profile
```
5. 刷新环境变量 `source /etc/profile`

## 安装C相关工具
因为Go是使用C编写的所以安装前需要C相关工具的支持，可以使用以下命令
```
yum install -y bison ed gawk gcc libc6-dev make
```

## $GOROOT_BOOTSTRAP(安装1.14以下版本可忽略此步骤)
由于Go版本大于 `1.14` 所以需要配置 $GOROOT_BOOTSTRAP
```
//安装git
yum install -y git
//克隆源码到本地
git clone --depth=1 https://github.com/golang/go.git $HOME/go1.14
//切换到1.14分支
git checkout -b release-branch.go1.14 origin/release-branch.go1.14
//编译安装
cd $HOME/go1.14/src && ./make.bash
//配置临时变量
export GOROOT_BOOTSTRAP=$HOME/go1.14
```

## 下载安装包并解压
```
//创建根目录
mkdir -p $GOROOT && cd $GOROOT
//下载安装包
curl -O https://dl.google.com/go/go1.15.7.linux-amd64.tar.gz
//解压
tar -zxvf go1.15.7.linux-amd64.tar.gz -C `cd $GOROOT && cd .. && pwd`
```

##编译安装
```
cd $GOROOT\src && ./all.bash
```

## 查看版本信息
```
go version
```
如果显示版本信息 `go version go1.15.7 linux/amd64` 说明安装成功