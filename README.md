# 🤖 Monitor Inteligente de Menções e Análise de Sentimento (n8n + OpenAI + JavaScript)

Este repositório contém a documentação, a arquitetura e o código fonte de uma automação corporativa ponta a ponta construída no **n8n**. O sistema automatiza o recebimento de feedbacks de clientes, realiza a triagem por Inteligência Artificial e aplica regras de negócio customizadas em código antes de registrar os dados de forma estruturada.

---

## 🎯 O que este projeto faz?
Em cenários de atendimento ao cliente e operações (RevOps/Customer Success), empresas recebem milhares de menções diárias. Analisar isso manualmente gera lentidão e risco de perder crises. Esta automação resolve o problema realizando o seguinte ciclo em segundos:
1. **Captura em Tempo Real (Webhook):** Recebe o payload HTTP (POST) contendo o comentário ou menção do cliente.
2. **Análise de Inteligência Artificial (OpenAI):** Processa o texto bruto, agindo como um analista de atendimento para classificar o sentimento do cliente, gerar um resumo analítico conciso e definir a urgência.
3. **Regras de Negócio e Tratamento de Dados (JavaScript Code Node):** Executa um script em JavaScript que realiza o *parse* seguro da resposta da IA, lida com exceções via `try/catch`, insere um carimbo de data/hora (`timestamp ISO`) e aplica uma matriz de criticidade automatizada.
4. **Persistência de Dados (Google Sheets):** Envia os dados limpos e categorizados diretamente para uma planilha centralizada para auditoria e ação imediata das equipes.

---

## 🛠️ Tecnologias e Conceitos Utilizados
* **n8n (Cloud/Self-hosted):** Orquestração avançada de fluxos e nós no-code/low-code.
* **OpenAI API (LLM):** Processamento de linguagem natural (NLP) estruturado em formato JSON puro.
* **JavaScript (Node Code):** Tratamento de payloads, manipulação de strings, filtragem de formatações markdown e aplicação de regras condicionais.
* **Google Sheets API:** Armazenamento relacional e estruturado de dados operacionais.

---

## 🔍 O que foi resolvido e corrigido durante o desenvolvimento?
Durante a construção e validação deste pipeline em ambiente real, alguns desafios técnicos foram superados:
* **Limpeza de Payload da IA:** Modelos de linguagem costumam retornar respostas encapsuladas em blocos de markdown (ex: ```json ... ```). Foi implementado um tratamento por expressão regular (Regex) no script JavaScript para sanitizar o texto antes da conversão para JSON, evitando falhas de execução.
* **Resiliência e Tratamento de Exceções:** Implementação de blocos `try/catch` no nó de código para que, caso a IA retorne um formato inesperado, o fluxo não quebre e registre um status de erro detalhado.
* **Matriz de Alerta Condicional:** Desenvolvimento de lógica booleana personalizada no código para cruzar dados (sentimento negativo + alta urgência) e gerar automaticamente o nível de alerta `"CRÍTICO - Requer ação imediata"`.

---

## 📂 Estrutura do Repositório
* `workflow.json`: O arquivo de exportação integral do fluxo pronto para importação no n8n.
* `custom-code.js`: O script JavaScript isolado e documentado que roda no nó de código.

---
*Desenvolvido com foco em automação avançada de processos e engenharia de dados.*
