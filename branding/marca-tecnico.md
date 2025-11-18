# NΞØ SMART FACTORY — branding.md v0.6

Guia prático para IA dev e front-end implementar identidade visual, tokens, CSS e componentes. Foco em precisão, auditabilidade e fácil manutenção.

---

## 1. Núcleo de marca

**Categoria:** Economy Assembly Layer
**Tese:** Linha de montagem que transforma ideias em economias verificáveis com precisão industrial.
**Tom verbal:** técnico, direto, seguro, com confiança hacker.
**Assinatura visual:** Ø inclinado 16°, macrotipografia brutalista, contraste acid sobre preto carbono, movimento com inércia curta.

---

## 2. Paleta e tokens de cor

Use nomes semânticos para desacoplar cor da função. Forneça também aliases de produto.

### 2.1 Cores base

* `color.neon.acid` `#D8F244`
* `color.neutral.black` `#0E0E0E`
* `color.neutral.white` `#FFFFFF`
* `color.neutral.gray.100` `#F4F6F8`
* `color.neutral.gray.200` `#E6E8EA`
* `color.neutral.gray.300` `#D4D6D9`
* `color.neutral.gray.400` `#BFC1C3`
* `color.neutral.gray.500` `#9A9DA0`
* `color.neutral.gray.600` `#6D7074`
* `color.neutral.gray.700` `#3C3F43`
* `color.neutral.gray.800` `#1A1C1F`
* `color.signal.magenta` `#FF2E9A`
* `color.signal.cyan` `#00E5FF`

### 2.2 Mapeamento semântico

* `color.bg.default` → `color.neutral.black`
* `color.bg.surface` → `color.neutral.gray.900` `#111214`
* `color.bg.elevated` → `color.neutral.gray.800`
* `color.text.primary` → `#ECEDEE`
* `color.text.secondary` → `color.neutral.gray.400`
* `color.border.muted` → `#2A2D31`
* `color.brand.primary` → `color.neon.acid`
* `color.brand.onPrimary` → `color.neutral.black`
* `color.state.active` → `color.signal.cyan`
* `color.state.warning` → `#FFC107`
* `color.state.error` → `color.signal.magenta`
* `color.state.success` → `#3BF07C`

### 2.3 Gradientes de trabalho

* `gradient.energy` linear 135deg, `#D8F244 0%` para `#B3FF4E 60%` para `#00E5FF 100%`
* `gradient.signal` linear 165deg, `#FF2E9A` para `#00E5FF`

---

## 3. Tipografia

* **Headlines** família recomendada: Monument Grotesk, GT America Expanded, Druk Wide. Peso 800 a 900.
* **Texto** família recomendada: Inter, IBM Plex Sans. Peso 400 a 600.
* **Monoespaçada**: JetBrains Mono para código.

### 3.1 Escala tipográfica

* `--font-size-xxl` 72px
* `--font-size-xl` 48px
* `--font-size-lg` 32px
* `--font-size-md` 20px
* `--font-size-sm` 16px
* `--font-size-xs` 14px

### 3.2 Regras

* Headlines curtas em caixa alta, tracking leve negativo em desktop `-0.5%`.
* `Ø` é caractere de assinatura. Use variação inclinada 16° em marcas e selos.
* Linhas de texto entre 60 e 72 caracteres.

---

## 4. Grid, espaçamentos, raios e sombras

* Unidade base 8.
* `space.1` 4, `space.2` 8, `space.3` 12, `space.4` 16, `space.6` 24, `space.8` 32, `space.12` 48, `space.16` 64.
* `radius.sm` 8, `radius.md` 12, `radius.lg` 16, `radius.xl` 24, `radius.2xl` 32.
* Sombra padrão: `0 4px 24px rgba(0,0,0,0.35)` para superfícies elevadas.
* Glow acid interno: `inset 0 0 12px rgba(216,242,68,0.45)` para bordas luminosas.

---

## 5. Movimento

* Duração padrão 140ms, easing `cubic-bezier(0.16, 1, 0.3, 1)`.
* Interações de foco mudam borda para `color.state.active` com leve overshoot.
* O selo `Ø` reage ao cursor com escala 0.98 em repouso e 1.02 ao hover.

---

## 6. Logotipo e selo

* **Wordmark:** `NΞØ SMART FACTORY` em caixa alta, Ø com corte de 16°.
* **Monograma:** `NΞØ` em contêiner quadrado com cantos 12, proporção 1:1.
* **Selo dinâmico:** Ø com três pontos orbitais indicando Core, Forge, Workbench.

**Margens de proteção:** altura do Ø em todos os lados.
**Fundo preferencial:** preto carbono.
**Aplicação acid:** o acid deve parecer emitir luz, use glow interno e textura leve.
**Assimilação pictórica:** o lettering deve absorver textura do suporte, sem efeito de adesivo. Configure blending `overlay` ou `soft-light` nas composições.

---

## 7. Sistema de módulos

Use a árvore de nomes para UI, docs e código.

* `neosmart-factory/Core` mecanismos ERC e segurança
* `neosmart-factory/Forge` CLI e pipelines de deploy
* `neosmart-factory/Workbench` PWA de montagem e simulação
* `neosmart-factory/Oracle` refinamento via LLM
* `neosmart-factory/DNA` parâmetros, utilidades, gamificação e ciclos de engajamento
* `neosmart-factory/Scriptorium` manifesto, whitepaper, pitch versionados
* `neosmart-factory/Kernel` 1-click pipeline e rollback
* `neosmart-factory/Sensor` telemetria
* `neosmart-factory/Atlas` blueprints certificados

---

## 8. Acessibilidade

* Contraste mínimo 4.5:1 para texto comum, 3:1 para grande.
* Combinações aprovadas: acid sobre preto para elementos curtos, texto longo deve usar `#ECEDEE` sobre `#0E0E0E`.
* Focus visível com borda 2px `color.state.active` e outline offset 2.

---

## 9. Design tokens JSON

```json
{
  "$schema": "https://design-tokens.org/schema.json",
  "brand": {
    "name": "NEO Smart Factory",
    "signatureAngle": {"value": 16}
  },
  "color": {
    "neon": {"acid": {"value": "#D8F244"}},
    "neutral": {
      "black": {"value": "#0E0E0E"},
      "white": {"value": "#FFFFFF"},
      "gray": {
        "100": {"value": "#F4F6F8"},
        "200": {"value": "#E6E8EA"},
        "300": {"value": "#D4D6D9"},
        "400": {"value": "#BFC1C3"},
        "500": {"value": "#9A9DA0"},
        "600": {"value": "#6D7074"},
        "700": {"value": "#3C3F43"},
        "800": {"value": "#1A1C1F"}
      }
    },
    "signal": {
      "magenta": {"value": "#FF2E9A"},
      "cyan": {"value": "#00E5FF"}
    },
    "semantic": {
      "bg": {
        "default": {"value": "{color.neutral.black.value}"},
        "surface": {"value": "#111214"},
        "elevated": {"value": "{color.neutral.gray.800.value}"}
      },
      "text": {
        "primary": {"value": "#ECEDEE"},
        "secondary": {"value": "{color.neutral.gray.400.value}"}
      },
      "border": {"muted": {"value": "#2A2D31"}},
      "brand": {
        "primary": {"value": "{color.neon.acid.value}"},
        "onPrimary": {"value": "{color.neutral.black.value}"}
      },
      "state": {
        "active": {"value": "{color.signal.cyan.value}"},
        "warning": {"value": "#FFC107"},
        "error": {"value": "{color.signal.magenta.value}"},
        "success": {"value": "#3BF07C"}
      }
    }
  },
  "space": {"1": {"value": 4}, "2": {"value": 8}, "3": {"value": 12}, "4": {"value": 16}, "6": {"value": 24}, "8": {"value": 32}, "12": {"value": 48}, "16": {"value": 64}},
  "radius": {"sm": {"value": 8}, "md": {"value": 12}, "lg": {"value": 16}, "xl": {"value": 24}, "2xl": {"value": 32}},
  "shadow": {"elevated": {"value": "0 4px 24px rgba(0,0,0,0.35)"}, "glowAcid": {"value": "inset 0 0 12px rgba(216,242,68,0.45)"}},
  "motion": {"duration": {"fast": {"value": "140ms"}}, "easing": {"productive": {"value": "cubic-bezier(0.16,1,0.3,1)"}}},
  "typography": {
    "headline": {"font": {"value": "'Monument Grotesk', 'GT America Expanded', system-ui"}, "weight": {"value": 800}},
    "body": {"font": {"value": "Inter, 'IBM Plex Sans', system-ui"}, "weight": {"value": 400}}
  }
}
```

---

## 10. CSS variables base

Coloque em `:root` para tema dark principal e em `.theme-light` para variação.

```css
:root {
  --color-bg-default: #0E0E0E;
  --color-bg-surface: #111214;
  --color-bg-elevated: #1A1C1F;
  --color-text-primary: #ECEDEE;
  --color-text-secondary: #BFC1C3;
  --color-border-muted: #2A2D31;
  --color-brand: #D8F244;
  --color-onbrand: #0E0E0E;
  --color-active: #00E5FF;
  --color-warning: #FFC107;
  --color-error: #FF2E9A;
  --color-success: #3BF07C;

  --radius-md: 12px;
  --radius-lg: 16px;
  --shadow-elevated: 0 4px 24px rgba(0,0,0,0.35);
  --glow-acid: inset 0 0 12px rgba(216,242,68,0.45);

  --font-headline: 'Monument Grotesk', 'GT America Expanded', system-ui;
  --font-body: Inter, 'IBM Plex Sans', system-ui;
}

.theme-light {
  --color-bg-default: #FFFFFF;
  --color-bg-surface: #F4F6F8;
  --color-text-primary: #0E0E0E;
  --color-text-secondary: #3C3F43;
  --color-border-muted: #D4D6D9;
}
```

---

## 11. Tailwind preset opcional

`tailwind.config.js`

```js
export default {
  darkMode: ['class'],
  theme: {
    extend: {
      colors: {
        bg: { DEFAULT: 'var(--color-bg-default)', surface: 'var(--color-bg-surface)', elevated: 'var(--color-bg-elevated)' },
        text: { primary: 'var(--color-text-primary)', secondary: 'var(--color-text-secondary)' },
        border: { muted: 'var(--color-border-muted)' },
        brand: { DEFAULT: 'var(--color-brand)', on: 'var(--color-onbrand)' },
        state: { active: 'var(--color-active)', warning: 'var(--color-warning)', error: 'var(--color-error)', success: 'var(--color-success)' }
      },
      borderRadius: { md: 'var(--radius-md)', lg: 'var(--radius-lg)' },
      boxShadow: { elevated: 'var(--shadow-elevated)' },
      fontFamily: { headline: 'var(--font-headline)', body: 'var(--font-body)' },
      transitionTimingFunction: { productive: 'cubic-bezier(0.16,1,0.3,1)' },
      transitionDuration: { fast: '140ms' }
    }
  }
}
```

---

## 12. Componentes referência

### 12.1 Botão primário

```css
.ns-button {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 12px 16px; border-radius: var(--radius-md);
  color: var(--color-onbrand); background: var(--color-brand);
  box-shadow: var(--shadow-elevated);
  transition: transform var(--transition, 140ms) cubic-bezier(0.16,1,0.3,1),
              box-shadow var(--transition, 140ms) cubic-bezier(0.16,1,0.3,1);
}
.ns-button:hover { transform: translateY(-1px); }
.ns-button:active { transform: translateY(0); }
.ns-button:focus-visible { outline: 2px solid var(--color-active); outline-offset: 2px; }
```

### 12.2 Card técnico

```css
.ns-card { background: var(--color-bg-surface); border: 1px solid var(--color-border-muted); border-radius: var(--radius-lg); padding: 16px; }
.ns-card--elevated { box-shadow: var(--shadow-elevated); }
```

### 12.3 Badge de estado

```css
.badge { border-radius: 999px; padding: 4px 8px; font: 600 12px/1 var(--font-body); }
.badge--active { background: color-mix(in oklab, var(--color-active) 20%, transparent); color: var(--color-text-primary); border: 1px solid var(--color-active); }
.badge--error { background: color-mix(in oklab, var(--color-error) 20%, transparent); color: var(--color-text-primary); border: 1px solid var(--color-error); }
```

### 12.4 Input industrial

```css
.input {
  background: var(--color-bg-elevated); color: var(--color-text-primary);
  border: 1px solid var(--color-border-muted); border-radius: var(--radius-md);
  padding: 12px 14px; outline: none; transition: border-color 140ms cubic-bezier(0.16,1,0.3,1);
}
.input:focus { border-color: var(--color-active); box-shadow: 0 0 0 3px color-mix(in srgb, var(--color-active) 25%, transparent); }
```

---

## 13. Layout e hero

```html
<section class="bg-[var(--color-bg-default)] text-[var(--color-text-primary)]">
  <div class="max-w-7xl mx-auto px-6 py-20 grid md:grid-cols-12 gap-8">
    <h1 class="md:col-span-7 font-headline text-6xl leading-[0.95] tracking-tight uppercase">
      Economias em minutos. Precisão de fábrica. Auditadas por padrão.
    </h1>
    <div class="md:col-span-5 flex flex-col gap-4">
      <p class="text-lg text-[var(--color-text-secondary)]">Linha de montagem para tokens, contratos e mecanismos sociais na Polygon, com simulação e verificação automática.</p>
      <div class="flex gap-3">
        <a class="ns-button" href="#workbench">Montar agora</a>
        <a class="ns-button" style="background:var(--color-active);color:#001015" href="#pipeline">Ver pipeline</a>
      </div>
    </div>
  </div>
</section>
```

---

## 14. Diretrizes de imagem

* Texturas metálicas, trilhos, tolerâncias, blueprint técnico.
* Evite render 3D genérico. Prefira macrofotografia de materiais reais.
* Aplique assimilação pictórica no wordmark quando coexistir com materialidade.

---

## 15. Conteúdo e microcopy

* Verbos de produção: montar, forjar, testar, assinar, operar.
* Evite promessas abstratas. Diga o que mede, quanto custa e quanto demora.
* Exemplos:

  * “Tempo até protocolo executável: 7 minutos médio”
  * “Coverage de testes do template ERC20: 92%”

---

## 16. Estrutura de pastas

```
/brand
  branding.md
  /tokens
    tokens.json
    css-vars.css
  /logo
    wordmark.svg
    monogram.svg
    seal-dynamic.svg
  /components
    button.css
    card.css
    input.css
```

---

## 17. Checklist de implementação

* [ ] Publicar `tokens.json` e `css-vars.css` no repositório monorepo
* [ ] Conectar Tailwind a CSS variables
* [ ] Revisar contrastes com testes automáticos
* [ ] Incluir exemplos no Storybook
* [ ] Expor no site painel de métricas públicas
* [ ] Testar o selo Ø com ângulo 16° em múltiplas densidades

---

## 18. Licenças e fontes

* Confirmar licença de headlines escolhidas. Caso não disponíveis, usar **Space Grotesk** como fallback ampliado para headlines.

---

## 19. Versão

`v0.6` pronta para iteração. Ajustes finos de tipografia e motion podem ser versionados em `tokens.json` sem quebrar UI.
