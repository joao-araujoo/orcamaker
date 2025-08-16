# Orçamaker 🤖

![Status do Projeto](https://img.shields.io/badge/status-concluído-brightgreen)
![Plataforma](https://img.shields.io/badge/plataforma-Make.com-blueviolet)

<p align="center">
  <em>Aplicação no-code para a geração e consulta de orçamentos, utilizando Inteligência Artificial para automatizar o processo.</em>
</p>

---

## 📖 Sobre o Projeto

A **API do Orçamaker** é uma solução no-code construída inteiramente na plataforma [Make.com](https://www.make.com/) para gerenciar o ciclo de vida de orçamentos de forma automatizada. O sistema foi projetado para receber dados de um formulário, processá-los com a IA do **Google Gemini** para gerar um orçamento detalhado e, por fim, armazenar os resultados em um banco de dados em tempo real no **Google Sheets**.

O projeto expõe dois endpoints principais: um para a **geração** de novos orçamentos e outro para a **consulta** do histórico dos últimos registros, oferecendo uma solução completa e eficiente sem a necessidade de uma única linha de código de back-end tradicional.

## 🏗️ Arquitetura e Tecnologias

A arquitetura do projeto é orquestrada por fluxos de automação no Make.com, onde cada módulo desempenha um papel específico no processamento dos dados.

### **Fluxo de Geração de Orçamento**

Este fluxo é iniciado por uma requisição POST, processa os dados com IA, realiza a limpeza do texto e armazena o orçamento finalizado no Google Sheets.

<p align="center">
  <img width="1525" height="263" alt="image" src="https://github.com/user-attachments/assets/70d438b5-62fd-4283-b1df-ebb6c24d71c2" />
</p>

O fluxo segue os seguintes passos:
1.  **Webhook**: Recebe a requisição POST do front-end com os dados do cliente.
2.  **Google Gemini AI**: Envia os dados para a IA, que gera o conteúdo do orçamento (descrição, valores, prazo, etc.).
3.  **Text Parsers**: Remove caracteres indesejados e formata o texto retornado pela IA.
4.  **JSON**: Converte o texto limpo em um objeto JSON estruturado.
5.  **Google Sheets**: Persiste os dados do orçamento em uma nova linha na planilha.

### **Fluxo de Consulta de Histórico**

Este fluxo é mais simples e ativado por uma requisição GET. Ele busca os dados mais recentes diretamente do banco de dados e os retorna.

<p align="center">
  <img width="1492" height="517" alt="image" src="https://github.com/user-attachments/assets/4a2e1b7f-4bcb-4f84-af78-f9d7788b16ad" />
</p>

O fluxo segue os seguintes passos:
1.  **Webhook**: Atua como o endpoint GET para a consulta.
2.  **Google Sheets**: Busca as 5 linhas mais recentes da planilha de histórico.
3.  **Webhook Response**: Retorna os dados encontrados em formato JSON para o cliente.

### **Banco de Dados (Google Sheets)**

O Google Sheets funciona como um banco de dados em tempo real, onde cada coluna representa um campo do orçamento, garantindo organização e fácil acesso aos dados.

<p align="center">
  <img width="1819" height="527" alt="image" src="https://github.com/user-attachments/assets/c7bfb0a8-6150-45f0-b7ff-1994d09408fd" />
</p>

---

## Endpoints da API

A API possui dois endpoints públicos para interação.

### `Endpoint 1: Geração de Orçamento`

Este endpoint recebe os dados do formulário, processa-os e armazena o novo orçamento.

-   **URL:** `https://hook.us2.make.com/3r5laprv565u5immk4k1nxjjc5dmsdnp` 
-   **Método:** `POST`
-   **Descrição:** Recebe as informações do cliente para gerar um orçamento personalizado com IA.

#### **Corpo da Requisição (Request Body)**
A requisição deve ser enviada em formato `application/json`.
```json
{
  "nome_da_empresa_cliente": "string",
  "produto_ou_servico_desejado": "string",
  "quantidade_escopo": "string",
  "observacoes_adicionais": "string"
}
```

#### **Resposta de Sucesso (200 OK)**
Retorna o orçamento gerado pela IA.
```json
{
  "descricao": "string",
  "valores_estimados": "string",
  "prazo_entrega": "string",
  "observacoes": "string"
}
```

---

### `Endpoint 2: Consulta de Histórico`

Permite a consulta dos últimos 5 orçamentos gerados, ordenados do mais recente para o mais antigo.

-   **URL:** `https://hook.us2.make.com/u8dq11xkduaelphlien7laotf27ukpfq`
-   **Método:** `GET` 
-   **Descrição:** Retorna um array com os últimos orçamentos salvos no banco de dados.

#### **Resposta de Sucesso (200 OK)**
Retorna um array de objetos, onde cada objeto é um orçamento salvo.
```json
[
  {
    "ID": "string",
    "Data de Geração": "string",
    "Nome do Cliente": "string",
    "Produto / Serviço": "string",
    "Quantidade / Escopo": "string",
    "Descrição": "string",
    "Valores": "string",
    "Prazo": "string",
    "Observações": "string"
  }
]
```

## 🛠️ Como Utilizar

Você pode interagir com os endpoints usando qualquer cliente HTTP, como Insomnia, Postman ou `cURL`.

### **Exemplo: Gerar um novo orçamento (cURL)**
```bash
curl --location '[https://hook.us2.make.com/3r5laprv565u5immk4k1nxjjc5dmsdnp](https://hook.us2.make.com/3r5laprv565u5immk4k1nxjjc5dmsdnp)' \
--header 'Content-Type: application/json' \
--data '{
    "nome_da_empresa_cliente": "Empresa Exemplo",
    "produto_ou_servico_desejado": "Sistema de estoque",
    "quantidade_escopo": "11 páginas completas",
    "observacoes_adicionais": "Gostaria de um design moderno e responsivo."
}'
```

### **Exemplo: Consultar o histórico (cURL)**
```bash
curl --location '[https://hook.us2.make.com/u8dq11xkduaelphlien7laotf27ukpfq](https://hook.us2.make.com/u8dq11xkduaelphlien7laotf27ukpfq)'
```

## 👤 Autor

Projeto desenvolvido por **João Araujo**.

-   **GitHub:** [@joao-araujoo](https://github.com/joao-araujoo)
-   **LinkedIn:** [João Araujo](https://www.linkedin.com/in/joao-araujoo/)
