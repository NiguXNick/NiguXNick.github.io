# niguxnick.github.io

Site pessoal — publicado em **https://niguxnick.github.io**

Página única, sem build e sem dependência de runtime: um `index.html` com CSS e JavaScript
embutidos. Abre direto no navegador, sem `npm install`.

## O que tem dentro

| Seção | O que é |
|---|---|
| **Stack** | As seis camadas de trabalho, do banco ao app |
| **Grafo** | Canvas com simulação de força: sistemas e domínios técnicos como nós ligados — arrastáveis, com destaque de vizinhança e painel de detalhe |
| **Projetos** | Sistemas internos com selo de autoria apurado no histórico de commits |
| **Terminal** | Shell funcional: `help`, `whoami`, `ls projetos`, `cat <projeto>`, `stack`, `tema` |

## O que deliberadamente não está aqui

Método de trabalho, playbooks técnicos, regra de negócio, modelo de dados e detalhe de
arquitetura dos sistemas. O site diz **o que** cada sistema resolve; **como** ele foi
resolvido não é conteúdo público.

## Identidade visual

Governada pelo [`DESIGN.md`](DESIGN.md) da raiz — identidade **Obsidian** do acervo
(roxo sobre grafite, dark-first), com tokens em OKLCH para os dois temas. A tipografia foi
adaptada ao contexto editorial deste site: *Bricolage Grotesque* nos títulos e
*IBM Plex Mono* no corpo.

Toda cor da página sai de token CSS. Não há hex solto no arquivo.

## Acessibilidade e desempenho

- Claro e escuro, com preferência do sistema respeitada e escolha persistida
- `prefers-reduced-motion` desliga a simulação do grafo, que assenta antes do primeiro quadro
- Canvas em DPR limitado a 2× e paleta lida uma vez por tema, não por nó a cada quadro
- Alvos de toque de 40px no mobile, foco visível e rótulo em todos os controles
- Sem rolagem horizontal a partir de 390px

## Editar

Alterar projetos ou domínios é mexer em um único objeto:

```js
const DADOS = { dominios: [...], projetos: [...] }
```

Cards, grafo e comandos do terminal são todos gerados a partir dele.
