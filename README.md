# Guidelines
1) Prevent overblocking by utilizing the [law of diminishing returns](https://pmctraining.com/site/wp-content/uploads/2018/04/Law-of-Diminishing-Returns-CHART.png) (e.g., using [sane](https://privacyguides.org/basics/threat-modeling), quality blocklists).
2) Pass the [girlfriend test](https://urbandictionary.com/define.php?term=Grandma%20Test) with few exceptions. These deviations are documented throughout the guide.

***

# Contents

1) Sign up
2) Profiles
    * Create a profile 
3) Devices
    * Create a device 
4) Customizations
    * Filters
        * Recommendations 
    * Services (TBD)
    * Custom Rules
    * Profiles Options
5) Multiple Devices and Profiles
    * Organizing profiles
    * Organizing devices

***

# Sign up

[Create an account](https://controld.com/personal/), or take advantage of Control D's [free resolvers](https://controld.com/free-dns).

***

# Profiles

Once you create an account, you will have a [Profile](https://docs.controld.com/docs/profiles). This will either be one of the pre-made profiles with example rules or a blank customizable profile.

:bulb: Since your Profile already exists when you create a new account, you only need to create your first [Device](https://docs.controld.com/docs/devices) and enforce this Profile to get up and running. This automatically generates the DNS resolvers while keeping things simple — associating one Profile to one Device.

Profiles are divided into Filters, Services, Custom Rules, and Profile Options.

### Create a profile

To create a profile, select the big green `+` button at https://controld.com/dashboard/profiles.

You'll be asked for a **Profile Name** and given a list of **Options**. See [Profile Options](https://github.com/yokoffing/Control-D-Config#profile-options) to decide which ones to enable.

# Devices

**Devices** enforce **profiles**. Every device is assigned to a profile.

### Create a device

To create a device, select the big green `+` button at https://controld.com/dashboard/devices and add the devices that you use.

When adding a new Device, you must select its type from one of the following categories: desktop or mobile OS, smart TV OS, web browser, or router.

While the device type does not impact the assigned DNS resolvers, it determines the setup guide and automatic configuration steps displayed later. The automated setup is recommended for most beginners.

***

## Filters

:bulb: A few well-chosen filters provide comprehensive protection.

:warning: Since DNS is vital for websites to load properly, overblocking will cause a lot of headaches. 

Filters, or blocklists, prevent select websites from resolving. They primarily target ads, [trackers](https://freecodecamp.org/news/what-you-should-know-about-web-tracking-and-how-it-affects-your-online-privacy-42935355525/), and malicious sites.

All filters are updated every 15-30 minutes.

### Native
Control D maintains these filters. Some filters have multiple [modes](https://docs.controld.com/docs/filters#modes) (Relaxed, Balanced, Strict).

### 3rd Party

These are popular community maintained filters. Hundreds of volunteers contribute to these lists in the [open-source](https://opensource.com/resources/what-open-source) community.

While most DNS blocklists [aggregate](https://blog.controld.com/why-you-should-block-ads-with-a-dns-service/#:~:text=Most%20popular%20third%2Dparty%20filters%20already%20block%20over%2090%25%20of%20the%20same%20content%2C%20so%20adding%20more%20provides%20minimal%20benefit.) their entries from other sources, they do not include their source's allowlist. They must manually build an allowlist over time. Therefore, when it comes to protecting yourself, adding multiple 3rd party lists does not provide substantial benefits. Rather, it only increases your chances of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

The key is to choose reputable filters that balance breadth with accuracy. Ultimately, [false positives](https://csrc.nist.gov/glossary/term/false_positive) can disrupt legitimate traffic, so quality is preferable over quantity when selecting blocklists.

I strongly recommend [Hagezi's](https://github.com/hagezi/dns-blocklists) DNS lists for his:
* sensible allowlist (doesn't overblock = smooth browsing experience)
* quick handling of [false positives](https://csrc.nist.gov/glossary/term/false_positive) (within the same day, if not sooner)
* unique entries combined with respected community filters like [OISD](https://oisd.nl/), [Steven Black](https://github.com/StevenBlack/hosts), and other [sources](https://github.com/hagezi/dns-blocklists/blob/main/sources.md)

You can choose other 3rd party lists, but they aren't needed.

### Recommendations
The first build, **Relaxed**, allows for seamless browsing while still blocking ads, trackers, and malicious sites.

The second build, **Hardened**, increases defenses against trackers and malicious sites, but with a higher chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

| Build               | Native                                                             | 3rd Party                                       |
|---------------------|--------------------------------------------------------------------|-------------------------------------------------|
| **Relaxed**  | Malware (Balanced) <br> Phishing                                    | Hagezi's DNS - Normal <br> Hagezi's DNS - TIF   |
| **Hardened** | Dynamic DNS <br> Malware (Strict) <br> New Domains * <br> Phishing | Hagezi's DNS - Pro Plus <br> Hagezi's DNS - TIF |

<sup> * Blocking newly registered domains (NRDs) may cause [false positives](https://csrc.nist.gov/glossary/term/false_positive) [occasionally](https://www.reddit.com/r/InternetIsBeautiful/comments/w2wdro/comment/iguvg8y/?context=3). Be selective when adding NRDs to your allowlist; and, if you do, **NEVER** give [sensitive information](https://egnyte.com/guides/governance/sensitive-information) to a NRD. </sup>

:memo: Control D recommends using their Malware Filter in [Balanced](https://docs.controld.com/docs/malware#relaxed) or [Strict](https://docs.controld.com/docs/malware#strict) mode. While these modes can [effectively](https://techblog.nexxwave.eu/public-dns-malware-filters-tested-in-2024/) catch and block more malicious domains, they also have a higher chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive). If you find that false positives are disrupting your browsing frequently, you may want to drop down to [Relaxed](https://docs.controld.com/docs/malware#relaxed) mode.
<p> </p>

<details><summary>Toggle me if you prefer to only use Native filters:</summary>

| Build                             | Native                                                                                                                                                | 3rd Party |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Relaxed (native only)**  | Ads & Trackers (Relaxed) <br> Malware (Balanced) <br> Phishing                                                                                         |           |
| **Hardened (native only)** | Ads & Trackers (Balanced) <br> Dynamic DNS <br> IoT Telemetry (for non-desktops) <br> Malware (Strict) <br> New Domains <br> Phishing |           |

:memo: Control D recommends using their Malware Filter in [Balanced](https://docs.controld.com/docs/malware#relaxed) or [Strict](https://docs.controld.com/docs/malware#strict) mode. While these modes can [effectively](https://techblog.nexxwave.eu/public-dns-malware-filters-tested-in-2024/) catch and block more malicious domains, they also have a higher chance of falsely identifying safe sites as unsafe (known as [false positives](https://csrc.nist.gov/glossary/term/false_positive)). If you find that false positives are disrupting your browsing frequently, you may want to drop down to [Relaxed](https://docs.controld.com/docs/malware#relaxed) mode.

Control D's Malware filter ([Balanced](https://docs.controld.com/docs/malware#relaxed) and [Strict](https://docs.controld.com/docs/malware#strict) mode) are recommended here by the company itself. While these modes are [effective](https://techblog.nexxwave.eu/public-dns-malware-filters-tested-in-2024/) (they have a higher chance of it catching and blocking a malicious domain), you are more likely to experience [false positives](https://csrc.nist.gov/glossary/term/false_positive).

</details>

:star: Congrats! By using these filters, you are significantly better off than most internet users.

***

## Services

*N/A for now*

***

## Custom Rules

Custom Rules allow you to add sites by Domain or by Folder. To keep thing tidy, setup two folders, and then add domains as needed to them.

For simplicity, I advise that you create two folders: an **Allowlist** folder and a **Denylist** folder.

### Allowlist
Domains added to the **Allowlist** folder will always resolve.

#### Create folder
1. Under the desired profile, add the folder by clicking the big green `+` button.
2. Select **Folder**.
3. Under **Folder Name**, type `Allowlist`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, select the middle option **[Bypass](https://docs.controld.com/docs/custom-rules#bypass)**.

### Denylist
Domains added to the **Denylist** folder entries are always blocked.

#### Create folder
1. Under the desired profile, add the folder by clicking the big green `+` button.
2. Select **Folder**.
3. Under **Folder Name**, type `Denylist`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, make sure **[Block](https://docs.controld.com/docs/custom-rules#block)** is selected.

Advanced users may also want to add a folder for [TLDs](https://github.com/yokoffing/NextDNS-Config#block-top-level-domains-tlds-1-2-3-4-5-) with a folder rule of **Block**.
***

## Profiles Options 
### AI Malware Filter
![Disabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/disabled.svg) Disable

*Enable in (Relaxed Mode) for Hardened profiles.*

### Safe Search
![Disabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/disabled.svg) Disable

*Enable for Kids profile.*

### Restricted Youtube
![Disabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/disabled.svg) Disable

*Enable for Kids profile.*

### DNS Rebind Protection
![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

[DNS Rebind Protection](https://help.nextdns.io/t/35hmval/what-is-dns-rebinding-protection) prevents malicious requests from bypassing security measures on your device. For example, if you visit `google.com` and it resolves to a private IP address like `10.0.0.1`, DNS Rebind Protection would block access. This stops attackers from using rebinding techniques to access private networks and endpoints that should not be publicly reachable.

### Disable DNSSEC
![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

:bulb: Control D sits between the user and the upstream DNS servers, giving it full control over the DNS records. This reduces the value of DNSSEC's authentication.

:warning: DNSSEC also makes things slower, and breaks some sites.

An argument can be made that using DoH alone does not eliminate the need for DNSSEC to validate DNS data integrity. However, when using DOH / DOT / DOQ protocols through a service like Control D, which can manipulate DNS records based on user-defined rules, there is little benefit to also enabling DNSSEC validation.

Control D also [states](https://discord.com/channels/1035992466203099147/1037876518778572860/1143716723883778088) that DNSSEC* requires a separate DNS resolver and cache, which impacts performance.

<sup>* At this time, [DNSSEC validation](https://www.quad9.net/support/faq/#dnssec) and [EDNS Client Subnet](https://www.quad9.net/support/faq/#edns) (ECS) are grouped together in this settings.</sup>

### TTL

![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

Every DNS record has a time-to-live (TTL) value that determines how long devices cache the record before requesting an update from the DNS server. This caching reduces DNS queries and can improve performance.

There are three TTLs that you can tweak in Profile Options. You can set values for [Block TTL](https://docs.controld.com/docs/ttl-overrides#block-ttl), [Redirect TTL](https://docs.controld.com/docs/ttl-overrides#redirect-ttl), or [Bypass TTL](https://docs.controld.com/docs/ttl-overrides#bypass-ttl).

Below are common values to use for DNS caching, measured in seconds.

| Value   | Duration  |
|---------|-----------|
| `60`    | 1 minute  |
| `300`   | 5 minutes |
| `3600`  | 1 hour    |
| `28800` | 8 hours   |
| `86400` | 24 hours  |

:bulb: Increasing the TTL values caches DNS records for longer periods, which minimizes queries and optimizes performance.

:warning: Do not set higher than 24 hours.

***

# Multiple Devices and Profiles
## Organizing profiles

This is where you can get creative. What you name the profiles doesn't matter much; what matters is the options you will enable with each profile.

For example, you may create two profiles, and then later link devices to one of the two profiles:

1. **Hardened** (for web browsers, computer, smartphone): more nuanced protection with greater risk of [false positives](https://csrc.nist.gov/glossary/term/false_positive).
2. **Relaxed** (for router, smart TV): [set-and-forget](https://glosbe.com/en/en/set-and-forget); low chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

Are you managing DNS for just you? Then you may need only one or two profiles. Your family? Then maybe three or four profiles.

If you have kids, you might have:

1. **Administrator** (you the administrator; stronger settings)
2. **Adults** (spouse, grandparents; slightly relaxed settings)
3. **Kids** (with parental controls active)

Or a combination of the two approaches:
1. **Hardened:** heightened security and privacy options, since you're maintaining the DNS and don't mind troubleshooting (for web browsers, computer, smartphone)
2. **Relaxed:** balance of security and privacy options (for smart TV, your spouse's devices)
3. **Kids:** same as Relaxed but with parental controls active
4. **Basic:** legacy resolver, security options, but minimal privacy filters (for router)

You get the idea.

### Organizing devices

Remember that **devices** enforce **profiles**.

You can add as many Devices as you'd like. I have a Device created for each web browser I use, and one for my phone, computer, smart TV, and router.

Let's use the profile names from earlier. You might have:

| **Device Name** | **Enforced Profile** |
|-----------------|----------------------|
| Firefox         | Hardened             |
| Chrome          | Hardened             |
| iPhone          | Hardened             |
| Wife's iPhone   | Relaxed              |
| Wife's Mac      | Relaxed              |
| Susie's iPad    | Kids                 |
| Living Room TV  | Basic                |
| Router          | Basic                |

If desired, Control D allows enforcing two profiles on a single device. [Multiple linked profiles](https://docs.controld.com/docs/multiple-enforced-profiles) allow you to enforce rules from two profiles simultaneously when using a device.
