---
title: "[iOS]既存サイトをアイコン指定してホーム画面に追加でアプリ化する"
date: 2020-06-11T00:00:22+09:00
img: ios-all-site-pwa
categories: ["Web"]
tags: ["ブログ","Web","サイトマップ","Google","Bing","GoogleSearchConsole"]
draft: true

---

```
data:text/html;charset=utf-8,<html><head><title>タイトル</title><meta name=apple-mobile-web-app-capable content=yes><meta name=apple-mobile-web-app-status-bar-style content=black><meta name=viewport content="width=device-width,initial-scale=1"><link rel=apple-touch-icon href=/seo/apple-touch-icon.png></head><body style=margin:0><script>if(!window.navigator.standalone){document.write("このページをホームに追加してください")}</script><iframe src="http://seig-boys.com/" width=100% height=100% frameborder=0></iframe></body></html>
```

```
data:text/html;charset=utf-8,<html><head><title>タイトル</title><meta name=apple-mobile-web-app-capable content=yes><meta name=apple-mobile-web-app-status-bar-style content=black><link rel=apple-touch-icon href=/seo/apple-touch-icon.png><meta name=viewport content="width=device-width,initial-scale=1"><script>if(window.navigator.standalone){location.href="https://mawatari.jp/"}else{document.write("このページをホームに追加してください")}</script></head></html>
```

```
data:text/html;charset=utf-8,<html><head><script>if(window.navigator.standalone){location.href="https://mawatari.jp/"}else{document.write("このページをホームに追加してください")}</script></head></html>
```

