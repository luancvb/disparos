# Como o trabalho foi feito

Página de um arquivo só que mostra como a base de contatos da campanha foi
montada, repartida entre os 12 números e o que voltou de resposta.

Não tem nome, telefone nem mensagem de ninguém: só contagens, municípios e a
divisão por número e por dia.

---

## Subir no GitHub Pages

1. Crie um repositório novo no GitHub (pode ser privado — o Pages funciona em
   repositório privado nos planos pagos; no plano grátis o repositório precisa
   ser público).
2. Mande estes dois arquivos para a raiz do repositório: `index.html` e este
   `README.md`.
3. No repositório, vá em **Settings → Pages**.
4. Em **Source**, escolha **Deploy from a branch**; em **Branch**, escolha
   `main` e a pasta `/ (root)`. Salve.
5. Em um ou dois minutos o endereço aparece na mesma tela, no formato
   `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

Pela linha de comando, se preferir:

```bash
git init
git add index.html README.md
git commit -m "Relatório da base de contatos"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git
git push -u origin main
```

Depois é só ligar o Pages em Settings → Pages, como nos passos 3 a 5.

---

## O que dá para fazer na página

- **Filtrar por clique.** Clicar num número (linha), num dia (coluna) ou numa
  célula da tabela filtra o resto da página. Os municípios e os textos são
  recalculados só com a seleção.
- **Alternar `nº` / `%`** na barra de filtro.
- **Atualizar com a planilha.** O botão no topo (ou arrastar o arquivo para cima
  da página) lê um `.xlsx` ou `.csv` e refaz a página inteira. Tudo acontece no
  navegador de quem abriu: **nada é enviado para lugar nenhum**, e a alteração
  vale só para aquela visita — quem abrir depois vê os dados originais.

A planilha precisa ter, no cabeçalho, as colunas `chip` e `dia_semana`.
`municipio` e `variacao` são opcionais. A aba usada é a `Contatos`, ou a
primeira que existir.

## Como mexer

Os dados ficam dentro do próprio `index.html`, numa linha só, logo depois de
`<script>`:

```js
var PADRAO = { "base": 2064, ... , "retorno": {"responderam": 768, "negativos": 52}, ... };
```

Para corrigir os números de resposta, mude `responderam` e `negativos` ali —
eles não vêm da planilha, porque não existem linha a linha.

## Detalhes técnicos

- Um arquivo só, sem dependência nenhuma. A única coisa que vem de fora são as
  fontes do Google Fonts; sem internet a página funciona igual, só troca a fonte.
- Tema claro e escuro automáticos, acompanhando o sistema de quem abre.
- A animação de entrada some sozinha para quem usa "reduzir movimento".
- A leitura do `.xlsx` é feita na própria página, sem biblioteca: descompacta o
  arquivo com `DecompressionStream` e lê o XML com `DOMParser`.
- A página está marcada com `<meta name="robots" content="noindex">`, ou seja,
  pede para o Google não indexar. Se quiser que apareça em busca, apague essa
  linha do `<head>`.
