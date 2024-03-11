# Guidelines
1) Prevent overblocking by utilizing the [law of diminishing returns](https://pmctraining.com/site/wp-content/uploads/2018/04/Law-of-Diminishing-Returns-CHART.png) (e.g., using [sane](https://privacyguides.org/basics/threat-modeling), quality blocklists).
2) Pass the [girlfriend test](https://urbandictionary.com/define.php?term=Grandma%20Test) with few exceptions. These deviations are documented throughout the guide.

***

# Contents

1) Sign up
2) Profiles
3) Devices
4) Customizations
    * Filters
        * Recommendations 
    * Services
    * Custom Rules
    * Profiles Options
5) Advanced Users
    * Multiple Devices and Profiles
    * Import & Export Folders
    * Wildcard rules
    * Spoofing location
    * Geo custom rules

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
# Customizations

## Filters

:bulb: A few well-chosen filters provide comprehensive protection.

:warning: Since DNS is vital for websites to load properly, overblocking will cause a lot of headaches. 

[Filters](https://docs.controld.com/docs/filters), or blocklists, prevent select websites from resolving. They primarily target ads, [trackers](https://freecodecamp.org/news/what-you-should-know-about-web-tracking-and-how-it-affects-your-online-privacy-42935355525/), and malicious sites.

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
| **Relaxed**  | Malware (Balanced)<sup>1</sup> <br> Phishing                                    | Hagezi's DNS - Normal <br> Hagezi's DNS - TIF   |
| **Hardened** | Dynamic DNS <br> Malware (Strict)<sup>1</sup> <br> New Domains<sup>2</sup> <br> Phishing | Hagezi's DNS - Pro Plus <br> Hagezi's DNS - TIF |

<sup> **1** [Balanced](https://docs.controld.com/docs/malware#relaxed) and [Strict](https://docs.controld.com/docs/malware#strict) mode blocks malicious domains [effectively](https://techblog.nexxwave.eu/public-dns-malware-filters-tested-in-2024/), but they may cause false positives. Switch to [Relaxed](https://docs.controld.com/docs/malware#relaxed) mode if [false positives](https://csrc.nist.gov/glossary/term/false_positive) frequently disrupt browsing. </sup>

<sup> **2** Blocking newly registered domains (NRDs) may cause [false positives](https://csrc.nist.gov/glossary/term/false_positive) [occasionally](https://www.reddit.com/r/InternetIsBeautiful/comments/w2wdro/comment/iguvg8y/?context=3). Be selective when adding NRDs to your allowlist; and, if you do, **NEVER** give [sensitive information](https://egnyte.com/guides/governance/sensitive-information) to a NRD. </sup>

<p> </p>

<details><summary>Toggle me if you prefer to only use Native filters:</summary>

| Build                             | Native                                                                                                                                                | 3rd Party |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Relaxed (native only)**  | Ads & Trackers (Relaxed) <br> Malware (Balanced)<sup>1</sup> <br> Phishing                                                                                         |           |
| **Hardened (native only)** | Ads & Trackers (Balanced) <br> Dynamic DNS <br> IoT Telemetry (for non-desktops) <br> Malware (Strict)<sup>1</sup> <br> New Domains <br> Phishing |           |

<sup> **1** [Balanced](https://docs.controld.com/docs/malware#relaxed) and [Strict](https://docs.controld.com/docs/malware#strict) mode blocks malicious domains [effectively](https://techblog.nexxwave.eu/public-dns-malware-filters-tested-in-2024/), but they may cause false positives. Switch to [Relaxed](https://docs.controld.com/docs/malware#relaxed) mode if [false positives](https://csrc.nist.gov/glossary/term/false_positive) frequently disrupt browsing. </sup>

</details>

:star: Congrats! By using these filters, you are significantly better off than most internet users.

***

## Services

[Services](https://docs.controld.com/docs/services) allows you to customize blocking and allowing sites and apps at a granular level.

To access Services, go to https://controld.com/dashboard/profiles > Edit > Services.

### Easy exceptions
You can use Services to create easy exceptions.

For example, let's say you want to block all social media except Instagram:
1) Enable the Social filter on your Profile to block all social media sites (Profile > Edit > Filters > Social).
2) Go to Services (Profiles > Edit > Services).
3) Open the Social category and toggle Instagram.
4) Create a [Bypass](https://docs.controld.com/docs/custom-rules#bypass) rule to allow Instagram.

Now you can still access Instagram while blocking other social media services.

### Targeted blocking

Alternatively, you can use Services to block only specific social media sites rather than the whole category.

In this scenario, you only want to block TikTok and Facebook:
1) Go to Services (Profiles > Edit > Services).
2) Open the Social category and toggle Facebook.
3) This will allow you to create a [Block](https://docs.controld.com/docs/custom-rules#block) rule to block Facebook.
4) Repeat 2 and 3 for TikTok.

This way, you can still access all social media companies except Facebook and TikTok.

As you can see, Services help you tailor your blocking to your specific needs, and it's easier than hunting down and copying + pasting URLs to your Custom Rules.

***

## Custom Rules

[Custom Rules](https://docs.controld.com/docs/custom-rules) allows you to organize domains into groups.

To access Custom Rules, go to https://controld.com/dashboard/profiles > Edit > Custom Rules.

### Logical groups
You can create folders to categorize domains, then apply [rules](https://docs.controld.com/docs/custom-rules#rule-actions) to those domains.

### Action folders
Alternatively, you can assign [one rule to an entire folder](https://docs.controld.com/docs/folder-rules#action-folders). That rule will then apply to all domains within that folder.

I advise that you do this when creating two folders, an **Allowlist** and a **Denylist**, and then add domains to them as needed.

#### Allowlist
Domains added to the **Allowlist** folder will always resolve.

To create an allowlist:
1. Under the desired profile, add the folder by clicking the big green `+` button.
2. Select **Folder**.
3. Under **Folder Name**, type `Allowlist`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, select the middle option **[Bypass](https://docs.controld.com/docs/custom-rules#bypass)**.

#### Denylist
Domains added to the **Denylist** folder entries are always blocked.

To create an denylist:
1. Under the desired profile, add the folder by clicking the big green `+` button.
2. Select **Folder**.
3. Under **Folder Name**, type `Denylist`.
4. Toggle **Folder Rule**.
5. Under **Select Rule**, make sure **[Block](https://docs.controld.com/docs/custom-rules#block)** is selected.

:memo: Note that Control D disables iCloud Private Relay by default [read more](https://docs.controld.com/docs/icloud-private-relay).

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
# Advanced Users
## Multiple Devices and Profiles
### Organizing profiles

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

:bulb: You can read more on advance rule logic in the [docs](https://docs.controld.com/docs/advanced-rules-creation-guide).

## Import & Export Folders
### Import
Control D allows you to import and export folders from other users under Custom Rules.

#### TLDs
You may want to add a folder for [TLDs](https://webtribunal.net/blog/tld-statistics).

You can import folders by clicking the `...` icon and selecting **Upload Folder**.

[Hagezi](https://github.com/hagezi/dns-blocklists) has [compiled folders](https://github.com/hagezi/dns-blocklists/tree/main/controld) that can be imported, such as:

* [Spam TLDs folder](https://github.com/hagezi/dns-blocklists/blob/main/controld/spam-tlds-folder.json)
* [Spam TLDs Allow folder](https://github.com/hagezi/dns-blocklists/blob/main/controld/spam-tlds-allow-folder.json)

To import a list above:
1) Click the link.
2) On Github, select the `...` button in the top-right corner.
3) Click **Download**.
4) On Control D - Custom Rules, select the `...` icon.
5) Click **Upload Folder**.

### Export
You can export your folder by clicking the `...` button in a folder and selecting **Download Rules**.

## Wildcard rules
[Wildcard rules](https://docs.controld.com/docs/custom-rules#rule-format) allow you to block a wide spectrum of domains without listing them separately. This format is what Control D uses in their blocklists.

Control D can block subdomains by adding wildcards like `*.example.com` to your Denylist. This will be converted to a regex expression automatically (e.g. `(^|.)example.com$`) to match subdomains.

This blocks all subdomains of `domain.com`, but NOT `domain.com`. For example, you can block `*.analytics.com` to block all subdomains of `analytics.com`. 

Utilize the [block](https://docs.controld.com/docs/custom-rules#block) rule when creating wildcards.

To access Custom Rules, go to https://controld.com/dashboard/profiles > Edit > Custom Rules.

## Spoofing location

A [Redirect](https://docs.controld.com/docs/services#redirect) rule proxies all domains associated with a [service](https://docs.controld.com/docs/services) to a location or IP address you specify.

Location spoofing may provide you with privacy benefits by hiding your real location. Control D goes a step further by incorporating proxy functionality.

You can unlock geo-restricted services by leveraging DNS-based traffic redirection. This allows users to route their internet traffic through servers in different locations, enabling them to bypass geo-restrictions and access content that may be blocked in their region. You can then view a broader range of content, such as different Netflix libraries, that would otherwise be unavailable due to licensing restrictions.

<details> <summary>:warning: Technical Limitations :warning: </summary>
   
* Websites or apps employing legacy security protocols might not be accessible when attempting to bypass geo-restrictions. The [redirect](https://docs.controld.com/docs/services#redirect) rule requires Server Name Indication (SNI), which is not supported in these older standards. This prevents the bypassing method from functioning as intended.
* Currently, the unencrypted SNI allows ISPs and network admins to see your visited sites when analyzing traffic with Deep Packet Inspection (DPI). [Encrypted Client Hello](https://github.com/yokoffing/Betterfox/blob/14de7b101d48f15f50df7dd5dbfffefca5b4a855/Securefox.js#L725-L729) (ECH) is coming but it's not widely used yet.
   
</details>

### Examples

| **Category** |     **Service**    | **Destination** |
|:------------:|:------------------:|:---------------:|
| Audio        | Apple Music        | Dallas, US      |
| News         | The New York Times | New York, US    |
| Video        | Netflix            | London, GB      |
| Video        | BBC iPlayer        | London, GB      |

### Instructions
Control D provides a simple and effective way to unlock geo-restricted services and enhance online privacy by leveraging DNS-based traffic redirection.

1) To access Services, go to https://controld.com/dashboard/profiles > Edit > Services.
2) Choose a category.
3) Select the third icon (globe).
4) Choose a proxy location.

## Geo Custom Rules
:warning: This feature is still in beta.

[Geo Custom Rules](https://docs.controld.com/docs/geo-custom-rules) (GCR) allow you to create custom rules based on the geo-location data of source and destination IPs for DNS queries.

GCRs start with any of the four formats below, followed by a two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements). For better understanding, I've divided these rules into outbound and inbound requests.

### Outbound Requests
Outbound rules indicate the destination country that the domain resolves to.

| **Symbol**   | **Definition**                                               |
|--------------|--------------------------------------------------------------|
| `@`          | A queried domain **resolves** to a destination country.      |
| `!@`         | The DNS query **does not resolve** to a destination country. |

### Inbound Requests
Inbound rules focus on the source country that a domain originates from. 

| **Symbol**   | **Definition**                                                             |
|--------------|----------------------------------------------------------------------------|
| `#`          | A queried domain **originates** from a source country IP address.          |
| `!#`         | The DNS query **does not originate** from a source country IP address.     |

### Examples
I want to **block** DNS queries to domains that resolve to servers in countries with known cybersecurity threats like Russia or China. I would create the following two rules: `@RU` and `@CN` both with a [block](https://docs.controld.com/docs/geo-custom-rules#block) rule, to prevent any DNS resolutions from the those domains.

| **Rule** | **Symbol** | **Country** | **Description**                                                        |
|----------|------------|-------------|------------------------------------------------------------------------|
| Block    | `@`        | `RU`        | Block DNS queries to domains that resolve to domains in Russia.        |
| Block    | `@`        | `CN`        | Block DNS queries to domains that resolve to domains in China.         |

I want to **allow** DNS queries from domains that originate from the United States and Canada. I would create the following rules: `#US` and `#CA` both with a [bypass](https://docs.controld.com/docs/geo-custom-rules#bypass) rule, to allow the resolutions to process normally.

| **Rule** | **Symbol** | **Country** | **Description**                                                        |
|----------|------------|-------------|------------------------------------------------------------------------|
| Bypass   | `#`        | `US`        | Allow DNS queries from the United States to process normally.          |
| Bypass   | `#`        | `CA`        | Allow DNS queries from Canada to process normally.                     |

But let's say you're a real glutton for punishment and want to really limit your network connections to the US and Canada **only**. You would use `!#US` and `!#CA` both with a [block](https://docs.controld.com/docs/geo-custom-rules#block) rule, to prevent any DNS resolutions to domains outside of these countries. In other words, American and Canadian domains resolve normally, while other countries' domains are blocked.

| **Rule** | **Symbol** | **Country** | **Description**                                                        |
|----------|------------|-------------|------------------------------------------------------------------------|
| Block    | `!#`       | `US`        | US domains resolve normally, but other countries' domains are blocked. |
| Block    | `!#`       | `CA`        | CA domains resolve normally, but other countries' domains are blocked. |

:warning: Control D can underestand multiple `!#` block rules, if you want to limit your DNS resolutions to specific countries. However, you should not [mix-and-match](https://docs.controld.com/docs/geo-custom-rules#this-is-not-ok) block and bypass rules with `!@` and `!#` formats.

### Create a folder (optional)
:world_map: To access Custom Rules, go to https://controld.com/dashboard/profiles > Edit > Custom Rules.

1. Under the desired profile, add the folder by clicking the big green `+` button.
2. Select **Folder**.
3. Under **Folder Name**, type `Geo Custom Rules`.
4. Click **Add Folder**.
