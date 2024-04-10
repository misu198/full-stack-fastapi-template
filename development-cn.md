# FastAPI Project - Development

在本地开发环境中，有时你可能希望使用不同于 `localhost` 的域名。例如，如果你遇到与需要子域名的 cookie 相关的问题，而 Chrome 不允许你使用 `localhost`，你可以考虑以下两种解决方案：

1. **修改系统 hosts 文件** - 你可以按照下面的说明在 **使用自定义 IP 的开发** 部分中修改你的系统 `hosts` 文件，将自定义域名指向本地的 IP 地址 `127.0.0.1`。
2. **使用 `localhost.tiangolo.com`** - 这是一个已经设置为指向 `localhost`（IP 地址 `127.0.0.1`）及其所有子域名的域名。由于它是一个实际的域名，浏览器将会存储你在开发过程中设置的 cookie 等。

如果你在生成项目时使用了默认的 CORS 允许的域名，`localhost.tiangolo.com` 已经被配置为允许的域名。如果没有，你需要在 `.env` 文件中的 `BACKEND_CORS_ORIGINS` 变量中添加它。

要在你的栈中配置它，请按照下面的 **更改开发“域名”** 部分的步骤操作，使用域名 `localhost.tiangolo.com`。

完成这些步骤后，你应该能够打开 http://localhost.tiangolo.com，并由你在 `localhost` 上的栈提供服务。

有关所有相应的可用 URL，请查看文末的相应部分。

# FastAPI 项目 - 开发

## 在 `localhost` 上使用自定义域名进行开发

如果你希望使用与 `localhost` 不同的域名进行开发，例如，如果你在使用需要子域名的 cookie 时遇到问题，而 Chrome 不允许你使用 `localhost`，你可以考虑以下两种解决方案：

1. **修改系统 hosts 文件** - 你可以按照下面的说明在 **使用自定义 IP 的开发** 部分中修改你的系统 `hosts` 文件，将自定义域名指向本地的 IP 地址 `127.0.0.1`。
2. **使用 `localhost.tiangolo.com`** - 这是一个已经设置为指向 `localhost`（IP 地址 `127.0.0.1`）及其所有子域名的域名。由于它是一个实际的域名，浏览器将会存储你在开发过程中设置的 cookie 等。

如果你在生成项目时使用了默认的 CORS 允许的域名，`localhost.tiangolo.com` 已经被配置为允许的域名。如果没有，你需要在 `.env` 文件中的 `BACKEND_CORS_ORIGINS` 变量中添加它。

要在你的栈中配置它，请按照下面的 **更改开发“域名”** 部分的步骤操作，使用域名 `localhost.tiangolo.com`。

完成这些步骤后你应该能够打开：http://localhost.tiangolo.com，它将由你的栈在 `localhost` 上提供服务。

检查所有相应的可用 URL 在文末的相应部分。

## 使用自定义 IP 进行开发

如果你正在使用不同于 `127.0.0.1` (`localhost`) 的 IP 地址运行 Docker，你将需要执行一些额外的步骤。这可能是你正在运行自定义虚拟机，或者你的 Docker 位于你网络中的另一台机器上的情况。

在这种情况下，你需要使用一个假的本地域名（例如 `dev.example.com`）并让你的计算机认为该域名是由自定义 IP（例如 `192.168.99.150`）提供的服务。

如果你有这样一个自定义域名，你需要将其添加到 `.env` 文件中的 `BACKEND_CORS_ORIGINS` 变量的列表中。

* 使用文本编辑器以管理员权限打开你的 `hosts` 文件：

  * **Windows 系统注意事项**：如果你使用的是 Windows 系统，在主菜单中搜索 "notepad"，右键点击并选择 "以管理员身份运行" 或类似选项。然后点击 "文件" 菜单，选择 "打开文件"，前往目录 `c:\Windows\System32\Drivers\etc\`，选择显示 "所有文件" 而不仅仅是 "文本 (.txt) 文件"，然后打开 `hosts` 文件。
  * **Mac 和 Linux 系统注意事项**：你的 `hosts` 文件可能位于 `/etc/hosts`，你可以在终端中运行 `sudo nano /etc/hosts` 来编辑它。

* 在可能已有的内容之外，添加一行新的，包括自定义 IP（例如 `192.168.99.150`）、一个空格字符和你的假本地域名：`dev.example.com`。

新行可能看起来像这样：

```
192.168.99.150    dev.example.com
```

* 保存文件。
  * **Windows 系统注意事项**：确保你以 "所有文件" 的格式保存文件，不要 `.txt` 扩展名。默认情况下，Windows 会尝试添加扩展名。确保文件以其原始形式保存，不带扩展名。

...这将使你的计算机认为假本地域名是由该自定义 IP 提供服务的，当你在浏览器中打开该 URL 时，它会直接与你本地运行的服务器通信，当它被要求访问 `dev.example.com` 时，它会认为是一个远程服务器而实际上它是在你的电脑上运行的。

要在你的栈中配置它，请按照下面的 **更改开发“域名”** 部分的步骤操作，使用域名 `dev.example.com`。

完成这些步骤后你应该能够打开：http://dev.example.com，它将由你在 `192.168.99.150` 上的栈提供服务。

检查所有相应的可用 URL 在文末的相应部分。

## 更改开发“域名”

如果你需要使用与 `localhost` 不同的域名来与你的本地栈一起使用，你需要确保你使用的域名指向你的栈设置的 IP 地址。

为了简化你的 Docker Compose 设置，例如，以便 API 文档（Swagger UI）知道在哪里可以找到你的 API，你应该让 Docker Compose 知道你在开发中使用的是哪个域名。

* 打开位于 `./.env` 的文件。它会有一行类似于：

```
DOMAIN=localhost
```

* 将其更改为你将要使用的域名，例如：

```
DOMAIN=localhost.tiangolo.com
```

这个变量将被 Docker Compose 文件使用。

之后，你可以通过以下命令重启你的栈：

```bash
docker compose up -d
```

并在文末的相应部分检查所有相应的可用 URL。

## Docker Compose 文件和环境变量

有一个主要的 `docker-compose.yml` 文件，包含了适用于整个栈的所有配置，它会被 `docker compose` 自动使用。

还有一个 `docker-compose.override.yml` 文件，用于开发时的覆盖设置，例如将源代码作为卷挂载。它被 `docker compose` 自动使用，以便在 `docker-compose.yml` 上应用覆盖。

这些 Docker Compose 文件使用 `.env` 文件中包含的配置，这些配置将被注入到容器中作为环境变量。

它们还使用脚本在调用 `docker compose` 命令之前设置的一些额外配置，这些配置来自环境变量。



## `.env` 文件

`.env` 文件包含了所有的配置信息，生成的密钥和密码等。根据你的工作流程，你可能希望将其从 Git 中排除，例如，如果你的项目是公开的。在这种情况下，你需要确保在构建或部署项目时，CI 工具能够获取到这些配置信息。

一种方法是将每个环境变量添加到你的 CI/CD 系统中，并更新 `docker-compose.yml` 文件，使其读取特定的环境变量而不是读取 `.env` 文件。

### 提前提交和代码检查

我们使用一个名为 [pre-commit](https://pre-commit.com/) 的工具来进行代码检查和格式化。

当你安装它后，它会在 Git 提交之前运行。这样它确保代码在提交之前是一致的并且格式正确。

你可以在项目的根目录下找到一个包含配置的 `.pre-commit-config.yaml` 文件。

#### 安装 pre-commit 以自动运行

`pre-commit` 已经是项目依赖的一部分，但如果你愿意，你也可以按照 [官方 pre-commit 文档](https://pre-commit.com/) 全局安装它。

安装了 `pre-commit` 工具并使其可用后，你需要在本地仓库中“安装”它，这样它就会在每次提交之前自动运行。

使用 Poetry，你可以这样做：

```bash
❯ poetry run pre-commit install
pre-commit installed at .git/hooks/pre-commit
```

现在，每当你尝试提交，例如使用：

```bash
git commit
```

...pre-commit 将会运行并检查和格式化你即将提交的代码，并要求你再次使用 git 添加（staging）代码后再进行提交。

然后你可以再次使用 `git add` 修改/修复的文件，现在你可以提交了。



#### 手动运行 pre-commit 钩子

你也可以手动对所有文件运行 `pre-commit` 钩子，可以使用 Poetry 执行：

```bash
❯ poetry run pre-commit run --all-files
check for added large files..............................................Passed
check toml...............................................................Passed
check yaml...............................................................Passed
ruff.....................................................................Passed
ruff-format..............................................................Passed
eslint...................................................................Passed
prettier.................................................................Passed
```

## URL 列表

生产或预发布环境的 URL 将使用相同的路径，但使用你自己的域名。

### 开发 URL 列表

本地开发用途的开发 URL。

前端：http://localhost

后端：http://localhost/api/

自动交互式文档（Swagger UI）：http://localhost/docs

自动替代文档（ReDoc）：http://localhost/redoc

Adminer：http://localhost:8080

Traefik UI：http://localhost:8090

### 使用自定义域名在 localhost 上进行开发时的 URL 列表

本地开发用途的开发 URL。

前端：http://localhost.tiangolo.com

后端：http://localhost.tiangolo.com/api/

自动交互式文档（Swagger UI）：http://localhost.tiangolo.com/docs

自动替代文档（ReDoc）：http://localhost.tiangolo.com/redoc

Adminer：http://localhost.tiangolo.com:8080

Traefik UI：http://localhost.tiangolo.com:8090

