# CriadorBlog Crew

Este projeto é uma aplicação Python baseada em IA para extração de textos de arquivos PDF, análise de conteúdo, criação de resumos e formatação de blogs. Toda a lógica é baseada na biblioteca **CrewAI**, que organiza os agentes e tarefas de forma orquestrada. Retornando um arquivo do tipo **.md** que pode ser utilizado em um blog.

## Requisitos

### Pré-requisitos no sistema

- Python 3.12 (ou compatível com a versão usada no projeto)

- Docker (caso for rodar via container)

- SonarQube (se quiser manter a análise de qualidade de código)

- Git

### Instalação de dependências Python

- crewai
- python-dotenv
- PyPDF2
- openai

### Pastas obrigatórias

- .env
    - Com a **OPENAI_API_KEY** para utilizar a llm da openai
- pdf_path 
    - Com os pdfs que serão utilizados


## Funcionamento

### Agente 1 — agente_leitor_pdf

- Função: Extrair texto bruto dos PDFs

- Usa a ferramenta ExtratorDeTexto() implementada em extrator_de_pdf.py

- Pega todos os arquivos da pasta pdf_path, lê cada PDF usando PyPDF2, extrai o texto e devolve como string.

Resultado: texto bruto extraído dos PDFs.


### Agente 2 — agente_analista
- Função: Analisar o texto extraído e identificar informações mais relevantes

- Usa o modelo openai/gpt-4 via CrewAI

- Recebe o texto da Task 1 como contexto e gera uma análise estruturada dos pontos mais importantes.

Resultado: texto analítico contendo as partes mais relevantes do texto original.


### Agente 3 — agente_resumo
- Função: Resumir o conteúdo analisado

- Usa o modelo openai/gpt-4

- Recebe o texto da Task 2 e produz um resumo conciso, mantendo a qualidade e fidelidade ao texto original.

Resultado: resumo bem estruturado e coerente.

### Agente 4 — agente_blog
- Função: Formatar o resumo em estilo de post de blog

- Usa o modelo openai/gpt-4

- Recebe o resumo da Task 3 e converte para um texto no formato de blog:

    - Título

    - Subtítulos

    - Conclusão

    - Fluidez e coesão, sem marcas de texto gerado por IA.

Resultado: conteúdo final pronto para publicação em um blog.


## Resultado

O Resultado da crew vai estar disponivel no arquivo **blog.md**, dentro da pasta src.








