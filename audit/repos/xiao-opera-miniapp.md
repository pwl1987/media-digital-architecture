# Archaeology — xiao-opera-miniapp

## 定位

公众文化消费端候选产品，保留为 `Yimeng Culture / Consumer Experience`。README 的产品构想包括戏曲展演、直播、音频、AI 创作、活动、用户中心与社交。fileciteturn178file0L2-L2

## 现实状态判断

README 的能力清单明显大于当前可验证的后端闭环。项目是微信原生小程序，数据层主要是本地缓存/数据管理器；因此不能把“用户系统、推荐、版权保护、社区”等描述理解成已经形成生产后端能力。fileciteturn178file0L2-L2

此前代码审计还发现 AI service 存在模拟生成路径，因此 AI 功能不能直接视为生产级真实能力。

## 高价值资产

- 小程序信息架构。
- 文化内容消费场景。
- 音频播放器/视频体验。
- AI 创作交互原型。
- 文化活动/内容发现的产品思路。

## 应重建的部分

- 登录/身份不应自行维护为孤立用户体系。
- AI 调用应走统一 Business/Intelligence API。
- 内容与媒体应引用 Canonical Asset/Content，而非本地 mock 数据。
- AI 创作结果必须带 Generation / Evidence / Provenance。

## 最终命运

**Rebuild as Consumer Experience**

保留产品原型与交互资产，重做数据/API/AI 接入；不让小程序直接访问任何数据库或 AI provider。

## 目标链路

```text
MiniApp
  ↓
Business API / Experience Gateway
  ↓
Content / Live / Intelligence
  ↓
Canonical Content + Asset + AIResult
```
