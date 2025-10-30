---

## 1) Correções gerais de layout e responsividade

### Orientação e dimensão

* Padronizar **largura máxima (max-width)** de 1280px com margens automáticas em todas as páginas (`margin: 0 auto;` e `padding: 1.5rem;`).
* Aplicar **sistema de grid flexível (Flexbox ou CSS Grid)** para garantir alinhamento central vertical/horizontal.
* Centralizar todos os objetos visuais e textuais nas seções principais (hero, cards, about, etc.).
* Garantir que o layout responda corretamente até **320px de largura (mobile)** sem quebra de elementos.
* Uniformizar espaçamentos verticais entre seções (mínimo `3rem`).

### Tipografia e equilíbrio visual

* Definir tamanhos proporcionais: títulos (2.5rem em desktop, 1.8rem em mobile), subtítulos (1.2rem), corpo (1rem fixo).
* Garantir contraste WCAG AA com base na paleta: `#705391` (texto principal) e `#A080CF` (detalhes).

---

## 2) Hero (Landing Page)

**Conteúdo único no centro da tela:**

```
Hannya Tech
```

O texto "Tech" será animado com o efeito de digitação, alternando entre três palavras:

```
Tech → Offsec → Intelligence → DevSecOps → (loop)
```

### Animação (efeito de digitação)

* Velocidade ajustada para parecer humana (~100ms por caractere).
* Cursor piscando ao final (como terminal `|`).
* Fade suave entre palavras (~250ms de transição).
* Alinhamento centralizado vertical/horizontal no viewport (100vh height).


---

## 3) Componente `whoami` — correção de velocidade e estética

### Problemas identificados

* Animação rápida e caótica.
* Falta de naturalidade ao simular digitação Bash.

### Correção

* Efeito mais lento (~90ms/caractere ao digitar e apagar).
* Adicionar cursor piscando.
* Sequência suave e linear (não randômica).
## 4) Internacionalização (i18n)

### Ajustes necessários

* Corrigir comportamento da página **NotFound**: quando alternar o idioma via `localeDropdown`, recarregar o conteúdo traduzido.
* Adicionar tradução de `404` em `i18n/en/docusaurus-theme-classic.json` e `i18n/pt-BR/...`.

```json
{
  "theme.NotFound.title": "Page not found",
  "theme.NotFound.title_pt": "Página não encontrada",
  "theme.NotFound.description": "The page you are looking for does not exist.",
  "theme.NotFound.description_pt": "A página que você procura não existe."
}
```

* Confirmar que o botão de idioma persiste o locale na URL (`/en/...`, `/pt-BR/...`).

---

## 5) Nova página — Anonimato / ProxyChains (25/10/2025)

Criar post no blog:
**`blog/2025-10-25-proxychains.md`**

````md
---
title: "Anonimato e ProxyChains — Defendendo sua origem na rede"
author: Aldry Albuquerque
tags: [Anonimato, Offsec]
date: 2025-10-25
---

## ProxyChains — introdução prática

ProxyChains é uma ferramenta poderosa para rotear conexões através de múltiplos proxies, preservando o anonimato e dificultando rastreamento. Neste artigo, discutiremos o uso ético da ferramenta em contextos de pesquisa e defesa.

### Conceito
ProxyChains intercepta as chamadas de rede e as redireciona via socks4, socks5 ou HTTP proxies. Permite camadas de anonimato (ex: TOR + Proxies Privados).

### Exemplo ético de uso
```bash
proxychains curl ifconfig.me
````

> *Nunca use ProxyChains para mascarar ações ilícitas. O foco é proteção e anonimato em ambientes de teste e pesquisa.*

```

---

## 6) Validação de código e deploy

- Rodar `npm run lint` e `npm run build` — garantir **0 warnings e 0 errors**.
- Testar `npm run serve` e validar responsividade (Chrome DevTools).
- Testar troca de idioma (EN/PT) em todas as rotas, incluindo NotFound.
- Testar modo claro/escuro e renderização da logo Hannya em ambos.
- Confirmar Lighthouse acima de 90 em Acessibilidade e Performance.

---

## 7) Resultado esperado

- Layout **simétrico, centralizado, responsivo**.
- `whoami` suave e natural (como digitação humana).
- Hero limpo com animação central "Hannya Tech".
- Alternância de idioma funcionando.
- Nova página de anonimato presente.
- Lint e build aprovados, prontos para deploy.

```
