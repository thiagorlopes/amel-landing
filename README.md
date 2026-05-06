# Amel.ia — Landing

Landing institucional estática da Amel.ia. HTML + CSS puros, zero build, deploy gratuito via **GitHub Pages**.

## Estrutura

```
amel-landing/
├── index.html          # página única
├── styles.css          # estilos
├── assets/
│   ├── amelia-logo.png   # logo horizontal (header, footer)
│   └── amelia-icon.png   # logo quadrado (favicon)
├── .nojekyll           # diz ao GitHub Pages para servir como estático puro
└── README.md
```

## Rodar local

Não precisa servidor — basta abrir `index.html` no navegador. Se quiser servidor local:

```bash
python3 -m http.server 8000
# abra http://localhost:8000
```

## Deploy — GitHub Pages (passo a passo)

### 1) Criar repositório

```bash
cd /home/thiago/amel-landing
git init
git add .
git commit -m "feat: landing inicial"
```

Cria o repo no GitHub (web ou `gh repo create`):

```bash
gh repo create amel-landing --public --source=. --remote=origin --push
```

### 2) Ativar GitHub Pages

No GitHub: **Settings → Pages**:

- **Source**: `Deploy from a branch`
- **Branch**: `main` / pasta `/ (root)`
- Salvar.

Em ~1 minuto o site fica em `https://<seu-usuario>.github.io/amel-landing/`.

### 3) (Opcional) Domínio próprio amel.ia

Se você já registrou `amel.ia`:

1. Em **Settings → Pages → Custom domain**, coloque `amel.ia` e salve.
2. Crie um arquivo `CNAME` na raiz do repo com o conteúdo `amel.ia`.
3. No painel DNS do domínio `.ia`:
   - Apontar `A` para os IPs do GitHub Pages: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
   - Para `www.amel.ia`, criar `CNAME` apontando para `<seu-usuario>.github.io`.
4. Marcar **Enforce HTTPS** após validação (15 min a algumas horas).

> Domínios `.ia` (Anguila) ficam em registrars como Namecheap, Gandi, Porkbun, com preços ~US$ 80–200/ano. Caro, mas você já tem a marca. Alternativa: `amel.com.br` (~R$ 40/ano via Registro.br).

## Captura de leads — Formspree (grátis)

O form na seção **Lista de espera** está com placeholder. Para ativar:

1. Crie conta grátis em [formspree.io](https://formspree.io) (50 envios/mês no free).
2. Crie um novo form, copie o ID (algo tipo `xyzabcde`).
3. Em `index.html`, troque:

```html
<form class="lead-form" action="https://formspree.io/f/SEU_ID" method="POST">
```

por:

```html
<form class="lead-form" action="https://formspree.io/f/xyzabcde" method="POST">
```

4. Commit + push. GitHub Pages atualiza em ~1 minuto.

Os leads chegam no email cadastrado no Formspree. Alternativas: Tally, Getform, Web3Forms — mesmo princípio.

## Atualizar o conteúdo

Tudo está em `index.html`. Texto, preços, FAQ — basta editar. Nenhum build, nenhuma dependência. Após editar:

```bash
git add index.html
git commit -m "copy: ajusta headline da seção planos"
git push
```

GitHub Pages re-publica automaticamente.

## Para o cadastro Sebrae

Inclua no formulário do Sebrae:

- **Site institucional**: `https://<seu-usuario>.github.io/amel-landing/` (ou `amel.ia` se já configurado)
- **Email de contato**: `contato@amel.ia` (configurar caixa antes — Google Workspace ou redirecionamento gratuito via registrar)
- **Pitch curto**: extrair do hero + seção "Proposta" — *"Inteligência financeira para o médico premium. Substituímos o serviço de wealth management — hoje só acessível a patrimônios acima de R$ 5 milhões — por um produto automatizado para a faixa underserved da classe média alta brasileira, entrando pelo médico estabelecido."*
- **Modelo de receita**: assinatura mensal (Founding Member R$ 149 lifetime / Core R$ 299 / Concierge R$ 799). Conteúdo já está na landing.
- **Estágio**: pré-MVP, validando ICP via cohort de Founding Members.

## Decisões de design

- **Stack**: HTML + CSS puros. Sem JS, sem build, sem framework. Carrega < 50KB (mais o logo PNG).
- **Tipografia**: Fraunces (serif) para títulos + Inter (sans) para corpo. Tom *private banking*, não *PFM SaaS*.
- **Paleta**: bordeaux `#5C1A26` (logo) + dourado `#C9A14A` (acento) + creme `#FBF8F3` (fundo).
- **Sem cookies, sem analytics no MVP** — adicionar Plausible ou Umami quando precisar (ambos têm tier free para projetos pessoais).
