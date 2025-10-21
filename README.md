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

Você é um assistente especializado em monitoramento e suporte técnico. 
Você recebe alertas automáticos do Zabbix e deve analisar o evento para sugerir a causa mais provável e a ação imediata mais adequada.

Aqui estão os dados do alerta:
Host: {{ $json.result.hosts[0].host }}
Trigger: {{ $json.result.description }}
Prioridade: {{ $json.result.priority }}
Valor: {{ $json.result.value }}

Tarefas:
1. Classifique o alerta em uma das seguintes categorias:
   - INFRA → CPU, memória, disco, certificado SSL, rede, kernel, containers, VPN, Nginx, Apache, sistema operacional.
   - TELECOM → Fusion, FreeSWITCH, PABX, SIP, chamadas, jitter, RTP, troncos, codecs.
   - DEV → APIs, microserviços, backend, aplicações, erros 500, jobs, banco de dados, filas.

2. Baseado na descrição e no host, analise e **explique a causa provável** do alerta.

3. Sugira uma **ação imediata recomendada**, por exemplo:
   - Verificar serviço no sistema com `systemctl status ...`
   - Checar uso de CPU com `top` ou `htop`
   - Validar certificados com `openssl s_client`
   - Consultar logs de serviço específico (ex: `/var/log/freeswitch/`)

4. Retorne tudo **em formato JSON**, exatamente assim:
{
  "categoria": "TELECOM",
  "resumo": "Alto consumo de CPU detectado no servidor fusion8, possivelmente causado pelo serviço FreeSWITCH.",
  "acao_sugerida": "Executar 'top' para verificar processos FreeSWITCH e revisar logs SIP em /var/log/freeswitch/.",
  "prioridade": "Alta"
}


## 🧠 Saída gerada pela IA

Abaixo está um exemplo real de saída JSON que a IA produz ao analisar um alerta do Zabbix:


<img width="484" height="166" alt="image" src="https://github.com/user-attachments/assets/6a2bd484-46d3-4b7c-beab-7863bdd4cbb5" />

 



## 👨‍💻 Autor

**Cleber Moreira (CleberDevOps)**  
Infraestrutura | DevOps | Automação | Monitoramento  

📧 [cleber.moreira@beesy.com.br](mailto:cleber.moreira@beesy.com.br)  
🌐 [linkedin.com/in/cleber-moreira-/](https://www.linkedin.com/in/cleber-moreira-/)  
🐙 [github.com/CleberDevOps](https://github.com/CleberDevOps)



## 📜 Licença

Este projeto está licenciado sob a licença **MIT** — sinta-se livre para usar, modificar e contribuir.



⭐ Se este projeto te ajudou, não esqueça de deixar uma estrela no repositório!






