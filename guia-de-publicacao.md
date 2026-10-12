# Mente sem Caos: guia de publicação

Arquivos: `index.html` (página de vendas), `obrigado.html` (página pós-compra) e `cancelar.html` (como cancelar a assinatura). Publique os três na mesma pasta.
Procure por `[PREENCHER` nos dois arquivos para achar tudo o que falta.

## 1. Conectar o checkout (quando escolher a plataforma)

1. Crie o produto na plataforma como **assinatura (recorrência) mensal de R$ 97**, não como venda avulsa, e copie o link de checkout.
   Antes de escolher a plataforma, confirme três coisas:
   - o assinante consegue **cancelar sozinho** pela área do cliente;
   - o cancelamento **impede a próxima cobrança** automaticamente;
   - você recebe um **aviso (e-mail ou webhook) a cada cancelamento** e a cada renovação recusada.
2. No início do `index.html`, cole o link em `data-checkout-url="https://..."`.
   Todos os botões passam a apontar para ele, levando junto os parâmetros `utm_*`, `src` e `sck` da URL.
3. Na plataforma, configure a **página de obrigado / redirecionamento pós-compra aprovada** para o endereço do seu `obrigado.html`.
4. No `obrigado.html`, cole o convite do grupo em `data-whatsapp-url="https://chat.whatsapp.com/..."`.
5. Cadastre o e-mail de boas-vindas (abaixo) como e-mail automático de compra aprovada.
6. No `cancelar.html`, preencha `data-cancel-url` (link da área do cliente da plataforma), `data-support-email` e `data-support-whatsapp`. Confira se os nomes dos menus descritos na página batem com os da plataforma.

Enquanto o link de checkout estiver vazio, os botões levam à seção da oferta e mostram um aviso de "checkout não conectado".

## 2. E-mail de boas-vindas

**Assunto:** Sua vaga na Mente sem Caos está confirmada

Olá, [NOME]!

Sua assinatura foi aprovada e sua vaga na Mente sem Caos está garantida.

**1. Entre no seu grupo no WhatsApp**
[LINK DE CONVITE DO GRUPO]
É por lá que chegam os avisos, os links dos encontros e as práticas da semana. O link é pessoal, por favor não compartilhe.

**2. Acesse o RespirApp**
[INSTRUÇÕES DE ACESSO AO APP]. Lá estão os áudios para praticar entre os encontros.

**3. Anote o primeiro encontro**
[DATA, HORÁRIO E LINK]. Os encontros são ao vivo, uma vez por semana, com 1 hora de duração.

**4. Até lá, um minuto por dia**
Inspire pelo nariz por 4 segundos e solte o ar por 6. Repita 6 vezes. É o mesmo exercício da página, e já é o começo do treino.

**Sobre a sua assinatura**
O valor é R$ 97 por mês e a renovação é automática. Você pode cancelar quando quiser, sem multa, e nenhuma nova cobrança é feita depois disso. Passo a passo: [LINK DA PÁGINA cancelar.html]

Você tem 7 dias a partir desta compra para desistir e receber o valor de volta. Basta responder este e-mail.

Dúvidas: [CONTATO DE SUPORTE]

Até o primeiro encontro,
Andrei Vargas
Mente sem Caos

*O programa é educacional e não substitui acompanhamento médico ou psicológico.*

## 3. Assinatura e cancelamento

A página de cancelamento informa o caminho. Quem para a cobrança de fato é a plataforma, e quem garante que nada escape é este processo.

### Regras que a página promete (mantenha as duas coisas iguais)
- Cancelar a qualquer momento, sem multa e sem justificativa.
- Nenhuma cobrança depois do cancelamento.
- Acesso ao grupo até o fim do mês já pago.
- Devolução integral se o cancelamento for em até 7 dias da primeira compra.
- Devolução integral de qualquer cobrança feita por engano depois do cancelamento.

### Quando a pessoa cancela pela plataforma
1. A plataforma encerra a assinatura e você recebe o aviso.
2. Anote nome, e-mail, data do cancelamento e data em que o período pago termina.
3. Se for dentro dos 7 dias da primeira compra, faça o reembolso na plataforma.
4. No fim do período pago, remova a pessoa do grupo do WhatsApp e desative o acesso dela ao RespirApp.

### Quando a pessoa pede pelo contato (e-mail ou WhatsApp)
1. Cancele você mesmo a assinatura no painel da plataforma, no mesmo dia útil.
2. Confira no painel que **não existe próxima cobrança agendada**.
3. Envie o e-mail de confirmação (abaixo).
4. Siga os passos 2 a 4 do item anterior.

### Todo mês
- Compare a lista de assinantes ativos na plataforma com os participantes do grupo.
- Quem está no grupo sem assinatura ativa sai do grupo.
- A cada nova turma, gere um novo link de convite do grupo.

### E-mail de confirmação de cancelamento

**Assunto:** Cancelamento da sua assinatura Mente sem Caos confirmado

Olá, [NOME].

Sua assinatura da Mente sem Caos foi cancelada em [DATA]. Nenhuma nova cobrança será feita.

Você continua no grupo da turma até [DATA DE FIM DO PERÍODO PAGO].
[SE DENTRO DE 7 DIAS: O reembolso de R$ 97 já foi solicitado e aparece na sua fatura ou conta conforme o prazo do meio de pagamento.]

Se notar qualquer cobrança depois desta data, responda este e-mail e o valor é devolvido integralmente.

Obrigado por ter praticado com a gente. Se quiser voltar, a porta está aberta.

Andrei Vargas
Mente sem Caos

### Aviso antes da renovação (recomendado)
Muitas plataformas enviam um e-mail automático antes de cada cobrança recorrente. Se a sua enviar, ative. Se não, mande este aviso uns 3 dias antes da primeira renovação:

**Assunto:** Sua assinatura Mente sem Caos renova em [DATA]

Olá, [NOME]. Em [DATA], sua assinatura da Mente sem Caos renova automaticamente por R$ 97 e você continua no grupo e com acesso ao RespirApp. Se preferir não continuar, cancele antes dessa data: [LINK cancelar.html]

## 4. Checklist de segurança

### Já feito no código
- [x] Nenhum dado de pagamento ou pessoal é coletado na página. Não há formulários.
- [x] Nenhuma chave de API, token ou segredo no código.
- [x] Zero requisições a terceiros: fontes embutidas no arquivo, sem CDN, sem scripts externos.
- [x] Content-Security-Policy restritiva: `default-src 'none'`, script liberado apenas pelo hash sha256, `base-uri 'none'`, `form-action 'none'`, `object-src 'none'`.
- [x] O link de checkout só é aceito se for `https://`. O do grupo só se for `https://chat.whatsapp.com/`.
- [x] Links externos com `rel="noopener noreferrer"`.
- [x] O link do WhatsApp não existe no `index.html` nem no `cancelar.html`.
- [x] `obrigado.html` com `noindex, nofollow, noarchive` e `referrer: no-referrer`.
- [x] Aviso de cookies com Aceitar/Recusar; Pixel e GA4 só carregam após o aceite. O aviso só aparece se você configurar um ID.
- [x] Acessibilidade: navegação por teclado, foco visível, link "pular para o conteúdo", `prefers-reduced-motion` respeitado.

### Limites que você precisa conhecer
- **Hash do script:** se editar qualquer caractere dentro do `<script>`, o navegador bloqueia o script até o hash da CSP ser atualizado (o console do navegador mostra o hash correto na mensagem de erro). Editar textos, HTML e os atributos `data-*` não afeta nada.
- **Estilos:** a CSP usa `style-src 'unsafe-inline'` para você poder editar o CSS livremente. É o ponto menos restrito da política.
- **Página de obrigado:** uma página estática não consegue verificar se quem a abriu pagou. Quem tiver o endereço vê o link. A proteção real é: ativar **"Aprovar novos participantes"** no grupo e conferir com a lista de compradores; trocar o link de convite a cada turma.
- **Pixel/GA4:** ao preencher `data-meta-pixel-id` ou `data-ga4-id`, acrescente à CSP:
  `script-src ... https://connect.facebook.net https://www.googletagmanager.com; connect-src https://www.facebook.com https://*.google-analytics.com https://*.googletagmanager.com; img-src 'self' data: https://www.facebook.com https://*.google-analytics.com`

### Para configurar na hospedagem
O GitHub Pages não permite cabeçalhos personalizados. Em Cloudflare Pages ou Netlify, crie um arquivo `_headers` na raiz:

```
/*
  Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()
  Content-Security-Policy: frame-ancestors 'none'
  X-Frame-Options: DENY

/obrigado*
  X-Robots-Tag: noindex, nofollow, noarchive
  Referrer-Policy: no-referrer
  Cache-Control: no-store
```

- [ ] HTTPS forçado no domínio
- [ ] Cabeçalhos acima ativos (teste em securityheaders.com)
- [ ] `obrigado.html` fora do sitemap e sem link em nenhuma página

## 5. Checklist de publicação
- [ ] Todos os `[PREENCHER]` resolvidos (dia e horário dos encontros, gravação, acesso ao app, bônus, foto, CNPJ/contato)
- [ ] Acesso ao RespirApp liberado para cada nova assinatura e retirado quando a pessoa cancela
- [ ] Política de Privacidade e Termos de Uso publicados, com as regras de assinatura e cancelamento nos Termos e ligados em `data-privacy-url` e `data-terms-url`
- [ ] Checkout conectado e uma compra de teste feita do início ao fim (pagar, cair no obrigado, entrar no grupo, receber o e-mail)
- [ ] Cancelamento de teste pela área do cliente, conferindo no painel que a próxima cobrança sumiu
- [ ] `cancelar.html` com área do cliente, e-mail e WhatsApp preenchidos
- [ ] Reembolso de teste na plataforma
- [ ] Página conferida no celular
