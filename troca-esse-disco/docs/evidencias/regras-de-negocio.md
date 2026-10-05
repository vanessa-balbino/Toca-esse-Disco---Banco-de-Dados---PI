# Regras de Negócio

Regras extraídas do enunciado do projeto. Cada regra possui um código (`RN`) para ser referenciada no MER, no DER, no dicionário de dados e nas consultas.

## 1. Catálogo

| Código | Regra |
|--------|-------|
| RN01 | Um **CD** representa um **título** do catálogo, e não uma unidade física. |
| RN02 | Cada **música** pertence a **um** CD. |
| RN03 | Cada música possui **um intérprete principal** (um cantor). |
| RN04 | A música é identificada pelo conjunto **(`id_cd`, `numero_musica`)**, ou seja, o número da faixa é único dentro do CD. |

## 2. Estoque físico

| Código | Regra |
|--------|-------|
| RN05 | Um CD pode possuir **vários exemplares** físicos. |
| RN06 | Cada **exemplar** pertence a **um** CD. |
| RN07 | Cada exemplar possui uma **conservação**, que só pode ser: `REGULAR`, `BOM`, `OTIMO` ou `NOVO`. |
| RN08 | Cada exemplar possui um **status**, que só pode ser: `DISPONIVEL` ou `TROCADO`. |

## 3. Clientes

| Código | Regra |
|--------|-------|
| RN09 | O **e-mail** do cliente deve ser **único**. |

## 4. Trocas

| Código | Regra |
|--------|-------|
| RN10 | Cada **troca** relaciona **um cliente**, **um exemplar entregue** e **um exemplar adquirido**. |
| RN11 | Os exemplares entregue e adquirido de uma mesma troca devem ser **distintos**. |
| RN12 | O **desconto** depende exclusivamente da **conservação do exemplar entregue**. |
| RN13 | O **valor final** é calculado sobre o **preço-base do exemplar adquirido**. |

### Tabela de descontos (RN12)

| Conservação do exemplar entregue | Desconto |
|----------------------------------|----------|
| `REGULAR` | 5%  |
| `BOM`     | 10% |
| `OTIMO`   | 15% |
| `NOVO`    | 20% |

### Fórmula (RN13)

```
valor_final = preco_base_do_exemplar_adquirido × (1 − percentual_de_desconto)
```

**Exemplo:** entregando um exemplar `BOM` (10%) para adquirir um CD com preço-base de R$ 50,00:
`50,00 × (1 − 0,10) = R$ 45,00`.

## 5. Regras de integridade

| Código | Regra | Como será garantida |
|--------|-------|---------------------|
| RN14 | Todas as relações entre tabelas são implementadas por **chaves estrangeiras**. | `FOREIGN KEY` no DDL |
| RN15 | Conservação e status aceitam apenas valores válidos. | `ENUM` (ou `CHECK`) no DDL |
| RN16 | Exemplares de uma troca são distintos. | `CHECK (id_exemplar_entregue <> id_exemplar_adquirido)` |
| RN17 | E-mail de cliente não se repete. | `UNIQUE` no DDL |
| RN18 | Nomes de tabelas e colunas obrigatórias não podem ser alterados. | Compatibilidade com os scripts de carga |

## 6. Decisões de modelagem derivadas das regras

- **Desconto não é armazenado.** Ele é derivado da conservação do exemplar entregue (RN12); gravá-lo na `troca` criaria redundância e risco de inconsistência. Será calculado nas consultas.
- **Valor final também é calculado**, a partir do preço-base do CD do exemplar adquirido (RN13).
- **Separação CD x Exemplar** (RN01, RN05, RN06): evita repetir título, artista e preço em cada cópia física.

## 7. Pontos a confirmar com o material do professor

Estes itens não constam no enunciado e dependem dos scripts de carga:

- Nomes exatos das colunas além das obrigatórias (ex.: preço-base, data da troca, ano do CD).
- Se o cantor do CD (artista do título) é o mesmo conceito do intérprete principal da música.
- Se o `status` do exemplar `TROCADO` é consistente com sua presença em alguma troca.
