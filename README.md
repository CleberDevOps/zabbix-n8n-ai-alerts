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
![Fluxo do n8n]

<img width="1663" height="642" alt="image" src="https://github.com/user-attachments/assets/3d85688e-b061-436c-8a26-6bc6bab8264e" />



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








