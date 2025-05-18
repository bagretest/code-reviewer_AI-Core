# Code Reviewer AI-Core: Sistema Inteligente de Revisão de Código com Agentes Gemini

Code Reviewer AI é uma ferramenta poderosa que utiliza a API Gemini do Google e uma arquitetura de múltiplos agentes especializados para realizar uma análise abrangente de código. Ele oferece feedback detalhado sobre diversos aspectos cruciais do desenvolvimento de software, ajudando desenvolvedores a melhorar a qualidade, segurança e eficiência de seus projetos.

## Visão Geral

Este projeto emprega seis agentes de IA, cada um focado em uma área específica da revisão de código:

1.  **`ErrorDetector`**: Identifica erros de sintaxe, problemas de tempo de execução comuns e falhas lógicas óbvias.
2.  **`PerfOptimizer`**: Analisa o código em busca de gargalos de performance, sugerindo otimizações em algoritmos, estruturas de dados e loops.
3.  **`CodeStylist`**: Avalia a aderência a guias de estilo (ex: PEP 8), a clareza da nomenclatura, a qualidade da documentação e a modularização do código.
4.  **`AccessibilityAuditor`**: (Para código front-end) Verifica a conformidade com as diretrizes de acessibilidade web (WCAG), como alternativas textuais, semântica HTML e navegabilidade por teclado.
5.  **`SecurityScanner`**: Realiza uma varredura básica por vulnerabilidades de segurança, incluindo XSS, SQL Injection, credenciais expostas e outras "red flags".
6.  **`CodeReviewerAI-Core` (Orquestrador)**: Gerencia o fluxo de análise, envia o código para os agentes especializados, consolida seus relatórios e apresenta um feedback final estruturado, incluindo pontuações por categoria.

## Funcionalidades Principais

*   **Análise Multifacetada**: Cobre erros, performance, estilo, acessibilidade e segurança.
*   **Arquitetura Baseada em Agentes**: Design modular com responsabilidades claras para cada agente.
*   **Tecnologia Gemini**: Utiliza os modelos avançados de linguagem da Google para análise e geração de feedback.
*   **Prompts Detalhados**: Cada agente é guiado por instruções específicas para garantir análises focadas e relevantes.
*   **Relatório Consolidado**: O agente orquestrador fornece um sumário e pontuações para facilitar a compreensão das áreas de melhoria.
*   **Feedback Construtivo**: As sugestões visam ser acionáveis e educativas.

## Tecnologias Utilizadas

*   **Python 3.x**
*   **Google Generative AI SDK (`google-generativeai`)**: Para interagir com a API Gemini.
*   **Google Agents Development Kit (`google.adk`)**: Para construir e gerenciar os agentes de IA. (Nota: Certifique-se de que esta SDK esteja acessível ou inclua instruções de instalação).
*   **Python Dotenv (`python-dotenv`)**: Para gerenciamento de chaves de API.
*   **IPython (`ipython`)**: Para exibição formatada em ambientes como Jupyter Notebooks ou Google Colab.

## Configuração e Pré-requisitos

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
    cd SEU_REPOSITORIO
    ```

2.  **Crie e Ative um Ambiente Virtual (Recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3.  **Instale as Dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure a API Key do Gemini:**
    *   Crie um arquivo chamado `.env` na raiz do projeto.
    *   Adicione sua chave da API Gemini ao arquivo:
        ```env
        GEMINI_API_KEY="SUA_CHAVE_API_AQUI"
        PROJECT_ID="SEU_PROJECT_ID_AQUI" #CASO USE O VERTEX AI -->
        ```

5.  **Configure o Projeto Vertex AI (se aplicável):**
    O cliente Gemini está configurado para usar Vertex AI:
    ```python
    client = genai.Client(
        vertexai=True, project=os.getenv("PROJECT_ID"), location='us-central1'
    )
    ```
    ou
    ```python
    client = genai.Client(
        vertexai=True, project='your-project-id', location='us-central1'
    )
    ```
    
    Certifique-se de:
    *   Substituir `'your-project-id'` pelo ID do seu projeto Google Cloud, ou adicionar no arquivo '.env'.
    *   Ter as permissões necessárias e a API Vertex AI habilitada no seu projeto GCP.
    *   Estar autenticado com o Google Cloud SDK (`gcloud auth application-default login`).
  
    Nota: Você também pode adicionar o seu "project ID" no arquivo .env; o arquivo já está configurado para isso!

## Como Usar

1.  Execute o script principal:
    ```bash
    python nome_do_seu_script_principal.py
    ```

2.  Quando solicitado, cole o trecho de código que você deseja analisar:
    ```
    Por favor, envie o código sobre o qual você deseja um feedback.
    ```

3.  O sistema processará o código através dos agentes e exibirá um relatório detalhado no console, formatado em Markdown.

## Exemplo de Código para Análise (Python)

```python
# Exemplo de código para testar
def calculate_sum_inefficient(n):
    total = 0
    for i in range(n): # Pode ser otimizado
        for j in range(i):
            total += 1
    print("Total:" + str(total)) # Evitar concatenação em logs, usar f-strings
    return total

# Outro exemplo
SECRET_KEY = "supersecretpassword123" # Credencial hardcoded!

def greet(nome):
    print('Ola ' + nome) # Problema de estilo e sem validação
```

Estrutura do Projeto (Simplificada)
```
.
├── seu_script_principal.py  # Contém a lógica dos agentes e o fluxo principal
├── .env                     # Arquivo para variáveis de ambiente (NÃO COMMITAR)
├── requirements.txt         # Lista de dependências Python
└── README.md                # Este arquivo
```

## Contribuições
Contribuições são bem-vindas! Se você tiver sugestões, melhorias ou correções de bugs, sinta-se à vontade para:
    * Fazer um Fork do projeto.
    * Criar uma nova Branch (git checkout -b feature/nova-feature).
    * Fazer commit de suas alterações (git commit -am 'Adiciona nova feature').
    * Fazer Push para a Branch (git push origin feature/nova-feature).
    * Abrir um Pull Request.
    
## Limitações Conhecidas
* A análise de segurança é básica e foca em "red flags" comuns. Não substitui uma auditoria de segurança completa por especialistas ou ferramentas dedicadas.
* A eficácia da análise depende da qualidade dos prompts dos agentes e das capacidades do modelo Gemini subjacente.
* O sistema não executa o código, realizando uma análise estática.
* Pode haver falsos positivos ou falsos negativos, especialmente em cenários complexos ou com dependências externas não visíveis no trecho de código fornecido.
* A análise de acessibilidade é focada em código front-end (HTML, CSS, JavaScript).

## Planos Futuros
* Integração com repositórios Git para análise de Pull Requests.
* Suporte para mais linguagens de programação.
* Interface web para facilitar o uso.
* Opção para configurar guias de estilo específicos.
* Relatórios mais interativos ou em formatos exportáveis (HTML, PDF).
Caso aplique algum deles, entre em contato comigo! Adoraria ver as possíveis adições e melhorias no código.

## Licença
Este projeto é distribuído sob a licença MIT LICENSE. Veja o arquivo LICENSE para mais detalhes.
