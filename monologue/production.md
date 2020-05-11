# 生产化部署

本文章内容主要叙述 Monologue 的生产化部署方式。文中所有流程的演示环境是

- Ubuntu 18.04 LTS
- Apache 2.4
- Python 3.7

**\*** Monologue 不支持 Python 2 环境运行。

!> 本文档中暂无 Nginx 相关教程，如果你熟悉，可以考虑给[本项目](//github.com/sotapmc/Book)发送 Pull Request。

在开始之前，你需要手动 `clone` 项目内容。

```bash
git clone https://github.com/sotapmc/Monologue.git
```

随后你将得到一个充满文件的目录。这个目录里包含了所有的前端内容和一个包含后端内容的文件夹 `backend`。也就是说，`clone` 下来的内容中，除了 `backend` 之外的所有内容都属于前端，而后端的所有文件则位于 `backend/mono-back` 中。由于是前后端分离程序，我们把前端和后端分开部署在不同的位置。

?> 💡 下文中使用 `@` 表示 `clone` 下来的项目根目录。例如 `@/backend/mono-back`。

## 后端

后端部署起来略显复杂，所以我们先讲如何部署后端。由于后端是用 Python 开发的，所以无法像 PHP 那样直接挂载到目录下就可访问。Python 开发的后端目前比较主流的部署办法是使用 WSGI。要开始，我们需要安装 WSGI。在 Apache 平台上，只需要手动安装 `libapache2-mod-wsgi-py3` 包即可。

```bash
sudo apt-get install libapache2-mod-wsgi-py3
```

安装后会自动帮你 `enable`。成功以后，我们需要安装项目的依赖。目前本项目依赖于如下几大库

|库名|用途|
|:-:|:-:|
|`flask`|Flask 框架，整个后端的基础框架|
|`flask-cors`|Flask CORS 解决方案|
|`flask-restful`|Flask RESTful API 解决方案|
|`pymysql`|Python MySQL 支持对数据库的访问|
|`pyyaml`|Python Yaml 解析配置文件（`.yml` 文件）|
|`markdown`|Python Markdown 解析 Markdown 语法|
|`pymdown-extensions`|使 markdown 支持拓展语法|

如果你追求快速，可以考虑直接全局使用 `pip` 安装：

```bash
pip install flask flask-cors flask-restful pymysql pyyaml markdown pymdown-extensions
```

如果你有其它的需求，例如需要模式化管理自己的项目，那么你可以使用*虚拟空间*的方法。虚拟空间的激活脚本位于 `@/backend/mono-back/Scripts/activate_this`。激活之后即可在虚拟空间内安装。

?> ❓ 目前处于开发阶段，Monologue 自带虚拟环境以及已经安装完成的包。

准备好了依赖以后，需要编写 Apache 的虚拟主机文件。

```bash
cd /etc/apache2/sites-available
```

我们此时假设站点的配置文件名称为 `backend.conf`。由于我们部署的是 WSGI，所以我们需要写上 WSGI 相关的设置，这需要路径配合。下面是一个参考：

```apache
<Virtualhost *:80>
    ServerName example.com

    WSGIDaemonProcess monologue threads=5 
    WSGIScriptAlias / @/backend/mono-back/App.wsgi

    <Directory @/backend/mono-back>
        WSGIProcessGroup monologue
        WSGIApplicationGroup %{GLOBAL}
        WSGIScriptReloading On
        Order deny,allow
        Allow from all
    </Directory>
</Virtualhost>
```

该配置文件中必须包含上面的例子里的内容，其它的设置可以根据需要再添加。我们已经提前写好了一份 `.wsgi` 脚本，放置在后端目录（`@/backend/mono-back`）下，名为 `App.wsgi`。因此，使用时只需要将 `WSGIScriptAlias` 指向该文件即可。

配置成功以后，需要手动修改 `App.wsgi` 的内容。

```python
import sys

activate_this = "/path/to/activate_this.py"
execfile(activate_this, dict(__file__=activate_this))

sys.path.insert(0, "/path/to/backend/root")

from App import app as application
```

`wsgi` 文件的内容中有两个可变量，一个是 `/path/to/activate_this.py`，这个路径需要指向一个 `activate_this.py` 文件。默认情况下，这个文件处于 `@/backend/mono-back/Scripts/activate_this.py`，直接将该文件的完整绝对路径填写上去即可。另一个是 `/path/to/backend/root` 需要指向后端根目录，即 `@/backend/mono-back`，将该目录的绝对路径填写上去即可。

?> ✅ 当然，你也可以根据自己的需求编写自己的 `wsgi` 文件。为了避免新版本冲突，请妥善保管文件内容。

上面的所有都完成之后，你需要回到后端的目录里，找到 `config.example.yml`（也就是后端的配置文件），将里面的内容改成你想要的样子，然后重命名为 `config.yml`。

!> 无论如何都必须进行重命名，否则主程序将因为无法找到配置文件而无法运行。

一切就绪以后，输入 `a2ensite backend.conf && systemctl reload apache2` 启用该站点并重载 Apache，后端就部署完成了。此时访问此虚拟主机所指向的域名和端口，便可以正常使用了。

## 前端

前端由于都是静态文件，所以部署起来基本上没有什么困难。按照一般的前端构建顺序，我们需要先安装依赖：

```bash
npm install
```

!> 执行 `npm install` 时请确保当前目录是 `@`，即包含 `package.json` 的目录。

执行成功后，进行正式的构建。如果不出问题，下面的这条指令在一分钟之内便可以执行完毕。

```bash
npm run build
```

`build` 成功以后，可以看到下面的内容

![](https://i.loli.net/2020/04/25/7CHc5MhipU4zTFN.png)

此时前端所构建的文件就都在 `@/dist` 下了。再按照一般的 Apache 静态页面的部署逻辑，将 `dist` 文件夹作为服务器的根目录即可。

## 后端 SSL 和反向代理问题和注意事项

如果你愿意将后端和前端部署在不同的位置上，推荐使用反向代理。在前端的配置文件里加入如下语句：

```apache
SSLProxyEngine On
ProxyPass /api/ <location>/api/
ProxyPassReverse /api/ <location>/api/
```

!> 必须写作 `/api/` 而非 `/api`，否则会导致代理错误。如果没有 SSL 可以将 `SSLProxyEngine` 去掉，但是如果有则必须加上。

同时，为了前端页面能够正常工作，我们需要手动取消对 `.var` 后缀的 Handler 支持。这是因为前端中使用了一种叫做 Inter 的字体，且使用的是它带有变量（variable）特性的版本。获取请求时，Apache 的默认行为也许会抢先处理 `.var`，导致无法正常获取该文件。**解决方法**：在前端的配置文件里找到 `<Directory> ... </Directory>`，在其中加入 `RemoveHandler .var` 即可。

若要为后端启用 SSL，其配置文件内容应和非 SSL 的配置文件保持一致，但是需要去掉 `WSGIDaemonProcess` 行来保证可以正常 `reload`。

