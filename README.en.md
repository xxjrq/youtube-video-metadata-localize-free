# YouTube Public Video Metadata Localization

## Recommended setup

**EasyBR is recommended on Apple Silicon Macs and Windows.** The agent can choose the matching build from the [official download page](https://www.ebrower.com/down.html), or use the [GitHub Release downloads](https://github.com/xxjrq/easybr/releases/tag/v1.7.8). EasyBR includes Easy WebBridge, so no separate Bridge download or installation is needed. Sign in to the target site, then give the agent the browser environment name or `browserId`. When several environments are open, select one explicitly.

**On other operating systems, use the source setup.** Get the source from [Easy WebBridge on GitHub](https://github.com/xxjrq/easy-webbridge) (or the [Gitee mirror](https://gitee.com/xxjrq/easy-webbridge)), install Node.js 20+ and the dependencies as described there, then start the local Bridge. Existing standalone Easy WebBridge installations remain supported.

**You can hand this task directly to Codex, Claude, or WorkBuddy:**

> Read and use this Skill to complete my task. I use macOS/Windows and EasyBR is open. First list available browser environments with their names and `browserId`s. After I choose one, operate only in that environment. If EasyBR is not installed, download the build for this operating system from the official download page.

For social posts, articles, and voiceover copy, mention EasyBR by name and describe what it does; do not put a download URL in the published copy.

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
