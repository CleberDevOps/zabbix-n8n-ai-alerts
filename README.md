# Zabbix + n8n + IA | Triagem Inteligente de Alertas

**Automação de monitoramento e resposta operacional** usando Zabbix, n8n e ChatGPT (AI Agent). Projeto de portfólio voltado a **SRE, observabilidade e automação de infraestrutura**.

> **Escopo do repositório:** documentação funcional e capturas do fluxo. O export do workflow n8n e scripts executáveis **não estão publicados neste repositório**. Não é um pacote pronto para instalação.

## O problema

Operações de infraestrutura recebem alertas de diferentes serviços, com níveis variados de prioridade. A triagem manual exige interpretar cada evento, determinar a equipe adequada e comunicar a ação inicial de diagnóstico.

## A solução

Um fluxo de automação documentado para enriquecer, classificar e encaminhar eventos do Zabbix:

1. **Recepção:** webhook recebe o evento gerado no Zabbix.
2. **Enriquecimento:** consulta à API do Zabbix para obter dados adicionais do evento/trigger.
3. **Análise assistida por IA:** o AI Agent interpreta os dados, produz um resumo e sugere verificações iniciais.
4. **Classificação:** categoriza o evento por área técnica (por exemplo, INFRA, TELECOM e DEV).
5. **Roteamento:** um nó de decisão direciona a notificação para e-mail ou Telegram conforme a categoria.

A IA **apoia a triagem**, mas suas hipóteses precisam ser confirmadas pela equipe técnica antes de ações em produção.

## Arquitetura funcional

```text
Zabbix (evento/trigger)
        |
        v
   Webhook n8n
        |
        v
  Consulta Zabbix API
        |
        v
 ChatGPT / AI Agent
        |
        v
 Análise + classificação
        |
        v
   Switch (categoria)
        |
        +--> INFRA   --> canal da equipe de infraestrutura
        +--> TELECOM --> canal da equipe de telecom
        +--> DEV     --> canal da equipe de desenvolvimento
```

## Tecnologias e conceitos

- **Zabbix:** monitoramento, triggers, eventos e API.
- **n8n:** orquestração, webhooks, requisições HTTP, transformação de dados e roteamento.
- **ChatGPT / AI Agent:** resumo técnico, hipóteses e ações recomendadas.
- **E-mail e Telegram:** canais de notificação.
- **Práticas SRE:** enriquecimento de alertas, triagem, escalonamento e rastreabilidade.

## Demonstração visual

**Fluxo de automação no n8n**

![Fluxo Zabbix, n8n e AI Agent](https://github.com/user-attachments/assets/3d85688e-b061-436c-8a26-6bc6bab8264e)

**Exemplo de saída estruturada da análise**

![Exemplo de classificação e resposta do agente](https://github.com/user-attachments/assets/6a2bd484-46d3-4b7c-beab-7863bdd4cbb5)

## Exemplo ilustrativo

Um alerta de CPU elevada em um servidor de telefonia pode ser classificado como **TELECOM**, com resumo do problema, indicação de prioridade e sugestão de consultar processos e logs do serviço.

Esse diagnóstico é uma **hipótese inicial**, não uma conclusão automática de causa raiz.

## Segurança e boas práticas

- Não versionar tokens de API, credenciais, dados pessoais ou configurações de produção.
- Manter segredos em mecanismos próprios de gerenciamento de credenciais.
- Aplicar controle de acesso aos webhooks e aos canais de notificação.
- Tratar saídas da IA como sugestões; validar mudanças e comandos antes de executá-los.
- Evitar incluir IPs, nomes de clientes, hostnames internos e conteúdo sensível nos exemplos públicos.

## Próximos aprimoramentos do portfólio

- Disponibilizar um **workflow de demonstração anonimizado**, se houver autorização de compartilhamento.
- Incluir exemplos fictícios de payload e resposta JSON.
- Adicionar documentação de testes, tratamento de erros e fluxo de reprocessamento.

## Autor

**Cleber Moreira — Infraestrutura Linux | SRE | Observabilidade | Automação**

- [GitHub — CleberDevOps](https://github.com/CleberDevOps)
- [LinkedIn — Cleber Moreira](https://www.linkedin.com/in/cleber-moreira-/)

## Licenciamento

O README anterior mencionava MIT, mas **não há arquivo LICENSE no repositório**. A definição formal do licenciamento deve ser confirmada pelo responsável antes de reutilizar ou distribuir componentes.
