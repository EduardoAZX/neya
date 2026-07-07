# Dra. Neya Penha · Landing Page

Landing page de captação de leads para a **Dra. Neya Penha**, especialista em tratamento de estrias e responsável pelo protocolo autoral **Beauty Derm** (microagulhamento associado a ativos regeneradores, em apenas 3 sessões).

---

## 📁 Estrutura de pastas

```
Neya Penha/
├── index.html          # Estrutura semântica das 4 dobras + modais de Termos/Privacidade
├── style.css             # Design system + componentes + responsividade
├── app.js                 # Reveals, máscara de WhatsApp, validação e submit do form, modais
├── README.md               # Este arquivo
├── obrigado.html            # Página de obrigado (redirecionada após o envio do formulário)
├── .htaccess                 # Remoção de .html da URL + headers de segurança
└── assets/
    ├── doctor.webp                        # Hero (foto Dra. Neya Penha)
    ├── doctor-about.webp                  # Foto para a seção "Sobre"
    ├── before-after-1..3-antes.webp       # Antes/depois, lado A (3 casos)
    ├── before-after-1..3-depois.webp      # Antes/depois, lado B (3 casos)
    └── fonts/                             # Fontes locais compradas (Bodoni Moda/Helixa, se aplicável)
```

> Todas as imagens referenciadas em `index.html` apontam para a pasta `assets/`.

---

## 🎨 Design system

| Token              | Valor        | Uso                                          |
|---------------------|--------------|-----------------------------------------------|
| `--c-primary`        | `#847967`    | Botões, badges, destaques (taupe/marrom claro) |
| `--c-primary-2`      | `#6F6555`    | Gradientes, itálicos de destaque               |
| `--c-secondary`      | `#EFEAE0`    | Fundos sutis, placeholders                     |
| `--c-accent`         | `#4B372E`    | CTA escuro, texto principal                    |
| `--c-bg`             | `#F7F4ED`    | Fundo padrão (creme)                           |
| `--c-text`           | `#4B372E`    | Texto principal                                |
| `--c-muted`          | `#8A8071`    | Texto secundário                               |
| `--c-line`           | `#E7E0D2`    | Bordas e divisores                             |

- **Fontes:** Bodoni Moda (serifada, títulos) e Inter (sans, corpo), via Google Fonts.
- **Efeitos:** glassmorphism (`backdrop-filter: blur`), sombras suaves em camadas (`--shadow-sm/md/lg/glow`).
- **Favicon:** SVG inline com a inicial **N** sobre o tom primário.

---

## 🧩 Seções da LP

### 🟠 Dobra 1 · Dor
- **Imagens:** `assets/doctor.webp`.
- H1 de dor (estrias/autoestima) + parágrafo de contexto + CTA primário (`#agendar`) e CTA fantasma (`#resultados`).
- Pills de diferenciais (tratamento individualizado, apenas 3 sessões, kit home care) e marquee decorativo.

### 🟠 Dobra 2 · Resultados
- **Imagens:** `assets/before-after-1..3-antes.webp` / `-depois.webp`.
- Grid de 3 cards com pares antes/depois lado a lado, checklist de diferenciais e selo de autoridade ("3 sessões apenas").

### 🟠 Dobra 3 · Formulário (captação)
- **Campos:** Nome, Telefone (WhatsApp, máscara `(00) 00000-0000`), Cidade, "Como surgiram suas estrias?" (rádio: Pós-parto / Pós-emagrecimento / Ganho de peso / Outro).
- Validação client-side em `app.js`. Ao validar com sucesso, envia para o webhook do Make (`MAKE_WEBHOOK_URL`) e redireciona para `obrigado.html`.

### 🟠 Dobra 4 · Sobre a Dra. Neya Penha
- **Imagens:** `assets/doctor-about.webp`.
- Copy de autoridade sobre o protocolo Beauty Derm + stats + CTA escuro.

### 🟠 Rodapé
- Barra inferior: copyright + links de Termos de Uso / Política de Privacidade (abrem em modal) / Desenvolvido por AZX Performance.

---

## 📜 Termos de Uso & Política de Privacidade

Acessíveis via modal a partir dos links no rodapé (`#openTerms` / `#openPrivacy`). A Política de Privacidade é redigida com base na **LGPD (Lei nº 13.709/2018)**, cobrindo: dados coletados (nome, telefone, cidade, como surgiram as estrias), finalidade do tratamento, base legal, compartilhamento, armazenamento/segurança e direitos do titular.

---

## 🔌 Integrações

- **Google Tag Manager:** container `GTM-MJQJPGBC` instalado no `<head>` e `<noscript>` de `index.html`/`obrigado.html`. `obrigado.html` dispara `dataLayer.push({event: 'lead'})` no carregamento, servindo de trigger de conversão no GTM.
- **Webhook (Make):** configurado em `app.js` (`MAKE_WEBHOOK_URL`). O submit handler envia o payload do formulário e só então redireciona para `obrigado.html`.
- **Meta Pixel / CAPI:** não instalado neste projeto.

---

## 📱 Responsividade

| Faixa                | Comportamento                                                   |
|-----------------------|------------------------------------------------------------------|
| **≥ 981px**            | Layouts em 2 colunas (hero, form, about); grid de resultados em 2 colunas |
| **820 a 980px**        | Form e about colapsam para 1 coluna                               |
| **≤ 880px**            | Hero colapsa para 1 coluna, foto centralizada                      |
| **≤ 620px**            | Grid de resultados vira 1 coluna                                    |
| **≤ 520px**            | Ajustes finos de tipografia e botões em largura total               |
| **≤ 400px**            | Ajustes finos adicionais (pills, eyebrow, stats)                   |

---

## 🔒 Segurança

- Sem `innerHTML`/`eval`/`document.write` no client-side (sem vetor de XSS via DOM).
- Links externos (`target="_blank"`) sempre com `rel="noopener noreferrer"`.
- Sem conteúdo via `http://` (mixed content).
- `.htaccess` com headers de segurança (X-Frame-Options, CSP, Referrer-Policy, etc.) e remoção de `.html` da URL.
- Validação client-side do formulário em `app.js`; validação server-side deverá ser adicionada junto da integração de envio, caso necessário.

---

## 🤝 Como contribuir

- **Adicionar uma nova seção:** crie o markup dentro de `index.html` entre duas dobras existentes, atribua um `data-screen-label="NN Nome"` e adicione as classes ao final de `style.css` seguindo o padrão `.nome-secao__elemento`.
- **Mudar a paleta:** edite as custom properties no topo de `style.css` (`:root`).
- **Mudar copy:** todas as strings estão diretamente em `index.html`, sem CMS ou template engine.

---

© 2026 Dra. Neya Penha. Todos os direitos reservados.
