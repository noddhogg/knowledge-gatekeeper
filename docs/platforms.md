# 平台适配清单

> 本文件回答一个问题：**你收藏的东西，能从哪些平台拿进来？**
>
> 本仓库**不做获取的实现**，只做获取的**集成**——把能力边界查清楚，告诉你用什么、能到哪、卡在哪。

数据来源：`yt-dlp` 提取器清单，版本 **2026.06.09**，共 **1747** 个提取器。
所有数字由本机实测导出，方法见文末「怎么复核」。**版本变了数字就会变**，请以你自己的实测为准。

---

## 三条红线

没有边界的"广泛"就是下限失守。这三条不是自我设限，是专业性。

| # | 红线 | 具体含义 |
|---|---|---|
| 1 | **不写下载器，用现有工具集成** | 获取能力来自 `yt-dlp` 这类成熟项目。我们只维护清单与接入约定，不分发下载代码 |
| 2 | **不绕风控，不写任何规避手段** | 遇到频率限制、登录墙、验证码，就减速、登录、或放弃。不提供绕过方案，**也不讨论** |
| 3 | **不碰付费 / 隐私 / DRM 内容** | 付费课程、需登录才能看的私人收藏、DRM 加密内容，一律不纳入。拿不到就跳过 |

第三条尤其适用于下面清单里标注「付费」的入口——例如 B 站 `cheese`（课堂）是付费课程，
提取器存在 **不代表** 我们建议去拉。列出来是为了说明"它存在且有这个限制"，不是发通行证。

---

## 支持清单

**表头说明**

- **提取器数** —— 该平台在 `yt-dlp` 中的提取器条目数。数字大 ≠ 能力强，多数是同一站点的不同入口（单条 / 收藏夹 / 搜索 / 专辑……）
- **能力** —— 由提取器名称直接读出，例如 `favoriteslist` 就是收藏夹
- **接入** —— 统一走 `yt-dlp <url>`；标注「需登录」的入口要带 cookies

### 国内视频

| 平台 | 类型 | 提取器数 | 主要入口（能力） | 限制 |
|---|---|---|---|---|
| **B 站** `bilibili` | 视频 | 19 | 单视频 `BiliBili`、收藏夹 `BilibiliFavoritesList`、稍后再看 `BilibiliWatchlater`、UP 主投稿 `BilibiliSpaceVideo` / 音频 `BilibiliSpaceAudio`、合集 `BilibiliCollectionList` / 系列 `BilibiliSeriesList`、搜索 `BiliBiliSearch`、分类 `Bilibili category extractor`、动态 `BiliBiliDynamic`、番剧 `BiliBiliBangumi`（含 season / media）、音频 `BilibiliAudio`（含 album）、播放器 `BiliBiliPlayer`、播放列表 `BilibiliPlaylist` | 收藏夹 / 稍后再看 / 动态 **需登录**；`BilibiliCheese` 与 `BilibiliCheeseSeason` 是**付费课堂**，见红线 3 |
| **抖音** `douyin` | 短视频 | 1 | 单条视频 `Douyin`，匹配 `douyin.com/video/<id>` | 只有单条入口，无收藏夹 / 主页；风控较严，易触发限制，见红线 2 |
| **小红书** `xiaohongshu` | 短视频 | 1 | 单篇 `XiaoHongShu`，匹配 `xiaohongshu.com/explore/<id>` 与 `/discovery/item/<id>` | 只有单篇入口；产出为视频，**图文笔记不在范围内**；需登录态，失败率高 |
| **微博** `weibo` | 视频 | 3 | 单条 `WeiboVideo`、用户 `WeiboUser`、主站 `Weibo` | 主页类入口需登录 |
| **知乎** `zhihu` | 视频 | 1 | 仅 `zhihu.com/zvideo/<id>`（知乎视频） | **只匹配视频，回答与文章正文不在范围内**——那是网页抓取，本仓库不涉及 |
| **优酷** `youku` | 长视频 | 2 | 单视频 `youku`、节目 `youku:show` | 会员内容需登录，见红线 3 |
| **爱奇艺** `iqiyi` | 长视频 | 1 | 单视频 `iqiyi` | 会员内容需登录，见红线 3 |
| **腾讯视频** `vqq` | 长视频 | 2 | 单视频 `vqq:video`、剧集 `vqq:series` | 会员内容需登录，见红线 3 |
| **西瓜视频** `Ixigua` | 中长视频 | 1 | 单视频 `Ixigua` | 只有单条入口 |
| **今日头条** `toutiao` | 图文 / 视频 | 1 | 单条 `toutiao` | 只有单条入口 |
| **梨视频** `pearvideo` | 短视频 | 1 | 单条 `pearvideo` | 只有单条入口 |
| **A 站** `acfun` | 视频 | 2 | 单视频 `AcFunVideo`、番剧 `AcFunBangumi` | — |
| **斗鱼** `douyu` | 直播 | 2 | 直播间 `DouyuTV`、节目 `DouyuShow` | 直播为实时流，录制需自行处理时长与存储 |
| **虎牙** `huya` | 直播 | 2 | 直播 `huya:live`、视频 `huya:video` | 同上 |

### 国内音频

| 平台 | 类型 | 提取器数 | 主要入口（能力） | 限制 |
|---|---|---|---|---|
| **喜马拉雅** `ximalaya` | 音频 / 播客 | 2 | 单条 `ximalaya`、专辑 `ximalaya:album` | 付费专辑见红线 3 |
| **网易云音乐** `netease` | 音乐 / 电台 | 7 | 歌曲 `netease:song`、专辑 `netease:album`、MV `netease:mv`、歌单 `netease:playlist`、歌手 `netease:singer`、节目 `netease:program`、**电台 `netease:djradio`** | 音乐版权受限，多数仅可下 MV 或试听片段；**版权内容不碰**，见红线 3 |
| **QQ 音乐** `qqmusic` | 音乐 | 6 | 歌曲 `qqmusic`、专辑 `qqmusic:album`、MV `qqmusic:mv`、歌单 `qqmusic:playlist`、歌手 `qqmusic:singer`、榜单 `qqmusic:toplist` | 同上，版权内容不碰 |
| **蜻蜓 FM** `qingting` | 音频 / 播客 | 1 | 单条 `qingting` | 只有单条入口 |

### 海外

| 平台 | 类型 | 提取器数 | 主要入口（能力） | 限制 |
|---|---|---|---|---|
| **YouTube** `youtube` | 视频 | 20 | 单视频、播放列表、音乐搜索、短片 `youtube:shorts:pivot:audio`、订阅 `youtube:subscriptions`、推荐 `youtube:recommended`、稍后再看 `youtube:watchlater`、收藏 `youtube:favorites`、历史 `youtube:history`、搜索 `youtube:search`、用户 `youtube:user`、频道 tab、clip、通知等；另有嵌入场景 `YoutubeYtBe` / `YoutubeLivestreamEmbed` 与截断处理 `youtube:truncated_id` / `truncated_url` | 订阅 / 收藏 / 历史 / 推荐 **需登录**；会员内容见红线 3 |
| **TikTok** `tiktok` | 短视频 | 7 | 单条 `TikTok`、用户 `tiktok:user`、合集 `tiktok:collection`、直播 `tiktok:live`；短链 `vm.tiktok` 另有独立条目 | **`tiktok:effect` / `tiktok:sound` / `tiktok:tag` 三个在 yt-dlp 中标注 CURRENTLY BROKEN**，不要用 |
| **Vimeo** `vimeo` | 视频 | 11 | 单视频 `vimeo`、频道 `vimeo:channel`、专辑 `vimeo:album`、用户 `vimeo:user`、稍后再看 `vimeo:watchlater`、喜欢 `vimeo:likes`、活动 `vimeo:event`、群组 `vimeo:group`、审查页 `vimeo:review`、Pro `vimeo:pro`、点播 `vimeo:ondemand` | 稍后再看 / 喜欢需登录；`vimeo:ondemand` 是**付费点播**，见红线 3；部分内容需密码 |
| **SoundCloud** `soundcloud` | 音频 | 9 | 单曲 `soundcloud`、歌单 `soundcloud:playlist` / `soundcloud:set`、用户 `soundcloud:user`（含 `soundcloud:user:permalink`）、搜索 `soundcloud:search`、相关推荐 `soundcloud:related`、电台 `soundcloud:trackstation`、嵌入 `SoundcloudEmbed` | 需登录的内容见红线 3 |
| **Twitter / X** `twitter` | 视频 / 图文 | 6 | 单条 `twitter`、卡片 `twitter:card`、语音 Spaces `twitter:spaces`、广播 `twitter:broadcast`、Amplify `twitter:amplify`、短链 `twitter:shortener` | 需登录，风控较严 |
| **Reddit** `reddit` | 视频 / 图文 | 1 | 单条 `reddit` | 只有单条入口 |
| **Apple Podcasts** | 播客 | 1 | 单节目 `ApplePodcasts` | 见下方播客说明 |

---

## 不支持清单

| 平台 / 类型 | 状态 | 为什么 / 怎么办 |
|---|---|---|
| **快手**（含 Kwai / GIF 快手的国际版） | **不支持** | 本机实测：提取器清单中 `kuaishou`、`kwai`、`gifshow` 均为 **0** 条匹配。需专门工具，本仓库不集成 |
| **微信视频号** | **不支持** | 实测：清单中 `weixin`、`wechat` 均为 **0** 条匹配。视频号无公开直链，不提供绕行方案（红线 2） |
| **Spotify** | **不支持** | 实测：清单中 `spotify` 为 **0** 条匹配。且其内容受 **DRM** 保护——即使有工具也属红线 3，**不做** |
| **播客 RSS** | **不通用** | 实测：清单中 `rss` 为 **0** 条匹配——**没有通用 RSS 提取器**。另有 **20 个平台专属**播客提取器（含上表的 `ApplePodcasts`，以及 `RadioFrancePodcast`、`tunein:podcast`、`NoicePodcast`、`zingmp3:podcast` 等），**逐个站点专用，不覆盖你订阅的任意播客**。**自解析 RSS 成本很低**：RSS 是标准 XML，`<item>` 里直接有 `<enclosure url>` 音频直链，一次 `GET` + XML 解析即可拿到链接，再交给 `yt-dlp` 下载。**这是最划算的自建路径** |
| **猫耳 FM** `missevan` | **不支持** | 实测 0 条匹配 |
| **好看视频** `haokan` | **不支持** | 实测 0 条匹配 |
| **秒拍** `miaopai` | **不支持** | 实测 0 条匹配 |

> 上表中的「0 条匹配」均来自本机 `yt-dlp --list-extractors` 实测，非印象判断。

---

## 通用提醒（跨所有平台）

这些是集成时必然遇到的，不是某个平台的问题：

1. **批量连续请求会触发频率限制。** 正常做法是减速、分批、加间隔。**不做规避**（红线 2）。
2. **长任务中凭据会失效，需要自动重建。** 跑几小时后 cookie 过期是常态，设计时要预期到。
3. **单条失败不应中断整批。** 记进账本的 `fail_reason` 与 `retry_count`，继续下一条。
4. **需登录的入口用 `--cookies-from-browser`**（已核实该参数存在于 2026.06.09 版）。
   注意：这只适用于**你本人有权访问**的内容。
5. **只要清单不要视频时，用 `--skip-download` + `--flat-playlist`**（均已核实）。
   `--flat-playlist` 只取条目不展开，比全量解析快得多，适合做增量对账。
6. **只要音轨用 `-x` / `--extract-audio`**，能显著省下存储与后续转写的时间。

---

## 怎么复核

数字会随版本变化。任何人都可以用下面这条命令自己验证，不必相信本文：

```bash
# 总数
yt-dlp --version
yt-dlp --list-extractors | wc -l

# 单平台
yt-dlp --list-extractors | grep -ci "^bilibili"
yt-dlp --list-extractors | grep -ci "^youtube"

# 看某个平台的全部入口
yt-dlp --list-extractors | grep -i "^bilibili"

# 查某平台是否损坏（yt-dlp 会直接标注）
yt-dlp --list-extractors | grep -i "^tiktok" | grep -i BROKEN

# 官方描述（部分提取器没有描述，此时看源码最准）
yt-dlp --extractor-descriptions | grep -i "^Zhihu"

# 查某提取器到底匹配哪些 URL —— 判断"能不能接"的最终依据
grep -A2 "_VALID_URL" "$(python -c 'import yt_dlp,os;print(os.path.dirname(yt_dlp.__file__))')/extractor/zhihu.py"
```

> **能力栏怎么写才不会错**：从提取器名与 `_VALID_URL` 正则**直读**，不要靠印象。
> 本文在核对时就靠这一条抓出了三处错：Vimeo 没有「影集 / 系列」、
> SoundCloud 没有「专辑 / 标签」、Twitter 没有「时间线 / 社区」——
> 三者都是凭印象写出来的，实际入口完全不同。

**计数口径**（重要，否则对不上数）：按**提取器名前缀**统计。
两个易错的例外：

- `web.archive:youtube` 是 archive.org 的存档包装，**不算** YouTube 提取器 → 不以前缀 `youtube` 开头，故 YouTube 为 20 而非 21
- `vm.tiktok` 是短链主机的独立条目，**不算** TikTok 提取器 → 不以前缀 `tiktok` 开头，故 TikTok 为 7 而非 8

---

## 贡献

欢迎补充平台条目，但**必须附实测输出**——只写"某平台支持"而不给命令与结果的 PR 会被关闭。

格式照上表：平台 / 类型 / 提取器数 / 主要入口 / 限制，并在 PR 里贴出你的 `yt-dlp --version` 与 grep 结果。

**不接受**：下载器、抓站脚本、风控规避手段。详见 [`../CONTRIBUTING.md`](../CONTRIBUTING.md)。
