在[kne-union](https://github.com/kne-union)中会托管npm包发布密钥，微信小程序token获取密钥，微信小程序发布密钥，你不需要获取这些也可以通过github
action任务完成对应操作。

我们需要你遵循以下规范，以确保你的代码能合进kne-union中：

1. 你需要将需要修改的kne-union中的项目fork到你自己的repositories中
2. 创建你自己名字和修改功能名称(也可以没有)的分支
3. 完成并提交代码修改，执行rebase最新的origin/release
4. 使用force push推送到github远程分支
5. 发起create pull request 使用merge pull request方式(默认方式)合并到kne-union对应项目的release分支上
6. kne-union管理员会在审核你提交的代码，进行必要的测试后执行合并操作
7. kne-union管理员会在一段时间内将release分支合并到master上，然后触发对应的publish action
8. 更新[ued-manifest](https://github.com/kne-union/ued-manifest)将变更发布到ued中

* 对于一个项目正处于开发阶段，代码审核将不会特别严格，以确保开发效率
* 当项目处于维护期，任何变更都需要慎重考虑兼容性。如果不得不进行破坏式更新，请确保你的项目版本号符合[语义化版本号](https://semver.org/lang/zh-CN/)规则，这非常重要。
