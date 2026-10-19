# CineMatch Studio · v0.3.1 实验版

[**点击下载 Mac 安装包**](https://github.com/Huajuan001/Alex/raw/refs/tags/v0.3.1/CineMatchStudio-v0.3.1-Monterey.zip)

## Monterey 12.7.6 修复

v0.3.1 修正上一版将最低系统误设为 macOS 13 的问题。安装器和调色应用的最低版本均改为 12.0，安装脚本接受 12.7.6。已静态核对 270 个 Intel 依赖切片的最低系统声明，均不高于 12.0；这不等于已在 Mac 实机运行。

请使用新解压的 **v0.3.1** 文件夹里的安装器。旧下载包不会自动更新；可从旧版安装状态直接备份升级。此修复针对 CineMatch 安装器，不改变 Resolve 自身的系统和硬件支持范围。

## 使用

1. 下载并解压 `CineMatchStudio-v0.3.1-Monterey.zip`。
2. 打开“安装 CineMatch Studio.app”，等待安装完成。首次需要联网下载约 180–250 MB 的独立运行环境，无需手动配置 Python 或运行终端命令。
3. 完全退出并重新打开 DaVinci Resolve，从“工作区 → 脚本 → CineMatch Studio”启动；也可能在 Utility 分组。
4. 选择 sRGB 或 DWG/Intermediate 模式。包内“DWG 示例”可先用于试跑。

目标 macOS 12 Monterey 及以上，Intel / Apple Silicon。开发版尚未签名/公证，如系统阻止，请按 macOS 提供的“打开”或“隐私与安全性 → 仍要打开”流程处理。

## 工作空间与限制

- sRGB 模式：普通显示参考图片；生成 sRGB→sRGB LUT，不可直接套到 Log / DWG。
- DWG 模式：源图须是真正编码为 DWG/Intermediate 的全范围 RGB16/浮点 TIFF；参考图为 sRGB。生成 DWG→DWG 的 33³ 调色 LUT，放在输出变换之前。编码域限 0..1。
- 相机原生 Log 必须先正确转换到 DWG；已由工程色彩管理转换时不要重复 CST。
- 名称含 `View` 的 LUT 是诊断显示变换，用于复现预览，不应与另一套输出显示变换叠加。预览与 Resolve DRT 不同。
- 当前帧读取和节点加载仍为手动流程；未调用未经本机文档核验的 Resolve API。

当前为全局统计匹配原型，没有语义肤色保护、局部遮罩或跟踪。

## 验证

Linux CPython 3.11 下完整测试 **117 项通过**，含独立色彩数学对照、HDR/强度/输入精度、双 LUT 预览、GUI、Lua 及安装升级/回退测试。macOS 安装、Resolve 21 菜单和实际输出一致性尚待实机验证。

完整源码、测试和文档在安装器包 `Contents/Resources/project` 中。界面内可点击“保存 Resolve 诊断信息”。日志在 `~/Library/Logs/CineMatchStudio/`。

同目录的 `.sha256` 文件提供安装包校验值。
