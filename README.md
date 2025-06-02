# 文件说明
## rule分支
### 下载地址

| 文件名 | Github release | JSdelivr | go-proxy|
|-|-|-|-|
| Country.mmdb | [下载](https://github.com/linzja/domain-list-custom/releases/download/rule/Country.mmdb) [下载2]( https://raw.githubusercontent.com/linzja/domain-list-custom/refs/heads/rule/Country.mmdb) | [下载](https://cdn.jsdelivr.net/gh/linzja/domain-list-custom@rule/Country.mmdb)  | [下载](https://gh-proxy.com/github.com/linzja/domain-list-custom/releases/download/rule/Country.mmdb)|
| geoip.dat | [下载](https://github.com/linzja/domain-list-custom/releases/download/rule/geoip.dat) [下载2](https://raw.githubusercontent.com/linzja/domain-list-custom/refs/heads/rule/geoip.dat)  | [下载](https://cdn.jsdelivr.net/gh/linzja/domain-list-custom@rule/geoip.dat)                                                        | [下载](https://gh-proxy.com/github.com/linzja/domain-list-custom/releases/download/rule/geoip.dat)                                                       |
| geosite.dat         | [下载](https://github.com/linzja/domain-list-custom/releases/download/rule/geosite.dat) [下载2](https://raw.githubusercontent.com/linzja/domain-list-custom/refs/heads/rule/geosite.dat)                                 | [下载](https://cdn.jsdelivr.net/gh/linzja/domain-list-custom@rule/geosite.dat)                                                     | [下载](https://gh-proxy.com/github.com/linzja/domain-list-custom/releases/download/rule/geosite.dat)                                                     |
| GeoLite2-ASN.mmdb   | [下载](https://github.com/linzja/domain-list-custom/releases/download/rule/GeoLite2-ASN.mmdb) [下载2](https://raw.githubusercontent.com/linzja/domain-list-custom/refs/heads/rule/GeoLite2-ASN.mmdb)                              | [下载](https://cdn.jsdelivr.net/gh/linzja/domain-list-custom@rule/GeoLite2-ASN.mmdb)                                                 | [下载](https://gh-proxy.com/github.com/linzja/domain-list-custom/releases/download/rule/GeoLite2-ASN.mmdb)                                                 |

### **Country.mmdb, GeoLite2-ASN, geoip.dat 内容**
同 [Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
- 新增类别（方便有特殊需求的用户使用）：
  - `geoip:cloudflare`
  - `geoip:cloudfront`
  - `geoip:facebook`
  - `geoip:fastly`
  - `geoip:google`
  - `geoip:netflix`
  - `geoip:telegram`
  - `geoip:twitter`
  - `geoip:apple`


## **geosite.dat 内容**
用法同 [Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)

替换类别源
- `geosite:private`
- `geosite:cn` 
- `geolocation-!cn` 
- `category-speedtest` 
新增类别
- `geosite:ads`
- `geosite:ai`
- `geosite:games-cn` 
- `geosite:pt` 

```yaml
rules:
  ## 自己的规则
  - RULE-SET,my_direct,DIRECT
  - RULE-SET,my_proxy,节点选择
  - RULE-SET,ai,AI
  # geosite
  - GEOSITE,category-ads-all,REJECT
  - GEOSITE,ads,REJECT
  # ai
  - GEOSITE,ai,AI
  - GEOSITE,private,DIRECT
  - GEOSITE,microsoft@cn,DIRECT
  - GEOSITE,games-cn,DIRECT
  - GEOSITE,apple@cn,DIRECT
  - GEOSITE,google@cn,DIRECT
  - GEOSITE,pt,DIRECT
  - GEOSITE,category-ntp,DIRECT
  - GEOSITE,category-speedtest,REJECT
  - GEOSITE,cn,DIRECT

  - GEOSITE,geolocation-!cn,节点选择
  # geoip
  - GEOIP,private,DIRECT,no-resolve
  - GEOIP,telegram,节点选择
  - GEOIP,fastly,DIRECT
  - GEOIP,cn,DIRECT
  - MATCH,漏网之鱼

fake-ip-filter:
  - 'rule-set:my_direct'
  - 'geosite:private'
  - 'geosite:games-cn'
  - 'geosite:microsoft@cn'
  - 'geosite:google@cn'
  - 'geosite:apple@cn'
  - 'geosite:pt'
  - 'geosite:category-ntp'
  - 'geosite:category-speedtest'
  - 'geosite:connectivity-check'
  - 'geosite:cn'
```

## domains分支
### 1. 文件类型
[mihomo](https://github.com/MetaCubeX/mihomo) rule-set 规则集文件（.list 格式），包含 `DOMAIN`、`DOMAIN-SUFFIX`、`DOMAIN-KEYWORD`、`DOMAIN-REGEX` 和 `PROCESS-NAME` 规则类型，适用于 `behavior: classical` 且 `format: text` 的使用场景
### 2. 数据源
每天凌晨 2 点（北京时间 UTC+8）自动构建  
1 **`fakeip-filter.list`** 源采用 [ShellCrash/public/fake_ip_filter.list](https://github.com/juewuy/ShellCrash/blob/dev/public/fake_ip_filter.list)  

2 **`private.list`** 源采用 [v2fly/domain-list-community/private](https://github.com/v2fly/domain-list-community/blob/master/data/private) 和 [blackmatrix7/ios_rule_script/Lan](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Lan)（仅域名）组合

3 **`ads.list`** 源采用 [privacy-protection-tools/anti-AD](https://github.com/privacy-protection-tools/anti-AD)

4 **`pt.list`** 源采用 [XIU2/TrackersListCollection](https://github.com/XIU2/TrackersListCollection/blob/master/all.txt)（仅域名）和 [ngosang/trackerslist](https://github.com/ngosang/trackerslist/blob/master/trackers_all.txt) 组合  

5 **`applications.list`** 源采用 [blackmatrix7/ios_rule_script/Download](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Download) 和 [Loyalsoldier/clash-rules/applications.txt](https://github.com/Loyalsoldier/clash-rules/blob/release/applications.txt) 组合  

6 **`microsoft-cn.list`** 源采用 [v2fly/domain-list-community/microsoft@cn](https://github.com/v2fly/domain-list-community/blob/master/data/microsoft)  

7 **`apple-cn.list`** 源采用 [v2fly/domain-list-community/apple@cn](https://github.com/v2fly/domain-list-community/blob/master/data/apple) 

8 **`google-cn.list`** 源采用 [v2fly/domain-list-community/google@cn](https://github.com/v2fly/domain-list-community/blob/master/data/google) 

9 **`games-cn.list`** 源采用 [v2fly/domain-list-community/category-games@cn](https://github.com/v2fly/domain-list-community/blob/master/data/category-games)、[v2fly/domain-list-community/category-game-platforms-download@cn](https://github.com/v2fly/domain-list-community/blob/master/data/category-game-platforms-download)、[blackmatrix7/ios_rule_script/SteamCN](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/SteamCN) 和 [blackmatrix7/ios_rule_script/GameDownloadCN](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Game/GameDownloadCN) 组合  

10 **`netflix.list`** 源采用 [blackmatrix7/ios_rule_script/Netflix](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Netflix)（仅域名）

11 **`disney.list`** 源采用 [blackmatrix7/ios_rule_script/Disney](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Disney)  

12 **`max.list`** 源采用 [blackmatrix7/ios_rule_script/HBO](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/HBO) 

13 **`primevideo.list`** 源采用  [blackmatrix7/ios_rule_script/PrimeVideo](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/PrimeVideo)   

14 **`appletv.list`** 源采用 [blackmatrix7/ios_rule_script/AppleTV](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/AppleTV) 

15 **`youtube.list`** 源采用 [blackmatrix7/ios_rule_script/YouTube](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/YouTube) 

16 **`tiktok.list`** 源采用  [blackmatrix7/ios_rule_script/TikTok](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/TikTok)  

17 **`bilibili.list`** 源采用 [blackmatrix7/ios_rule_script/BiliBili](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/BiliBili)  

18 **`spotify.list`** 源采用  [blackmatrix7/ios_rule_script/Spotify](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Spotify)

19 **`global-video.list`** 源采用 `netflix, disney, max primevideo, appletv, youtube, tiktok`组合

20 **`ai.list`** 源采用 [SukkaW/Surge/ai](https://raw.githubusercontent.com/SukkaW/Surge/refs/heads/master/Source/non_ip/ai.conf) 组合  

21 **`proxy.list`** 源采用 [v2fly/domain-list-community/geolocation-!cn](https://github.com/v2fly/domain-list-community/blob/master/data/geolocation-!cn)（删除了带有 `@cn` 和 `@ads` 的域名，并新增了 [v2fly/domain-list-community/cn](https://github.com/v2fly/domain-list-community/blob/master/data/cn) 中带有 `@!cn` 的域名）、[gfwlist](https://github.com/gfwlist/gfwlist) 和 [blackmatrix7/ios_rule_script/Global](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Global) 组合  

22 **`cn.list`** 源采用 [v2fly/domain-list-community/cn](https://github.com/v2fly/domain-list-community/blob/master/data/cn)（删除了带有 `@!cn` 和 `@ads` 的域名，并新增了 [v2fly/domain-list-community/geolocation-!cn](https://github.com/v2fly/domain-list-community/blob/master/data/geolocation-!cn) 中带有 `@cn` 的域名）、[blackmatrix7/ios_rule_script/ChinaMax](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/ChinaMax) 和 [~~felixonmars/dnsmasq-china-list/accelerated-domains.china.conf~~](https://github.com/felixonmars/dnsmasq-china-list/blob/master/accelerated-domains.china.conf) 组合  


20 **`download.list`** 源采用 [SukkaW/Surge/ai](https://raw.githubusercontent.com/SukkaW/Surge/refs/heads/master/Source/domainset/download.conf) 组合  
