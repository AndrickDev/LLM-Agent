# Projeto LLM de Busca e Geração de Respostas

Este projeto demonstra a integração de Large Language Models (LLMs) com APIs de busca (DuckDuckGo e SerpApi) para gerar respostas dinâmicas e contextuais. O objetivo é simular diferentes comportamentos de resposta de um LLM (neste caso, a API Groq) com base em informações pesquisadas em tempo real.

## Sumário

  * [Visão Geral](https://www.google.com/search?q=%23vis%C3%A3o-geral)
  * [Pré-requisitos](https://www.google.com/search?q=%23pr%C3%A9-requisitos)
  * [Configuração](https://www.google.com/search?q=%23configura%C3%A7%C3%A3o)
  * [Estrutura do Código](https://www.google.com/search?q=%23estrutura-do-c%C3%B3digo)
  * [Como Executar](https://www.google.com/search?q=%23como-executar)
  * [Personalização](https://www.google.com/search?q=%23personaliza%C3%A7%C3%A3o)

## Visão Geral

O script `ExercicioLLM.ipynb` é um notebook Python que:

1.  **Instala as dependências** necessárias para interagir com as APIs.
2.  **Configura as chaves de API** para DuckDuckGo, SerpApi e Groq.
3.  Define funções para **realizar buscas** no DuckDuckGo e no Google (via SerpApi).
4.  Define uma função para **gerar respostas** usando a API Groq, incorporando os resultados das buscas.
5.  Executa uma série de **testes predefinidos**, demonstrando diferentes "comportamentos" do LLM (ex: especialista em nutrição acessível vs. acadêmico, especialista em marketing influenciador vs. formal) para os mesmos temas, utilizando as informações obtidas nas buscas.

## Pré-requisitos

Para utilizar este projeto, você precisará de:

  * **Python 3.x**
  * **Google Colab** ou **Jupyter Notebook** para executar o arquivo `.ipynb`.
  * **Chaves de API** para:
      * **Groq API:** Para utilizar os modelos de linguagem.
      * **SerpApi:** Para realizar buscas no Google.

## Configuração

Siga os passos abaixo para configurar o ambiente e suas chaves de API:

1.  **Clone este repositório** (ou faça o download do `ExercicioLLM.ipynb`).

2.  **Abra o `ExercicioLLM.ipynb`** no Google Colab ou Jupyter Notebook.

3.  **Instale as dependências:**
    Execute a primeira célula do notebook:

    ```python
    !pip install -q duckduckgo-search
    !pip install -q serpapi
    !pip install -q groq
    ```

4.  **Obtenha suas chaves de API:**

      * **GROQ API Key:**

        1.  Acesse [https://groq.com/](https://groq.com/).
        2.  Crie uma conta ou faça login.
        3.  Navegue até a seção de chaves de API e gere uma nova chave.
        4.  Substitua o placeholder na segunda célula do notebook pela sua chave de API Groq.

      * **SERPAPI API Key:**

        1.  Acesse [https://serpapi.com/](https://serpapi.com/).
        2.  Crie uma conta ou faça login.
        3.  Navegue até a seção de chaves de API e copie sua chave.
        4.  Substitua o placeholder na segunda célula do notebook pela sua chave de API SerpApi.

    Após obter suas chaves, a segunda célula do notebook deverá se parecer com o seguinte (com suas chaves reais):

    ```python
    import os
    os.environ["GROQ_API_KEY"] = "SUA_CHAVE_GROQ_AQUI"
    os.environ["SERPAPI_API_KEY"] = "SUA_CHAVE_SERPAPI_AQUI"
    ```

    **Lembre-se de manter suas chaves de API seguras e nunca as exponha em repositórios públicos.**

## Estrutura do Código

O notebook está organizado nas seguintes seções:

  * **Instalação de Pacotes:** Instala as bibliotecas Python necessárias.
  * **Configuração de Variáveis de Ambiente:** Define as chaves das APIs.
  * **Funções de Busca:**
      * `buscar_no_ddg(consulta, max_resultados=3)`: Realiza buscas textuais no DuckDuckGo.
      * `buscar_com_serpapi(consulta, num_resultados=3)`: Realiza buscas no Google via SerpApi.
  * **Função de Geração de Resposta (Groq):**
      * `gerar_resposta_com_groq(comportamento, tema, dados_ddg, dados_google, modelo="llama3-70b-8192", temperatura=0.7)`: Envia as informações coletadas e o comportamento desejado para a API Groq para gerar uma resposta.
  * **Função de Processamento de Testes:**
      * `processar_testes(testes)`: Orquestra o fluxo, iterando sobre uma lista de cenários de teste, realizando as buscas e gerando as respostas.
  * **Definição e Execução dos Testes:** A parte principal onde os cenários de teste são definidos e processados, e os resultados são exibidos.

## Como Executar

1.  **Siga as etapas de Configuração** para instalar as bibliotecas e configurar suas chaves de API.
2.  **Execute todas as células** do notebook sequencialmente.
      * No Google Colab, você pode usar "Ambiente de execução" -\> "Executar tudo".
      * No Jupyter Notebook, vá em "Cell" -\> "Run All".
3.  O notebook irá:
      * Imprimir o progresso das buscas e da geração de respostas para cada teste.
      * Ao final, exibir um resumo com o `ID` de cada teste e a `RESPOSTA` gerada pelo modelo Groq.

## Personalização

Você pode facilmente personalizar o comportamento e os temas dos testes:

  * **Modificar os Testes:** Edite a lista `testes` na última célula do notebook para adicionar, remover ou modificar cenários.

    ```python
    testes = [
        {
            "id": "1",
            "comportamento": "Aja como um especialista em nutrição que responde de maneira simples e acessível",
            "tema": "Como alimentos podem interferir na glicose"
        },
        {
            "id": "5",
            "comportamento": "Seja um professor de história divertido e conte sobre a Revolução Francesa.",
            "tema": "Revolução Francesa"
        }
    ]
    ```

  * **Ajustar Parâmetros da Groq:** Na função `gerar_resposta_com_groq`, você pode alterar:

      * `modelo`: Experimente diferentes modelos disponíveis na Groq (verifique a documentação da Groq para opções). O padrão é `llama3-70b-8192`.
      * `temperatura`: Um valor entre 0 e 1 que controla a aleatoriedade da saída. Valores mais baixos (ex: 0.2) tornam a resposta mais determinística; valores mais altos (ex: 0.9) a tornam mais criativa.

  * **Número de Resultados de Busca:**

      * Na função `buscar_no_ddg`, o parâmetro `max_resultados` controla quantos resultados do DuckDuckGo serão considerados.
      * Na função `buscar_com_serpapi`, o parâmetro `num_resultados` controla quantos resultados orgânicos do Google serão considerados.
