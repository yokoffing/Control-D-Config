# Guidelines
1) Prevent overblocking by utilizing the [law of diminishing returns](https://pmctraining.com/site/wp-content/uploads/2018/04/Law-of-Diminishing-Returns-CHART.png) (e.g., using [sane](https://privacyguides.org/basics/threat-modeling), quality blocklists).
2) Pass the [girlfriend test](https://urbandictionary.com/define.php?term=Grandma%20Test) with few exceptions. These deviations are documented throughout the guide.

***
# Sign up

[Create an account](https://controld.com/), or take advantage of Control D's [free resolvers](https://controld.com/free-dns).

***
# Devices

Select the big green + button at `https://controld.com/dashboard/devices` and add the devices that you use.

### Organizing devices

Add as many as you'd like. For instance, I have a Device option for each web browser I use (I test a lot of websites!), and one for my phone, computer, smart TV, and router.

Every Device option will be connected to a Profile.

For instance, using the template from [Organizing profiles], you might have:

| **Device Name** | **Enforced Profile** |
|-----------------|----------------------|
| Firefox         | Hardened             |
| Chrome          | Hardened             |
| iPhone          | Hardened (or Relaxed) |
| Wife's iPhone   | Relaxed              |
| Wife's Mac      | Relaxed              |
| Susie's iPad    | Kids                 |
| Living Room TV  | Basic                |
| Router          | Basic                |

***

# Profiles

To create a profile, select the big green + button at `https://controld.com/dashboard/devices`.

Profiles are divided into Filters, Services, Custom Rules, and Profile Options.

### Organizing profiles

This is where you can get creative. What you name the profiles doesn't matter much; what matters is the options you will enable with each profile.

Are you managing DNS for just you? Then you may need only one or two profiles. Your family? Then maybe three or four profiles.

For example, if you are the only user, you may have two profiles:

1. Hardened (for web browsers, computer, smartphone)
2. Relaxed (for router, smart TV)

If you have kids, you might have:

1. Administrator (you; stronger settings)
2. Adults (spouse, grandparents; slightly relaxed settings)
3. Kids (with parental controls active)

Or a combination of the two apporaches:
1. Hardened: heightened security and privacy options, since you're maintaining the DNS and don't mind troubleshooting (for web browsers, computer, smartphone)
2. Relaxed: balance of security and privacy options (for smart TV, your spouse's devices)
3. Kids: same as Relaxed but with parental controls active
4. Basic: legacy resolver, security options, but minimal privacy filters (for router)

You get the idea.

Also note that **Analytics** are tied to Device, not the Profile.

## Filters
Filters, or blocklists, prevent select websites from resolving. They primarily target ads, [trackers](https://freecodecamp.org/news/what-you-should-know-about-web-tracking-and-how-it-affects-your-online-privacy-42935355525/), and malicious sites.

All filters are updated every 30-60 minutes.

### Native
Control D maintains these filters. Some filters have multiple [modes](https://docs.controld.com/docs/filters#modes) (Relaxed, Balanced, Strict).

### 3rd Party
These are popular community maintained filters. Hundreds of volunteers contribute to these lists in the [open-source](https://opensource.com/resources/what-open-source) community.

I strongly recommend [Hagezi's](https://github.com/hagezi/dns-blocklists) DNS lists:
* sensible allowlist (doesn't overblock = smooth browsing experience)
* quickly handles false positives (within the same day, if not sooner)
* unique entries combined with respected community filters like [OISD](https://oisd.nl/), [Steven Black](https://github.com/StevenBlack/hosts), and other [sources](https://github.com/hagezi/dns-blocklists/blob/main/sources.md)

### Recommendations
The first build, **Set-and-forget**, allows for seamless browsing while still blocking ads, trackers, and malicious sites.

The second build, **More protection**, increases defenses against trackers and malicious sites, but with a higher chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

| Build               | Native                                                             | 3rd Party                                       |
|---------------------|--------------------------------------------------------------------|-------------------------------------------------|
| **Set-and-forget**  | Malware (Relaxed) <br> Phishing                                    | Hagezi's DNS - Normal <br> Hagezi's DNS - TIF   |
| **More protection** | Dynamic DNS <br> Malware (Relaxed) <br> New Domains <br> Phishing | Hagezi's DNS - Pro Plus <br> Hagezi's DNS - TIF |

:star: Congrats! By using these handful of filters, you are significantly better off than most internet users.

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

Advanced users may also want to add a folder for [TLDs], or make folders more specific.

### Allow
Folder Rule: [Bypass](https://docs.controld.com/docs/custom-rules#bypass)

#### Create folder
1. Under the desired profile, add the folder by clicking the big green + button.
2. Select **Folder**.
3. Under **Folder Name**, type `Allow`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, select the middle option **Bypass**.

Domains added to the **Allow** folder will always resolve.

### Deny
Folder Rule: [Block](https://docs.controld.com/docs/custom-rules#block)

#### Create folder
1. Under the desired profile, add the folder by clicking the big green + button.
2. Select **Folder**.
3. Under **Folder Name**, type `Deny`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, make sure **Block** is selected.

Domains added to the **Deny** folder entries are always blocked.
***

## Profiles Options
### AI Malware Filter
_Disable_ <br>

### DNS Rebind Protection
_Enable_ <br>

[DNS Rebind Protection](https://help.nextdns.io/t/35hmval/what-is-dns-rebinding-protection) prevents malicious requests from bypassing security measures on your device. For example, if you visit `google.com` and it resolves to a private IP address like `10.0.0.1`, DNS Rebind Protection would block access. This stops attackers from using rebinding techniques to access private networks and endpoints that should not be publicly reachable.


### Disable DNSSEC
_Enable_ <br>

:warning: DNSSEC makes things slower, and breaks some sites.

[DNSSEC validation](https://www.quad9.net/support/faq/#dnssec) and [EDNS Client Subnet](https://www.quad9.net/support/faq/#edns) (ECS) are coupled together in the settings.

An argument can be made that using DoH alone does not eliminate the need for DNSSEC to validate DNS data integrity. However, when using DOH, DOT, or DOQ protocols through a service like Control D, which can manipulate DNS records based on user-defined rules, there is little benefit to also enabling DNSSEC validation. Control D sits between the user and the upstream DNS servers, giving it full control over the records, reducing the value of DNSSEC's authentication.

Control D also [states](https://discord.com/channels/1035992466203099147/1037876518778572860/1143716723883778088) that DNSSEC requires a separate DNS resolver and cache, which impacts performance.

### TTL

:bulb: Increasing the TTL values caches DNS records for longer periods, which minimizes queries and optimizes performance.

Every DNS record has a time-to-live (TTL) value that determines how long devices cache the record before requesting an update from the DNS server. This caching reduces DNS queries and can improve performance.

There are three TTLs that you can tweak in Profile Options. You can set TTL values for [block](https://docs.controld.com/docs/ttl-overrides#block-ttl), [redirect](https://docs.controld.com/docs/ttl-overrides#redirect-ttl), or [bypass](https://docs.controld.com/docs/ttl-overrides#bypass-ttl) requests.

Below are common values to use for DNS caching, measured in seconds.

| Value   | Duration  |
|---------|-----------|
| `60`    | 1 minute  |
| `300`   | 5 minutes |
| `3600`  | 1 hour    |
| `28800` | 8 hours   |
| `86400` | 24 hours  |

:warning: Do not set any higher than 24 hours.

### Disable
Use the dropdown in the UI to temporarily disable Control D services.
