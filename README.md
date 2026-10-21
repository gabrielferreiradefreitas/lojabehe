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
| `favicon.ico`, `assets/icon-192.png`, `assets/apple-touch-icon.png` | Ícones da aba do navegador, do resultado do Google e da tela inicial do celular |
| `assets/og-lojabehe.jpg` | Cartão que aparece quando o link é compartilhado (WhatsApp, Instagram, Facebook) |
| `robots.txt`, `sitemap.xml` | Liberam a página para os buscadores e dizem onde ela está |
| `404.html` | Página de "não encontrada" (o GitHub Pages usa sozinho para qualquer endereço que não existe) |
| `CNAME` | Diz ao GitHub Pages que o domínio é `lojabehe.com` — não apague |
| `.nojekyll` | Publica os arquivos como estão, sem processamento do Jekyll |

## Como editar o que mais muda

Tudo fica no `index.html`. Procure pelos marcadores:

- **Fotos:** cada imagem provisória (Unsplash) tem um comentário `<!-- TROCAR: ... -->` logo acima. Coloque a foto real em
  `assets/` (de preferência `.webp`, até ~200 KB) e troque o `src`/`srcset` pelo caminho relativo, por exemplo
  `assets/produtos/sony-fx30-800.webp`. Mantenha `width` e `height` com as proporções da foto nova.
- **Prints de clientes (mural de Stories):** mesma coisa — os quadros 9:16 da seção "Quem Compra, Recomenda" estão
  marcados para receber os prints reais.
- **WhatsApp:** todos os botões usam `https://wa.me/5545998382728?text=...`. Para trocar o número, substitua
  `5545998382728` em todo o arquivo (busca e troca) **e também** o número escrito `99838-2728` (dados estruturados no
  `<head>`, chamada final e rodapé). Cada botão manda uma mensagem com `(origem: lp-...)`, que mostra
  no próprio WhatsApp de qual botão a pessoa veio.
- **Pixel do Meta e Google Analytics:** os blocos estão prontos e comentados no `<head>`. Coloque o ID real no lugar de
  `SEU_PIXEL_ID` / `G-XXXXXXX` e apague só as duas linhas marcadas com ✂ de cada bloco. Os cliques no WhatsApp já disparam `Contact` (Meta) e
  `clique_whatsapp` (Google) quando esses scripts estiverem ativos.
- **Produtos em destaque:** os seis cards da seção "Os Mais Pedidos do Momento" usam as fotos reais que a loja mandou
  (`assets/produtos/<produto>-800.webp` e `-480.webp`, recorte 4:5). Cada card tem nome, tag, 3 especificações e a mensagem
  do WhatsApp com a origem (`lp-destaque-…`). Sem preço na página: o preço muda com o dólar e é passado no WhatsApp.

## SEO (Google)

- **Título e descrição** ficam no começo do `<head>`: título com até 60 caracteres, descrição com até 155.
- **Cartão de compartilhamento**: `assets/og-lojabehe.jpg` (1200×630). O WhatsApp guarda a prévia pelo endereço
  da imagem; ao trocar o cartão, salve com **nome novo** e atualize o nome nas tags `og:image`/`twitter:image` e no JSON-LD.
- **Dados estruturados (JSON-LD)** no fim do `<head>`: loja online, site, página e perguntas frequentes.
  O bloco de perguntas repete o texto da seção "Perguntas Frequentes": mudou uma resposta lá, mude no JSON-LD também.
- **Só números e depoimentos reais.** "+2.300 clientes" vem da bio do Instagram da loja e "+3.600" dos seguidores do
  @behe_ofc (aparecem no topo, na seção de satisfação, na descrição e no JSON-LD). Não há nota nem avaliação nos dados
  estruturados de propósito: o Google não mostra estrelas de avaliações publicadas pela própria loja e pune dado falso.
- **Títulos**: um único `<h1>` (no topo); cada seção tem um `<h2>` e os cards têm `<h3>` com marca e categoria.
- **Fotos**: toda foto de conteúdo tem `alt` descrevendo a imagem real. Ao trocar uma foto, troque o `alt` também.
- **Ao mudar o conteúdo**, atualize a data `<lastmod>` do `sitemap.xml` (e liste lá as fotos novas de produto).
- **`c940f27d30032e845ff535f132157a98.txt`** na raiz é a chave do IndexNow (o aviso de página nova para o Bing e
  outros buscadores) — não apague. Para avisar de uma mudança: `curl "https://www.bing.com/indexnow?url=https%3A%2F%2Flojabehe.com%2F&key=c940f27d30032e845ff535f132157a98"`.

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
