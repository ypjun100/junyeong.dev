# [junyeong.dev](https://junyeong.dev)

개인 포트폴리오 겸 기술 블로그입니다. 글은 모두 `content/` 아래의 마크다운 파일에서 읽어 옵니다.

## 로컬 실행

```bash
bundle install
bundle exec jekyll serve
```

`http://127.0.0.1:4000`에서 열립니다.

## 검증

```bash
bundle exec jekyll build --strict_front_matter
bundle exec htmlproofer _site --disable-external --allow-hash-href --ignore-missing-alt
```

## 배포

`main`에 푸시하면 `.github/workflows/pages.yml`이 빌드와 링크 검사를 거쳐 GitHub Pages로 배포합니다.

## 글 추가하기

작성 규칙과 front matter 스키마는 [AGENTS.md](AGENTS.md)에 있습니다.

## Analytics

The site reports to Google Analytics 4 through the web stream `G-JVGDLR3RB9` (`analytics.measurement_id` in `_config.yml`). `_includes/analytics.html` renders the Google tag only into production builds (`JEKYLL_ENV=production`, which the deploy workflow sets) that have a non-empty ID, and the script returns before loading anything unless the page is served from the host in `site.url`, `junyeong.dev`. `jekyll serve`, local builds, and a production build opened on localhost or a preview host send nothing. To read the rendered tag locally, build with `JEKYLL_ENV=production`. A running `jekyll serve` has to be restarted to pick up a changed ID.

### Collected data

Page views are the `page_view` that the `config` call sends by default. Every event on a page also carries:

| Parameter | Value |
| --- | --- |
| `content_group` | `home`, `about`, `posts`, `blog`, `project`, `award`, or `other` |
| `content_category` | Blog posts only: the first entry of `categories`, or `uncategorized` |

`content_category` compares posts by their first category alone, so `일상` covers the travel posts along with every other everyday post.

Three custom events mark intent on specific links, activated by a primary click, keyboard, or middle click. Right clicks are ignored. Each carries only `link_type` and `link_location`, never the URL, the link text, or the email address.

| Event | Links | `link_type` | `link_location` |
| --- | --- | --- | --- |
| `contact_click` | Sidebar email | `email` | `sidebar` |
| `profile_click` | Sidebar GitHub and LinkedIn | `github`, `linkedin` | `sidebar` |
| `portfolio_link_click` | Project and award header links from `urls`, internal ones included | The link's `type` if it is `github`, `youtube`, `website`, `news`, or `link`; otherwise `other` | `content_header` |

A click is an attempt, not an outcome: `contact_click` means a mail app was asked to open, not that a message was sent. Navigation is never held back for an event, so a click made while the tag is blocked or right before the page unloads can go unrecorded. Outbound links also raise enhanced measurement's `click`, which counts all outbound navigation, while the custom events count intent in the areas above. Compare the two; never add them up.

### Property setup

Settings in the GA4 property do not follow from this repository. Check them in the property:

1. The web stream's URL is `https://junyeong.dev` and its measurement ID is `G-JVGDLR3RB9`.
2. Enhanced measurement (Admin > Data collection and modification > Data streams > the stream): keep page views, scrolls, outbound clicks, and file downloads on. Under the page views advanced settings, turn off **Page changes based on browser history events**; every navigation on this site is a full page load. Turn off site search and form interactions, since the site has neither. Video engagement only reports YouTube embeds with JS API support (`enablejsapi=1`), which none of the current embeds have.
3. Register three event-scoped custom dimensions under Admin > Data display > Custom definitions: `content_category`, `link_type`, and `link_location`. `content_group` already reports as the built-in **Content group** dimension, so don't register it. New dimensions can take 24–48 hours to reach reports.
4. Once `contact_click` has arrived, mark it as a key event (Admin > Data display > Events, star icon). It stands for an email attempt, not a lead or a hire. Leave `profile_click` and `portfolio_link_click` as interest signals.
5. Leave **Google signals data collection** off (Admin > Data collection and modification > Data collection); the tag already sends `allow_google_signals: false` and `allow_ad_personalization_signals: false`. Keep email data redaction on (the stream's **Redact data** setting, on by default for new properties) and keep personal data out of URL query strings. Enhanced measurement records page and link URLs on its own, so leaving them out of the custom events does not keep them out of the property.
6. Decide the cookie and data-collection notice before deploying. The tag sets the first-party `_ga` and `_ga_<container-id>` cookies, kept for two years by default, and turning Google signals off does not stand in for consent. If consent is needed, the site has to ask before the tag loads and keep and withdraw the choice. Consent Mode does neither; it only adjusts the tag to a choice the site supplies. That needs its own change before deploying.
7. Confirm reception on the live domain in Realtime, and in DebugView through Tag Assistant (tagassistant.google.com) rather than a `debug_mode` flag in the code. Those visits land in the property as real traffic, so keep them few. Local checks should intercept requests to Google instead of reporting into the property.

### Possible additions

Not built. Settle the question each one would answer before adding it.

- `article_read`: once per page, when a blog post's body has been scrolled to 90% and the tab has been visible for 30 seconds in total. Tells reading a long post apart from skimming it. It is strict on short posts and still not proof the post was read. The built-in `scroll` only means 90% of the whole page came into view.
- `image_view`: when the lightbox opens. Compares interest in project screenshots and travel photos. Send `content_group` and the image's position on the page, not its URL.
- `content_category_secondary`: the second category as its own parameter, if the first proves too coarse.

A funnel exploration of visit → content → outbound link or email attempt fits the site: source / medium for acquisition, page path and title with `content_group` and `content_category` for content, and the custom events for intent. Data starts on the day the tag ships, and click differences on small samples say little about hiring.
