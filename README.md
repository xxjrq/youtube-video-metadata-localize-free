# YouTube 公开视频元数据中文化

把一个已授权、公开可见的 YouTube 视频页面整理成适合中文受众审阅的标题与简介草稿。输入是**一个公开视频 URL、中文受众要求和指定 browserId**；结果包括原题/简介要点、中文标题/简介草稿、真实来源链接与明确缺项。默认只读，不修改 YouTube 后台。

![推广图](assets/promo.png)

## 适用场景

上线前审阅公开视频的中文元数据；当简介读不到或主张不清晰时，Skill 保留原词并标注待确认，而不是编造内容。

## 安装与使用

```bash
npx skills add xxjrq/youtube-video-metadata-localize-free
```

这是浏览器 Skill，需要先安装 Easy WebBridge：主下载 [GitHub](https://github.com/xxjrq/easy-webbridge)，备用 [Gitee](https://gitee.com/xxjrq/easy-webbridge)。每次运行必须由用户指定一个 `browserId`；Skill 只管理自己的 session 和标签组，不广播到多个账号。

完整工作流、只读边界和离线整理器见 [SKILL.md](SKILL.md)。可独立验收：

```bash
node scripts/self-test.mjs
```

## 翻译与组装

Agent根据原页面可见文字执行中文翻译，按受众调整术语解释与句式，原文事实保持一致。脚本只校验/组装Agent译文，要求每条保留原文、编号、来源URL与字段，不提供本地自动通用翻译。不可见简介不译，模糊术语保留原词并列待确认。译文语义仍由Agent对照原文复核。

```bash
node scripts/compose-draft.mjs --input fixtures/success-page.json --translations fixtures/success-translations.json --output /tmp/localized.json
```

独立骑行材料示例：[入门受众输入](fixtures/new-input-beginner.json) → [实际中文交付](fixtures/forward-beginner.json)；[熟悉装备的受众输入](fixtures/new-input-experienced.json) → [实际交付](fixtures/forward-experienced.json)。两版事实相同，前者用日常词，后者保留Bikepacking术语。[简介不可见输入](fixtures/new-input-failure.json) → [限制交付](fixtures/forward-failure.json)。实际结果由Agent先写译文，再真实运行组装脚本生成。

fixtures 是离线文字材料，示例视频地址未在线访问，不代表已跑通浏览器工作流。自检校验两受众组装、逐项来源、不可见简介及四种错误合同拒绝；不代替真实翻译语义验收。

## 来源与许可

业务用途参考了 [social-media-skills/skills](https://github.com/social-media-skills/skills) 中的 YouTube 元数据主题；本仓库的说明、流程和代码为原创实现，未复制其文本或源码。见 [LICENSE](LICENSE)。
