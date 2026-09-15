# LP Educação · versão leve

Reprodução estática de `conteudo.vanzolini.org.br/cursos-educacao/`, sem WordPress, sem
Elementor, sem jQuery, sem Font Awesome e sem nenhuma requisição a terceiros para fontes.

## Onde vive

Repositório: `communitascom/vanzolini-lp-educacao` (privado).
A pasta de origem é `LP Educacao - versao leve/` no Drive da campanha.

> **Antes de publicar no domínio da Vanzolini, remova o `<meta name="robots"
> content="noindex,nofollow">` do `index.html`.** Ele existe só para a cópia de
> homologação no GitHub Pages não ser indexada e competir com a página real. Está
> marcado com um bloco de comentário em caixa alta no topo do arquivo.

## Como publicar

Suba os dois itens juntos, preservando a estrutura:

```
index.html
assets/
```

Funciona em qualquer hospedagem estática (pasta no servidor, subdomínio, Netlify, Vercel,
S3/CloudFront). Não precisa de PHP, banco nem build.

Antes de publicar, ajuste em `index.html`:

- `<link rel="canonical">` — hoje aponta para a URL antiga.
- `og:image` — está relativo (`assets/hero-educacao.webp`); troque pela URL absoluta final.

Sirva os `.woff2` com `Content-Type: font/woff2` e cache longo (`max-age=31536000, immutable`).

## Fidelidade ao original

Conferida contra o WordPress renderizado a 1440px, medindo pixel a pixel. As dez faixas
horizontais da página batem em **cor e altura exatas**, e a página inteira tem os mesmos
**5497px** de altura:

| Faixa | Cor | Altura original | Esta versão |
|---|---|---|---|
| header | `#060653` | 90 | 90 |
| hero | `#33357F` | 482 | 482 |
| números | `#060653` | 152 | 152 |
| formatos | `#E5E5EE` | 911 | 911 |
| áreas temáticas | `#32347F` | 1012 | 1012 |
| in company | `#060653` | 816 | 816 |
| sobre | `#29296B` | 695 | 695 |
| CTA | `#060653` | 326 | 326 |
| contato | `#FFFFFF` | 729 | 729 |
| rodapé | `#24285C` | 284 | 284 |

A posição do conteúdo dentro de cada faixa está alinhada com desvio de 0 a 6px. O peso do
traço tipográfico foi aferido por densidade de tinta e está entre 0,92x e 1,09x do original.
Os quatro cards de formato usam as cores do original: `#32347F`, `#060653`, `#7E81E6`,
`#654EBE`. O botão do CTA final é `#005F55`.

## Peso

Recursos próprios da página, com tudo carregado, **sem contar os disparos do GTM**:

| | Original (Elementor) | Esta versão |
|---|---|---|
| HTML + CSS + JS + imagens | ~2,2 MB em 61 requisições | **168 KB em 17 requisições** |
| Fontes | Google Fonts, 6 famílias | **67 KB em 2 arquivos locais** |
| Bibliotecas | jQuery, Elementor, Elementor Pro, JetElements, tema Kava, 4x Font Awesome | nenhuma |
| DOMContentLoaded (local) | — | 60–190 ms |

**89% mais leve, com 69% menos requisições.**

As fontes são os arquivos **variáveis** de Work Sans e Inter Tight, com subset para os
caracteres do português. Um arquivo por família cobre toda a faixa de pesos: 2 requisições e
67 KB, contra 8 requisições e 378 KB que o Google Fonts entregaria para os mesmos 7 pesos.
Ambas são SIL Open Font License, que permite auto-hospedar e fazer subset.

**Atenção ao GTM.** O container `GTM-PF3JC3K` sozinho dispara cerca de 80 requisições para 28
domínios (Meta, LinkedIn, Clarity, DoubleClick, Spotify, Retargetly, Bing). Isso é idêntico ao
da página original e não veio desta reconstrução, mas é o que vai dominar o carregamento.
Vale uma auditoria separada do container: o ganho lá pode ser maior que o desta página.

## Movimento

Tudo em CSS/JS nativo, sem biblioteca:

- header que solidifica e encolhe ao rolar
- H1 revelado palavra a palavra
- parallax horizontal na arte do topo e vertical no padrão de setas
- revelação em scroll com escalonamento (IntersectionObserver)
- contadores animados (+100 / +200 / +3.000)
- cards com elevação no hover
- botão de WhatsApp flutuante com pulso

Tudo desligado sob `prefers-reduced-motion: reduce`. Os números corretos já vêm no HTML: se o
JS não rodar, ou se o observer perder o evento num scroll muito rápido, os valores continuam
certos.

## Pendências para você decidir

1. **Contraste do card "EAD Gravado".** Branco sobre `#7E81E6` dá **3,40:1**, abaixo do mínimo
   WCAG AA de 4,5:1 para texto. **A página original tem exatamente a mesma falha** — foi
   herdada, não introduzida aqui, e mantive por fidelidade. Duas saídas, se quiser corrigir:
   escurecer o fundo para `#6B6EC3` (4,52:1, praticamente a mesma cor) ou usar texto navy
   `#060653` sobre o fundo atual (5,32:1). Os outros três cards passam com folga.

## Diferenças conscientes em relação ao original

1. **Formulário único (decidido).** A página usa **um só** formulário RD Station, o
   `institucional-cursos-fundacao-2332474ddb3449457e8f`, na seção "Fale com a gente". O botão
   "Falar sobre in company" rola para ele (`#contato`) em vez de abrir um popup. No original,
   esse botão abria um popup do Elementor com um segundo formulário; ele foi dispensado, então
   todos os leads da página entram por um único formulário.
2. **Mobile.** O original **quebra no celular**: em 390px o logo, o H1 e os textos dos números
   ficam cortados por estouro horizontal. Aqui o hero empilha (foto em faixa no topo, texto
   embaixo sobre cor chapada, que é o arranjo que o original tenta fazer) e nada é cortado.
3. **`fundo-setas.webp` (176 KB) virou um padrão SVG em linha.** O arquivo original é de linhas
   escuras sobre fundo branco e não funcionava sobre o azul da seção. O SVG reproduz o motivo,
   pesa zero e acompanha o parallax.
4. **Ícones sociais viraram SVG em linha**, o que dispensa os 4 arquivos de Font Awesome.
5. **Link do LinkedIn corrigido**: o original aponta para `/company/40540/admin/`, uma URL de
   administração que não abre para o público. Aqui está `/company/40540/`.
6. Os links de tema que estavam em `http://` foram para `https://`.
7. **Botão de WhatsApp flutuante** é um acréscimo, não existe no original. Se não quiser, é só
   remover o elemento `<a class="wpp">`.
8. **`-webkit-font-smoothing:antialiased` foi removido** de propósito: afinava o traço no
   macOS e deixava a tipografia mais leve que a do original.

## Revisão de código

O arquivo passou por revisão no Codex. Foram corrigidos: brilho de hover dos cards que ficava
invisível atrás do fundo opaco (removido, não existe no original), falta de indicador de foco
nos links que cobrem o card inteiro, `getBoundingClientRect()` a cada frame de rolagem (agora
medido uma vez e no resize), e parallax do hero que ampliava a foto além do `cover` exato.
