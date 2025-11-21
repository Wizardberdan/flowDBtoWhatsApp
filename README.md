# 🚀 Agente de BI Autônomo com IA Generativa & WhatsApp

> Automação "End-to-End" que transforma dados brutos de SQL Server em insights estratégicos, entregues via WhatsApp.

![n8n Version](https://img.shields.io/badge/n8n-latest-orange) ![Docker](https://img.shields.io/badge/Docker-Compose-blue) ![Status](https://img.shields.io/badge/Status-Functional-brightgreen)

## 📋 Sobre o Projeto

Este projeto elimina a fricção no acesso a indicadores de negócio. O sistema extrai dados de um ERP corporativo, processa as informações utilizando **IA Generativa (Claude 3.5 Haiku)** para gerar um resumo executivo humanizado e entrega o relatório proativamente no WhatsApp da diretoria.

**O Problema:** Diretores precisavam fazer login em sistemas complexos ou aguardar extrações manuais para saber o fechamento de vendas do dia.
**A Solução:** Um analista de dados virtual que "acorda" agendado, analisa os números e envia um briefing direto no celular.

---

## 🛠️ Arquitetura e Stack

O projeto é 100% containerizado com Docker.

* **Orquestração:** [n8n](https://n8n.io/) (Self-hosted workflow automation)
* **Banco de Dados (Fonte):** Microsoft SQL Server
* **Inteligência Artificial:** LangChain + Anthropic (Claude Haiku 3.5)
* **Mensageria:** WhatsApp via [Evolution API](https://github.com/EvolutionAPI/evolution-api)
* **Infraestrutura:** Docker & Docker Compose (com Postgres e Redis para suporte)

### Fluxo de Dados (Workflow)
1.  **Cron:** Gatilho temporal (ex: todos os dias às 18h).
2.  **MS SQL:** Query analítica para extrair vendas e metas por loja.
3.  **Tratamento (JS):** Sanitização do JSON para reduzir custo de tokens.
4.  **LLM Chain:** A IA analisa os dados, identifica a "Loja Campeã" e escreve o texto.
5.  **WhatsApp:** Envio da mensagem formatada via API.

---

## 🚀 Como Executar

### Pré-requisitos
* Docker e Docker Compose instalados.
* Conta na Anthropic (API Key).
* Instância da Evolution API configurada (ou rodando no compose).

### 1. Clone o Repositório
```bash
git clone [https://github.com/seu-usuario/seu-projeto-bi-whatsapp.git](https://github.com/seu-usuario/seu-projeto-bi-whatsapp.git)
cd seu-projeto-bi-whatsapp
````

### 2\. Configuração de Variáveis (.env)

Crie um arquivo `.env` na raiz baseado no exemplo abaixo:

```ini
# Credenciais n8n
N8N_USER=admin
N8N_PASS=sua_senha_segura

# Integrações
ANTHROPIC_API_KEY=sk-ant-xxx
EVO_API_KEY=sua_key_evolution
EVO_INSTANCE_URL=http://evolution-api:8080

# Banco de Dados (Evolution API)
POSTGRES_USER=evolution
POSTGRES_PASSWORD=evolution
POSTGRES_DB=evolution
```

### 3\. Subir os Containers

```bash
docker-compose up -d
```

### 4\. Importar o Workflow

Acesse o n8n em `http://localhost:5678`, crie um novo workflow e importe o arquivo `flowDBtoWhatsApp.json` disponível neste repositório.

-----

## 🧠 Engenharia de Prompt

O "cérebro" do projeto utiliza o seguinte prompt para garantir formatação legível no mobile:

> "Atue como um Assistente Executivo de Business Intelligence. (...)
> Formatação WhatsApp: Use emojis (📊, 🏆) e asteriscos para negrito.
> Estrutura: Saudação, Destaque do Dia, Faturamento Total e Insight Rápido."

-----

## 🔮 Roadmap e Limitações

Este projeto é um MVP funcional. As próximas evoluções mapeadas incluem:

  * **BI Conversacional (Text-to-SQL):** Permitir que o usuário pergunte "Quanto a loja X vendeu?" e o bot responda sob demanda.
  * **Arquitetura Multi-Agentes:** Implementação de agentes validadores para mitigar riscos de segurança (SQL Injection) e alucinação da IA.
  * **Visualização:** Geração de gráficos com Python (Matplotlib) enviados como imagem no chat.

-----

## 📞 Contato

**Alberdan Gomes Bezerra de Menezes**

  * [LinkedIn]
  Link: https://www.linkedin.com/in/alberdangomes/
  * [Portfólio]
  Link: https://berdanthewise.notion.site/Portf-lio-1e4087e630c8809d89eadfd5dcc09a5c
