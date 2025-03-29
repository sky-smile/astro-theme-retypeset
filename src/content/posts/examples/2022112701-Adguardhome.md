---
title: AdguardHome配置
published: 2024-12-19
tags: ["AdguardHome","OpenWrt"]
lang: zh
abbrlink: adguardhome
---

# AdguardHome配置

AdguardHome简单设置及常用规则，方便我自己重装的时候使用。

## DNS设置

### 上游 DNS 服务器

上游使用openclash

```code
127.0.0.1:7874
```

### Bootstrap DNS 服务器

```
223.5.5.5
119.29.29.29
2400:3200::1
2400:3200:baba::1
```

## DNS拦截列表

按照需求勾选，规则数目不要太多，否则影响访问速度及使用体验。

```code
AdGuard DNS filter
https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt

CHN: anti-AD
https://anti-ad.net/easylist.txt

minority-mv
https://raw.githubusercontent.com/xinggsf/Adblock-Plus-Rule/master/minority-mv.txt

mv
https://raw.githubusercontent.com/xinggsf/Adblock-Plus-Rule/master/mv.txt

rule
https://raw.githubusercontent.com/xinggsf/Adblock-Plus-Rule/master/rule.txt

tvbox
https://raw.githubusercontent.com/vokins/yhosts/master/data/tvbox.txt

cjx-annoyance
https://raw.githubusercontent.com/cjx82630/cjxlist/master/cjx-annoyance.txt

大圣净化 - 针对国内视频网站
https://raw.githubusercontent.com/jdlingyu/ad-wars/master/hosts

去除大部分软件的开屏广告
https://raw.githubusercontent.com/banbendalao/ADgk/master/ADgk.txt

百度搜索结果内屏蔽百家号
https://raw.githubusercontent.com/banbendalao/ADgk/master/kill-baidu-ad.txt

常见国内app去广告
https://raw.githubusercontent.com/zqzess/rule_for_quantumultX/master/AdguardHome/TVAdBlock.txt

番茄小说广告屏蔽
https://raw.githubusercontent.com/zqzess/rule_for_quantumultX/master/AdguardHome/FanQieNovel.txt
```

## DNS允许列表

常见允许列表，即使在拦截列表内也允许。

```code
cats允许列表 Cats-Team/AdRules：常见允许列表
https://raw.githubusercontent.com/Cats-Team/AdRules/main/allow.txt

anti白名单
https://raw.githubusercontent.com/privacy-protection-tools/dead-horse/master/anti-ad-white-list.txt
```
