# 7. New Series of Attacks, June | 2025 – Second Phishing Attempt

At the start of June, the company faced the same type of attack. In a single day, they received 7 phishing emails with the same pretext. A key detail: the attacker used the target’s own corporate email domain, a clear sign of email spoofing from their own domain. Unlike the previous attack—which used a TLD-squatting email from another company—this one showed no signs of typosquatting or other tricks; it was genuinely a spoofed support email.

The Hybrid-Analysis sandbox returned nothing, probably because this is a very recent phishing campaign. Attackers often spin up new domains with short lifespans so analysis tools can’t flag them in time.

Until June 3rd, the link worked; now, not only is the page gone, but Google Safe Browsing already marks it as malicious.

| Button link |
| - |
| hxxp[://]webmailsecureonlinelogin83kksdmsmsm[.]weebly[.]com/ |

The “Verify your account here” button points not to IPFS but to a legitimate domain provider, Weebly. This provider has a documented history of hosting phishing sites, as noted [here](https://blog.eclecticiq.com/financially-motivated-threat-actor-leveraged-google-docs-and-weebly-services-to-target-telecom-and-financial-sectors) and [here](https://unit42.paloaltonetworks.com/platform-abuse-phishing/).

The VirusTotal link analysis showed two platforms flagged it as malicious, but the DETAILS only reflected the provider’s domain, not the attacker’s.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura20.png" width="600">
    <p>Figure 20: Link analysis on VirusTotal</p>
  </div>
</div>

## Analysis with BurpSuite

Since VirusTotal and Hybrid-Analysis turned up nothing, I inspected the HTTP requests via BurpSuite.

As soon as the malicious page loads, the request below fires. On line 09 there’s an `XMLHttpRequest` (an AJAX/XHR call) that typically fetches JSON payloads via JavaScript in the background—here connecting to the attacker’s API.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura21.png" width="600">
    <p>Figure 21: HTTP header</p>
  </div>
</div>

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura22.png" width="600">
    <p>Figure 22: Requests in BurpSuite</p>
  </div>
</div>

On the page, credentials (username and password) were entered to see backend behavior. As shown below, a `POST` request is sent to the malicious site’s AJAX server with the credentials in plaintext. **It’s obvious the attack’s goal was credential harvesting.**

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura23.png" width="600">
    <p>Figure 23: Credentials submission</p>
  </div>
</div>

**Previous:** [Sandbox analysis - First email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/06-analise-com-HA-prim-email.md)

**You're here:** [New attack - Second email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/07-novo-ataque-seg-email.md)

**Next:** [Vulnerability tracking and conclusion](https://github.com/e-v-s/CTI-case-study/blob/main/docs/8-rastreamento-de-vuln.md)
