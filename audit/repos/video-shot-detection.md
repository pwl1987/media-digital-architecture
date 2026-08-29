# Archaeology — video-shot-detection

## 定位

**专业算法 Engine**，不是业务产品。README/V4.0 已形成较明确的镜头边界检测 pipeline：TransNetV2 + visual/motion/black/audio + adaptive fusion + NMS/postprocess，并提供 CLI/Gradio/API 形态。fileciteturn170file0L2-L2

## 可复用资产

- V4 pipeline 编排。
- 多模态校验与融合。
- FFmpeg 预处理/关键帧输出。
- 统一异常体系和 recovery hint。
- 结构化日志 + JSONL 审计。
- Path Traversal 与 subprocess timeout 防护。
- CSV/EDL/FFmpeg/关键帧导出。

## 主要问题

1. 产品入口使用 Gradio，适合算法验证，不应成为企业统一 UI。
2. 结果语义仍以 `scene` 为主，需要映射到母架构 `VideoShot`/`Artifact`。
3. 当前能力仍偏单次 pipeline；缺少统一 Job/Artifact/asset lineage。
4. 如果继续扩展大量业务管理页面，就会重新走“引擎变平台”的老路。

## 最终命运

**Extract**

保留源码作为 `Shot Detection Engine`；增加标准 API/Job/Artifact adapter，把检测输出注册为 `VideoShot` Artifact。

## 目标调用链

```text
Content/Media Asset
  ↓
Processing Job
  ↓
Shot Detection Engine
  ↓
VideoShot Artifacts
  ↓
Keyframe Artifacts / Events
```
