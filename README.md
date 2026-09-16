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
| `ENDPOINT` | Edge Function `captura-lead` do Supabase (projeto Revita CRM) — **já preenchido** |
| `META_PIXEL` | ID do pixel **da Revita** — nunca o de outra marca do grupo |
| `GA4` | ID de medição |

Vazio significa desligado: a página continua funcionando, avisa no console o que
falta, e o lead fica numa fila local que é reenviada sozinha quando o endpoint existir.

## Onde a lead cai

`formulario` → `POST` na Edge Function `captura-lead` → tabela `public.leads`
(projeto Supabase **Revita CRM**, `xejbwyrqgktrqhhtavdh`).

A função escreve com `service_role`, que nunca sai do servidor. A tabela tem RLS
ligado e **nenhuma policy**: fora essa função, nada lê nem escreve. Por isso não
há chave de banco neste repositório, que é público.

A função também: normaliza nome e e-mail, converte o telefone para `+55DDDNNNNNNNN`
(sem quebrar DDD 55, do Rio Grande do Sul), separa os UTMs em colunas, deduplica
por e-mail via upsert — quem preenche duas vezes atualiza a própria linha e mantém
a data da primeira inscrição — e descarta bot pelo campo isca `#site-url`.

Se a função estiver fora do ar, o `enviar()` da página guarda a lead em
`localStorage` e reenvia sozinho no próximo carregamento. A tela de sucesso
aparece de qualquer jeito: falha de webhook nunca pode bloquear a pessoa de
entrar no grupo.

## Estrutura

`tarja com contagem` → `hero` → `o inimigo` → `o código` → `rodapé` → `modal de captação`

Imagens do produto em `assets/produto/` (as mesmas já embutidas no HTML).
