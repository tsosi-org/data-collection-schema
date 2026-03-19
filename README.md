
# Schema used by TSOSI to collect data

TSOSI is a recent data platform launched in June 2025; see [tsosi.org](https://tsosi.org). It promotes transparency regarding financial support made for open science infrastructure. It's a tool for research institutions and infrastructures to implement open data related to financial support. 

**Institutions** and **infrastructure** are welcome to share their financial data. Please use provided templates to structure your data.


- [Download template for institution](https://github.com/tsosi-org/data-collection-schema/raw/refs/heads/main/2026--TSOSI-data-schema-institution-template.xlsx)

- [Download template for infrastructure](https://github.com/tsosi-org/data-collection-schema/raw/refs/heads/main/2026--TSOSI-data-schema-infra-template.xlsx)
<br />
<br />


TSOSI invites institutions and infrastructures to share their data using a standardized spreadsheet. Each row of the spreadsheet will describe one transfer, while the columns will delineate the specific details of this transfer.

The information and table below provides a detailed explanation of the columns and the expected data formats. For any questions or concerns, please feel free to contact us: https://tsosi.org/pages/faq#join-tsosi

## Schema outline

```
TSOSI transfer/payment
    |
    |--- institution
    |       |
    |       |--- name [1.1]             [Required for infrastructure]
    |       |
    |       |--- ror_id [1.2]
    |       |
    |       |--- wikidata_id [1.3]
    |
    |--- intermediary
    |       |
    |       |--- name [2.1]
    |       |
    |       |--- ror_id [2.2]
    |       |
    |       |--- wikidata_id [2.3]
    |
    |--- infrastructure
    |       |
    |       |--- name [3.1]             [Required for institutions]
    |       |
    |       |--- ror_id [3.2]
    |       |
    |       |--- wikidata_id [3.3]
    |
    |--- amount [4]                     [Required]
    |
    |--- date_invoice [5]               [Required*]
    |
    |--- date_sent [6]                  [Required*]
    |
    |--- date_received [7]              [Required*]
    |
    |--- contract [8]                   [Required*]
    |       |
    |       |--- date_start [8.1]
    |       |
    |       |--- date_end [8.2]
```

## Data schema


| **Number** | **Field name**             | **Required** | **Description**                                                                                                                                  | **Example**               |
| ---------- | -------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------- |
| 1.1        | institution/name           | Required for infrastructures    | The full name of the supporting entity (university, company, library, ...).                                                                      | Université Grenoble Alpes |
| 1.2        | institution/ror_id         |              | The full ROR ID of the entity. The ROR ID is strongly preferred over the other fields wikidata_id, country and website.                          | 02rx3b187                 |
| 1.3        | institution/wikidata_id    |              | The wikidata ID of the entity, e.g. Q1227538. Not relevant when a ROR ID is entered.                                                             | Q945876                   |
| 2.1        | intermediary/name          |              | The full name of the intermediray entity, if any. This should be filled when a transfer is done through another entity like a library consortia. | Couperin                  |
| 2.2        | intermediary/ror_id        |              | The full ROR ID of the entity. The ROR ID is strongly preferred over the other fields wikidata_id, country and website.                          | 035c9qf67                 |
| 2.3        | intermediary/wikidata_id   |              | The wikidata ID of the entity, e.g. Q12546. Not relevant when a ROR ID is entered.                                                               | Q2994760                  |
| 3.1        | infrastructure/name        | Required for institutions    | The full name of the supported entity.                                                                                                           | DOAJ                      |
| 3.2        | infrastructure/ror_id      |              | The full ROR ID of the entity. The ROR ID is strongly preferred over the other fields wikidata_id, country and website.                          | 05amyt365                 |
| 3.3        | infrastructure/wikidata_id |              | The wikidata ID of the entity, e.g. Q1227538. Not relevant when a ROR ID is entered.                                                             | Q1227538                  |
| 4          | amount                     | Required     | The amount of the transfer/payment. This is the amount paid by the supporting entity. It should include all taxes.                               | 1250                      |
| 5          | date_invoice               | Required\*   | The invoice date for the transfer.                                                                                                               | 2023-05-02                |
| 6          | date_sent                  | Required\*   | The transfer issue date by the supporting institution.                                                                                           | 2023-05-31                |
| 7          | date_received              | Required\*   | The date of receipt of the transfer.                                                                                                             | 2023-07-01                |
| 8.1        | contract/date_start        | Required\*   | The start date of the contract. It is usually the start date of the support agreement.                                                           | 2023-01-01                |
| 8.2        | contract/date_end          | Required\*   | The end date of the contract. It is usually the end date of the support agreement.                                                               | 2025-12-31                |

### Footnotes

`Required*`</span>: At least one date field must be entered.


Date values can be entered with one of the following formats according to the accuracy:
- Year only: `2024`
- Year and month: `2024-03`
- Year, month and day: `2024-03-13`


## Interoperability

This data schema for institutions is interoperable with that of OpenCost (see https://github.com/opencost-de/opencost/tree/main)
