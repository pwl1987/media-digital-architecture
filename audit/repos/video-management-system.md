# Archaeology — video-management-system

## 定位

早期“视频管理一体化”原型：上传、转码、视频管理、AI 分析、HLS 剪辑、用户、监控全部放在一个应用。README 的技术栈为 Python3.12/FastAPI/SQLAlchemy、SQLite→PostgreSQL、Redis/Celery、FFmpeg/OpenCV、Whisper/OpenAI、Vue3/ElementPlus。fileciteturn181file0L2-L2

## 现实问题

1. 与 `news-media-system` + Media Processing Engines 存在明显职责重复。
2. “完整视频上传/转码/AI/HLS剪辑/监控”是产品目标描述，不等同于每条流程已经通过真实环境验证。项目本身规模较小，而 README 中存在重复目录和多版本使用说明，说明历史演进未完全收口。fileciteturn181file0L2-L2
3. SQLite、PostgreSQL、Redis/Celery、Vue/ElementPlus 等技术与当前目标基线存在明显分叉。
4. HLS 剪辑、AI 分析、上传、用户、监控一体化会造成“视频应用大单体”，不利于与统一 Media Asset/Artifact/Job 模型衔接。

## 可复用资产

- 视频上传/处理需求梳理。
- HLS clipping 产品交互思路。
- Whisper/AI 分析集成经验。
- Prometheus/Grafana 运维思路。

## 最终命运

**Freeze / Extract**

不继续恢复为独立视频平台。抽取真实有用的 HLS clipping、AI analysis、上传断点续传等需求，重新落到 Media Asset + Processing Job + Artifact 模型。

## 目标归位

```text
news-media-system
  ↓ Content/Asset
Media Processing
  ├── Transcode
  ├── Shot
  ├── ASR
  └── HLS Clip
  ↓
Artifact
```
