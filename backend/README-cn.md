# FastAPI 项目 - 后端

## 需求

* [Docker](https://www.docker.com/)。
* [Poetry](https://python-poetry.org/) 用于 Python 包和环境管理。

## 本地开发

* 使用 Docker Compose 启动栈：

```bash
docker compose up -d
```

* 现在你可以打开浏览器并与以下 URL 交互：

前端，使用 Docker 构建，根据路径处理路由：http://localhost

基于 OpenAPI 的后端 JSON 格式 Web API：http://localhost/api/

使用 Swagger UI 自动交互式文档（来自 OpenAPI 后端）：http://localhost/docs

Adminer，数据库 Web 管理：http://localhost:8080

Traefik UI，查看代理如何处理路由：http://localhost:8090

**注意**：第一次启动你的栈时，可能需要一分钟才能准备就绪。在此期间，后端会等待数据库准备就绪并配置所有内容。你可以查看日志来监控它。

要检查日志，请运行：

```bash
docker compose logs
```

要检查特定服务的日志，请添加服务名称，例如：

```bash
docker compose logs backend
```

如果你的 Docker 没有在 `localhost` 上运行（上面的 URL 将无法工作），你需要使用 Docker 运行的 IP 或域名。

### 后端本地开发，附加细节

#### 通用工作流程

默认情况下，依赖项使用 [Poetry](https://python-poetry.org/) 管理，请前往该网站并安装它。

从 `./backend/` 目录，你可以使用以下命令安装所有依赖项：

```console
$ poetry install
```

然后，你可以使用以下命令启动一个带有新环境的 shell 会话：

```console
$ poetry shell
```

确保你的编辑器正在使用正确的 Python 虚拟环境。

在 `./backend/app/models.py` 中修改或添加 SQLModel 模型以处理数据和 SQL 表，在 `./backend/app/api/` 中添加 API 端点，在 `./backend/app/crud.py` 中添加 CRUD（创建、读取、更新、删除）工具。

#### VS Code

已经配置好了通过 VS Code 调试器运行后端的相关设置，这样你就可以使用断点、暂停和探索变量等。

此外，还配置了通过 VS Code Python 测试标签运行测试的设置。

这些设置旨在提高开发效率和调试体验，使你能够更加轻松地开发和测试你的后端应用程序。通过使用 Poetry 管理依赖项和 VS Code 进行代码编辑和调试，你可以保持你的开发环境整洁和一致，同时利用强大的工具来加速开发过程。

### Docker Compose 覆盖

在开发过程中，你可以在 `docker-compose.override.yml` 文件中更改仅影响本地开发环境的 Docker Compose 设置。

对该文件的更改仅影响本地开发环境，不影响生产环境。因此，你可以添加有助于开发工作流程的“临时”更改。

例如，后端代码所在的目录被作为 Docker “宿主卷”挂载，将你实时更改的代码映射到容器内部的目录。这允许你立即测试更改，无需重新构建 Docker 镜像。这应该只在开发期间进行，在生产环境中，你应该使用最新版本的后端代码构建 Docker 镜像。但在开发期间，它允许你非常快速地迭代。

还有一个命令覆盖，它运行的是 `/start-reload.sh`（包含在基础镜像中），而不是默认的 `/start.sh`（也包含在基础镜像中）。它启动单个服务器进程（而不是生产环境中的多个）并在代码更改时重新加载进程。请注意，如果你有一个语法错误并保存了 Python 文件，它将会中断并退出，容器也会停止。之后，你可以通过修复错误并再次运行以下命令来重新启动容器：

```console
$ docker compose up -d
```

还有一个被注释掉的 `command` 覆盖，你可以取消注释它并注释掉默认的命令。它使后端容器运行一个“无操作”的进程，但保持容器处于活动状态。这允许你进入正在运行的容器内部并执行命令，例如 Python 解释器来测试已安装的依赖项，或启动在检测到更改时重新加载的开发服务器。

要使用 `bash` 会话进入容器，你可以启动栈：

```console
$ docker compose up -d
```

然后在运行中的容器内部 `exec`：

```console
$ docker compose exec backend bash
```

你应该看到一个像这样的输出：

```console
root@7f2607af31c3:/app#
```

这意味着你在一个 `bash` 会话中进入了你的容器，作为一个 `root` 用户，在 `/app` 目录下，该目录下还有一个名为 "app" 的目录，那就是你的代码在容器内部的位置：`/app/app`。

在那里，你可以使用 `/start-reload.sh` 脚本来运行调试实时重载服务器。你可以从容器内部运行该脚本：

```console
$ bash /start-reload.sh
```

...它将看起来像这样：

```console
root@7f2607af31c3:/app# bash /start-reload.sh
```

然后按回车。这将运行实时重载服务器，它会在检测到代码更改时自动重载。

尽管如此，如果它没有检测到更改但检测到语法错误，它将仅以错误停止。但因为容器仍然处于活动状态，并且你在一个 Bash 会话中，你可以在修复错误后快速重启它，运行相同的命令（"上箭头" 和 "Enter"）。

...前面的细节是使容器保持活动状态并运行实时重载服务器变得有用的地方。

### 后端测试

要测试后端，请运行：

```console
$ bash ./scripts/test.sh
```

测试使用 Pytest 进行，修改并添加测试到 `./backend/app/tests/` 目录。

如果你使用 GitHub Actions，测试将会自动运行。

#### 测试运行栈

如果你的栈已经启动，你只是想运行测试，你可以使用：

```bash
docker compose exec backend bash /app/tests-start.sh
```

这个 `/app/tests-start.sh` 脚本在确保其余栈正在运行后，仅调用 `pytest`。如果你需要给 `pytest` 传递额外的参数，你可以传递给该命令，它们将被转发。

例如，要在第一个错误时停止：

```bash
docker compose exec backend bash /app/tests-start.sh -x
```

#### 测试覆盖率

当测试运行时，会生成一个 `htmlcov/index.html` 文件，你可以在浏览器中打开它来查看测试的覆盖率。

### 迁移

由于在本地开发期间你的应用目录被作为卷挂载到容器内部，你同样可以在容器内部使用 `alembic` 命令运行迁移，迁移代码将在你的应用目录中（而不是仅在容器内部）。这样你可以将它添加到你的 git 仓库中。

确保你为模型创建了一个“修订版”，并且每次更改模型时都使用该修订版“升级”你的数据库。因为这将更新你数据库中的表。否则，你的应用程序将会出现错误。

* 启动后端容器的交互式会话：

```console
$ docker compose exec backend bash
```

* Alembic 已经配置好从 `./backend/app/models.py` 导入你的 SQLModel 模型。

* 更改模型后（例如，添加一个列），在容器内部创建一个修订版，例如：

```console
$ alembic revision --autogenerate -m "Add column last_name to User model"
```

* 提交到 git 仓库中 alembic 目录下生成的文件。

* 创建修订版后，运行数据库中的迁移（这将实际更改数据库）：

```console
$ alembic upgrade head
```

如果你根本不想使用迁移，取消注释 `./backend/app/core/db.py` 文件中以：

```python
SQLModel.metadata.create_all(engine)
```

结束的行，并注释掉 `prestart.sh` 文件中包含：

```console
$ alembic upgrade head
```

的行

如果你不想从默认模型开始，并且想从一开始就删除它们/修改它们，没有任何之前的修订版，你可以删除 `./backend/app/alembic/versions/` 下的修订文件（`.py` Python 文件）。然后按照上面描述的方式创建第一个迁移。
