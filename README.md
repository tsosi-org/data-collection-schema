
# Schema used by TSOSI for data collection

## Infrastructure data

**Infrastructure organizations** are welcome to share their financial data. Please use the following file to structure the data: [`2025--TSOSI-data-schema-infra-template.xlsx`](./2025--TSOSI-data-schema-infra-template.xlsx).

### Schema definition

The following table describes all the fields of the template spreadsheet.
Each individual payment should be entered as a separate row.

Note before reading the specifications:

- We strongly encourage you to fill the **ROR ID** of the involved institution (and intermediary) when it’s available, rather than the institution’s wikidata ID, country and website.
    
    We use the ROR ID to de-duplicate the data and to enrich it with additional information from the ROR records (including wikidata ID, country and website).

- <span id="required-yes-single-star">`Required = Yes*`</span> - At least 1 of the date fields with this value must be entered. The `date_emitted` or `date_received` fields are preferred.

- <span id="required-no-double-star">`Required = No**`</span> - This is not required but it is strongly recommended to fill it when possible.

- `Data type = Date` values can be entered with one of the following formats according to the accuracy:
    * year format - `2024`
    * year-month format - `2024-03` for March 2024
    * day format - `2024-03-13` for March 13th 2024.



| Number | Field name                | Data type | Required | Description                                                                                                                                                               | Example                   |
|--------|---------------------------|-----------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| 1.1    | `institution/name`        | String    | **Yes**  | The full name of the supporting entity (university, company, library, ...).                                                                                               | Université Grenoble Alpes |
| 1.2    | `institution/ror_id`      | String    | No       | The full ROR ID of the entity. The ROR ID is strongly preferred over the other fields `wikidata_id`, `country` and `website`.                                             | https://ror.org/02rx3b187 |
| 1.3    | `institution/wikidata_id` | String    | No       | The wikidata ID of the entity, e.g. Q12546. Not relevant when a ROR ID is entered.                                                                                        | Q945876                   |
| 1.4    | `institution/country`     | String    | No       | The country [ISO 3166-1 alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) (preferred) or English name of the entity. Not relevant when a ROR ID is entered. | FR                        |
| 1.5    | `institution/website`      | String    | No       | The website URL of the entity. Not relevant when a ROR ID is entered.                                                                                                      | https://www.univ-grenoble-alpes.fr |                     |
| 2.1    | `intermediary/name`        | String    | No       | The full name of the intermediray entity, if any. This should be filled when a transfer is done through another entity like a library consortia.                                                                                                                                   | COUPERIN                           |
| 2.2    | `intermediary/ror_id`      | String    | No       | The full ROR ID of the entity. The ROR ID is strongly preferred over the other fields `wikidata_id`, `country` and `website`.                                                                               | https://ror.org/035c9qf67          |
| 2.3    | `intermediary/wikidata_id` | String    | No       | The wikidata ID of the entity, e.g. Q12546. Not relevant when a ROR ID is entered.                                                                                         | Q2994760                           |
| 2.4    | `intermediary/country`     | String    | No       | The country [ISO 3166-1 alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) (preferred) or English name of the entity. Not relevant when a ROR ID is entered.  | FR                                 |
| 2.5    | `intermediary/website`     | String    | No       | The website URL of the entity. Not relevant when a ROR ID is entered.                                                                                                      | https://www.couperin.org/          |
| 3      | `amount`        |  Number    | **Yes**            | The amount of the transfer/payment. This can be the amount received by the infrastructure or the amount paid by the supporting institution.                                                                                                            | 1250                               |
| 4      | `currency`      |  String    | **Yes**            | The currency [ISO 4217 code](https://en.wikipedia.org/wiki/ISO_4217) of the the transfered money.                                                                                                                                                      | EUR                                |
| 5      | `hide_amount`   |  Boolean   | No             | Whether the transfer amount should not be disclosed. No data equals `False`.                                                                                                                                                                           | FALSE                              |
| 6      | `date_invoice`  |  Date      | [Yes*]( #required-yes-single-star) | The invoice date for the transfer.                                                                                                                                                                                                                     | 2023-05-02                         |
| 7      | `date_emitted`  |  Date      | [Yes*]( #required-yes-single-star) | The transfer issue date by the supporting institution. The 2 dates `date_emitted` and `date_received` can differ greatly when the money passes through an intermediary.                                                                                | 2023-05-31                         |
| 8      | `date_received` |  Date      | [Yes*]( #required-yes-single-star) | The date of receipt of the transfer.                                                                                                                                                                                                                   | 2023-07-01                         |                                    |
| 9.1    | `contract/id`              | String    | [No**](#required-no-double-star)             | Any string uniquely identifying the contract/subsidy/support agreement the transfer is a part of. This is useful when several transfers are made within the same contract to link them, e.g. 3 transfers respectively made in 2022, 2023 and 2024 within a 3-year supporting agreement.                                                                                                                                                                                                | L2167                                   |
| 9.2    | `contract/description`     | String    | No             | A description of the contract.                                                                                                                                                                                                                         | 3-year support agreement           |
| 9.3    | `contract/date_start`      | Date      | [Yes*]( #required-yes-single-star) | The start date of the contract. It usually to the start date of the support agreement.                                                                                                                                                                 | 2023-01-01                         |
| 9.4    | `contract/date_end`        | Date      | [Yes*]( #required-yes-single-star) | The end date of the contract. It usually to the start date of the support agreement.                                                                                                                                                                   | 2025-12-31                         |

### Schema outline

```
TSOSI transfer/payment
    |
    |--- institution (entity) [1]
    |       |
    |       |--- name [1.1]
    |       |
    |       |--- ror_id [1.2]                   [optionnal]
    |       |
    |       |--- wikidata_id [1.3]              [optionnal]
    |       |
    |       |--- country [1.4]                  [optionnal]
    |       |
    |       |--- website [1.5]                  [optionnal]
    |
    |--- intermediary (entity) [2]              [optionnal]
    |       |
    |       |--- name [2.1]  
    |       |
    |       |--- ror_id [2.2]
    |       |
    |       |--- wikidata_id [2.3]
    |       |
    |       |--- country [2.4]
    |       |
    |       |--- website [2.5]
    |
    |--- amount [3]
    |
    |--- currency [4]
    |
    |--- hide_amount [5]                        [optionnal]
    |
    |--- date_invoice [6]                       [optionnal]
    |
    |--- date_emitted [7]                       [optionnal]
    |
    |--- date_received [8]                      [optionnal]
    |
    |--- contract [9]                           [optionnal]
    |       |
    |       |--- id [9.1]
    |       |
    |       |--- description [9.2]
    |       |
    |       |--- date_start [9.3]
    |       |
    |       |--- date_end [9.4]
    |
```


## Institution data

For institutions, TSOSI plans to use the data schema of OpenCost to collect data: https://github.com/opencost-de/opencost/tree/main

<br />

> The more we highlight those who have funded, the more funders we will attract
