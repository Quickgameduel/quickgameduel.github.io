# Guia do Quick Duel

O jogo inteiro é **um único arquivo: `index.html`**. Os outros arquivos são o que faz o app instalável.

## Arquivos
- `index.html`: o jogo (regras, fases, visual, textos, tudo).
- `sw.js`: guarda o jogo para abrir rápido. **Sempre que mudar o `index.html`, troque o número em `const C="qgd-v15"` (ex.: `qgd-v16`)** para os aparelhos pegarem a versão nova.
- `manifest.webmanifest`, `icon-*.png`: nome e ícone do app instalado.
- `privacidade.html`: política de privacidade (link exigido pela Play Store).

## Como editar pelo celular
1. No GitHub, abra o arquivo, toque no lápis (editar), mude e toque em **Commit changes**.
2. Espere 1 a 2 minutos. No celular, feche e abra o jogo para ver a mudança.
3. Dica: dentro do arquivo, use a busca do navegador para achar o nome indicado abaixo.

## Onde mudar cada coisa (procure este texto no `index.html`)
- **Endereço do Firebase (modo Online):** `const NET_URL=`
- **Preço da caixa surpresa:** `const BOX_PRICE`
- **Moedas por fase (facílimo, fácil, difícil, muito difícil, extremamente difícil):** `const COIN_T=`
- **Fases 1 a 10 (tutorial) e poderes de cada uma:** `const PA=` (lista de poderes) e logo abaixo os textos das regras.
- **Fases 11 em diante:** `function buildLevels2` → listas `E` (fácil), `H` (difícil), `V` (muito difícil) e `X` (extremamente difícil). Cada fase é algo como `{cards:7,rev:1,margin:2,head:1}`:
  - `cards`: quantas cartas · `rev:1`: menor carta vence · `noPow:1`: você sem poderes · `margin:2`: vencer por 2 pontos · `head:1`: o robô começa com 1 ponto.
  - A inteligência do robô por dificuldade fica em `const SMT=`.
  - Fases extras: `const EXTRA=[]`.
- **Chance de vitória mostrada em cada fase:** `const WIN=` (números aproximados; precisam ser refeitos se mudar as regras).
- **Textos em português, inglês e espanhol:** `const L={` (e os blocos `Object.assign(L.pt`, `L.en`, `L.es`).
- **Cores da tela, avatares, letras e estampas:** `COL_POOL`, `AV_POOL`, `FONT_IDS`, `CS_POOL`.

## Atenção
- Se o jogo ficar em branco depois de uma edição, quase sempre é uma vírgula, aspas ou chave apagada. Desfaça a edição em **Commits → Revert** e tente de novo.
- Não apague o `sw.js` nem o `manifest.webmanifest`.
- O modo Online usa o Firebase (projeto `quick-duel-b29fe`). As regras do banco ficam no console do Firebase → Realtime Database → Regras.

## Play Store
Para publicar, use https://www.pwabuilder.com com o endereço https://quickgameduel.github.io . A política de privacidade fica em https://quickgameduel.github.io/privacidade.html
