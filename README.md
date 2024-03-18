# Guidelines
1) Prevent overblocking by utilizing the [law of diminishing returns](https://pmctraining.com/site/wp-content/uploads/2018/04/Law-of-Diminishing-Returns-CHART.png) (e.g., using [sane](https://privacyguides.org/basics/threat-modeling), quality blocklists).
2) Pass the [girlfriend test](https://urbandictionary.com/define.php?term=Grandma%20Test) with few exceptions. These deviations are documented throughout the guide.

***

# Contents

1) [Sign up](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#sign-up)
2) [Profiles](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#profiles)
3) [Devices](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#devices)
4) [Customizations](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#customizations)
    * [Filters](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#filters)
        * [Recommendations](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#recommendations)
    * [Services](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#services)
    * [Custom Rules](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#custom-rules)
    * [Profile Options](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#profile-options)
        * [TTL Overrides](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#ttl-overrides)
5) [Advanced Users](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#advanced-users)
    * [Multiple Devices and Profiles](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#multiple-devices-and-profiles)
    * [Wildcard Rules](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#wildcard-rules)
    * [Import & Export Folders](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#import-&-export-folders)
    * [Spoofing Domains](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#spoofing-domains)
    * [Geo Custom Rules](https://github.com/yokoffing/Control-D-Config?tab=readme-ov-file#geo-custom-rules)

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
I have three builds below, using a combination of both native and 3rd party filters:
* The first build, **Basic**, allows for seamless browsing while still blocking ads, trackers, and malicious sites.
* The second build, **Hardened**, increases defenses against trackers and malicious sites.
* A third build, **Aggressive**, goes further but with a higher chance of [false positives](https://csrc.nist.gov/glossary/term/false_positive).

These are only suggestions. Feel free to mix and match.

| Build               | Native                                                                  | 3rd Party                                       |
|---------------------|-------------------------------------------------------------------------|-------------------------------------------------|
| **Basic**  | Malware ([Relaxed](https://docs.controld.com/docs/malware#relaxed)) <br> Phishing                                                | Hagezi's DNS - Normal <p><p>Hagezi's DNS - TIF   |
| **Hardened** | Dynamic DNS <br> Malware ([Balanced](https://docs.controld.com/docs/malware#balanced)) <br> New Domains<sup>1</sup> <br> Phishing | Hagezi's DNS - Pro <p><p> Hagezi's DNS - TIF |
| **Aggressive** | Clickbait <br> Dynamic DNS <br> IoT Telemetry <br> Malware ([Strict](https://docs.controld.com/docs/malware#strict))<sup>2</sup> <br> New Domains<sup>1</sup> <br> Phishing | Hagezi's DNS - Pro Plus <p><p> Hagezi's DNS - TIF |

<sup> **1** A domain is considered new if it has been registered for less than 30 days. Blocking newly registered domains (NRDs) may cause [false positives](https://csrc.nist.gov/glossary/term/false_positive) [occasionally](https://www.reddit.com/r/InternetIsBeautiful/comments/w2wdro/comment/iguvg8y/?context=3). Be selective when adding NRDs to your allowlist; and, if you do, **NEVER** give [sensitive information](https://egnyte.com/guides/governance/sensitive-information) to a NRD. </sup>
<br>
<sup> **2** [Strict](https://docs.controld.com/docs/malware#strict) mode may be especially prone to false positives. Drop down to [Balanced](https://docs.controld.com/docs/malware#relaxed) mode if [false positives](https://csrc.nist.gov/glossary/term/false_positive) frequently disrupt browsing. </sup>

[Not all ads](https://www.reddit.com/r/nextdns/comments/14nsfhv/comment/jq982bi/?context=3) can be blocked at the DNS level. You will need an [ad blocker](https://github.com/yokoffing/NextDNS-Config#i-need-a-browser-with-ad-blocking-which-one-should-i-choose) to block what's leftover.

This is because not all ads come from third-party domains. Some ads come directly from the site you're visiting, like [YouTube](https://discourse.pi-hole.net/t/how-do-i-block-ads-on-youtube/253/2). DNS blockers stop the resolution of a domain, and content blockers filter page content.

* Find web browser and ad blocker [recommendations](https://github.com/yokoffing/NextDNS-Config/tree/main#i-need-a-browser-with-ad-blocking-which-one-should-i-choose) to easily install a lightweight ad blocker.
* Want to block more with your ad blocker? Check out my [custom filter lists](https://github.com/yokoffing/filterlists).

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

:memo: Note that Control D disables iCloud Private Relay by default ([read more](https://docs.controld.com/docs/icloud-private-relay)).

***

## Profiles Options 
### AI Malware Filter
![Disabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/disabled.svg) Disable

*Enable in (Relaxed Mode) for Aggressive profiles.*

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

:bulb: Control D sits between you and the upstream DNS servers, giving it full control over your DNS records. This reduces the value of DNSSEC's authentication.

:warning: DNSSEC can make things slower and break some sites.

[DNSSEC](https://www.upguard.com/blog/dnssec#toc-1) is a security protocol that enhances DNS by using digital signatures to verify the authenticity and integrity of DNS data. The protocol cryptographically signs DNS records using [public key cryptography](https://www.cloudflare.com/dns/dnssec/how-dnssec-works/), allowing the DNS resolver to verify that the DNS responses they receive are valid and from the authoritative source, rather than being [manipulated](https://www.cloudflare.com/learning/dns/dns-security/) by attackers.

DNS over HTTPS (DoH) and similar protocols do **not** eliminate the need for DNSSEC to validate the integrity of DNS data. However, when using a service like Control D that can modify DNS records based on user-defined rules, there is little added benefit to enabling DNSSEC validation.

Control D also [states](https://discord.com/channels/1035992466203099147/1037876518778572860/1143716723883778088) that DNSSEC<sup>1</sup> requires a separate DNS resolver and cache, which impacts performance.

<sup> **1** At this time, [DNSSEC validation](https://www.quad9.net/support/faq/#dnssec) and [EDNS Client Subnet](https://www.quad9.net/support/faq/#edns) (ECS) are grouped together in this settings.</sup>

### TTL Overrides
:bulb: Increasing the TTL values caches DNS records for longer periods, which minimizes queries and optimizes performance.

:warning: Do not set higher than 24 hours.

Every DNS record has a time-to-live (TTL) value that determines how long devices cache the record before requesting an update from the DNS server. This caching reduces DNS queries and can improve performance.

Below are possible values to use for DNS caching, measured in seconds.

| Value   | Duration  |
|---------|-----------|
| `60`    | 1 minute  |
| `300`   | 5 minutes |
| `3600`  | 1 hour    |
| `28800` | 8 hours   |
| `43200` | 12 hours  |
| `86400` | 24 hours  |

#### Block TTL
![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

**Default value:** `10` (10 seconds)
<br> **Recommended value:** `60` (1 minute)

[Block TTL](https://docs.controld.com/docs/ttl-overrides#block-ttl) increases the time-to-live for DNS records blocked by Control D. A higher value means fewer DNS lookups for blocked requests, but also a longer delay between unblocking a domain and it becoming accessible.

:bulb: The less aggressive your Profile is, the more comfortable you may be setting this to a higher value.

#### Redirect TTL
![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

**Default value:** `20` (20 seconds)
<br> **Recommended value:** `300` (5 minutes)

A redirect rule spoofs the domain to a proxy location or alternate IP address. [Redirect TTL](https://docs.controld.com/docs/ttl-overrides#redirect-ttl) increases the time-to-live for DNS redirected by a Service, Custom Rule, or the Default Rule. A higher value means fewer DNS lookups, but also a longer delay between changing locations and the new location settings taking effect on a Device.

:warning: If you adjust redirect rules often, you may want to leave this disabled.

#### Bypass TTL
![Enabled](https://github.com/yokoffing/Control-D-Config/blob/main/assets/enabled.svg) Enable

**Default value:**  `60` (1 minute)
<br> **Recommended value:** `3600` (1 hour) or `86400` (24 hours)

[Bypass TTL](https://docs.controld.com/docs/ttl-overrides#bypass-ttl) increases the time-to-live for DNS records that were not blocked or redirected (i.e. 'normal' requests), and passed to the upstream resolver. A higher value means fewer DNS lookups, but can cause websites to break if set beyond 24 hours.

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

## Wildcard rules
[Wildcard rules](https://docs.controld.com/docs/custom-rules#rule-format) allow you to [block](https://docs.controld.com/docs/custom-rules#block) a wide spectrum of domains without listing them separately. This format is what Control D uses in their blocklists.

Control D can block subdomains by adding wildcards like `*.domain.com` to your Denylist. Blocking `*.domain.com` prevents access to all subdomains of `domain.com` without blocking the root domain itself.

For instance, adding `*.analytics.com` to the Denylist stops requests to subdomains like `tracking.analytics.com` or `metrics.analytics.com` while still allowing access to the main `analytics.com` site.

:world_map: To access Custom Rules, go to https://controld.com/dashboard/profiles > Edit > Custom Rules.

## Import & Export Folders
### Import
Control D allows you to import and export folders from other users under Custom Rules.

To download a folder:
1) Click the link.
2) On Github, select the `...` button in the top-right corner.
3) Click **Download**.
4) On Control D - Custom Rules, select the `...` icon.
5) Click **Upload Folder**.

#### TLDs
You may want to add a folder to block certain [TLDs](https://webtribunal.net/blog/tld-statistics) and [IDNs](https://alldomains.hosting/en/what-are-idn-domains.html#what-is-an-idn-domain).

[Hagezi](https://github.com/hagezi/dns-blocklists) has compiled folders for you to easily import into Control D.

* [Spam TLDs](https://github.com/hagezi/dns-blocklists/blob/main/controld/spam-tlds-folder.json)
* [Spam TLDs Allow](https://github.com/hagezi/dns-blocklists/blob/main/controld/spam-tlds-allow-folder.json)
* [Spam IDNs](https://github.com/hagezi/dns-blocklists/blob/main/controld/spam-idns-folder.json)

#### International IPs
I created a folder to block IP addresses from certain countries (see Geo Custom Rules). These countries have high rates of cybercrime or state-sponsored spyware activity.

After importing the folder, review the list and disable certain rules if they affect your region or travel destinations. The list excludes or disables rules affecting countries with high server traffic from other countries, such as the Netherlands and Israel.

The list excludes or disables rules affecting countries that have high server traffic from other nations, such as the Netherlands and Israel.

* [Potentially Malicious IPs](https://github.com/yokoffing/Control-D-Config/blob/main/folders/potentially-malicious-ips.json)

### Export
Want to share your folder? You can export it by clicking the `...` button in a folder and selecting **Download Rules**.

## Spoofing Domains

A [redirect](https://docs.controld.com/docs/services#redirect) rule proxies all domains associated with a [Service](https://docs.controld.com/docs/services) to a location or IP address you specify.

### Examples

| **Category** |     **Service**    | **Destination** |
|:------------:|:------------------:|:---------------:|
| Finance      | Citi               | Dallas, US      |
| News         | The New York Times | New York, US    |
| Tools        | Bing               | Charlotte, US   |

<details> <summary>:warning: Technical Limitations </summary>
   
* Websites or apps employing legacy security protocols might not be accessible when attempting to bypass geo-restrictions. The [redirect](https://docs.controld.com/docs/services#redirect) rule requires Server Name Indication (SNI), which is not supported in these older standards. This prevents the bypassing method from functioning as intended.
* Currently, the unencrypted SNI allows ISPs and network admins to see your visited sites when analyzing traffic with Deep Packet Inspection (DPI). [Encrypted Client Hello](https://github.com/yokoffing/Betterfox/blob/14de7b101d48f15f50df7dd5dbfffefca5b4a855/Securefox.js#L725-L729) (ECH) is coming but it's not widely used yet.
* Control D is not a VPN; it will not bypass government restrictions.

</details>

### Instructions
Control D provides a simple and effective way to use DNS-based traffic redirection for popular services

1) To access services, go to https://controld.com/dashboard/profiles > Edit > Services.
2) Choose a category.
3) Select the third icon (globe).
4) Choose a proxy location.

## Geo Custom Rules
:warning: This feature is still in beta.

[Geo Custom Rules](https://docs.controld.com/docs/geo-custom-rules) (GCRs) allow you to create custom rules based on the geo-location data of source and destination IPs for DNS queries. These rules allow you to redirect, block, or bypass domains that resolve to IPs in the chosen country.

GCRs start with the formats below, followed by a two-letter [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements).

| **Symbol**   | **Definition**                                                        |
|--------------|-----------------------------------------------------------------------|
| `@`          | Domains **resolve** to an IP address in a destination country.        |
| `!@`         | Domains **do not resolve** to an IP address in a destination country. |

### Create a folder (optional)
I recommend you put all these rules in their own folder:
1. To access Custom Rules, go to https://controld.com/dashboard/profiles > Edit > Custom Rules.
2. Under the desired profile, add the folder by clicking the big green `+` button.
3. Select **Folder**.
4. Under **Folder Name**, type `Geo Custom Rules`.
5. Click **Add Folder**.

### Block Examples
#### 1) Block specific countries
Let's assume you only want to **block** DNS queries to domains that resolve to servers in countries with known cybersecurity threats like Russia or China.

You would create the following two rules `@RU` and `@CN` both with a [block](https://docs.controld.com/docs/geo-custom-rules#block) rule, to stop anything that resolves to a Russian or Chinese IP.

| **Rule** | **Symbol** | **Country** | **Description**                                             |
|----------|------------|-------------|-------------------------------------------------------------|
| Block    | `@`        | `RU`        | Block domains that resolve to a Russian IP address.        |
| Block    | `@`        | `CN`        | Block domains that resolve to a Chinese IP address.         |

Result: Web requests that would resolve in those countries are blocked.

:bulb: I created a folder called [Potentially Malicious IPs](https://github.com/yokoffing/Control-D-Config/blob/main/folders/potentially-malicious-ips.json) to block countries with high suspected state-sponsored spyware activity or cybercrime rates. If you live outside the U.S. or travel internationally, you should review the list after importing.

#### 2) Lockdown network
So let's say you're a real glutton for punishment and want to limit your network connections to **only** the United States and Canada. Control D can understand multiple `!@` block rules, if you want to limit your DNS resolutions to a handful of countries.

You would use `!@US` and `!@CA` both with a [block](https://docs.controld.com/docs/geo-custom-rules#block) rule, to prevent any DNS resolutions to domains outside of these countries.

| **Rule** | **Symbol** | **Country** | **Description**                                                        |
|----------|------------|-------------|------------------------------------------------------------------------|
| Block    | `!@`       | `US`        | Block domains that **don't** resolve to a United States IP address. |
| Block    | `!@`       | `CA`        | Block domains that **don't** resolve to a Canadian IP address. |

Result: DNS resolutions are blocked unless the domains resolve to servers located in the United States or Canada.

:warning: The method described above imposes greater restrictions compared to Example 1. This will lead to unforeseen complications during everyday web browsing.

### Redirect Examples
#### 3) Resolve IP address in a chosen country
You can use a [redirect](https://docs.controld.com/docs/geo-custom-rules#redirect) rule to resolve to IPs in the chosen country.

| **Rule** | **Location Override** | **Symbol** | **Country** | **Description**                                                |
|----------|-----------------------|------------|-------------|----------------------------------------------------------------|
| Redirect | Mexico City, MX       | `@`        | `MX`        | Redirect domains that resolve to an IP address in Mexico through a Mexican proxy server. |

Result: You're essentially browsing the internet as if you were physically located in Mexico.

#### 4) Resolve foreign domains via a proxy
In this example, let's assume you live in the United States. You can automatically [redirect](https://docs.controld.com/docs/geo-custom-rules#redirect) non-US IP addresses through a proxy.

| **Rule** | **Location Override** | **Symbol** | **Country** | **Description**                                                |
|----------|-----------------------|------------|-------------|----------------------------------------------------------------|
| Redirect | New York, US          | `!@`       | `US`        | Redirect domains that **don't** resolve to a United States IP address through a New York proxy server. |

Result: You route any requests originating outside the United States through a proxy server located in New York.

### Bypass Example
#### 5) Create exceptions for the proxy
This setup is useful if you have the [Default Rule](https://docs.controld.com/docs/default-rule) set to redirect ([read more](https://docs.controld.com/docs/default-rule#redirect)) and want to make exceptions, to resolve certain requests without a proxy.

| **Rule** | **Symbol** | **Country** | **Description**                                                        |
|----------|------------|-------------|------------------------------------------------------------------------|
| Bypass   | `@`        | `US`        | Domains with a United States IP address are resolved normally.         |

Result: All requests are redirected through a proxy via the Default Rule except domains with a United States IP address.

The inverse of this is similar to the chart in Example 4.

:memo: You can also make rules for source IPs, not just destination. Read the [docs]((https://docs.controld.com/docs/geo-custom-rules)) if you're curious. 
