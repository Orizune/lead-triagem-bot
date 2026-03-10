# 🤖 Lead Triagem Bot

Bot de triagem automática de leads via Telegram com classificação por IA.

Recebe mensagens → IA classifica (QUENTE/MORNO/FRIO) → responde automaticamente.

---

## 🧩 Como funciona

```
Usuário manda mensagem no Telegram
        ↓
n8n recebe via webhook (ngrok ou servidor)
        ↓
IF filtra comandos como /start
        ↓
Groq (LLM) classifica o lead
        ↓
Bot responde no Telegram
```

---

## 🛠️ Stack

| Ferramenta | Função | Custo |
|---|---|---|
| n8n | Orquestração do fluxo | Grátis (self-hosted) |
| Telegram Bot API | Canal de comunicação | Grátis |
| Groq API | Classificação por IA (llama-3.3-70b) | Grátis |
| ngrok | Túnel HTTPS para desenvolvimento | Grátis |
| Docker | Rodar o n8n localmente | Grátis |

---

## ⚙️ Pré-requisitos

- Docker Desktop instalado
- Conta no [Telegram](https://telegram.org)
- Conta no [Groq](https://console.groq.com) (gratuita)
- Conta no [ngrok](https://ngrok.com) (gratuita)
- n8n rodando via Docker

---

## 🚀 Instalação

### 1. Subir o n8n com ngrok

Inicie o ngrok apontando para a porta do n8n:

```bash
ngrok http 5678
```

Copie a URL gerada (ex: `https://abc123.ngrok-free.app`) e rode:

```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  -e N8N_COMMUNITY_PACKAGES_ENABLED=true \
  -e WEBHOOK_URL=https://SUA-URL-NGROK.ngrok-free.app \
  n8nio/n8n
```

### 2. Criar o bot no Telegram

1. Abra o [@BotFather](https://t.me/BotFather) no Telegram
2. Digite `/newbot`
3. Escolha nome e username (deve terminar em `bot`)
4. Guarde o token gerado

### 3. Obter chave do Groq

1. Acesse [console.groq.com/keys](https://console.groq.com/keys)
2. Crie uma conta gratuita
3. Gere uma API key

### 4. Importar o workflow no n8n

1. Acesse `http://localhost:5678`
2. Vá em **Workflows → Import**
3. Importe o arquivo `workflows/lead-triagem-bot.json`
4. Configure as credenciais do Telegram com seu token
5. Configure o HTTP Request com sua chave do Groq no header `Authorization: Bearer SUA_CHAVE`
6. Ative o workflow

---

## 📁 Estrutura do projeto

```
lead-triagem-bot/
├── workflows/
│   └── lead-triagem-bot.json     ← Workflow para importar no n8n
├── docs/
│   └── COMO-ADAPTAR.md           ← Como personalizar para cada nicho
├── .env.example                  ← Exemplo de variáveis de ambiente
└── README.md
```

---

## 🎯 Classificação de leads

O prompt da IA classifica cada mensagem em:

| Classificação | Critério |
|---|---|
| 🔥 QUENTE | Interesse claro + urgência |
| 🌡️ MORNO | Interesse sem urgência |
| ❄️ FRIO | Sem interesse claro ou mensagem genérica |

---

## 🔧 Como adaptar para um nicho

Veja o arquivo `docs/COMO-ADAPTAR.md` para instruções detalhadas de como personalizar o bot para clínicas, imobiliárias, pet shops e outros nichos.

---

## 📈 Próximas funcionalidades

- [ ] Resposta diferente por classificação (QUENTE/MORNO/FRIO)
- [ ] Salvar leads em Google Sheets automaticamente
- [ ] Notificar dono do negócio quando lead QUENTE chegar
- [ ] Histórico de conversa em JSON local
- [ ] Deploy em Oracle Cloud Free (sem ngrok)

---

## ⚠️ Aviso

Este projeto usa o Telegram como canal de prototipagem. Para produção com WhatsApp, utilize a [Evolution API](https://github.com/EvolutionAPI/evolution-api) com WhatsApp Business API oficial.

---

## 👤 Autor

**Guilherme Siqueira Benites**
- GitHub: [@Orizune](https://github.com/Orizune)
- LinkedIn: [guilherme-siqueira-no-code-low-code](https://linkedin.com/in/guilherme-siqueira-no-code-low-code)
- Campo Grande, MS — Brasil

---

*Projeto desenvolvido como parte do portfólio de automação no-code/low-code com IA.*
