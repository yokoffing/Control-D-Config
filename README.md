# Guidelines
1) Prevent overblocking by utilizing the [law of diminishing returns](https://pmctraining.com/site/wp-content/uploads/2018/04/Law-of-Diminishing-Returns-CHART.png) (e.g., using [sane](https://privacyguides.org/basics/threat-modeling), quality blocklists).
2) Pass the [girlfriend test](https://urbandictionary.com/define.php?term=Grandma%20Test) with few exceptions. These deviations are documented throughout the guide.

***

# Devices

***

# Profiles

## Filters
Filters, or blocklists, prevent select websites from resolving. They primarily target ads, [trackers](https://freecodecamp.org/news/what-you-should-know-about-web-tracking-and-how-it-affects-your-online-privacy-42935355525/), and malicious sites.

All filters update every hour to their latest release | OR | All filters are rebuilt and deployed every 30 minutes.

### Native
Control D maintains these filters.

Some filters have multiple [modes](https://docs.controld.com/docs/filters#modes).

### 3rd Party
These are popular community maintained filters. Hundreds of volunteers contribute to these lists in the [open-source](https://opensource.com/resources/what-open-source) community.

I strongly recommend using one of [Hagezi's](https://github.com/hagezi/dns-blocklists) DNS lists:
* sensible allowlist (doesn't overblock = smooth browsing experience)
* quickly handles false positives (within the same day, if not sooner)
* unique entries combined with respected community filters like [OISD](https://oisd.nl/), [Steven Black](https://github.com/StevenBlack/hosts), and other [sources](https://github.com/hagezi/dns-blocklists/blob/main/sources.md)

### Recommendations
The first build, **[Set-and-forget](https://glosbe.com/en/en/set-and-forget)**, allows for seamless browsing while still blocking ads, trackers, and malicious sites.

The second build, **More protection**, increases defenses against trackers and malicious sites, but with a higher chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

| Build               | Native                                                             | 3rd Party                                       |
|---------------------|--------------------------------------------------------------------|-------------------------------------------------|
| **Set-and-forget**  | Malware (Relaxed) <br> Phishing                                    | Hagezi's DNS - Normal <br> Hagezi's DNS - TIF   |
| **More protection** | Dynamic DNS <br> Malware (Relaxed) <br> New Domains <br> Phishing | Hagezi's DNS - Pro Plus <br> Hagezi's DNS - TIF |

If you prefer to only use Control D's filters:

| Build                             | Native                                                                                                                                                | 3rd Party |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Set-and-forget (native only)**  | Ads & Trackers (Relaxed) <br> Malware (Relaxed) <br> Phishing                                                                                         |           |
| **More protection (native only)** | Ads & Trackers (Balanced) <br> Dynamic DNS <br> IoT Telemetry (for non-desktops) <br> Malware (Balanced) <br> New Domains <br> Phishing |           |

The more filters you use, the greater the risk of [false positives](https://csrc.nist.gov/glossary/term/false_positive). This is because most blocklists [aggregate](https://blog.controld.com/why-you-should-block-ads-with-a-dns-service/#:~:text=Most%20popular%20third%2Dparty%20filters%20already%20block%20over%2090%25%20of%20the%20same%20content%2C%20so%20adding%20more%20provides%20minimal%20benefit.) from other sources, so adding multiple lists does not necessarily increase coverage.

The key is to choose reputable filters that balance breadth with accuracy. Ultimately, false positives can disrupt legitimate traffic, so quality is preferable over quantity when selecting blocklists.

:bulb: Two or three well-chosen filters provide comprehensive protection.

:warning: Since DNS is vital for websites to load properly, overblocking will cause a lot of headaches. 

DNS filtering should act as an initial barrier to block unwanted connections, but not your only defense.

For web browsers:
* Desktops: [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/all/#product-desktop-release) with [Betterfox](https://github.com/yokoffing/Betterfox) and [uBlock Origin](https://ublockorigin.com/).
* Android: [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/all/#product-desktop-release) with [uBlock Origin](https://ublockorigin.com/).
* iOS: Safari with [AdGuard](https://apps.apple.com/us/app/adguard-for-safari/id1440147259?mt=12).

***

## Services

***

## Custom Rules
### Allow
### Deny
### False Positives
### International
Geo-based custom rules
### TLDs

***

## Profiles Options
### AI Malware Filter
### DNS Rebind Protection
### Disable DNSSEC
### TTL
#### Block
#### Redirect
#### Bypass
### Compatibility Mode

Free resolvers
CTAs
