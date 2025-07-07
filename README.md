# CTI-case-study

No contexto atual da digitalização de processos corporativos, o e-mail permanece como um dos principais vetores de comunicação e ao mesmo tempo um dos mais explorados por agentes maliciosos. A engenharia social, aliada a técnicas cada vez mais sofisticadas de spoofing e clonagem de páginas legítimas, permite que atacantes influenciem usuários a revelar credenciais críticas ou a executar ações que comprometam a segurança organizacional.

Este relatório apresenta a aplicação prática de Cyber Threat Intelligence (CTI) para a análise de um e-mail de phishing direcionado a uma empresa de pequeno porte do setor de energia. Com base em ferramentas consolidadas como VirusTotal, Hybrid-Analysis e MITRE ATT&CK, aliado ao uso de BurpSuite para inspeção manual, busquei identificar padrões de ataque, indicadores de comprometimento e vulnerabilidades exploradas.

Ao explorar tanto o design do e-mail (pretexto, entrega e técnicas de spoofing), quanto o comportamento dinâmico de páginas clonadas e back-end malicioso, o documento tem como objetivo demonstrar os riscos inerentes à ausência de controles de autenticação de origem (SPF, DKIM, DMARC) e propõe um procedimento replicável de mitigação. Dessa forma, esta análise serve de base para fortalecer a postura de defesa contra campanhas de phishing futuras.

[Contexto](https://github.com/e-v-s/CTI-case-study/blob/main/docs/02-contexto.md)
[Objetivos](https://github.com/e-v-s/CTI-case-study/blob/main/docs/03-objetivos.md)
[Análise dos emails](https://github.com/e-v-s/CTI-case-study/blob/main/docs/04-analise-dos-emails.md)
[Análise do source code - Primeiro email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/05-analise-source-code-prim-email.md)
[Análise com sandbox - Primeiro email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/06-analise-com-HA-prim-email.md)
[Novo ataque - Segundo email](https://github.com/e-v-s/CTI-case-study/blob/main/docs/07-novo-ataque-seg-email.md)
[Rastreamento de vulnerabilidades e Conclusão](https://github.com/e-v-s/CTI-case-study/blob/main/docs/8-rastreamento-de-vuln.md)
