---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 搜寻数据存储库
{: #crawling-your-data-repository}

搜寻器选项全部正确配置后，即可以对数据存储库运行搜寻。
{: shortdesc}

切勿以 `root` 用户身份运行搜寻器，除非您需要访问仅 `root` 用户可以读取的文件。
{: tip}

运行以下命令：`crawler`

搜寻器会提示您查看说明要执行的操作的文档。您可以运行测试搜寻，或运行添加有其他搜寻选项的搜寻。

## 运行测试搜寻

运行以下命令：`crawler testit`

此命令运行测试搜寻，以仅搜寻种子 URL 并显示所有排队的 URL。如果种子 URL 生成可建立索引的内容（例如，文档），那么该内容将发送到输出适配器，并且该内容会显示在屏幕上。如果种子 URL 检索操作导致将 URL 排队，那么将显示这些 URL，并且不会将任何内容发送到输出适配器。缺省情况下，将显示五个排队的 URL。

还可以将定制配置文件指定为 testit 命令的选项，例如：`crawler testit --config [config/myconfigfile.conf]`

`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径格式（如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或绝对路径（如 `/path/to/config/myconfigfile.conf`）。

此外，还可以设置显示的排队 URL 数的限制作为 testit 命令的选项，例如：`crawler testit --limit [number]`

## 运行搜寻

运行以下命令：`crawler crawl`

此命令使用缺省配置文件 (`crawler.conf`) 运行搜寻。

还可以将定制配置文件指定为 crawl 命令的选项，例如：`crawler crawl --config [config/myconfigfile.conf]`

`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径格式（如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或绝对路径（如 `/path/to/config/myconfigfile.conf`）。

## 重新启动搜寻

运行以下命令：`crawler restart`

此命令通过使用缺省配置文件 (`crawler.conf`) 启动新搜寻来运行重新启动搜寻。

还可以将定制配置文件指定为 restart 命令的选项，例如：`crawler restart --config [config/myconfigfile.conf]`

`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径格式（如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或绝对路径（如 `/path/to/config/myconfigfile.conf`）。

## 恢复搜寻

运行以下命令：`crawler resume`

此命令使用缺省配置文件 (`crawler.conf`) 从搜寻停止的位置恢复该搜寻。

还可以将定制配置文件指定为 resume 命令的选项，例如：`crawler resume --config [config/myconfigfile.conf]`

`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径格式（如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或绝对路径（如 `/path/to/config/myconfigfile.conf`）。

## 刷新搜寻

运行以下命令：`crawler refresh`

此命令使用缺省配置文件 (`crawler.conf`) 刷新先前的搜寻。

还可以将定制配置文件指定为 refresh 命令的选项，例如：`crawler refresh --config [config/myconfigfile.conf]`

`--config` 选项中传递的配置文件的路径必须是限定路径。即，此路径必须为相对路径格式（如 `config/myconfigfile.conf` 或 `./myconfigfile.conf`）或绝对路径（如 `/path/to/config/myconfigfile.conf`）。
