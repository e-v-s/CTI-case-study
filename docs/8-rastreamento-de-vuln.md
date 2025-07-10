# 8 Vulnerability Tracking

## 8.1 Email Spoofing

Email spoofing happens when an attacker sends a message pretending to be from a legitimate email or domain. Unlike the TLD squatting we saw in the first phishing case, here the attacker forges the `From:` or other header fields.

To illustrate, assuming our company codename is MSolutions and the domain is `msolutions.com`, the attacker used `no-reply@msolutions.com`, a spoofed address. The target’s server didn’t flag it as spam. That’s a failure of the domain and web server configuration; with proper protections, this spoofed mail would have been blocked or quarantined. Since it wasn’t, we can conclude the target’s webmail and DNS lacked necessary safeguards. **So, what protections prevent corporate email spoofing?**

There are three defenses to implement: Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM), and Domain-based Message Authentication, Reporting & Conformance (DMARC). We’ll dive into each next.

## 8.2 SPF

SPF is an authentication mechanism letting a domain owner publish, via DNS TXT records, which IP addresses or hostnames can send email on that domain’s behalf. By default, SMTP doesn’t verify the `From:` address, so an attacker with any mail server can simply spoof the header.

In our case, the attacker set `From: no-reply@msolutions.com`—an address that doesn’t exist. This vulnerability in the target’s SPF configuration was exploited. The small size of the company “helped,” since the CEO recognizes valid internal addresses.

SPF lives in the domain’s DNS TXT record (e.g. for `msolutions.com`). At the time, the SPF record was configured—but evidently not strict enough.

## 8.3 DKIM

DKIM authenticates email by having an authorized mail server “sign” outgoing messages with a private key, ensuring integrity and legitimacy.

The mail server generates a public/private key pair. The public key goes in DNS as a TXT record under a selector subdomain (e.g. `default._domainkey.msolutions.com`). With DKIM in place, outgoing mail is signed with the private key; recipients fetch the public key via DNS, recompute the hash, and verify the signature.

<mark style="background-color: rgb(220, 72, 55);">At the DNS provider, DKIM was not configured.</mark> This made domain spoofing trivially easy. Some mail servers outright reject unsigned mail, so missing DKIM can also block legitimate messages.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura24.png" width="600">
    <p>Figure 24: DKIM implementation</p>
  </div>
</div>

DKIM was added by generating a key in the email provider, then publishing the public key in DNS under `default._domainkey`. After correct setup, the provider reports a valid DKIM.

## 8.4 DMARC

DMARC is a DNS-published policy telling recipient servers how to handle emails failing SPF and/or DKIM checks. It must be added to the domain’s DNS.

DMARC policies include **none** (take no action), **quarantine** (send to spam), and **reject** (deny delivery).

A DMARC record requires SPF and DKIM to be in place. Since DKIM was missing, <mark style="background-color: rgb(220, 72, 55);">DMARC was also absent</mark>.

DMARC can also specify reporting emails:

```
  v=DMARC1; p=quarantine; rua=mailto:dmarc-aggregate@msolutions.com; ruf=mailto:dmarc-forensic@msolutions.com
```

A simple policy like the one above was added after DKIM was validated.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura25.png" width="600">
    <p>Figure 25: DMARC implementation</p>
  </div>
</div>

# 9. Conclusion

All organizations, big or small, are vulnerable to spoofing attacks. To prevent credential leaks via phishing, and protect user privacy and corporate integrity, email authentication controls (SPF, DKIM, DMARC) and ongoing monitoring must be implemented.

These controls strengthen the **confidentiality**, **integrity**, and **availability** pillars of information security. By blocking domain and email spoofing, they reduce the risk of credential exposure, preventing:

- Employees’ data from being phished (confidentiality);  
- System outages caused by compromised credentials (availability);  
- Tampering with legitimate corporate emails (integrity);  
- Attackers from abusing the company domain in future campaigns, which could also target clients.  

**Previous:** [New attack - Second email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/07-novo-ataque-seg-email.md)

**You're here:** [Vulnerability tracking and conclusion](https://github.com/e-v-s/CTI-case-study/blob/main/docs/8-rastreamento-de-vuln.md)
