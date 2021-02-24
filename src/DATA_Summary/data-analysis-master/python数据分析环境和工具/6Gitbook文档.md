Gitbook文档
===

---

Gitbook：生成文档和电子书

* 每次修改文档后执行命令生成网页文档：

```bash
gitbook build --gitbook=2.6.7
```

---

安装Gitbook
---

1. 安装Node.js（见下载软件）
1. 检查Node.js是否安装成功：
    * `node -v`
1. 安装Gitbook（在线安装）
    * 终端执行命令：`npm install -g gitbook-cli`
    * 检查：`gitbook -V`

---

使用Gitbook
---

* 新建目录，终端进入新建目录
* 创建gitbook文档：`gitbook init` （新建目录后只能执行一次，第一次执行命令会联网下载gitbook）
* 预览：`gitbook serve`，关闭预览`ctrl+c`
* 生成HTML文档：`gitbook build --gitbook=2.6.7`（第一次执行会联网下载包）

---

生成pdf和mobi电子书
---

* 安装Calibre（见下载软件）
* 执行命令：
    * `gitbook pdf`
    * `gitbook mobi`

#### 电子书封面图片

图像大小建议：1800*2360 像素并且遵循建议：
图片的格式为 jpg 格式。把图片重命名为cover.jpg放到电子书项目文件夹即可

* 没有边框
* 清晰可见的书本标题
* 任何重要的文字在小版本中应该可见



