# zabbix-n8n-ai-alerts
Automação de alertas do Zabbix com n8n e ChatGPT (AI Agent) — análise, classificação e envio inteligente.

# 🤖 Zabbix + n8n + ChatGPT (AI Agent) — Alertas Inteligentes

Automação de alertas do **Zabbix** com o **n8n** e **ChatGPT (AI Agent)** — análise, classificação e envio inteligente de alertas com ações sugeridas e roteamento automático por categoria.

---

## 🧠 Visão Geral

Este projeto cria uma automação completa de alertas do **Zabbix** usando o **n8n** e o **ChatGPT**, capaz de:

- Receber alertas via **Webhook do Zabbix**
- Consultar detalhes do trigger via **API do Zabbix**
- Enviar os dados para o **AI Agent (ChatGPT)**
- Classificar automaticamente a categoria do alerta (`INFRA`, `DEV`, `TELECOM`, etc.)
- Gerar um **resumo** e uma **ação sugerida**
- Enviar notificações formatadas por **e-mail** e **Telegram**
- Roteamento inteligente por área (Infraestrutura, Dev, Telecom...)

---

## ⚙️ Fluxo n8n

O fluxo principal do n8n processa o alerta, consulta o Zabbix, envia para o ChatGPT e distribui conforme a classificação.

📸 **Fluxo completo:**
![Fluxo do n8n](n8n-screenshots/Captura%20de%20tela%202025-10-20%20184146.png)

---

## 📬 Exemplo de E-mail

O alerta chega formatado com detalhes e ações sugeridas:

📸 **Exemplo de e-mail:**
![Email Exemplo](n8n-screenshots/Captura%20de%20tela%202025-10-20%20184157.png)

---

## 💬 Exemplo no Telegram

O mesmo alerta é enviado automaticamente ao grupo do time responsável no Telegram:

📸 **Exemplo de alerta no Telegram:**
![Telegram Exemplo](n8n-screenshots/Captura%20de%20tela%202025-10-20%20184211.png)

---

## 🧩 Estrutura do Fluxo (Resumo dos Nós)

| Etapa | Função |
|-------|--------|
| **Webhook n8n Zabbix** | Recebe o alerta via HTTP do Zabbix |
| **HTTP Request – Zabbix API** | Busca detalhes do trigger |
| **AI Agent (ChatGPT)** | Analisa o alerta e gera resumo + ação sugerida |
| **Code (JavaScript)** | Converte o JSON retornado pela IA |
| **Switch Node** | Define categoria (INFRA, DEV, TELECOM...) |
| **Send Email / Telegram** | Envia a notificação formatada para o canal correto |

---

## 🧠 Exemplo de Análise do ChatGPT

**Entrada:**


**Saída gerada pela IA:**
```json

{
  "categoria": "INFRA",
  "resumo": "O alerta indica uso elevado de CPU no host fusion8.",
  "acao_sugerida": "Verificar processos com alto consumo usando top/htop e avaliar necessidade de escalonamento de recursos.",
  "prioridade": "Alta"
}








