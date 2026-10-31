# 课题组官网模板

![PHP](https://img.shields.io/badge/PHP-7.2%2B-777BB4?logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-5.7%2B-4479A1?logo=mysql&logoColor=white)
![No Framework](https://img.shields.io/badge/Framework-None-lightgrey)
![License](https://img.shields.io/badge/License-Unspecified-lightgrey)

面向高校科研课题组 / 实验室的轻量级官网系统。原生 PHP 编写，不依赖框架与 Composer，内置安装向导、可视化后台、Markdown 编辑器、图片上传、留言审核、访问统计与站点地图生成，开箱即可搭建一个结构完整、移动端适配的课题组网站。

## 界面预览

<table>
  <tr>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-12-06.jpg" alt="首页" width="100%"><br><b>首页</b>：轮播图与内容区块</td>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-12-15.jpg" alt="新闻动态" width="100%"><br><b>新闻动态</b>：分类筛选与分页</td>
  </tr>
  <tr>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-12-29.jpg" alt="导师团队" width="100%"><br><b>导师团队</b>：成员列表与职称筛选</td>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-12-40.jpg" alt="导师详情" width="100%"><br><b>导师详情</b>：个人信息与研究介绍</td>
  </tr>
  <tr>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-12-51.jpg" alt="留言板" width="100%"><br><b>留言板</b>：留言、评论与分页</td>
    <td width="50%" align="center"><img src="img/Snipaste_2026-10-31_12-13-09.jpg" alt="后台控制面板" width="100%"><br><b>后台控制面板</b>：访问统计与内容概览</td>
  </tr>
</table>

## 功能特性

### 前台

- **首页**：全屏轮播图（自动切换 + 手动切换）、新闻动态、研究成果、导师团队、研究方向五个内容区块
- **新闻动态**：分类筛选、分页浏览、详情页 Markdown 渲染
- **科研团队**：导师、博士后、博士、硕士、毕业生五类成员，支持列表、详情、导师按职称筛选
- **研究方向**：图文卡片展示与详情页
- **研究成果**：成果列表与详情页
- **招生招聘**：招生 / 招聘分类展示与详情页
- **关于我们**：支持 Markdown 排版的团队介绍页
- **留言板**：访客留言、楼中楼评论、后台审核后展示、分页
- **全站搜索**：覆盖新闻、研究成果、招生招聘、导师信息，关键词高亮与摘要截取
- **站点信息**：友情链接、联系方式、ICP / 公安备案、运行天数、累计浏览量
- **响应式导航**：移动端汉堡菜单、下拉子菜单、折叠搜索框

### 后台（`/admin/`）

- **控制面板**：今日 PV / UV / IP、累计 PV、近 30 天访问明细、内容数量统计、待审核留言提醒
- **网站设置**：站点名称、图标、Logo、关键词、描述、版权、ICP 备案、公安备案、邮箱、地址、站点 URL，以及管理员用户名 / 密码修改
- **导航菜单**：父子两级菜单、排序、启用状态、当前窗口 / 新窗口打开
- **轮播图片**：上传、排序、启用状态、删除（同时清理图片文件）
- **友情链接**：新增、编辑、排序、启用状态
- **关于本站**：Markdown 编辑器在线编辑
- **新闻动态**：新闻增删改查、封面图上传、分类管理（有内容时禁止删除分类）
- **团队管理**：导师、博士后、博士、硕士、毕业生五类成员增删改查，照片上传、排序、富文本介绍
- **招生招聘**：招生 / 招聘信息管理
- **研究成果**：成果增删改查、封面图上传
- **研究方向**：方向增删改查、封面图上传、排序
- **留言管理**：留言与评论审核 / 删除、状态筛选、分页

## 环境要求

- PHP >= 7.2
- MySQL >= 5.7
- Nginx
已在 Nginx 1.15.10 + MySQL 5.7.23 + PHP 7.2 环境下运行验证。

## 快速开始


### 1. 上传程序

将项目文件上传至 Web 根目录（如 `/www/wwwroot/your-domain/`）。

### 2. 运行安装向导

浏览器访问：

```text
https://your-domain.com/install.php
```

填写数据库主机、用户名、密码、数据库名，提交后安装程序将：

1. 创建全部数据表（表前缀固定为 `group_`）
2. 写入默认站点配置、导航菜单、新闻分类、友情链接、轮播图与示例数据
3. 生成 `include/config.php`
4. 生成 `install.lock` 安装锁文件

安装完成后：

- 前台首页：`/`
- 后台入口：`/admin/login.php`
- 初始账号：`admin`
- 初始密码：`admin`

> 首次登录后请立即在「网站设置 → 账户设置」中修改用户名与密码。

### 3. 服务器配置

**Nginx**（站点地图重写，使 `/sitemap.xml` 输出动态内容）：

```nginx
index index.php index.html;

location = /sitemap.xml {
    rewrite ^/sitemap.xml$ /sitemap.php last;
}
```


## 目录结构

```text

├── index.php                  # 首页（轮播、新闻、成果、导师、研究方向）
├── install.php                # 安装向导（建表、写配置、生成 install.lock）
├── sitemap.php                # 动态输出 sitemap.xml
├── robots.txt                 # 搜索引擎抓取规则
├── nginx.htaccess             # Nginx 站点地图重写规则示例
├── include/
│   ├── config.php             # 数据库与站点常量（安装时生成）
│   ├── db.class.php           # mysqli 单例封装（查询 / 增删改）
│   ├── common.php             # 公共函数：站点配置、菜单、上传、统计、SEO
│   └── markdown.php           # 轻量 Markdown 解析器（标题/表格/图片/图标等）
├── templates/
│   ├── header.html            # 公共头部：SEO、导航、搜索
│   └── footer.html            # 公共底部：联系方式、友链、备案、统计
├── admin/                     # 后台管理（19 个页面）
│   ├── login.php / logout.php
│   ├── index.php              # 控制面板与访问统计
│   ├── config.php             # 网站设置与账户设置
│   ├── menu.php               # 导航菜单
│   ├── slide.php              # 轮播图
│   ├── friend_link.php        # 友情链接
│   ├── about.php              # 关于本站
│   ├── news.php               # 新闻动态
│   ├── news_category.php      # 新闻分类
│   ├── teacher.php / postdoc.php / master.php / doctor.php / graduate.php
│   ├── recruit.php            # 招生招聘
│   ├── research.php           # 研究成果
│   ├── research_direction.php # 研究方向
│   └── message.php            # 留言审核
├── about/                     # 关于我们
├── news/                      # 新闻列表 / 详情
├── teacher/                   # 导师团队列表 / 详情
├── postdoc/                   # 博士后团队列表 / 详情
├── doctor/                    # 博士团队列表 / 详情
├── master/                    # 硕士团队列表 / 详情
├── graduate/                  # 毕业生团队列表 / 详情
├── research/                  # 研究成果列表 / 详情
├── research_direction/        # 研究方向详情
├── recruit/                   # 招生招聘列表 / 详情
├── message/                   # 留言板
├── search/                    # 全站搜索
├── editor/                    # editormd + CodeMirror 前端资源
├── static/
│   ├── css/style.css          # 前台样式
│   ├── css/admin.css          # 后台样式
│   ├── js/main.js             # 轮播、移动端菜单、搜索框
│   └── images/                # Logo、默认背景图
└── upload/                    # 上传图片（按 年/月 归档）
```
技术支持：[yanweb.top](https://www.yanweb.top/)
