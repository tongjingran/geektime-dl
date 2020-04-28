## geektime-dl

[![Go Report Card](https://goreportcard.com/badge/github.com/mmzou/geektime-dl)](https://goreportcard.com/report/github.com/mmzou/geektime-dl)
[![GitHub release](https://img.shields.io/github/v/release/mmzou/geektime-dl.svg)](https://github.com/mmzou/geektime-dl/releases)

👾 Geektime-dl 是使用Go构建的快速、简单的 [极客时间](https://time.geekbang.org/) 下载器.

- [安装](#%e5%ae%89%e8%a3%85)
  - [必要条件](#%e5%bf%85%e8%a6%81%e6%9d%a1%e4%bb%b6)
  - [使用`go get`安装](#%e4%bd%bf%e7%94%a8go-get%e5%ae%89%e8%a3%85)
- [入门](#%e5%85%a5%e9%97%a8)
  - [查看视频或专栏列表](#%e6%9f%a5%e7%9c%8b%e8%a7%86%e9%a2%91%e6%88%96%e4%b8%93%e6%a0%8f%e5%88%97%e8%a1%a8)
  - [专栏音频和视频的下载](#%e4%b8%93%e6%a0%8f%e9%9f%b3%e9%a2%91%e5%92%8c%e8%a7%86%e9%a2%91%e7%9a%84%e4%b8%8b%e8%bd%bd)
  - [可恢复继续下载](#%e5%8f%af%e6%81%a2%e5%a4%8d%e7%bb%a7%e7%bb%ad%e4%b8%8b%e8%bd%bd)
  - [登录](#%e7%99%bb%e5%bd%95)
- [参考仓库](#%e5%8f%82%e8%80%83%e4%bb%93%e5%ba%93)
- [License](#license)

## 安装

### 必要条件

以下为必须安装依赖：

* **[FFmpeg](https://www.ffmpeg.org)**

> **Note**: FFmpeg的使用是为了最后视频文件合并成需要的格式。

* **[Google-Chrome](https://www.google.cn/intl/zh-CN/chrome/)**

> **Note**: 需要谷歌浏览器支持，所以需要你本机安装谷歌浏览器。

### 使用`go get`安装

安装Geektime-dl，可以使用如下`go get`命令，或者从[Releases](https://github.com/mmzou/geektime-dl/releases) 页面下载二进制文件.

```bash
$ go get github.com/mmzou/geektime-dl
```

## 入门

使用方法:

```bash
#下载
geektime-dl [OPTIONS] 课程ID  [目录ID]
#查看专栏、视频，登录及其他命令操作
geektime-dl [OPTIONS] command
```

包含命令

```text
  login    登录极客时间
  who      获取当前帐号
  users    获取帐号列表
  su       切换极客时间帐号
  buy      获取已购买过的专栏和视频课程
  column   获取专栏列表
  video    获取视频课程列表
  help, h  Shows a list of commands or help for one command
```

### 查看视频或专栏列表

```bash
#查看专栏列表
$ geektime-dl column
+----+-----+---------------------------+------------+------------------+------+
| #  | ID  |           名称            |    时间    |       作者       | 购买 |
+----+-----+---------------------------+------------+------------------+------+
|  0 |  42 | 技术与商业案例解读        | 2017-09-07 | 徐飞             |      |
|  1 |  43 | AI技术内参                | 2017-09-11 | 洪亮劼           |      |
|  2 |  48 | 左耳听风                  | 2017-09-20 | 陈皓             | 是   |
|  3 |  49 | 朱赟的技术管理课          | 2017-11-09 | 朱赟             | 是   |
|  4 |  50 | 邱岳的产品手记            | 2017-11-16 | 邱岳             |      |
|  5 |  62 | 人工智能基础课            | 2017-12-01 | 王天一           | 是   |
|  6 |  63 | 赵成的运维体系管理课      | 2017-12-13 | 赵成             |      |
|  7 |  74 | 推荐系统三十六式          | 2018-02-23 | 刑无刀           |      |
|  8 |  76 | 深入浅出区块链            | 2018-03-19 | 陈浩             | 是   |


#查看视频列表
$ geektime-dl video
+----+-----+------------------------------------------+------------+--------------+------+
| #  | ID  |                   名称                   |    时间    |     作者     | 购买 |
+----+-----+------------------------------------------+------------+--------------+------+
|  0 |  66 | 微服务架构核心20讲                       | 2018-01-08 | 杨波         | 是   |
|  1 |  77 | 9小时搞定微信小程序开发                  | 2018-03-22 | 高磊         |      |
|  2 |  84 | 微服务架构实战160讲                      | 2018-05-03 | 杨波         | 是   |
|  3 |  98 | 零基础学Python                           | 2018-05-25 | 尹会生       |      |
```

### 专栏音频和视频的下载

下载为购买的视频或者专栏，只能下载免费观看的部分

```console
$ geektime-dl 66
01 - 什么是微服务架构？ 107.55 MiB / 107.54 MiB [==================================================================] 100.01% 1.42 MiB/s 1m15s
02 - 架构师如何权衡微服务的利弊？ 92.10 MiB / 92.09 MiB [============================================================] 100.01% 1.69 MiB/s 54s
03 - 康威法则和微服务给架构师怎样的启示？ 69.38 MiB / 69.38 MiB [====================================================] 100.01% 1.68 MiB/s 41s
04 - 企业应该在什么时候开始考虑引入微服务？ 114.20 MiB / 114.20 MiB [==============================================] 100.00% 1.41 MiB/s 1m21s
05 - 什么样的组织架构更适合微服务？ 121.10 MiB / 121.09 MiB [======================================================] 100.00% 1.66 MiB/s 1m13s
06 - 如何理解阿里巴巴提出的微服务中台战略？65.23 MiB / 126.82 MiB [=========================>------------------------] 51.43% 1.68 MiB/s 1m15s
```

查看课程中可下载的目录

```console
$ geektime-dl -i 66
+----+------+------+----------------------------------------------+---------+---------+---------+------+
| #  |  ID  | 类型 |                     名称                     |   SD    |   LD    |   HD    | 下载 |
+----+------+------+----------------------------------------------+---------+---------+---------+------+
|  0 | 2184 | 视频 | 01 什么是微服务架构？                        | 86.52M  | 53.45M  | 107.54M |  ✔   |
|  1 | 2185 | 视频 | 02 架构师如何权衡微服务的利弊？              | 71.43M  | 44.12M  | 92.09M  |  ✔   |
|  2 | 2154 | 视频 | 03 康威法则和微服务给架构师怎样的启示？      | 54.32M  | 33.57M  | 69.38M  |  ✔   |
|  3 | 2186 | 视频 | 04 企业应该在什么时候开始考虑引入微服务？    | 90.07M  | 55.67M  | 114.20M |  ✔   |
|  4 | 2187 | 视频 | 05 什么样的组织架构更适合微服务？            | 90.22M  | 55.79M  | 121.09M |  ✔   |
|  5 | 2188 | 视频 | 06 如何理解阿里巴巴提出的微服务中台战略？    | 126.82M | 100.05M | 61.79M  |  ✔   |
|  6 | 2189 | 视频 | 07 如何给出一个清晰简洁的服务分层方式？      | 45.89M  | 62.07M  | 61.95M  |  ✔   |
|  7 | 2222 | 视频 | 08 微服务总体技术架构体系是怎样设计的？      | 85.67M  | 52.91M  | 109.83M |  ✔   |
|  8 | 2269 | 视频 | 09 微服务最经典的三种服务发现机制            | 94.00M  | 73.18M  | 45.21M  |  ✔   |
```

可下载课程中的某个目录

```console
$ geektime-dl 66 2276
16 - 微服务监控系统分层和监控架构 11.22 MiB / 97.55 MiB [======>--------------------------------------------------]  11.51% 1.30 MiB/s 01m06s
```

下载专栏时，可以同时下载专栏文章内容为PDF文档（`需要谷歌浏览器支持`）

```console
04 - 静态容器：办公用品如何表达你的内容？ 13.94 MiB / 13.94 MiB [==============] 100.00% 2.23 MiB/s 6s
正在生成文件：【04 - 静态容器：办公用品如何表达你的内容？.pdf】 完成
```

> **注**: `如果生成文件提示失败，可以重复执行命令针对失败的文件再次生成`，已生成的文件不会重复生成。如果尝试多次都是失败，可以Issues提问。

### 可恢复继续下载

<kbd>Ctrl</kbd>+<kbd>C</kbd> 中断下载。

存在 `.download` 临时文件，使用相同的参数执行 `geektime-dl` 命令，则下载进度将从上一个会话恢复。

### 登录

通过账号密码登录：

```console
$ geektime-dl login --phone xxxxxx --password xxxxxx
极客时间账号登录成功： XXX
```

通过Cookie登录：

```console
$ geektime-dl login --gcid xxxxxx --gcess xxxxxx --serverId 'xxxxxxx'
极客时间账号登录成功： XXX
```

## 参考仓库

* [annie](https://github.com/iawia002/annie)


## License

MIT

Copyright (c) 2020-present, mmzou
