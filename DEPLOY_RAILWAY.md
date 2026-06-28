# 🚀 Guia de Deploy — EloSaúde no Railway

## Opção 1: Deploy via GitHub (Recomendado ⭐)

### Passo 1: Preparar GitHub

```bash
# Na raiz do projeto
git init
git add .
git commit -m "EloSaúde v2: Lab analyzer com IMC"
git branch -M main
git remote add origin https://github.com/esterevelise/elosaude-analyzer.git
git push -u origin main
```

### Passo 2: Railway.app Setup

1. **Criar conta:** railway.app → Sign up com GitHub
2. **Novo projeto:** 
   - New Project → GitHub Repo
   - Selecione `elosaude-analyzer`
3. **Configurar variáveis:**
   - Settings → Variables
   - Adicione: `ANTHROPIC_API_KEY=sua_chave_aqui`
   - Adicione: `NODE_ENV=production`
4. **Deploy automático:**
   - Railway auto-detecta `package.json`
   - Lê `Dockerfile` automaticamente
   - Deploy ocorre em cada push

### Resultado
- **URL:** `seu-projeto-name.up.railway.app`
- **Logs:** Railway Dashboard → Logs
- **Atualizações:** Automáticas com cada `git push`

---

## Opção 2: Deploy Manual (Railway CLI)

### Passo 1: Instalar CLI

```bash
npm install -g @railway/cli
```

### Passo 2: Login e Deploy

```bash
# Login com GitHub
railway login

# Fazer deploy
railway up

# Ver logs em tempo real
railway logs

# Ver URL da aplicação
railway logs | grep "listening"
```

---

## Opção 3: Deploy via Docker Local (Teste)

```bash
# Build
docker build -t elosaude-analyzer .

# Run
docker run -p 3000:3000 \
  -e ANTHROPIC_API_KEY="sua_chave" \
  -e NODE_ENV=production \
  elosaude-analyzer

# Acesse: http://localhost:3000
```

---

## ⚠️ Troubleshooting

### Erro: "ANTHROPIC_API_KEY is not set"
- ✅ Railway → Project Settings → Variables
- ✅ Confirme nome exato: `ANTHROPIC_API_KEY`
- ✅ Redeploy após adicionar

### Erro: "Port already in use"
- Railway automaticamente mapeia para port aleatória
- Verifique a URL gerada no dashboard

### Logs em branco?
```bash
railway logs --follow
```

### Quer resetar tudo?
```bash
railway down
railway up
```

---

## 📊 Verificar Saúde da Aplicação

```bash
# Health check
curl https://seu-projeto.up.railway.app/

# POST IMC test
curl -X POST https://seu-projeto.up.railway.app/calcular-imc \
  -H "Content-Type: application/json" \
  -d '{"peso": 70, "altura": 170, "genero": "M", "nome": "Teste"}'
```

---

## 💰 Preço Railway

- **Free tier:** 5 USD/mês em créditos
- EloSaúde usa ~1-2 USD/mês com uso normal
- Sem cartão de crédito necessário para começar

---

## 🔗 Links Úteis

- Dashboard: https://railway.app/dashboard
- Documentação Railway: https://docs.railway.app
- Antropic API Keys: https://console.anthropic.com

---

**Última atualização:** 24 de junho de 2026
