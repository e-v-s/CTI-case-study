# 4 Análise dos Emails

## 4.1 Pretextos

Os atacantes usaram técnicas psicológicas de engenharia social como **urgência**, ao tratar de assuntos sensíveis como acesso indevido e inativação de conta, e **autoridade** ao se direcionar ao alvo como RH (primeira tentativa de phishing, março-2025 Figura 1), e como o suporte da própria plataforma de email da empresa (segunda tentativa, junho-2025, Figura 2).

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura1.png" width="200">
    <p>Figura 1: Pretexto do primeiro email</p>
  </div>
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura2.png" width="200">
    <p>Figura 2: Pretexto do segundo email</p>
  </div>
</div>

## 4.2 Páginas Clonadas

Neste tópico veremos as páginas clonadas do **primeiro** e do **segundo** ataque, em contraste com a **página oficial**.

Na **página oficial**, logo abaixo, podemos notar que a URL está correta e o site usa https.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura3.png" width="400">
    <p>Figura 3: Página original</p>
  </div>
</div>

No **primeiro** clone, nota-se uma URL completamente diferente da original, e o email do usuário já está populado. Os idiomas abaixo também estão mal escritos. No **segundo** clone, o atacante usou um provedor de sites web, nota-se o mesmo problema na apresentação dos idiomas, além das caixas de input não parecerem profissionais.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura4.png" width="200">
    <p>Figura 4: Primeiro clone</p>
  </div>
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura5.png" width="400">
    <p>Figura 5: Segundo clone</p>
  </div>
</div>

## 4.3 Objetivo do Atacante

Com base no clone das páginas de login e na análise feita com o software BurpSuite, o phishing tinha como objetivo coletar as credenciais do alvo. O spoofing do email e seu uso como remetente facilita a exposição de credenciais e possível vazamento de dados em cadeia, comprometendo tanto a privacidade do alvo, quanto a dos clientes para os quais o alvo fornece serviços.

Na Figura 7, observa-se que, ao clicar no botão Log in, as credenciais são enviadas em um request do tipo POST para um servidor malicioso, também identificado na imagem. Detalhe que as informações são enviadas em *plaintext*, ou seja, completamente sem criptografia.

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura6.png" width="400">
    <p>Figura 6: Exemplo de inserção de credenciais.</p>
  </div>
</div>

<div style="display: flex;">
  <div style="justify-items: center; margin: 50px;">
    <img src="../images/figura7.png" width="400">
    <p>Figura 7: Resquest POST.</p>
  </div>
</div>
