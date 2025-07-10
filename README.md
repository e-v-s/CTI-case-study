# CTI-case-study

In today’s world of digitized business processes, email is still a primary communication channel—and also a favorite playground for bad actors. Social engineering, combined with ever-more-sophisticated spoofing and fake “clone” websites, lets attackers trick people into handing over key credentials or taking actions that undermine a company’s security.

This report shows a hands-on Cyber Threat Intelligence (CTI) analysis of a phishing email aimed at a small energy firm. Using established tools like VirusTotal, Hybrid-Analysis and the MITRE ATT&CK framework—alongside manual inspection with BurpSuite—I’ve mapped out attack patterns, identified compromise indicators and zeroed in on exploited vulnerabilities.

By dissecting both the email’s design (its pretext, delivery methods and spoofing tricks) and the dynamic behavior of cloned pages and malicious back-ends, this document highlights the dangers of skipping origin-authentication controls (SPF, DKIM, DMARC). It then lays out a repeatable mitigation procedure. In short, this analysis is your playbook for bolstering defenses against future phishing campaigns.

[1 Context](https://github.com/e-v-s/CTI-case-study/blob/main/docs/02-contexto.md)

[2 Objectives](https://github.com/e-v-s/CTI-case-study/blob/main/docs/03-objetivos.md)

[3 Email analysis](https://github.com/e-v-s/CTI-case-study/blob/main/docs/04-analise-dos-emails.md)

[4 Source code analysis - First email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/05-analise-source-code-prim-email.md)

[5 Sandbox analysis - First email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/06-analise-com-HA-prim-email.md)

[6 New attack - Second email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/07-novo-ataque-seg-email.md)

[7 Vulnerability tracking and conclusion](https://github.com/e-v-s/CTI-case-study/blob/main/docs/8-rastreamento-de-vuln.md)
