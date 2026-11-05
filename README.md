# cell_ppt

用于做pptx。

## 安装与配置

需要 Python 3.11 或更新版本。将本仓库克隆到 Codex 的 Skills 目录，文件夹名保持为 `cell_ppt`，例如：

```bash
git clone https://github.com/yrui-cmd/cell_ppt.git ~/.codex/skills/cell_ppt
cd ~/.codex/skills/cell_ppt
```

如设置了 `CODEX_HOME`，请改用其下的 `skills/cell_ppt`。在实际运行 Skill 的 Python 环境中执行：

```bash
python -m pip install -r requirements.txt
python -X utf8 scripts/ppt_credentials.py setup
python -X utf8 scripts/ppt_credentials.py check
```

`setup` 隐藏输入自己的 PPT 客户端密钥。Windows 用 DPAPI 加密，macOS 使用系统钥匙串；不要分发 `config/`。更新时在本仓库目录执行 `git pull --ff-only`。本机 `config/` 已加入忽略规则，不会上传到 GitHub。

## 使用

安装后重启 Codex 并新建聊天。本仓库可独立使用，无需安装 Cell 总入口。源码采用 [MIT 许可](LICENSE)。

在 Codex 中说“使用 cell_ppt”并提供主题、论文、图片或参考模板。流程先检查 API，再逐项问答，准备逐页安排与资料包，确认版本及报价后才上传制作。完整规则见 [SKILL.md](SKILL.md)。

新接口只上传一份交接 PDF。服务从内嵌 `ppt-material-index.json` 读取最终 PPT 内容页数，每页 1 个 PPT 页额度；模板、问答、资料和正文续页不另计费。规划及模板 PPTX 留在本地审阅。进度面板展示估算时间和订单状态；重复查询及恢复沿用原订单。上传确认入队并打开进度面板后，聊天立即停止，只保留进度入口；后台继续更新进度，并在完成后下载、校验成品 PPTX 和启动预览。

元素预览需要桌面版 Microsoft PowerPoint，Windows 通过 PowerShell/COM、macOS 通过 AppleScript 控制独立预览副本。macOS 首次可能要求自动化授权。Linux 可用于部分离线工具，但不支持当前凭据配置及桌面预览流程。

代码依赖固定外部接口 `https://xiaomiao-ai.com/api/ppt/v1`，首次使用应持有该服务的 PPT 客户端密钥和足够页额度。开源不代表远端制作免费，也不包含 PowerPoint 软件许可。

## 逐页内容规划

先逐项确认风格、受众、页数、语言、比例（推荐 16:9）、可选模板以及时间、重点、范围和资料，再直接整理 `outline.json`，不生图。每页包含实际正文、排版、素材依据和制作注释。交接 PDF 按“问答 → 模板 → 资料 → PPT内容”排列，开头标明 PPT 总页数和模板，每页内容以 `# 第 N 页：标题` 开头。文件版本与额度确认后，沿用原有上传和后台进度流程。
