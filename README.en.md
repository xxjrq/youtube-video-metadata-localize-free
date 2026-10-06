# YouTube Public Video Metadata Localization

Turn one authorized, publicly visible YouTube video into a reviewable Chinese metadata draft. Provide a video URL, Chinese audience guidance, and a chosen `browserId`; receive original-title/description points, Chinese title/description drafts, source URLs, and explicit gaps. It is read-only by default and never changes YouTube Studio.

![Promo image](assets/promo.png)

Install with `npx skills add xxjrq/youtube-video-metadata-localize-free`. This browser skill requires [Easy WebBridge on GitHub](https://github.com/xxjrq/easy-webbridge), with a [Gitee mirror](https://gitee.com/xxjrq/easy-webbridge). Use one user-selected browser environment and one task-owned session only.

Run `node scripts/self-test.mjs` for offline fixture validation. Fixtures simulate visible pages; they are not online collection results.

See [SKILL.md](SKILL.md) for browser workflow and boundaries.


## Translation is an Agent task

The Agent translates actual visible text and adapts wording to the requested Chinese audience while preserving facts. `compose-draft.mjs` only validates and assembles separately supplied translations; it is not a local general translator. Each translated title and point must retain its exact original, index, source URL and field. The Agent must review semantic fidelity; the script cannot prove it. Invisible descriptions remain empty.

```bash
node scripts/compose-draft.mjs --input fixtures/success-page.json --translations fixtures/success-translations.json --output /tmp/localized.json
```

An independent cycling-text case demonstrates [beginner wording](fixtures/forward-beginner.json) and [experienced-audience wording](fixtures/forward-experienced.json) from the same source facts. The [hidden-description case](fixtures/forward-failure.json) does not invent details. These are actual Agent translations assembled by an executed script from offline text materials; no browser, source-page visit, or online success is claimed. The self-test checks assembly, per-point provenance and four invalid-contract rejections, not translation quality.
