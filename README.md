# niguxnick.github.io

Site pessoal — publicado em **https://niguxnick.github.io**

Página única, sem build e sem dependência de runtime: um `index.html` com CSS e JavaScript
embutidos. Abre direto no navegador, sem `npm install`.

## O que tem dentro

| Seção | O que é |
|---|---|
| **Stack** | As seis camadas de trabalho, do banco ao app |
| **Grafo** | Canvas com simulação de força: sistemas e domínios técnicos como nós ligados — arrastáveis, com destaque de vizinhança e painel de detalhe |
| **Projetos** | Sistemas internos, cada um com selo do papel que tive nele |
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
- `prefers-reduced-motion` desliga a camada de movimento inteira: entrada, revelação ao
  rolar, boot do terminal, física do grafo e cena de fundo. Todo o conteúdo permanece
  presente e legível — nada depende de animação para aparecer, inclusive sem JavaScript
- A cena de fundo custa perto de zero: a nebulosa é pintada num canvas de 200×126 e
  ampliada, no lugar de `filter: blur()` sobre a viewport, que derrubava a página de 60
  para 19 quadros por segundo. Gradientes são pré-computados, não recriados por quadro
- Os dois canvas param de desenhar quando saem da viewport ou a aba fica oculta
- Alvos de toque de 40px no mobile, foco visível e rótulo em todos os controles
- Sem rolagem horizontal a partir de 320px

## Editar

Os projetos são os cards que já estão no HTML — assim buscador, leitor de tela e prévia de
link veem a lista sem JavaScript. Para incluir um projeto, copie um `<article class="proj">`
e preencha `data-id`, `data-autoria` e `data-liga`.

O grafo e o terminal leem daí, de uma fonte só:

```js
const DADOS = {
  dominios: [...],                                  // escritos à mão
  projetos: [...document.querySelectorAll('.proj')] // lidos dos cards
}
```

Os domínios técnicos e os comandos do terminal ficam nesse mesmo bloco de script.
