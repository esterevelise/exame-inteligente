# EloSaúde Analyzer v2.0 — Com suporte a IMC

Plataforma AI-assistida para análise inteligente de exames laboratoriais com cálculo e visualização de IMC baseada em protocolo de medicina funcional e integrativa.

## 🏥 Sobre

**EloSaúde** é uma solução que integra:
- Análise automática de resultados de exames via PDF
- Comparação com tabela customizada de valores ideais (não laboratoriais)
- Cálculo de IMC com visualização gender-specific
- Geração de relatórios profissionais em HTML/PDF
- Relatórios para pacientes em linguagem acessível

**Responsável profissional:** Eloise Mari Mendes, COREN/PR 740225

## 📋 Funcionalidades

### Etapas Implementadas (6 total)

1. **Extração** — Lê PDF, extrai valores + peso/altura/gênero
2. **Análise com Criticidade** — Compara com tabela EloSaúde, classifica severidade
3. **Relatório Clínico** — Gerado para uso de Eve (profissional)
4. **Alertas Automáticos** — Valores críticos disparam notificações
5. **IMC com Visualização** — Cálculo + silhueta gender-specific (mulher/homem)
6. **Relatório do Paciente** — HTML/PDF pronto para envio ao paciente

## 🚀 Deploy no Railway

### 1. Requisitos
- Conta no GitHub (para push)
- Conta no Railway (railway.app)
- Chave API da Anthropic

### 2. Setup Local

```bash
# Clone o repositório
git clone https://github.com/esterevelise/elosaude-analyzer.git
cd elosaude-analyzer

# Instale dependências
npm install

# Configure variáveis
cp .env.example .env
# Edite .env com sua ANTHROPIC_API_KEY

# Teste localmente
npm run dev
# Acesse http://localhost:3000
```

### 3. Deploy no Railway

#### Opção A: Conectar GitHub (Recomendado)

1. Push para GitHub:
```bash
git add .
git commit -m "Initial commit: EloSaúde v2 com IMC"
git push origin main
```

2. No Railway.app:
   - Sign in com GitHub
   - New Project → GitHub Repo
   - Selecione `elosaude-analyzer`
   - Configure variáveis de ambiente:
     - `ANTHROPIC_API_KEY` = sua chave
     - `NODE_ENV` = production
   - Deploy automático após cada push

#### Opção B: Deploy Manual (Railway CLI)

```bash
# Instale Railway CLI
npm i -g @railway/cli

# Login
railway login

# Deploy
railway up

# View logs
railway logs
```

## 📊 Estrutura de Arquivos

```
elosaude-analyzer/
├── server.js                      # Servidor Express com rotas
├── package.json                   # Dependências
├── .env.example                   # Template de variáveis
├── .gitignore                     # Ignore patterns
├── README.md                      # Esta documentação
└── public/
    ├── index.html                 # Página inicial
    └── formulario-imc.html        # Formulário de IMC
```

## 🔗 Endpoints da API

### 1. GET `/` — Home
Retorna página inicial com botões de ação.

### 2. GET `/imc` — Formulário IMC
Página com campos para **peso** (kg), **altura** (cm), **gênero** e **nome**.

### 3. POST `/calcular-imc`
**Body:**
```json
{
  "peso": 70,
  "altura": 170,
  "genero": "M",
  "nome": "João"
}
```

**Response:**
```json
{
  "success": true,
  "imc": 24.2,
  "classificacao": "Peso Normal",
  "html": "<div>...</div>"
}
```

### 4. POST `/analisar` — Análise Completa
**Body:**
```json
{
  "pdfBase64": "iVBORw0KGgoAAAAN...",
  "patientName": "João Silva"
}
```

Executa 6 etapas:
1. Extração
2. Análise com criticidade
3. Relatório clínico
4. Alertas
5. IMC
6. PDF para paciente

## 📸 Screenshots de Uso

### Formulário IMC
- Input: peso (kg), altura (cm), gênero
- Output: IMC + silhueta gender-specific

### Relatório Paciente
- Análise de exames com cores por criticidade
- Seção IMC com visualização
- Linguagem acessível

## 🔐 Segurança

- CORS habilitado para acesso remoto
- Limite de upload: 50MB (PDF base64)
- API Key via variável de ambiente (nunca no código)
- HTTPS recomendado em produção

## 🛠️ Troubleshooting

### Porta já em uso
```bash
# Mude a PORT
export PORT=3001
npm start
```

### Erro na API Anthropic
- Verifique `ANTHROPIC_API_KEY` em `.env`
- Teste a chave no console Anthropic

### PDF não processa
- PDF deve ser válido com texto legível
- Máximo 50MB base64

## 📚 Referências

- **Protocolo EloSaúde:** `/mnt/project/CLAUDE_meu_FINAL_4.md`
- **Tabelas de Valores Ideais:** Embarcadas no `server.js`
- **Imagens IMC:** Base64 geradas automaticamente

## 👨‍⚕️ Responsável

**Eloise Mari Mendes**
- COREN/PR 740225
- Especialista em Medicina Funcional e Integrativa
- EloSaúde — Cuidado e Conhecimento

## 📝 Changelog

### v2.0.0 (Jun 2026)
- ✅ Integração de IMC (Passo 5)
- ✅ Visualização gender-specific (mulher/homem)
- ✅ Deploy em Railway.app
- ✅ Novo projeto estruturado (sem quebrar produção)

### v1.0.0
- Análise básica de exames (4 etapas)
- Geração de PDF

## 📄 Licença

PROPRIETARY — Exclusivo de EloSaúde

---

**Última atualização:** 24 de junho de 2026
