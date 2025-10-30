# Prompt para Trae — Implementação e identidade visual para blog DevSecOps / Cybersecurity

> Objetivo: transformar uma base Docusaurus numa **landing page estética, responsiva e multilingue** com identidade visual inspirada na estética japonesa (hannya mask minimalista), foco em cybersegurança/DevSecOps, blog como principal produto e components interativos (animação `whoami`, modo claro/escuro, seleção de idioma). Forneça código, arquivos e instruções de integração prontos para deploy.

---

## 1) Resumo do projeto
* O nome é Hannya
* Base: **Docusaurus** (v2+). Substituir visual padrão (dinossauro) pela nova marca e landing page.
* Público-alvo: pesquisadores, profissionais e entusiastas de segurança, DevSecOps.
* Tom: sério, minimalista, elegante, com traços japoneses sutis — cores sóbrias com detalhes roxos.
* Idiomas: **Português (pt-BR)** e **Inglês (en)**. Botão de seleção no topo.
* Acessibilidade: contraste respeitado, alternância claro/escuro.

---

## 2) Identidade visual

**Paleta:**

* `#705391` — Cor principal (roxo profundo)
* `#A080CF` — Detalhe secundário (lavanda)
* `#F6F6FA` — Fundo predominante (quase branco)

**Tipografia (sugestão):**

* Inter ou system sans para corpo (legibilidade)
* Noto Sans JP para suportar Kanji com boa estética

**Logo:** Máscara de **Hannya** — minimalista, geometrizada, linhas finas, ícone SVG monocromático (usar `#705391` como fill/outline dependendo do contexto). A logo deverá ter variantes: `logo.svg` (full), `logo-mark.svg` (apenas o ícone circular) e `favicon`.

> *Observação para designer:* gerar SVG em curvas limpas, evitar muitos detalhes (para manter leitura em small sizes). Deve transmitir proteção/alerta, mas sem ser agressiva.

---

## 3) Estrutura e páginas principais

* `/` — **Landing / Home** (hero com logo, kanji animado, slogan/descrição curta, CTA para posts recentes)
* `/blog` — área principal (substituir o comportamento docs -> blog). Mostrar posts por categoria (rows/tile): **Offsec** e **DevSecOps**, com subtemas listados (Malware, Web Application, Anonimato, Plataforma, Kubernetes)
* `/about` — página sobre o autor (foto criativa, título, bio curta alinhada ao tema)
* `/contribute` — explicando como outros pesquisadores podem colaborar / ter sua própria página
* `/post/teste-thanos` — post de teste sobre o malware *Thanos* (markdown inicial já criado)

---

## 4) Funcionalidades interativas e animações

### 4.1 `whoami` visual no topo (esquerda)

* No `navbar` (lado esquerdo), renderizar um pequeno bloco que imita uma sessão de terminal: `whoami:` seguido por uma animação rápida com logs.
* Logs (sequência que aparece e apaga):

  * `骨人#8f3a7a` -> transforma para `boneka@cybernetica` -> apaga
  * `朔6d4a2` -> transforma para `puka6doll` -> apaga
  * `刃0x86` -> transforma para `kidbuu_da_fana0x86` -> apaga
  * `阿ldryA` -> transforma para `Aldry Albuquerque` -> apaga
  * `...OtherNames...` -> repetir ciclo

Comportamento desejado:

* Ao aparecer: mostrar primeiro **kanji/hash** (ou glyphs japoneses + hash) por ~150ms
* Fazer morph/fade para nome real em ~120ms
* Mostrar o nome real por ~300ms
* Apagar com um efeito de backspace rápido (~80–120ms por caractere)
* Loop contínuo, porém pouco intrusivo (volume visual discreto). Preferir CSS + small JS (React + framer-motion opcional).

### 4.2 Dark / Light mode

* Implementar suporte via `themeConfig.colorMode` do Docusaurus e fornecer um toggle no topo. Mudar também a `logo` variante (outline vs fill) conforme o modo.

### 4.3 Kanji e estética japonesa

* No hero da landing, apresentar 2–3 Kanji relevantes com animação sutil (opacidade → slide in). Sugestões de Kanji e significados a exibir (em badge discreta):

  * `守` — proteja / proteger
  * `防` — defesa
  * `安` — segurança

---

## 5) Conteúdo e organização (Docs -> Blog)

* Converter /docs em `/blog` ou apenas usar a feature de blog do Docusaurus. O importante é **redesenhar** a seção técnica para ter apresentação de posts (data, autor, tags), não como documentação estática.
* Tags / categorias: `Offsec`, `Malware`, `Web`, `Anonimato`, `DevSecOps`, `Kubernetes`, `Plataforma`.
* Layout de listagem: agrupado por row — cada row representa um tema (ex.: **Offsec** row com cards: Malware, Web App, Anonimato).

---

## 6) Multilinguismo (i18n)

* Usar `i18n` do Docusaurus. Padrão `pt-BR` + `en`.
* Traduções principais a incluir: navbar labels, CTA do hero, 'About', 'Contribute', 'Read more', meta de posts (Author, Date), placeholders na página de contribuição.
* Colocar seletor de idioma no topo direito.

---

## 7) Arquivos e snippets práticos (exemplos)

### 7.1 `docusaurus.config.js` (trecho relevante)

```js
module.exports = {
  title: 'Cybernetica',
  tagline: 'Evolvendo a régua de cybersegurança',
  url: 'https://yourdomain.com',
  baseUrl: '/',
  i18n: {
    defaultLocale: 'pt-BR',
    locales: ['pt-BR','en'],
  },
  themeConfig: {
    colorMode: { defaultMode: 'light', respectPrefersColorScheme: true },
    navbar: {
      title: '',
      logo: { src: 'img/logo-mark.svg', alt: 'Hannya logo' },
      items: [
        {
          to: '/blog',
          label: 'Blog',
          position: 'left'
        },
        { to: '/about', label: 'About', position: 'left' },
        { to: '/contribute', label: 'Contribute', position: 'left' },
        {
          type: 'localeDropdown',
          position: 'right'
        },
        {
          position: 'right',
          // aqui será o componente whoami - substitua por React component
          html: `<div id="whoami-root"></div>`
        }
      ]
    }
  }
};
```

> Observação: o `html` no navbar pode ser substituído por `navbarItem` custom React se preferir integrar via swizzling.

### 7.2 Estilização global (CSS / Tailwind)

* Criar `src/css/custom.css` com variáveis :root para as cores da paleta.
* Manter `F6F6FA` como fundo padrão, `#705391` para CTAs, `#A080CF` para hover/links.

```css
:root{
  --color-bg: #F6F6FA;
  --color-primary: #705391;
  --color-accent: #A080CF;
}
```

### 7.3 Componente React: `components/WhoamiTicker.jsx` (esqueleto)

```jsx
import React, {useEffect, useState} from 'react';

const entries = [
  {glyph: '骨人#8f3a7a', name: 'boneka@cybernetica'},
  {glyph: '朔6d4a2', name: 'puka6doll'},
  {glyph: '刃0x86', name: 'kidbuu_da_fana0x86'},
  {glyph: '阿ldryA', name: 'Aldry Albuquerque'},
];

export default function WhoamiTicker(){
  const [i,setI] = useState(0);
  const [phase,setPhase] = useState('glyph');
  const [display, setDisplay] = useState(entries[0].glyph);

  useEffect(()=>{
    let mounted=true;
    const cycle = async ()=>{
      while(mounted){
        // show glyph
        setPhase('glyph'); setDisplay(entries[i].glyph);
        await new Promise(r=>setTimeout(r,150));
        // morph to name
        setPhase('morph'); setDisplay(entries[i].name);
        await new Promise(r=>setTimeout(r,300));
        // backspace effect (quick clear)
        setPhase('erase'); setDisplay('');
        await new Promise(r=>setTimeout(r,120));
        setI((prev)=>(prev+1)%entries.length);
      }
    }
    cycle();
    return ()=>{mounted=false}
  },[i]);

  return (
    <div className="whoami">
      <code>whoami: <span className={`tick ${phase}`}>{display}</span></code>
    </div>
  )
}
```

> Ajustar animações CSS para criar efeito de morph/backspace. Preferir `requestAnimationFrame` se quiser micro-performances.

---

## 8) Exemplo de post de teste: `blog/2025-10-25-thanos.md`

```md
---
title: "Thanos: breve análise de um ransomware / malware"
author: Aldry Albuquerque
tags: [Malware, Offsec]
---

## Thanos — resumo técnico

Thanos é um ransomware que ganhou notoriedade por X, Y e Z. (Aqui incluir um resumo neutro e informativo, sem instruções maliciosas operacionais). O objetivo deste post é discutir vetores de infecção, indicativos de comprometimento (IoCs) e medidas de mitigação.

### Indicadores e mitigação
- Isolar e investigar imagens de containers suspeitas.
- Revisar políticas de RBAC no Kubernetes.
- Monitoramento de EDR e análise de logs.

> Nota: manter sempre a ética. Não publicar payloads ou instruções que facilitem replicação maliciosa.
```

---

## 9) Sobre a página "About" e a foto

* Layout: card com `logo-mark` ao fundo (em baixa opacidade), lado esquerdo foto do autor (circular com máscara em SVG recortada), lado direito bio curta (3–4 linhas), links para redes e CV.
* Pedir uma foto quadrada profissional — o componente deve recortar e adicionar um frame leve com element Japanese pattern (asanoha) em `border` ou `overlay`.

---

## 10) Página de contribuição

* Texto explicando: como criar uma conta/PR, guidelines de publicação, template de artigo (frontmatter), política de revisão.
* Botão `Start a guest post` que abre um formulário (ou link para um PR template no GitHub).

---

## 11) Deployment

* Construir com `npm run build` e `npm run serve` para testes. Deploy sugerido: Vercel, Netlify, Github Pages.
* Garantir `og:image` com `logo-mark` e um banner custom (1200x630) que mescle a Hannya e `守 防 安` em diagonal.

---

## 12) Checklist para o dev (passo-a-passo)

1. Substituir `static/img` dino por `logo.svg` e `logo-mark.svg`.
2. Atualizar `docusaurus.config.js` (i18n + navbar + colorMode).
3. Criar `src/components/WhoamiTicker.jsx` e importar no navbar (swizzle se necessário).
4. Criar `src/css/custom.css` com variáveis e overrides.
5. Migrar conteúdo relevante para `blog/` e aplicar frontmatters de tags/categorias.
6. Implementar toggle dark/light e variantes de logo.
7. Criar `about` e `contribute` pages com imagens e templates.
8. Criar post de teste `thanos.md` (ver seção 8).
9. Testes: responsividade, acessibilidade (contraste), performance lighthouse.
10. Deploy e configuração de domínio + imagens OG.

---
