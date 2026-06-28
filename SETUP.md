# ⚡ Setup Rápido — EloSaúde Local

## 1️⃣ Clonar/Baixar

```bash
git clone https://github.com/esterevelise/elosaude-analyzer.git
cd elosaude-analyzer
```

## 2️⃣ Instalar Dependências

```bash
npm install
```

Espera instalar:
- `@anthropic-ai/sdk` (API Claude)
- `express` (framework web)
- `cors` (cross-origin requests)

## 3️⃣ Configurar API Key

**Opção A: Arquivo `.env` (Recomendado)**
```bash
cp .env.example .env
# Edite .env com seu editor
# ANTHROPIC_API_KEY=sk-ant-...
```

**Opção B: Variável de Ambiente**
```bash
export ANTHROPIC_API_KEY=sk-ant-...
```

## 4️⃣ Iniciar Servidor

```bash
npm start
```

Você deve ver:
```
Servidor EloSaude rodando na porta 3000
```

## 5️⃣ Acessar

Abra no navegador:
```
http://localhost:3000
```

### Telas Disponíveis:
- **Home:** http://localhost:3000
- **Formulário IMC:** http://localhost:3000/imc
- **API /calcular-imc:** POST para calcular IMC

---

## 🧪 Testar IMC via cURL

```bash
curl -X POST http://localhost:3000/calcular-imc \
  -H "Content-Type: application/json" \
  -d '{
    "peso": 70,
    "altura": 170,
    "genero": "M",
    "nome": "João Silva"
  }'
```

Resposta esperada:
```json
{
  "success": true,
  "imc": "24.22",
  "classificacao": "Peso Normal",
  "html": "<div>...</div>"
}
```

---

## 🔧 Variáveis Disponíveis

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `PORT` | 3000 | Porta do servidor |
| `NODE_ENV` | development | Ambiente (production em Railway) |
| `ANTHROPIC_API_KEY` | (obrigatório) | Chave API Claude |

---

## 📁 Estrutura do Projeto

```
elosaude-analyzer/
├── server.js              ← Servidor principal (Express + Anthropic)
├── package.json           ← Dependências
├── .env.example           ← Template de variáveis
├── Dockerfile             ← Para Railway
├── README.md              ← Documentação geral
├── DEPLOY_RAILWAY.md      ← Instruções de deploy
├── SETUP.md               ← Este arquivo
└── public/                ← Arquivos estáticos (se houver)
```

---

## ✅ Checklist de Funcionamento

- [ ] `npm install` rodou sem erros
- [ ] `.env` tem `ANTHROPIC_API_KEY` válida
- [ ] `npm start` mostra "rodando na porta 3000"
- [ ] GET http://localhost:3000 carrega a home
- [ ] GET http://localhost:3000/imc carrega formulário
- [ ] POST /calcular-imc retorna JSON com IMC

---

## ❌ Erros Comuns

### "EADDRINUSE: address already in use :::3000"
```bash
# Mude a porta
PORT=3001 npm start
```

### "Error: API key is not defined"
- Verifique se `.env` existe e tem `ANTHROPIC_API_KEY`
- Reinicie o servidor depois de editar `.env`

### "Cannot GET /imc"
- Verifique se o server está rodando
- Acesse http://localhost:3000 (home) primeiro

---

## 🚀 Próximo Passo: Deploy no Railway

Quando tudo estiver funcionando localmente, siga `DEPLOY_RAILWAY.md` para publicar online.

---

**Última atualização:** 24 de junho de 2026
