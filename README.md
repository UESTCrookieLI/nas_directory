# NAS 入门指南

以下用 NAS:/ 表示 NAS 的根目录，GPU:/ 表示各显卡服务器的根目录。

## 管理

用户组：administrators, managers, members，每人拥有一个账户，可能属于 members 用户组或同时属于 members, managers 用户组
* administrators: NAS 管理员（[NAS 管理员说明](documents/nas/README_admin.md)），为 NAS 本地用户
* managers: Public、github 仓库管理员（[managers 管理员说明](documents/nas/README_managers.md)）
* members: 普通用户
    * 允许：
        * 访问部分 NAS 应用，如 Download Station（[NAS 使用说明-访问-管理页面](documents/nas/README.md/#访问)）
        * 以只读权限访问 NAS:/Public 文件夹
        * 将 NAS 文件夹挂载到个人电脑（[NAS 使用说明-访问-挂载](documents/nas/README.md/#访问)）
    * 负责：向 github 仓库发起 pull request，贡献公共数据集和说明（[贡献](#贡献)）
    * 权限：
        * 对个人文件夹 NAS:/homes/{user_name} 的读写权限，但有容量限制
        * 显卡服务器上所有命令的 sudo 权限（暂定）

用户：在 NAS 和各显卡服务器上是通用的，administrators 用户组之外的用户密码会在各服务器之间同步，{user_name} 按以下规则命名
* members, managers: 姓名拼音命名，如 chencai, zhengzinan, zhangcheng
* administrators: 在 members 命名规则上添加 _admin 后缀。包括默认的 admin 用户（拥有最高权限）以及其他 NAS 管理员用户。

认证：
* administrators 为 NAS 本地用户组，只能在 NAS 上登陆
* managers, members 为集中认证用户组，可以在 NAS 和 显卡服务器上登陆


## 目录结构

NAS 私有文件夹 NAS:/homes/{user_name}，称为各用户的 home 文件夹：
* 存放个人的代码、数据集、软件等
* 只有 members 用户组的成员拥有，仅拥有者有读写权限
* members 和 managers 用户组的成员对 NAS:/homes 目录和他人的 home 文件夹有只读权限
* NAS:/homes 挂载到 GPU:/home 路径下，各用户可以将 anaconda 等软件安装于 home，使其在各显卡服务器间共享
* 各用户的存储空间有配额，可通过贡献或使用共享数据集避免个人配额的占用

NAS 共享文件夹 NAS:/Public，对 members 只读，存储说明文件和公共数据集：
* datasets: 公共数据集，通常是网上发布的，成熟的数据集，维护一个列表方便共享
    * {dataset_name}: 
        * 以完整原始目录结构（作者发布时的目录结构）保存在 {dataset_name} 文件夹下，每个数据集一个文件夹，目录结构不应有空格
        * 如果数据集下载为压缩包，需要解压至对应文件夹
        * 使用时链接到需要使用的目录下 #TODO: 如何链接
    * README.md: 存放数据集的上传者、链接、分类、hash、大小等信息
    * 说明：任何人都可以
* documents: 存放团队器材、服务器资料和文档
    * eos_r: [EOS R 相机使用说明](documents/eos_r/README.md)
    * nas: [NAS 使用说明](documents/nas/README.md)和规范
    * server: [服务器使用说明](documents/server/README.md) #TODO、装机脚本和装机软件
* README.md: 解释目录结构、新手入门


## 说明

* [NAS 使用说明](documents/nas/README.md)
* [服务器使用说明](documents/server/README.md) #TODO
* [EOS R 相机使用说明](documents/eos_r/README.md)


## 贡献

所有用户都可以通过以下方式对 NAS 的管理和使用做出贡献。

公共数据集：使用公共数据集可以节省 home 文件夹空间
* NAS:/Public/datasets 文件夹用于存储公共数据集，只读
* 管理员和普通用户均通过以下步骤申请公共数据集入库：
    1. 下载数据集到个人 home 文件夹
    2. 将数据集解压到个人 home 文件夹中，以数据集名称命名，命名应不包含空格，空格以 '_' 替代
    3. 将 [nas_directory](https://github.com/pidan1231239/nas_directory) 仓库克隆到个人电脑，编辑 datasets/README.md，按格式添加数据集的信息
    4. 完善 commit 信息并提交 commit
    5. 向原仓库发起 pull request，交由 managers 进行 merge 并将数据集入库到 NAS:/Public/datasets

建议和补充：
* 对 README 和 NAS:/Public/documents 等说明文件有修改建议和补充的：
    1. 将 [nas_directory](https://github.com/pidan1231239/nas_directory) 仓库克隆到个人电脑，进行修改和补充
    1. 完善 commit 信息并提交 commit
    1. 向原仓库发起 pull request，交由 managers 进行 merge
* 注意：pdf 等文件请勿提交到 commit 中，因为文件可能较大且无法追踪更改，应将此类文件暂存到个人 home 文件夹文件夹，并在 pull request 中说明此类文件的增改（说明将新增文件移动到 NAS:/Public 下的哪个文件或覆盖哪个文件）

TODO：详细贡献数据集、贡献说明，github 使用说明，GUI git 软件建议，pull request 发起说明


