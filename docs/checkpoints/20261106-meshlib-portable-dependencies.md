# meshlib 构建依赖可移植性 checkpoint

范围：仅删除此前本地联调加入的八条工作区绝对路径 replace。没有修改 Go 产品源码、require 版本或 go.sum，没有增加功能或调整性能参数。

远端源码起点 `6e736f6767e7c8a993aedf103163d70021f03cc7`，本地依赖适配起点 `aadd74ce0877cdefe2d3d5edfdfe6753d52e791c`，当前分支 `test/meshlib-local-integration-20261105`，继续在本仓库已有 worktree 修改。

该模块是本次相关 Go 模块的依赖底层，直接依赖中没有其他六仓库模块，因此不需要保留相关远端 replace。上层引用本仓库时，仍需按用户确认的方案使用指向 `github.com/junliurs/cloudwego-gopkg` 固定提交版本的远端映射，保持既有 `github.com/cloudwego/gopkg` import 路径。

验证：Go 1.26.1，GOWORK=off、mod=readonly，`go build -p=8 ./...` 和 `go test -p=8 -vet=off -exec=/bin/true ./...` 通过。后者仅验证测试代码链接，没有执行测试。GOGC=100，不设 GOMEMLIMIT/GODEBUG；临时文件和构建缓存均位于用户工作空间。

当前环境向 GitHub fork 的 HTTPS/SSH dry-run 均未取得写权限，已告知用户配置凭证；没有实际 push。需先推送本提交并取得可获取的模块版本，再逐层固定上层依赖，不能把本地提交可用写成其他机器已经可以下载。本次只提交本模块依赖清理和此 checkpoint。
