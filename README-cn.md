# 全栈 FastAPI 模板

<a href="https://github.com/tiangolo/full-stack-fastapi-template/actions?query=workflow%3ATest"  target="_blank"><img src="https://github.com/tiangolo/full-stack-fastapi-template/workflows/Test/badge.svg"  alt="测试"></a>
<a href="https://coverage-badge.samuelcolvin.workers.dev/redirect/tiangolo/full-stack-fastapi-template"  target="_blank"><img src="https://coverage-badge.samuelcolvin.workers.dev/tiangolo/full-stack-fastapi-template.svg"  alt="覆盖率"></a>

## 技术栈和特性

- ⚡ [**FastAPI**](https://fastapi.tiangolo.com) 用于 Python 后端 API。
    - 🧰 [SQLModel](https://sqlmodel.tiangolo.com) 用于 Python SQL 数据库交互（ORM）。
    - 🔍 [Pydantic](https://docs.pydantic.dev)，由 FastAPI 使用，用于数据验证和设置管理。
    - 💾 [PostgreSQL](https://www.postgresql.org) 作为 SQL 数据库。
- 🚀 [React](https://react.dev) 用于前端。
    - 💃 使用 TypeScript、hooks、Vite 以及现代前端栈的其他部分。
    - 🎨 [Chakra UI](https://chakra-ui.com) 用于前端组件。
    - 🤖 自动生成的前端客户端。
    - 🦇 支持深色模式。
- 🐋 [Docker Compose](https://www.docker.com) 用于开发和生产环境。
- 🔒 默认情况下安全的密码哈希。
- 🔑 JWT 令牌认证。
- 📫 基于电子邮件的密码恢复。
- ✅ 使用 [Pytest](https://pytest.org) 进行测试。
- 📞 [Traefik](https://traefik.io) 作为反向代理/负载均衡器。
- 🚢 使用 Docker Compose 提供部署指南，包括如何设置前端 Traefik 代理以处理自动 HTTPS 证书。
- 🏭 基于 GitHub Actions 的 CI（持续集成）和 CD（持续部署）。

### 仪表板登录

[![API 文档](img/login.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 仪表板 - 管理员

[![API 文档](img/dashboard.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 仪表板 - 创建用户

[![API 文档](img/dashboard-create.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 仪表板 - 项目列表

[![API 文档](img/dashboard-items.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 仪表板 - 用户设置

[![API 文档](img/dashboard-user-settings.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 仪表板 - 深色模式

[![API 文档](img/dashboard-dark.png)](https://github.com/tiangolo/full-stack-fastapi-template) 

### 交互式 API 文档

[![API 文档](img/docs.png)](https://github.com/tiangolo/full-stack-fastapi-template)

## 如何使用它

你可以 **仅仅通过复制或克隆** 这个仓库，并原样使用它。

✨ 它开箱即用。✨

### 如何使用私有仓库

如果你想拥有一个私有仓库，GitHub 不允许你简单地复制它，因为它不允许更改复制的可见性。

但你可以做以下操作：

- 创建一个新的 GitHub 仓库，例如 `my-full-stack`。
- 手动克隆这个仓库，使用你想要的项目名称设置名称，例如 `my-full-stack`：

```bash
git clone git@github.com:tiangolo/full-stack-fastapi-template.git my-full-stack
```

- 进入新目录：

```bash
cd my-full-stack
```

- 将新的 origin 设置为你的新仓库，从 GitHub 界面复制它，例如：

```bash
git remote set-url origin git@github.com:octocat/my-full-stack.git
```

- 添加这个仓库作为另一个 "remote"，以便你以后能够获取更新：

```bash
git remote add upstream git@github.com:tiangolo/full-stack-fastapi-template.git
```

- 将代码推送到你的新仓库：

```bash
git push -u origin master
```

通过这种方式，你可以拥有一个私有的全栈应用程序模板，并且当原始模板有更新时，你可以轻松地将这些更新合并到你的私有仓库中。这样，你可以保持你的应用程序与最新的安全更新和功能改进同步，同时还能保持你的代码和数据的私密性。

### 从原始模板更新

在克隆了仓库并在其中做了更改之后，你可能会想要获取这个原始模板的最新更改。

- 确保你已经将原始仓库添加为远程仓库，你可以用以下命令来检查：

```bash
git remote -v

origin    git@github.com:octocat/my-full-stack.git (fetch)
origin    git@github.com:octocat/my-full-stack.git (push)
upstream    git@github.com:tiangolo/full-stack-fastapi-template.git (fetch)
upstream    git@github.com:tiangolo/full-stack-fastapi-template.git (push)
```

- 拉取最新更改但不合并：

```bash
git pull --no-commit upstream master
```

这将会下载这个模板的最新更改，但不会提交它们，这样你可以在提交之前检查一切都是正确的。

- 如果有冲突，在你的编辑器中解决它们。

- 完成后，提交更改：

```bash
git merge --continue
```

这个过程允许你保持你的项目与原始模板的同步，同时确保你对项目的更改保持控制。通过这种方式，你可以利用原始模板的最新功能和改进，同时保留你对自己项目的定制和更改。这对于确保你的应用程序或服务能够持续接收重要的更新和安全修复是非常有帮助的。

### 配置

然后你可以在 `.env` 文件中更新配置来定制你的设置。

在部署之前，请确保至少更改以下值：

- `SECRET_KEY`
- `FIRST_SUPERUSER_PASSWORD`
- `POSTGRES_PASSWORD`

你可以（并且应该）将这些值作为环境变量从秘密中传递。

阅读[deployment.md](./deployment.md)文档以获取更多详细信息。

### 生成密钥

`.env` 文件中的一些环境变量默认值为 `changethis`。

你必须用密钥替换它们，要生成密钥，你可以运行以下命令：

```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

复制输出的内容并将其作为密码/密钥使用。再次运行该命令以生成另一个安全的密钥。

这些步骤确保了你的应用程序配置是安全的，并且适合你的特定环境。`SECRET_KEY` 用于加密会话和保护你的应用程序免受某些类型的攻击。`FIRST_SUPERUSER_PASSWORD` 用于设置第一个超级用户账户的密码，而 `POSTGRES_PASSWORD` 用于配置 PostgreSQL 数据库的访问权限。通过使用环境变量和生成安全的密钥，你可以保护你的应用程序免受未授权访问和其他安全威胁。

## 如何使用 - 使用 Copier 的替代方法

这个仓库还支持使用 [Copier](https://copier.readthedocs.io) 生成一个新项目。

它将复制所有文件，询问你配置问题，并用你的回答更新 `.env` 文件。

### 安装 Copier

你可以使用以下命令安装 Copier：

```bash
pip install copier
```

或者更好的是，如果你有 [`pipx`](https://pipx.pypa.io/)，你可以直接运行它：

```bash
pipx install copier
```

**注意**：如果你有 `pipx`，安装 copier 是可选的，你可以直接运行它。

### 使用 Copier 生成一个项目

为你的新项目的目录决定一个名称，你将在下面使用它。例如，`my-awesome-project`。

进入将成为你项目父目录的目录，并使用你的项目名称运行命令：

```bash
copier copy https://github.com/tiangolo/full-stack-fastapi-template  my-awesome-project --trust
```

如果你有 `pipx` 并且你没有安装 `copier`，你可以直接运行它：

```bash
pipx run copier copy https://github.com/tiangolo/full-stack-fastapi-template  my-awesome-project --trust
```

使用 Copier 的这种方法提供了一种更加交互式和定制化的方式来创建一个新的项目。Copier 会引导你完成整个配置过程，确保你的新项目是根据你的特定需求来定制的。这种方法特别适合那些希望从头开始，但又想利用这个模板提供的强大功能和结构的用户。通过 Copier，你可以确保你的项目设置正确，并且所有的配置文件都被正确地更新，以匹配你的项目名称和其他重要信息。

**注意** `--trust` 选项是必需的，以便能够执行一个[创建后脚本](https://github.com/tiangolo/full-stack-fastapi-template/blob/master/.copier/update_dotenv.py)，该脚本会更新你的 `.env` 文件。

### 输入变量

Copier 会要求你提供一些数据，在生成项目之前你可能需要准备好这些数据。

但不用担心，你可以在之后直接在 `.env` 文件中更新这些内容。

输入变量及其默认值（有些是自动生成的）如下：

- `project_name`：（默认：`"FastAPI Project"`）项目名称，在 `.env` 中显示给 API 用户。
- `stack_name`：（默认：`"fastapi-project"`）用于 Docker Compose 标签和项目名称的堆栈名称（无空格，无句点）（在 `.env` 中）。
- `secret_key`：（默认：`"changethis"`）项目的密钥，用于安全，存储在 `.env` 中，你可以使用上面的方法生成一个。
- `first_superuser`：（默认：`"admin@example.com"`）第一个超级用户的电子邮件（在 `.env` 中）。
- `first_superuser_password`：（默认：`"changethis"`）第一个超级用户的密码（在 `.env` 中）。
- `smtp_host`：（默认：`""`）用于发送电子邮件的 SMTP 服务器主机，你可以稍后在 `.env` 中设置。
- `smtp_user`：（默认：`""`）用于发送电子邮件的 SMTP 服务器用户，你可以稍后在 `.env` 中设置。
- `smtp_password`：（默认：`""`）用于发送电子邮件的 SMTP 服务器密码，你可以稍后在 `.env` 中设置。
- `emails_from_email`：（默认：`"info@example.com"`）发送电子邮件的电子邮件账户，你可以稍后在 `.env` 中设置。
- `postgres_password`：（默认：`"changethis"`）PostgreSQL 数据库的密码，存储在 `.env` 中，你可以使用上面的方法生成一个。
- `sentry_dsn`：（默认：`""`）如果你使用 Sentry，这里是 Sentry 的 DSN，你可以稍后在 `.env` 中设置。

## 后端开发

后端文档：[backend/README.md](./backend/README.md)。

以上信息提供了使用 Copier 生成新项目时需要注意的一些关键点，包括必要的 `--trust` 选项以及 Copier 会询问的输入变量。这些变量对于定制化你的项目非常重要，确保你根据项目需求准备好相应的信息。同时，也指出了即使在生成项目后，你仍然可以更新 `.env` 文件中的配置，这为用户提供了灵活性。此外，还提供了后端开发文档的链接，以便用户可以深入了解和开始后端开发工作。

## 前端开发

前端文档：[frontend/README-cn.md](./frontend/README-cn.md)。

## 部署

部署文档：[deployment-cn.md](./deployment-cn.md)。

## 开发

一般开发文档：[development.md](./development.md)。

这包括使用 Docker Compose、自定义本地域名、`.env` 配置文件等。

## 更新日志

查看文件 [release-notes.md](./release-notes.md)。

## 许可证

全栈 FastAPI 模板根据 MIT 许可证的条款获得授权。