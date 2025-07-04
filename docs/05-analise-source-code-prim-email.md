# 5. Análise do *Source Code* -- Primeira Tentativa de Phishing 

Aqui será analisado o *source code* da primeira tentativa de phishing, onde será feita uma análise *in depth* dos headers.

## 5.1 Cadeia de Recebimento (*Received Chain*)

A cadeia de recebimento (*received chain*) é formada pelos servidores que manipularam o e-mail, incluindo o servidor do destinatário. Podemos fazer um rastreamento percorrendo o source code do e-mail na direção *top -> bottom*. 

No *top* está a conexão mais recente (geralmente o servidor do destinatário), enquanto que no *bottom* está a conexão mais antiga, ou seja, a do servidor que originou a comunicação.

A importância destes elementos reside no fato de que todos os endereços de IP dos servidores estão no *source code*, o que nos permite analisar o caminho feito pelo e-mail. Porém, isso nos dará apenas uma ideia do que
pode ter ocorrido, já que os IPs não são uma fonte confiável de *intel*.

No **primeiro bloco** do email temos o último ponto de contato (servidor mais recente): ``cpanel-003-fra.hostingww.com``, usando o protocolo LMTP. Este contato é o servidor do provedor de email do cliente.

```
  X-Mozilla-Status: 0001
  X-Mozilla-Status2: 00000000
  Return-Path: <hr@corridorconstructioniowa.cam>
  Delivered-To: ceo@msolutions.com
  Received: from cpanel-003-fra.hostingww.com
    by cpanel-003-fra.hostingww.com with LMTP
    id EGKZEk+WC2jNvzYA2p0M4Q
    (envelope-from <hr@corridorconstructioniowa.cam>)
    for <ceo@msolutions.com>; Fri, 25 Apr 2025 14:03:59 +0000
  Return-path: <hr@corridorconstructioniowa.cam>
  Envelope-to: ceo@msolutions.com
  Delivery-date: Fri, 25 Apr 2025 14:03:59 +0000
```

No **segundo bloco** temos outro servidor, de IP ``148.113.172.133`` e URL ``vps-58680c2d.vps.ovh.ca``. Neste bloco o servidor de envio ``vps-58680c2d.vps.ovh.ca`` se anuncia ao servidor de recebimento usando o
``helo=mail.corridorconstructioniowa.cam``, e o servidor do cliente aceita receber o email. O ``helo`` funcionaria como um "handshake" e é uma parte essencial no protocolo SMTP, já que ele verifica a saúde dos servidores.

```
  Received: from vps-58680c2d.vps.ovh.ca ([148.113.172.133]:46792 helo=mail.corridorconstructioniowa.cam)
    by cpanel-003-fra.hostingww.com with esmtps  (TLS1.3) tls TLS_AES_256_GCM_SHA384
    (Exim 4.98)
    (envelope-from <hr@corridorconstructioniowa.cam>)
    id 1u8Jep-0000000FOHA-1KmS
    for ceo@msolutions.com;
    Fri, 25 Apr 2025 14:03:59 +0000
  DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/simple;
    d=corridorconstructioniowa.cam; s=202502; t=1745589723;
    bh=27SJj8BZJ8l+ac4w7EED3uS3UQaeMwpWWY+B6MYbbRw=;
    h=Reply-To:From:To:Subject:Date:From;
  
```
