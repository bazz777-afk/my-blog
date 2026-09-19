# my-blog

个人技术博客，用 MkDocs + Material 主题写，推送到 main 后由 GitHub Actions 自动发布到 GitHub Pages。

- 网站地址：<https://bazz777-afk.github.io/my-blog/>
- 部署流程：`.github/workflows/deploy.yml`

## 本地预览

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows；macOS / Linux 用 source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve                    # 浏览器打开 http://127.0.0.1:8000
```

改文件会自动热重载。提交前跑一次严格构建，坏链接会直接报错：

```bash
mkdocs build --strict
```

## 写一篇新文章

1. 在 `docs/` 下新建 Markdown 文件，建议按「日期-标题」命名，例如 `docs/posts/2026-09-19-hello.md`。
2. 在 `mkdocs.yml` 的 `nav` 里登记这个文件，否则它不会出现在侧边栏。
3. 本地 `mkdocs serve` 看过效果满意后，再提交推送。

## 目录结构

```
docs/
  index.md              首页
  first-post.md         第一篇博客
mkdocs.yml              站点配置（导航、主题、站点信息）
requirements.txt        依赖版本（固定版本，保证 CI 和本地一致）
.github/workflows/      GitHub Actions 部署流程
```

## 两个容易踩的坑

- `nav` 里写错路径**不会**让构建失败，只会让那一项从侧边栏消失、指向它的链接变成死链。所以本地要跑 `mkdocs build --strict`（CI 里也已经开了）。
- 文章文件必须放在 `docs/` 下。多套一层目录（例如 `docs/docs/`）它就不算进站点，会变成一个奇怪的地址。
