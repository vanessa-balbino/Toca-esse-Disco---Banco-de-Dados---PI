# Briefing do Projeto

## Ô, Meu! Troca Esse Disco

> **"Na Sé, até disco parado vira desconto."**

## 1. Contexto

A **Ô, Meu! Troca Esse Disco** é um sebo fictício de CDs usados, localizado na região da Praça da Sé, em São Paulo. A loja trabalha com um catálogo de títulos, mantém um estoque de cópias físicas (exemplares) e permite que clientes **troquem** um CD usado por outro, recebendo um desconto de acordo com o estado de conservação do disco entregue.

## 2. Objetivo

Modelar e implementar, do zero, um banco de dados relacional em **MySQL** capaz de representar:

- o **catálogo** (cantores, CDs e músicas);
- o **estoque físico** (exemplares, com conservação e status);
- as **trocas** realizadas pelos clientes.

O projeto aplica conceitos de modelagem de dados (MER e DER), **DDL**, **DML** e **DQL**, com versionamento e documentação no **GitHub**.

## 3. Escopo

### Inclui

- Análise de requisitos e regras de negócio;
- Elaboração do MER e do DER, com justificativa das escolhas;
- Dicionário de dados;
- Criação das seis tabelas obrigatórias: `cantor`, `cd`, `musica`, `cliente`, `exemplar` e `troca`;
- Implementação da estrutura via DDL;
- Carga da massa de dados fornecida pelo professor;
- Desenvolvimento das 20 consultas SQL obrigatórias;
- Validação de integridade e dos resultados, com registro de evidências;
- Organização e versionamento no GitHub, com commits incrementais e Board de acompanhamento.

### Não inclui

- Interface gráfica ou aplicação para o usuário final;
- Controle financeiro além do valor calculado da troca;
- Qualquer entidade além das seis tabelas obrigatórias.

## 4. Massa de dados

| Tabela     | Registros |
|------------|-----------|
| `cantor`   | 64        |
| `cd`       | 520       |
| `musica`   | 3.640     |
| `cliente`  | 48        |
| `exemplar` | 680       |
| `troca`    | 40        |

Os scripts de carga devem ser executados na ordem indicada no material didático, **após** a criação e validação da estrutura.

## 5. Restrições do projeto

- Os nomes das tabelas e colunas obrigatórias devem ser mantidos, para compatibilidade com os scripts de carga fornecidos.
- A tabela `musica` possui chave primária composta `(id_cd, numero_musica)`.
- As relações são implementadas por chaves estrangeiras.
- O e-mail do cliente é único.
- O banco deve ser **reproduzível a partir de um banco vazio**: criar estrutura, carregar dados e executar as consultas.

## 6. Entregáveis

| Entregável                  | Local                                   |
|-----------------------------|-----------------------------------------|
| Briefing                    | `docs/briefing.md`                      |
| Regras de negócio           | `docs/regras-de-negocio.md`             |
| MER                         | `docs/mer.md`                           |
| DER                         | `docs/der.md`                           |
| Dicionário de dados         | `docs/dicionario-de-dados.md`           |
| Evidências                  | `docs/evidencias/`                      |
| DDL                         | `database/ddl/01_criar_estrutura.sql`   |
| DML (scripts de carga)      | `database/dml/`                         |
| 20 consultas                | `database/dql/consultas.sql`            |
| Apresentação do projeto     | `README.md`                             |

A entrega no Blackboard consiste **somente no link do repositório GitHub**.

## 7. Etapas de desenvolvimento

1. Estrutura do repositório e Board
2. Briefing e regras de negócio
3. MER e DER
4. Dicionário de dados
5. DDL e validação da estrutura
6. Carga dos dados (DML) e conferência das contagens
7. Consultas (DQL)
8. Evidências
9. README e entrega
