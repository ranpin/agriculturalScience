# agriculturalScience

> **这是一个存档仓库**：仓库根目录只有两个 RAR 压缩包，**源码没有以可直接浏览的形式入库**。下面的内容是**通过列出压缩包内文件清单推断**出来的（未解压、未逐行读源码），具体能否运行未验证。

## 仓库里有什么

| 文件 | 大小 | 说明 |
| --- | --- | --- |
| `Inet(1).rar` | 约 7 MB（2837 个条目） | 移动端前端工程 `Inet/` |
| `worksystem(1).rar` | 约 91 MB（1339 个条目） | Java Web 后端工程 `worksystem/` |

两个包都是 **RAR v5** 格式。从内容看它们是**同一套系统的前后端**：`Inet` 里硬编码的后端地址是 `http://192.168.43.114:8082/worksystem/`，正好指向 `worksystem` 这个后端工程。

## Inet(1).rar —— 移动端前端

- 一个 **Justep BeX5（起步 X5）** 移动应用工程，页面标题为「**智慧e农**」（见 `Inet/main.w`）。
- 主要内容：`.w` 窗口 XML + `.js` + `.css`，目录有 `leftmenu/`、`leftpage/`、`rightpage/`、`main/`、`img/`，以及 `.cache/`、`.release/`、`.idea/`（IDEA 模块名 `cxl.iml`）等。
- 依赖外部天气接口（`tianqi.qq.com`）和上面的 `worksystem` 后端。

## worksystem(1).rar —— Java Web 后端

- 一个 **IntelliJ IDEA 的 Java EE Web 工程**，页面标题为「**土圈后台管理系统**」（见 `worksystem/web/html/index.html`、`login.html`）。
- 技术栈（据 `lib/` 下的 jar 判断）：**Struts2 2.1.6**（含 convention/json/spring 插件）+ **Spring**（2.5 schema）+ **Hibernate3**，数据库 **MySQL**（`mysql-connector-java-5.1.14`），连接池 commons-dbcp；另有 POI/jxl（Excel 导出）、JFreeChart（图表）、UEditor（富文本）、thumbnailator（图片）、log4j、ehcache 等。前端资源为 layui + jQuery + md5.js。
- 数据源配置（`src/spring-config.xml`）：`jdbc:mysql://localhost:3306/hlwtq`，账号/密码 `root/root`。
- 代码结构：`src/com/` 下分 `Action`、`Entity`、`Service`（含 `Impl`）、`Base`、`ExcelUtil`、`filter`、`page`、`socket` 等包。
- 从 Action/Entity 包名可见的业务域（**拼音缩写，含义为推断，未逐一确认**）：党建（Dangjian）、流程审批（Liucheng）、新闻/要闻（News/Yaowen）、签到（qiandao）、通知（tongzhi）、评论（Comments）、意见反馈（Feedback）、会议（Meeting）、自动回复（AutoReply）、日志（Log）、数据中心（Sjzx）、用户（User）等。
- 注意：包里还带了 IDEA 构建产物 `out/`（含 `artifacts/worksystem/WEB-INF/lib`）和两个嵌套压缩包 `worksystem.zip`、`web/html.zip`，体积较大主要来自这里。

## 如何查看 / 运行

仓库本身**不含可直接运行的代码**，需先解包：

1. 用支持 RAR5 的工具解压（如 The Unarchiver / `unar` / `7z`），**不要把解压产物提交回本仓库**。
2. `worksystem/`：用 IntelliJ IDEA 打开（含 `.idea/` 与 `.iml`），配置 Tomcat 与本地 MySQL（库 `hlwtq`）后部署 war；数据库账号密码在 `spring-config.xml` 里写死为 `root/root`。
3. `Inet/`：需要一个 BeX5/X5 运行环境来承载，并把后端地址从 `192.168.43.114:8082` 改成实际可用的后端。

> 由于依赖的数据库、后端 IP 都是当年本机/内网环境，**开箱即用的可能性很低**；本仓库的定位就是存档备份。
