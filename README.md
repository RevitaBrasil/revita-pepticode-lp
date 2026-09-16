# Revita Derma · Pepti Code — LP do grupo VIP

Landing page de captação para o encontro de pré-lançamento do **Pepti Code**,
dia **24/09 às 20h**. Arquivo único e autocontido: `index.html`.

## No ar

- **Produção** — https://lp.revitaderma.com.br
- **Preview direto** — https://raw.githack.com/operacaorevitaderma-design/revita-pepticode-lp/main/index.html

`revitaderma.com.br` (raiz e `www`) é do Shopify. Esta LP vive só no subdomínio `lp.`,
servida pelo GitHub Pages a partir da `main`.

### Como o domínio está ligado

| Onde | Registro | Valor |
|---|---|---|
| GoDaddy (DNS) | `CNAME` `lp` | `operacaorevitaderma-design.github.io` |
| Este repo | `CNAME` (arquivo) | `lp.revitaderma.com.br` |
| GitHub | Settings → Pages | branch `main`, `/ (root)`, Enforce HTTPS ligado |

O arquivo `CNAME` na raiz do repo é o que mantém o domínio depois de cada push —
se ele sumir, o Pages volta pro endereço `github.io` e o subdomínio cai.

Para ligar o Pages: Settings → Pages → Source `Deploy from a branch` → Branch `main` → `/ (root)`.

## Antes de apontar mídia paga

Preencher o bloco `window.RVT`, no topo do `index.html`:

| Chave | O que é |
|---|---|
| `GRUPO_WHATSAPP` | link do grupo (`https://chat.whatsapp.com/…`) |
| `ENDPOINT` | webhook que recebe o lead (ActiveCampaign, SendFlow ou n8n) |
| `META_PIXEL` | ID do pixel **da Revita** — nunca o de outra marca do grupo |
| `GA4` | ID de medição |

Vazio significa desligado: a página continua funcionando, avisa no console o que
falta, e o lead fica numa fila local que é reenviada sozinha quando o endpoint existir.

## Estrutura

`tarja com contagem` → `hero` → `o inimigo` → `o código` → `rodapé` → `modal de captação`

Imagens do produto em `assets/produto/` (as mesmas já embutidas no HTML).
