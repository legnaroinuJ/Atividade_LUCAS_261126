# Banco de Dados — Plataforma de Hospedagem

Repositório contendo os scripts de definição de estrutura (DDL) do banco de dados **MySQL** da aplicação `plataforma_hospedagem`.

## Especificações Técnicas

* **SGBD:** MySQL 8.0 (`8.0.45`)
* **Engine:** InnoDB

## Estrutura de Arquivos

Esses são os scripts enviados, que foram trabalhados em aulas

| Arquivo | Tabela | Descrição |
| :--- | :--- | :--- |
| `plataforma_hospedagem_proprietario.sql` | `proprietario` | Cadastro de proprietários dos imóveis (`proprietario_id`, `nome`, `cpf_cnpj`, `contato`). |
| `plataforma_hospedagem_enderecos.sql` | `enderecos` | Cadastro de localização dos imóveis (`endereco_id`, `rua`, `numero`, `bairro`, `cidade`, `estado`, `cep`). |
| `plataforma_hospedagem_hospedagens.sql` | `hospedagens` | Cadastro de imóveis disponíveis para hospedagem (`hospedagem_id`, `tipo`, `endereco_id`, `proprietario_id`, `ativo`). |
| `plataforma_hospedagem_cliente.sql` | `cliente` | Cadastro de clientes da plataforma (`cliente_id`, `nome`, `cpf`, `contato`). |

## Relacionamentos (Chaves Estrangeiras)

* **`hospedagens.endereco_id`** referencia **`enderecos.endereco_id`** (`hospedagens_ibfk_1`)
* **`hospedagens.proprietario_id`** referencia **`proprietario.proprietario_id`** (`hospedagens_ibfk_2`)

## Como Restaurar o Banco

Como a tabela `hospedagens` possui chaves estrangeiras apontando para `enderecos` e `proprietario`, execute os scripts respeitando a ordem:

### Via Terminal (MySQL CLI)

```bash
# 1. Crie o banco de dados
mysql -u seu_usuario -p -e "CREATE DATABASE IF NOT EXISTS plataforma_hospedagem CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;"

# 2. Importe primeiro as tabelas independentes
mysql -u seu_usuario -p plataforma_hospedagem < plataforma_hospedagem_proprietario.sql
mysql -u seu_usuario -p plataforma_hospedagem < plataforma_hospedagem_enderecos.sql
mysql -u seu_usuario -p plataforma_hospedagem < plataforma_hospedagem_cliente.sql

# 3. Importe a tabela com chaves estrangeiras
mysql -u seu_usuario -p plataforma_hospedagem < plataforma_hospedagem_hospedagens.sql
```

### Via MySQL Workbench

1. Conecte-se ao seu servidor MySQL e crie o schema `plataforma_hospedagem`.
2. Acesse **Server > Data Import**.
3. Selecione **Import from Self-Contained File** e execute os arquivos seguindo a mesma ordem: `proprietario`, `enderecos`, `cliente` e, por último, `hospedagens`.
