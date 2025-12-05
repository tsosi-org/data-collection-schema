
# Schema used by TSOSI to collect data

TSOSI is a recent data platform launched in June 2025; see [tsosi.org](https://tsosi.org). It promotes transparency regarding financial support made for open science infrastructure. It's a tool for research institutions and infrastructures to implement open data related to financial support. At launch, the data source consists solely of infrastructure, and we are working on designing a process that will also allow institutions to provide data. See: 

- [Data schema for infrastructure](#data-schema-for-infrastructure)

- [Data schema for institution](#data-schema-for-institution)


<br />
<br />
<br />
<br />

## Data schema for infrastructure

**Infrastructure** are welcome to share their financial data. Please use the following file to structure the data: [`2025--TSOSI-data-schema-infra-template.xlsx`](./2025--TSOSI-data-schema-infra-template.xlsx).

### Schema definition

The following table describes all the fields of the template spreadsheet. Each individual payment should be entered as a separate row. TSOSI highly rely on the ROR registry. We use it to de-duplicate the data and to enrich with additionnal information like country, website and wikidata identifier. As far as possible, please fill the **ROR ID** column, and you will not have to fill the country, website and wikidata columns. 

- `Data type = Date` values can be entered with one of the following formats according to the accuracy:
    * year format - `2024`
    * year-month format - `2024-03` for March 2024
    * day format - `2024-03-13` for March 13th 2024.



| Number | Field name                | Data type | Required | Description                                                                                                                                                               | Example                   |
|--------|---------------------------|-----------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| 1.1    | `institution/name`        | String    | **Yes**  | The full name of the supporting entity (university, company, library, ...).                                                                                               | Université Grenoble Alpes |
| 1.2    | `institution/ror_id`      | String    | No       | The ROR ID of the entity. The ROR ID is strongly preferred over the other fields `wikidata_id`, `country` and `website`.                                             | 02rx3b187 |
| 1.3    | `institution/wikidata_id` | String    | No       | The wikidata ID of the entity, e.g. Q12546. Not relevant when a ROR ID is entered.                                                                                        | Q945876                   |
| 1.4    | `institution/country`     | String    | No       | The country [ISO 3166-1 alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) (preferred) or English name of the entity. Not relevant when a ROR ID is entered. | FR                        |
| 1.5    | `institution/website`      | String    | No       | The website URL of the entity. Not relevant when a ROR ID is entered.                                                                                                      | https://www.univ-grenoble-alpes.fr |                     |
| 2.1    | `intermediary/name`        | String    | No       | The full name of the intermediray entity, if any. This should be filled when a transfer is done through another entity like a library consortia.                                                                                                                                   | COUPERIN                           |
| 2.2    | `intermediary/ror_id`      | String    | No       | The ROR ID of the entity. The ROR ID is strongly preferred over the other fields `wikidata_id`, `country` and `website`.                                                                               | 035c9qf67          |
| 2.3    | `intermediary/wikidata_id` | String    | No       | The wikidata ID of the entity, e.g. Q12546. Not relevant when a ROR ID is entered.                                                                                         | Q2994760                           |
| 2.4    | `intermediary/country`     | String    | No       | The country [ISO 3166-1 alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) (preferred) or English name of the entity. Not relevant when a ROR ID is entered.  | FR                                 |
| 2.5    | `intermediary/website`     | String    | No       | The website URL of the entity. Not relevant when a ROR ID is entered.                                                                                                      | https://www.couperin.org/          |
| 3      | `amount`        |  Number    | **Yes**            | The amount of the transfer/payment. This can be the amount received by the infrastructure or the amount paid by the supporting institution. It should include all taxes.                                                                                                             | 1250                               |
| 4      | `currency`      |  String    | **Yes**            | The currency [ISO 4217 code](https://en.wikipedia.org/wiki/ISO_4217) of the the transfered money.                                                                                                                                                      | EUR                                |
| 5      | `date_invoice`  |  Date      | [Yes*]( #required-yes-single-star) | The invoice date for the transfer.                                                                                                                                                                                                                     | 2023-05-02                         |
| 6      | `date_emitted`  |  Date      | [Yes*]( #required-yes-single-star) | The transfer issue date by the supporting institution. The 2 dates `date_emitted` and `date_received` can differ greatly when the money passes through an intermediary.                                                                                | 2023-05-31                         |
| 7      | `date_received` |  Date      | [Yes*]( #required-yes-single-star) | The date of receipt of the transfer.                                                                                                                                                                                                                   | 2023-07-01                         |                                    |
| 8.1    | `contract/id`              | String    | [No**](#required-no-double-star)             | Any string uniquely identifying the contract/subsidy/support agreement the transfer is a part of. This is useful when several transfers are made within the same contract to link them, e.g. 3 transfers respectively made in 2022, 2023 and 2024 within a 3-year supporting agreement.                                                                                                                                                                                                | L2167                                   |
| 8.2    | `contract/description`     | String    | No             | A description of the contract.                                                                                                                                                                                                                         | 3-year support agreement           |
| 8.3    | `contract/date_start`      | Date      | [Yes*]( #required-yes-single-star) | The start date of the contract. It usually to the start date of the support agreement.                                                                                                                                                                 | 2023-01-01                         |
| 8.4    | `contract/date_end`        | Date      | [Yes*]( #required-yes-single-star) | The end date of the contract. It usually to the start date of the support agreement.                                                                                                                                                                   | 2025-12-31                         |
| 9      | `scoss` |  Boolean      | No | Whether the transfer is related to [SCOSS funding cycles](https://scoss.org/how-it-works/funding-cycles/). No data equals `FALSE`.                                                                                                                                                                                                                    | TRUE                         |                                    |



- <span id="required-yes-single-star">`Required = Yes*`</span> - At least 1 of the date fields with this value must be entered. The `date_emitted` or `date_received` fields are preferred.

- <span id="required-no-double-star">`Required = No**`</span> - This is not required but it is strongly recommended to fill it when possible.


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
    |--- date_invoice [5]                       [optionnal]
    |
    |--- date_emitted [6]                       [optionnal]
    |
    |--- date_received [7]                      [optionnal]
    |
    |--- contract [8]                           [optionnal]
    |       |
    |       |--- id [8.1]
    |       |
    |       |--- description [8.2]
    |       |
    |       |--- date_start [8.3]
    |       |
    |       |--- date_end [8.4]
    |
    |--- scoss [9]                             [optionnal]
```


<br />
<br />
<br />
<br />

## Data schema for institution

TSOSI is working with OpenCost to design a data schema that is accurate for institutions. See the OpenCost data schema: https://github.com/opencost-de/opencost/tree/main