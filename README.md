# BeHe Import — landing page (lojabehe.com)

Página de venda da **BeHe Import** (equipamentos audiovisuais premium). Feita para quem chega pelo link da bio do
Instagram [@behe_ofc](https://www.instagram.com/behe_ofc/), no celular, e termina a compra no WhatsApp.

- **No ar:** https://lojabehe.com (o `www` redireciona para o domínio principal)
- **Hospedagem:** GitHub Pages, publicado a partir da branch `main`, pasta raiz
- **Domínio e DNS:** Cloudflare (conta da BeHe), registros sem proxy apontando para o GitHub Pages

## O que tem aqui

| Arquivo | Para que serve |
|---|---|
| `index.html` | A página inteira: HTML, CSS (no `<style>`) e JavaScript (no `<script>`) num arquivo só |
| `assets/logo-behe.webp` / `.png` | Logo real da BeHe (fundo transparente) |
| `assets/favicon.png`, `assets/apple-touch-icon.png` | Ícones da aba do navegador e da tela inicial do celular |
| `assets/og-behe.jpg` | Imagem que aparece quando o link é compartilhado (WhatsApp, Instagram, Facebook) |
| `CNAME` | Diz ao GitHub Pages que o domínio é `lojabehe.com` — não apague |
| `.nojekyll` | Publica os arquivos como estão, sem processamento do Jekyll |

## Como editar o que mais muda

Tudo fica no `index.html`. Procure pelos marcadores:

- **Fotos:** cada imagem provisória (Unsplash) tem um comentário `<!-- TROCAR: ... -->` logo acima. Coloque a foto real em
  `assets/` (de preferência `.webp`, até ~200 KB) e troque o `src`/`srcset` pelo caminho relativo, por exemplo
  `assets/sony-a7iv.webp`. Mantenha `width` e `height` com as proporções da foto nova.
- **Prints de clientes (mural de Stories):** mesma coisa — os quadros 9:16 da seção "Quem Compra, Recomenda" estão
  marcados para receber os prints reais.
- **WhatsApp:** todos os botões usam `https://wa.me/5545998382728?text=...`. Para trocar o número, substitua
  `5545998382728` em todo o arquivo (busca e troca) **e também** o número escrito `99838-2728` (dados estruturados no
  `<head>`, chamada final e rodapé). Cada botão manda uma mensagem com `(origem: lp-...)`, que mostra
  no próprio WhatsApp de qual botão a pessoa veio.
- **Pixel do Meta e Google Analytics:** os blocos estão prontos e comentados no `<head>`. Coloque o ID real no lugar de
  `SEU_PIXEL_ID` / `G-XXXXXXX` e apague só as duas linhas marcadas com ✂ de cada bloco. Os cliques no WhatsApp já disparam `Contact` (Meta) e
  `clique_whatsapp` (Google) quando esses scripts estiverem ativos.
- **Produtos em destaque:** os quatro cards da seção "Os Mais Pedidos do Momento" — nome, tag, especificações e a
  mensagem do WhatsApp de cada um.

## Publicar uma alteração

```bash
git add -A
git commit -m "feat: descreva a mudança"
git push
```

O GitHub Pages republica sozinho em 1 a 2 minutos. Acompanhe em *Actions* no repositório.

## Decisões técnicas

- **CSS escrito à mão, sem Tailwind pelo CDN e sem Font Awesome.** Mais de 85% das visitas vêm do celular; o Tailwind
  pelo CDN compila o CSS no navegador a cada visita e o Font Awesome baixa uma fonte inteira de ícones. Aqui os ícones
  são SVG dentro da página e o CSS já vem pronto — a página abre mais rápido no 4G.
- **Funciona sem JavaScript.** Os links do WhatsApp já vêm prontos no HTML; o JavaScript só cuida do menu do celular, dos
  eventos de medição e de pequenos detalhes.
- **DNS sem proxy da Cloudflare.** O GitHub emite e renova o certificado HTTPS sozinho quando o domínio aponta direto para
  ele; o domínio está verificado na conta do GitHub (registro TXT `_github-pages-challenge-…`), o que impede outra conta de
  publicar nele.
