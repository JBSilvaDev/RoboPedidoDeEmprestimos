# Robo de Pedido de Empréstimos

Este é um projeto de automação desenvolvido com UiPath que utiliza o Robotic Enterprise Framework (REFramework) para processar pedidos de empréstimo a partir de uma planilha do Excel.

## Como Funciona

O robô segue a estrutura padrão do REFramework, que é dividida em quatro estados principais:

1.  **Inicialização (Initialization):**
    *   Lê as configurações do arquivo `Data/Config.xlsx`, que inclui informações como a URL do site UiBank, credenciais de login e configurações de e-mail.
    *   Mata todos os processos desnecessários para garantir uma execução limpa.
    *   Abre as aplicações necessárias, neste caso, o site UiBank.

2.  **Obter Dados da Transação (Get Transaction Data):**
    *   Lê os dados da planilha `Data/Input/Loan Quotes.xlsx`.
    *   Para cada linha na planilha, o robô extrai as informações do pedido de empréstimo e as armazena em um item de transação (DataRow).

3.  **Processar Transação (Process Transaction):**
    *   Para cada item de transação, o robô executa as seguintes etapas:
        *   Verifica se o e-mail no pedido de empréstimo é válido.
        *   Se o e-mail for válido, o robô navega até o site do UiBank, faz o login e preenche o formulário de pedido de empréstimo com os dados da transação.
        *   Após submeter o pedido, o robô obtém o resultado da solicitação e atualiza a planilha com o status.
        *   Se o e-mail for inválido, o robô marca a transação como uma exceção de negócio (Business Rule Exception).

4.  **Finalizar Processo (End Process):**
    *   Fecha todas as aplicações abertas durante o processo.
    *   Envia um e-mail com o status final da execução.

## Dados de Entrada

O robô utiliza a planilha `Data/Input/Loan Quotes.xlsx` como entrada. A planilha deve conter as seguintes colunas:

*   `LoanEmail`: O endereço de e-mail do solicitante.
*   `LoanAmount`: O valor do empréstimo solicitado.
*   `LoanTerm`: O prazo do empréstimo em meses.
*   `LoanIncome`: A renda anual do solicitante.
*   `LoanAge`: A idade do solicitante.
*   `LoanName`: O nome do solicitante.

## Pré-requisitos

*   UiPath Studio
*   Acesso à internet para acessar o site UiBank.
*   As credenciais de login e a URL do site UiBank devem ser configuradas no arquivo `Data/Config.xlsx`.

## Como Executar

1.  Abra o projeto no UiPath Studio.
2.  Certifique-se de que o arquivo `Data/Input/Loan Quotes.xlsx` esteja preenchido com os dados dos pedidos de empréstimo.
3.  Configure o arquivo `Data/Config.xlsx` com as informações do ambiente (URL do UiBank, credenciais, etc.).
4.  Execute o arquivo `Main.xaml` a partir do UiPath Studio.