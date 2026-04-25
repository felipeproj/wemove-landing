# WeMove — Landing Page

> Site público do WeMove hospedado em `wemoveapp.co`

---

## O que é o WeMove

WeMove é uma ferramenta de planejamento de mudança assistida por IA. O usuário descreve o apartamento para o qual vai se mudar (quantos quartos, ambientes, número de moradores) e a IA gera automaticamente uma lista de compras personalizada — organizada por ambiente, com prioridade e estimativa de custo para cada item.

A lista gerada pode ser editada livremente, compartilhada por link (com permissão de visualização ou edição), e atualizada conforme os itens vão sendo comprados.

---

## O que é este repositório

Este é o site público do WeMove — uma landing page estática hospedada em `wemoveapp.co`. É o primeiro ponto de contato com novos usuários: explica o produto, demonstra o fluxo e direciona para o app.

O site é um único arquivo `index.html` com HTML e CSS embutidos. Não há framework, não há build step, não há dependências de npm.

```
wemove-landing/
├── index.html      # Site completo (HTML + CSS inline)
├── vercel.json     # Configuração de deploy e redirects
└── README.md       # Este arquivo
```

### Seções da landing page

- **Hero com CTA** — headline, subtítulo, botão "Criar minha lista grátis" e mockup do app
- **Social proof** — métricas de tempo de geração, volume de itens e custo zero
- **Como funciona** — quatro passos com simulação visual do chat com a IA
- **Features** — grid com os principais recursos do produto
- **CTA final** — chamada para conversão com fundo gradiente

---

## Arquitetura do projeto WeMove

O WeMove é composto por três serviços independentes, cada um em seu próprio repositório e domínio:

| Serviço | Repositório | Domínio |
|---|---|---|
| **Landing page** (este repo) | `felipeproj/wemove-landing` | `wemoveapp.co` |
| **App React** (frontend) | `felipeproj/wemove-app` | `app.wemoveapp.co` |
| **API** (backend) | `felipeproj/wemove-api` | `api.wemoveapp.co` |

### Fluxo do usuário

```
wemoveapp.co  →  clica em "Começar grátis"
     ↓
app.wemoveapp.co  →  descreve o apartamento para a IA
     ↓
api.wemoveapp.co  →  IA gera a lista de compras personalizada
     ↓
app.wemoveapp.co  →  lista pronta para editar, marcar e compartilhar
```

---

## Tech stack

| Camada | Tecnologia |
|---|---|
| Landing page | HTML + CSS (sem framework, sem build) |
| Frontend app | React + TypeScript + Vite + Tailwind CSS |
| Estado global | Zustand |
| Backend / API | Node.js |
| Banco de dados | Supabase (PostgreSQL) |
| IA | OpenAI / Claude (geração de listas e recomendações) |
| Deploy | Vercel |
| DNS / CDN | Cloudflare |

---

## Deploy

O deploy é automático via Vercel. A cada `git push` para a branch `main`, o Vercel publica uma nova versão em `wemoveapp.co`.

### Configuração Vercel

| Campo | Valor |
|---|---|
| Framework Preset | Other |
| Root Directory | `.` (raiz do repositório) |
| Build Command | _(nenhum)_ |
| Output Directory | `.` |

### DNS (Cloudflare)

Os registros abaixo devem ser adicionados no painel do Cloudflare com o proxy **desativado** (nuvem cinza — modo "DNS only"). Com o proxy ativo, o Vercel não consegue emitir o certificado SSL.

| Tipo | Nome | Valor | Proxy |
|---|---|---|---|
| `A` | `@` | `76.76.21.21` | DNS only ☁️ |
| `CNAME` | `www` | `cname.vercel-dns.com` | DNS only ☁️ |

---

## Desenvolvimento local

Não há build. Para visualizar localmente, basta abrir o `index.html` no navegador:

```bash
# Abrir direto no macOS
open index.html

# Servidor local simples
npx serve .

# ou com Python
python3 -m http.server 8080
```

---

## Licença

MIT
