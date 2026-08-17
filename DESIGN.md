# DESIGN.md — Obsidian

> Leitura independente de padrões visuais publicamente observáveis, reescrita em tokens próprios.
> Não é o design system oficial de Obsidian, não reproduz marcas ou ativos da empresa e não há vínculo ou endosso.

**Use quando:** Roxo sobre grafite — base de conhecimento pessoal, notas ligadas, grafo.

| | |
|---|---|
| Modo padrão | dark-first |
| Densidade | confortável |
| Raio base | 0.375rem |
| Tipografia | Inter + mono |
| Stack | Tailwind v4 + shadcn/ui, tokens em OKLCH |

## Filosofia

Ferramenta de pensamento, não de apresentação. Fundo escuro para leitura longa, roxo apenas no link interno e no nó do grafo, e markdown visível como cidadão de primeira classe: a sintaxe faz parte do desenho, não é sujeira a esconder.

## Assinatura visual

- Roxo exclusivo de link interno e nó de grafo
- Markdown visível: colchetes e cerquilhas fazem parte da estética
- Painéis lado a lado redimensionáveis, sem sombra
- Grafo como elemento visual da identidade

## Tipografia

- Inter no corpo da nota, 16px, entrelinha 1.6
- Mono em bloco de código, propriedade de frontmatter e tag
- Títulos H1–H6 com escala curta e visível na barra lateral
- Títulos com `text-wrap: balance`; prosa com no máximo 65 caracteres por linha.
- Rótulo em caixa alta sempre com `letter-spacing` — sem isso vira bloco ilegível.

## Tokens

Cole em `app/globals.css`. Toda cor da interface sai daqui — nenhum hex solto no componente.

```css
:root {
  --background: oklch(0.9860 0.0040 300);
  --foreground: oklch(0.2400 0.0180 300);
  --card: oklch(0.9860 0.0040 300);
  --card-foreground: oklch(0.2400 0.0180 300);
  --popover: oklch(0.9860 0.0040 300);
  --popover-foreground: oklch(0.2400 0.0180 300);
  --primary: oklch(0.5400 0.2000 300);
  --primary-foreground: oklch(1 0 0);
  --secondary: oklch(0.9500 0.0150 300);
  --secondary-foreground: oklch(0.2400 0.0180 300);
  --muted: oklch(0.9650 0.0090 300);
  --muted-foreground: oklch(0.5200 0.0250 300);
  --accent: oklch(0.9250 0.0300 300);
  --accent-foreground: oklch(0.3800 0.1400 300);
  --destructive: oklch(0.5700 0.2000 25);
  --destructive-foreground: oklch(1 0 0);
  --border: oklch(0.9050 0.0150 300);
  --input: oklch(0.9050 0.0150 300);
  --ring: oklch(0.5400 0.2000 300);
  --radius: 0.375rem;
}

.dark {
  --background: oklch(0.1650 0.0150 300);
  --foreground: oklch(0.9150 0.0130 300);
  --card: oklch(0.1650 0.0150 300);
  --card-foreground: oklch(0.9150 0.0130 300);
  --popover: oklch(0.1650 0.0150 300);
  --popover-foreground: oklch(0.9150 0.0130 300);
  --primary: oklch(0.6900 0.1800 300);
  --primary-foreground: oklch(0.1500 0.0150 300);
  --secondary: oklch(0.2500 0.0250 300);
  --secondary-foreground: oklch(0.9150 0.0130 300);
  --muted: oklch(0.2150 0.0200 300);
  --muted-foreground: oklch(0.7000 0.0250 300);
  --accent: oklch(0.3100 0.0650 300);
  --accent-foreground: oklch(0.9000 0.0400 300);
  --destructive: oklch(0.6500 0.2000 25);
  --destructive-foreground: oklch(0.1500 0.0150 300);
  --border: oklch(0.2800 0.0280 300);
  --input: oklch(0.2800 0.0280 300);
  --ring: oklch(0.6900 0.1800 300);
  --radius: 0.375rem;
}
```

## Layout e espaçamento

- Tamanho base do texto: 15px · densidade confortável.
- Linha de tabela: 44px · padding de card: 18px · gap entre irmãos: 16px.
- Espaçamento por `flex`/`grid` + `gap` — nunca por margem em cada elemento.
- Conteúdo largo (tabela, código, gráfico) rola dentro do próprio container com `overflow-x: auto`; a página nunca rola na horizontal.
- Largura máxima do painel: 1200px. Prosa: 65ch.

## Componentes

- **Botão** — um primário por tela; `ghost` para apoio; `destructive` só para ação destrutiva. Alvo mínimo de 44px no mobile. Loading trava o botão e mantém o rótulo.
- **Select** — sempre com campo de busca no topo, foco automático, filtro acento-insensível e estado vazio com texto. Nunca dropdown puro de rolar.
- **Input** — rótulo acima, foco com ring de 2px em `--ring`, erro que nomeia o campo e diz a correção. Proibido “algo deu errado”.
- **Status** — cor semântica (verde/âmbar/vermelho/cinza) separada de `--primary`, sempre acompanhada de rótulo ou ícone; cor nunca é o único sinal.
- **Tabela** — cabeçalho ordenável, `font-variant-numeric: tabular-nums` em toda coluna numérica, números à direita, hover de linha.
- **Feedback** — toast para o comum, overlay em tela cheia só para erro crítico; modal apenas para decisão focada.
- **Foco** — todo controle alcançável por Tab com `:focus-visible` visível. `outline: none` sem substituto é bug.

## Aplicativo mobile

A identidade atravessa inteira — os tokens acima valem sem alteração. O que muda é a medida: no telefone o alvo tem piso físico e o rodapé divide espaço com o gesto do sistema.

| | |
|---|---|
| Navegação | Tab bar de 3 a 4 abas + bottom sheet para todo secundário |
| Corpo do texto | 16px · linha de lista 56px |
| App bar | 56px · padding de card 16px · gap 14px |
| Bottom sheet | raio de topo `0.75rem` (2× o raio base) |

- **Navegação** — tab bar de 3 a 4 abas + bottom sheet para todo secundário, porque ferramenta de trabalho vive de ação rápida sobre um item da lista. Comando e opções por folha inferior, nunca por menu suspenso de desktop.
- **Alvo de toque** — mínimo de 48 × 48px (o maior piso entre os 44pt do HIG e os 48dp do Material) e 8px de folga entre alvos vizinhos. O rótulo pode ser menor; a área tocável, não.
- **Safe area** — `viewport-fit=cover` no viewport e `padding-bottom: max(14px, env(safe-area-inset-bottom))` em toda barra fixa de rodapé. Sem isso o CTA fica sob a barra de gesto.
- **Zona do polegar** — ação primária no rodapé, dentro do alcance; ação destrutiva nunca colada à faixa do gesto, onde o toque acidental acontece.
- **Bottom sheet no lugar de menu** — alça visível, dois estágios de altura, fecha por arraste e por toque fora. Modal em tela cheia só para decisão que não pode ser adiada.
- **Listas** — linha de 56px, divisor de 1px em `--border`; cartão só quando a linha carrega mídia. Ação por deslize sempre duplicada em toque longo ou em botão — gesto invisível não é a única saída.
- **Campos** — nunca abaixo de 16px: menos que isso e o Safari dá zoom ao focar, deslocando a tela. `inputmode` e `autocomplete` corretos, e o botão de envio acima do teclado, não atrás dele.
- **Feedback** — snackbar acima da tab bar (nunca sobre ela), com ação de desfazer quando a operação for reversível. Skeleton na primeira carga; spinner só em ação disparada pelo toque.
- **Tema** — claro e escuro seguem o sistema por `prefers-color-scheme`; a ficha pede escuro por padrão, e isso define o padrão, não o único.

**Nunca faça no telefone**

- Hover como único estado de um controle — no toque ele não existe.
- Tab bar com seis ou mais abas, ou aba sem rótulo.
- Tabela densa de desktop reaproveitada na tela do telefone: vira lista, ou vira gráfico.
- Texto de conteúdo abaixo de 12px, ou desligar o ajuste de tamanho do sistema.

## Movimento

- Painel abre sem animação. Só o grafo tem física própria.
- Respeitar `prefers-reduced-motion: reduce` desligando animação e transição.

### Exceção desta página

A ficha acima descreve uma **ferramenta de trabalho**, onde movimento é atrito.
Esta página é peça de apresentação: aqui o movimento carrega significado, e a
regra é estendida — não abandonada. Os limites que valem:

- **Duração e curva são token** (`--t-fast/--t-mid/--t-slow`, `--ease-out`,
  `--ease-soft`). Nenhum tempo ou curva solto no componente, como nenhuma cor.
- **Um momento orquestrado por seção**, não micro-animação espalhada: a entrada
  do título em cascata, a grade revelando em série, o boot do terminal.
- **Movimento contínuo só onde ele é o conteúdo** — os pulsos do grafo e a
  deriva do brilho de fundo. Nada mais pisca sozinho.
- **Movimento nunca é a única via**: todo conteúdo que entra animado existe no
  HTML e reaparece por `<noscript>` e por `prefers-reduced-motion`.
- **Nada de física em elemento de leitura** — sem paralaxe, sem rolagem
  sequestrada, sem texto que se monta letra por letra fora do terminal.
- **Elevação por `transform`, entrada por `translate`.** Uma animação com
  `forwards` trava a propriedade que ela animou; misturar as duas mata o hover.

Checklist extra desta página: `prefers-reduced-motion` verificado com a página
inteira legível, e o canvas do grafo parado quando está fora da viewport.

## Nunca faça

- Esconder a sintaxe markdown para “ficar limpo”
- Roxo em botão de ação genérico
- Interface clara como padrão dessa identidade
- Cor fora dos tokens acima, inclusive “só nesse componente”.
- Tema claro entregue e escuro esquecido — os dois são produto.

## Checklist de aceite

- [ ] Light e dark verificados na mesma tela
- [ ] Contraste AA em texto, chip e estado desabilitado
- [ ] Foco visível em todos os controles, navegável por teclado
- [ ] Nenhum hex solto: tudo por token
- [ ] Densidade confortável respeitada em tabela e formulário
- [ ] `prefers-reduced-motion` respeitado
- [ ] Telefone (390 × 844) verificado: alvo ≥ 48px, safe area no rodapé, nada sob a barra de gesto
- [ ] Campo de texto ≥ 16px — focar não dá zoom nem desloca a tela
