### Huginn-Chinese

[Huginn](https://github.com/huginn/huginn) 是一款自动化软件，通过多个 Agent (代理) 来完成一系列复杂的任务，目前已经在 Github 上收获了 38K 的Star！

但是目前 Huginn 尚未支持多语言，为了便于使用，本项目通过修改硬编码的方式对其进行了汉化

### 如何使用

强烈建议通过 Docker 来部署和使用 Huginn

#### 快速上手

本项目已经发布了汉化好的 Huginn 镜像，可以使用如下的命令尝试一下 Huginn-Chinese：

```
docker run -d -p 3000:3000 ghcr.io/yhdsl/huginn:latest
```

这将使 Huginn 在后台运行，并且可以通过 http://localhost:3000 访问其页面

默认的用户名是`admin`，而密码是`password`

#### 进一步部署与设置

如果需要持久化保存，可以使用下面的命令：

```
docker run -d -p 3000:3000 -v /home/huginn/mysql-data:/var/lib/mysql ghcr.io/yhdsl/huginn:latest
```

这将在`/home/huginn/mysql-data`目录下储存你的数据库文件

- Huginn 还支持更换数据库，请参考[官方的 Docker 仓库](https://hub.docker.com/r/huginn/huginn/)了解更多的信息
- 对于 Huginn 镜像所支持的环境变量，请参考 [.env 参考文件](https://github.com/huginn/huginn/blob/master/.env.example)，这将解决诸如邀请码是什么的问题
- 对于 Huginn 单线程镜像，请参考[该 Docker 仓库](https://hub.docker.com/r/huginn/huginn-single-process)了解更多的信息

#### 更换现有的 Huginn 镜像

请将镜像更换为 `ghcr.io/yhdsl/huginn:latest` 即可

但请注意：

- 由于官方的 Docker 镜像采用SHA作为标签，并不方便做版本控制，强烈建议仅使用 latest 标签
- Huginn 的部分页面做了 i18n (本地化) 处理，因此本项目在设置中将语言切换为了`zh-CN`，因此如果你有修改[该文件夹下](./huginn)的待替换的文件，请务必合并修改

#### 其他运行方式

请首先参考下文的汉化过程手动对源代码进行处理，然后按照官方的安装教程安装

### 是如何处理的

本项目包含两步处理过程，目前镜像的构建由 Github Action 自动进行，也可以参考[CI文件](.github/workflows/CI.yml)了解汉化过程

#### 硬编码处理

本项目使用了[该翻译脚本](https://github.com/yhdsl/Translator-Tool)对硬编码文件做处理,翻译脚本所需要的规则文件[在此](./rules)

#### i18n 处理

由于 Huginn 的用户管理使用了其他开源项目，因此部分UI文本是使用本地化处理的，添加的中文翻译[在此](./huginn/config/locales)，这些文件将被复制到本地化文件夹中

#### 下拉选项的汉化

部分 Huginn 文本是根据变量名直接转换来的，无法直接通过处理硬编码进行替换，本项目对处理的函数做了些修改，并通过[这些文件](./huginn/config)来存储翻译内容，这些文件将被复制到`config`文件夹中

此步骤随前两步一同执行，不需要额外的操作

### 汉化进度

目前已完成绝大部分页面的汉化工作，尚在进行以及需要帮助的内容统计如下：

#### 正在进行的工作

- 添加新代理页面中右侧对各代理的描述内容，由于文本量过大，目前正在缓慢的推进中
- 通知文本由于散步在源代码的各个部分，很容易存在遗漏，目前正在尽力补齐

#### 需要帮助的内容

如果你希望为本项目尽一份力量，欢迎来帮助我们解决以下困扰

- 为本项目添加自动化测试，目前[官方的CI](https://github.com/huginn/huginn/blob/master/.github/workflows/ci.yml)无法正常工作
- 开始页面的北欧神话的片段，请帮助我们翻译为合适的书面翻译
- 部分页面无法通过硬编码或者本地化进行翻译，请帮助我们解决它们
