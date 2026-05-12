# Projeto Integrado: RAG Seguro com Proteção contra Prompt Injection

Repositório destinado à entrega do CP2 das disciplinas de Generative AI Advanced Net e Governança em IA & Business Analytics (Turma: 2TIAPF-2026 - FIAP).

## Objetivo do Projeto
Este projeto implementa um pipeline de Retrieval-Augmented Generation (RAG) do zero utilizando Python. O objetivo principal é demonstrar a vulnerabilidade de sistemas LLM integrados a bases vetoriais corporativas contra ataques de *Prompt Injection* e, na sequência, implementar e validar uma camada de segurança e governança para mitigação de exfiltração de dados sensíveis.

## Arquitetura e Tecnologias
* **Linguagem:** Python 3.10+
* **Ambiente:** Jupyter Notebook (Otimizado para Google Colab)
* **Framework LLM:** LangChain e LangChain Groq
* **Modelo de Linguagem (LLM):** `llama-3.3-70b-versatile` via API da Groq
* **Modelo de Embeddings:** `sentence-transformers/all-MiniLM-L6-v2` (Hugging Face local)
* **Banco de Dados Vetorial:** FAISS (`faiss-cpu`)
* **Análise de Dados:** Pandas

## Estrutura do Notebook (`Checkpoint_2_Genai.ipynb`)
O desenvolvimento está centralizado em um único arquivo de notebook, dividido nas seguintes etapas lógicas:
1.  **Configuração do Ambiente:** Instalação de dependências e importação de pacotes.
2.  **Parametrização:** Definição dos modelos, *chunking strategy* (size 600, overlap 60) e chaves de API.
3.  **Processamento Vetorial:** Criação de um mock de documento confidencial (contendo PII, credenciais e dados financeiros), tokenização via `RecursiveCharacterTextSplitter` e indexação no FAISS.
4.  **Cenário Vulnerável:** Implementação de um fluxo de RAG padrão sem salvaguardas de *input/output*.
5.  **Camada de Proteção:** Implementação de funções de validação de *input* via expressões regulares (Regex) para detecção de *bypass*, além de isolamento de contexto através de *System Prompts* estritos.
6.  **Bateria de Testes Empíricos:** Execução automatizada de 5 vetores de ataque distintos (Instrução Direta, Exfiltração, Engenharia Social, Jailbreak e Ofuscação) contra ambas as arquiteturas (vulnerável e segura).
7.  **Análise de Governança:** Tabela comparativa de resultados e discussão técnica baseada nos frameworks OWASP LLM Top 10, LGPD e NIST AI RMF.

## Instruções de Execução

Para reproduzir os resultados e testar a aplicação, siga as etapas abaixo:

1. Clone o repositório ou faça o download do arquivo `Checkpoint_2_Genai.ipynb`.
2. Recomenda-se a execução no **Google Colab** devido à integração nativa com o gerenciador de segredos (`userdata`). Faça o upload do notebook na plataforma.
3. Obtenha uma chave de API gratuita no [GroqCloud Console](https://console.groq.com/).
4. No Google Colab, vá até a aba lateral "Secrets" (ícone de chave), crie um novo segredo com o nome `GROQ_API_KEY` e cole o valor da sua chave. Ative a chave para o notebook atual (toggle "Notebook access").
5. Execute as células sequencialmente (menu `Runtime` > `Run all`). 
6. *Nota:* A primeira célula instalará os pacotes necessários automaticamente (`langchain`, `faiss-cpu`, `sentence-transformers`, etc.).

## Autores (Grupo)
* Marcelo Maso (RM: 562163)
* Luiz Felipe Tragl (RM: 565009)
* Henry Browne (RM: 562089)
* Luis Filipe Chaves (RM: 564706)
* Davi Gravina (RM: 565619)
