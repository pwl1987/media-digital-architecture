# Archaeology — video-compression-system

## 定位

小型专用媒体质量/压缩工程，不应继续演化成独立平台。

仓库元数据显示其核心描述为“FFmpeg 重编码 + VMAF/SSIM/PSNR 质量门禁”，语言为 Python，约 1.2MB，创建/近期更新均在 2026-06，且当前没有开放 Issue。fileciteturn172file0L2-L2

根目录同时存在 `main.py`、`cli.py`、`app/`、`config/`、`docs/`、`openspec/`、`plans/`、`tests/`，说明它已经有工程化骨架，但不能据此推断成完整产品。fileciteturn182file0L2-L2

## 可复用资产

- FFmpeg 编码参数策略。
- VMAF/SSIM/PSNR 质量判定。
- CLI/程序入口。
- 质量门禁设计和测试样例。

## 风险

- 根目录存在异常命名文件（如 `-encoders`、`csv=p=0`），提示仓库可能混入命令行输出/误操作产物，应在整理阶段清理。
- 具体 README/完整运行证据不足，不能把“存在 main/app/tests”解释为生产完成。
- 若自行发展 API、用户、项目、素材管理，会与 news-media/Media Processing 产生重复。

## 最终命运

**Extract / Freeze**

将它的编码与质量门禁提炼进统一 `Media Processing Contract`。仓库本身可保留为 reference implementation，冻结业务扩张。

## 目标调用链

```text
Media/Artifact
  ↓
Compression Job
  ↓
FFmpeg
  ↓
Quality Gate
  ↓
DeliveryArtifact
```
