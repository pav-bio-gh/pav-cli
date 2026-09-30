# Pav Enterprise API CLI Reference

Full command reference for `pav`.

## Commands

- [`pav accelerated-approvals`](#pav-accelerated-approvals)
- [`pav advisory-committee-meetings`](#pav-advisory-committee-meetings)
- [`pav companies`](#pav-companies)
- [`pav complete-response-letters`](#pav-complete-response-letters)
- [`pav deals`](#pav-deals)
- [`pav drug-applications`](#pav-drug-applications)
- [`pav drugs`](#pav-drugs)
- [`pav orange-book-exclusivities`](#pav-orange-book-exclusivities)
- [`pav orange-book-patents`](#pav-orange-book-patents)
- [`pav orange-book-products`](#pav-orange-book-products)
- [`pav orphan-designations`](#pav-orphan-designations)
- [`pav patents`](#pav-patents)
- [`pav programs`](#pav-programs)
- [`pav purple-book-products`](#pav-purple-book-products)
- [`pav recalls`](#pav-recalls)
- [`pav stats`](#pav-stats)
- [`pav trials`](#pav-trials)
- [`pav warning-letters`](#pav-warning-letters)

---

### `pav accelerated-approvals`

#### `pav accelerated-approvals get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/accelerated-approvals/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav accelerated-approvals list`

One per product and indication. `status` is `ongoing`, `verified` or `withdrawn`; `event_date` is the projected confirmatory completion. `from`/`to` filter on the approval date.

`GET /v1/accelerated-approvals`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav advisory-committee-meetings`

#### `pav advisory-committee-meetings get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/advisory-committee-meetings/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav advisory-committee-meetings list`

Past and scheduled meetings with links to FDA's materials. `status` is `held` or `scheduled`. `from`/`to` filter on the meeting day.

`GET /v1/advisory-committee-meetings`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav companies`

#### `pav companies get`

One company with its tickers, owner and website.

`GET /v1/companies/{company_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `integer` | Yes | Company id. |

#### `pav companies list`

Biopharma companies Pav tracks. `company` and `ticker` are exact, not full-text: a `company` value matching more than one tracked company is a 400 naming the candidates. `country` is a company attribute; only ~22% of tracked companies with an active program have one on file.

`GET /v1/companies`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--ticker` | `string` | No | Current stock ticker, comma-separated. |
| `--company-type` | `string` | No | `public` or `private`. |
| `--country` | `string` | No | Headquarters country, exact name (`United States`), case-insensitive. |
| `--has-pipeline` | `string` | No | Only companies with (or without) a tracked pipeline. |
| `--sort` | `string` | No | One of `asset_count`, `name`; prefix `-` to descend. Default `-asset_count`. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav complete-response-letters`

#### `pav complete-response-letters get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/complete-response-letters/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav complete-response-letters list`

Published complete response letters, one per letter. `status` is `Approved` if the application was later approved, else `Unapproved`. `from`/`to` filter on the letter date.

`GET /v1/complete-response-letters`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav deals`

#### `pav deals get`

One deal with its full terms, lifecycle events and source documents.

`GET /v1/deals/{deal_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--deal-id` | `string (uuid)` | Yes | Deal id. |

#### `pav deals list`

M&A, licensing, collaborations, options, joint ventures and distribution deals, one row per deal. `from`/`to` filter on `announced_at`.

`GET /v1/deals`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--drug-id` | `string` | No | Drug ids, comma-separated. |
| `--deal-type` | `string` | No | Deal types, comma-separated: `acquisition`, `merger`, `asset_purchase`, `licensing`, `collaboration`, `option`, `joint_venture`, `distribution`, `other`. |
| `--status` | `string` | No | Current lifecycle state (`latest_event_type`), comma-separated: `proposed`, `announced`, `completed`, `amended`, `terminated`, `update`. |
| `--target` | `string` | No | Target name, gene symbol or term id; comma-separated. |
| `--modality` | `string` | No | Modality, subclass or format; comma-separated. |
| `--therapeutic-area` | `string` | No | Areas, comma-separated: `cardiovascular`, `dermatology`, `endocrine_metabolic`, `gastroenterology`, `hematology`, `hepatology`, `immunology`, `infectious_disease`, `musculoskeletal`, `nephrology`, `neurology`, `oncology`, `ophthalmology`, `otolaryngology`, `pain`, `psychiatry`, `reproductive_womens_health`, `respiratory`, `urology_mens_health`. |
| `--min-value-usd` | `string` | No | Minimum `total_potential_value` in USD. |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | One of `activity_date`, `announced_at`, `completed_at`, `total_value`, `total_potential_value`; prefix `-` to descend. Default `-activity_date`. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav drug-applications`

#### `pav drug-applications get`

One application with every FDA record on it and its submissions, newest first. `records_total` and `submissions_total` count everything on it.

`GET /v1/drug-applications/{application_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--application-key` | `string` | Yes | `N:` (NDA), `A:` (ANDA) or `BLA:` plus the application number. |

#### `pav drug-applications list`

NDAs, ANDAs and BLAs, one per application. `document_date` is the first approval and `event_date` the latest FDA action. `from`/`to` filter on `document_date`.

`GET /v1/drug-applications`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav drugs`

#### `pav drugs get`

One drug with its names, holders and programs. `status` picks which programs count (default `active`). A merged id returns the surviving drug.

`GET /v1/drugs/{drug_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--drug-id` | `integer` | Yes | Drug id. |
| `--status` | `string` | No | `active` (default), `inactive`, `discontinued`; comma-separated. |

#### `pav drugs list`

One drug across every company that develops it. `drug` is a complete name, code or brand (`TEV-574`, `Leqvio`), exact; case and punctuation are ignored.

`GET /v1/drugs`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--drug` | `string` | No | Drug name, INN, code or brand, exact. |
| `--drug-id` | `string` | No | Drug ids, comma-separated. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--multi-company` | `boolean` | No | Only drugs held by more than one company. |
| `--status` | `string` | No | `active` (default), `inactive`, `discontinued`; comma-separated. |
| `--sort` | `string` | No | One of `highest_phase`, `name`, `program_count`; prefix `-` to descend. Default `-highest_phase`. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav orange-book-exclusivities`

#### `pav orange-book-exclusivities get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/orange-book-exclusivities/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav orange-book-exclusivities list`

Marketing exclusivities on Orange Book products. `from`/`to` filter on the expiry (`event_date`).

`GET /v1/orange-book-exclusivities`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--product-key` | `string` | No | Application + product, e.g. `N:209637:001`. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav orange-book-patents`

#### `pav orange-book-patents get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/orange-book-patents/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav orange-book-patents list`

Patents listed against Orange Book products. `from`/`to` filter on the expiry (`event_date`).

`GET /v1/orange-book-patents`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--product-key` | `string` | No | Application + product, e.g. `N:209637:001`. |
| `--patent-number` | `string` | No | Listed patent number. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav orange-book-products`

#### `pav orange-book-products get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/orange-book-products/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav orange-book-products list`

Approved drug products in FDA's Orange Book (current edition). `from`/`to` filter on the approval date.

`GET /v1/orange-book-products`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--product-key` | `string` | No | Application + product, e.g. `N:209637:001`. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav orphan-designations`

#### `pav orphan-designations get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/orphan-designations/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav orphan-designations list`

Orphan drug designations, one per designation; approvals under it are in `details.approvals`. `from`/`to` filter on the designation date.

`GET /v1/orphan-designations`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--designation-id` | `string` | No | Orphan designation id. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav patents`

#### `pav patents get`

One family with members, ownership changes, prosecution events, FDA-listed drugs and statutory term (from the earliest nonprovisional filing, no extensions). `family_id` may also be a member's patent, publication or application number.

`GET /v1/patents/{family_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--family-id` | `string` | Yes | Pav patent family id, or a member patent/publication/application number. |

#### `pav patents list`

US patent families. `from`/`to` filter on `earliest_priority_date`. `view=full` adds up to 30 members.

`GET /v1/patents`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--patent-number` | `string` | No | A member's patent, publication or application number. |
| `--cpc` | `string` | No | CPC prefix on any member (`A61K38/26`). |
| `--status` | `string` | No | `live` (a member pending or in force) or `lapsed`. |
| `--granted` | `string` | No | Whether at least one member is granted. |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | One of `latest_status_date`, `earliest_priority_date`, `member_count`; prefix `-` to descend. Default `-latest_status_date`. |
| `--view` | `View` | No | `full` (default) or `slim` for light rows. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav programs`

#### `pav programs get`

One program with its trials and ontology terms. A merged id returns the surviving program.

`GET /v1/programs/{program_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--program-id` | `integer` | Yes | Program id. |

#### `pav programs list`

Drug programs: one drug in one indication at one company. `from`/`to` filter on `last_updated`. Only `active` programs unless `status` says otherwise. `company_type` and `country` are company attributes, not program attributes: `company_type` is maintained directly (reliable); only ~22% of tracked companies with an active program have a `country` on file, so a `country` filter under-counts.

`GET /v1/programs`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--company-type` | `string` | No | `public` or `private`. |
| `--country` | `string` | No | Headquarters country, exact name (`United States`), case-insensitive. |
| `--drug-id` | `string` | No | Drug ids, comma-separated. |
| `--drug` | `string` | No | Drug name, INN, code or brand, exact; comma-separated. |
| `--program-id` | `string` | No | Program ids, comma-separated. |
| `--phase` | `string` | No | Normalized phase, comma-separated: `preclinical`, `phase_1`, `phase_1_2`, `phase_2`, `phase_2_3`, `phase_3`, `filed`, `registration`, `approved` (also accepts `1`, `2`, `3`, or `Phase 2`). Unknown values 400 with this list. |
| `--status` | `string` | No | `active` (default), `inactive`, `discontinued`; comma-separated. |
| `--indication` | `string` | No | Disease name, synonym or MONDO id; includes narrower diseases. Comma-separated; for a name containing a comma, use its id. |
| `--target` | `string` | No | Target name, gene symbol or term id (`TL1A`, `TNFSF15`); comma-separated. |
| `--modality` | `string` | No | Normalized modality, subclass (`sirna`) or format (`bispecific`); comma-separated. Unknown values 400 with the allowed list. |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | One of `company`, `drug`, `indication`, `target`, `modality`, `phase`, `last_updated`; prefix `-` to descend. Default `company`. |
| `--view` | `View` | No | `full` (default) or `slim` for light rows. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav purple-book-products`

#### `pav purple-book-products get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/purple-book-products/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav purple-book-products list`

Licensed biologics in FDA's Purple Book. `from`/`to` filter on the license date.

`GET /v1/purple-book-products`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--product-key` | `string` | No | Application + product, e.g. `N:209637:001`. |
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav recalls`

#### `pav recalls get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/recalls/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav recalls list`

Drug, biologic and device recalls: `title` is the product, `description` the reason. `from`/`to` filter on the recall date.

`GET /v1/recalls`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav stats`

#### `pav stats get`

Counts of active programs and companies, by phase and by modality.

`GET /v1/stats`

---

### `pav trials`

#### `pav trials get`

One ClinicalTrials.gov trial with its linked programs and companies.

`GET /v1/trials/{nct_id}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--nct-id` | `string` | Yes | ClinicalTrials.gov NCT identifier. |

#### `pav trials list`

ClinicalTrials.gov trials with their links to Pav programs and companies. `company`/`company_id` match sponsors, collaborators and linked programs. `from`/`to` filter on `start_date`.

`GET /v1/trials`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--nct-id` | `string` | No | NCT ids, comma-separated. |
| `--phase` | `string` | No | Phases, comma-separated (`1`-`4`). |
| `--status` | `string` | No | Recruitment statuses, comma-separated. |
| `--study-type` | `string` | No | Study types, comma-separated. |
| `--indication` | `string` | No | Condition name, synonym, MeSH or MONDO id; includes narrower conditions. Comma-separated; for a name containing a comma, use its id. |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | One of `start_date`, `last_update_post_date`, `enrollment_count`, `nct_id`; prefix `-` to descend. Default `nct_id`. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

### `pav warning-letters`

#### `pav warning-letters get`

One record by `record_key`. Keys are built from FDA identifiers and survive new FDA editions.

`GET /v1/warning-letters/{record_key}`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--record-key` | `string` | Yes | `record_key` from a list response. May contain `/`, `:` and spaces. |

#### `pav warning-letters list`

Warning letters from FDA's drug, biologic and device offices. `from`/`to` filter on the letter date.

`GET /v1/warning-letters`

| Flag | Type | Required | Description |
|------|------|----------|-------------|
| `--company-id` | `string` | No | Company ids, comma-separated. Includes the companies each one owns. |
| `--company` | `string` | No | Ticker, company slug, or exact registered name/synonym; comma-separated. Includes the companies each one owns. Ambiguous text (matches more than one tracked company) is a 400 naming the candidates. |
| `--application-key` | `string` | No | FDA application, e.g. `N:209637` or `BLA:761508`. |
| `--status` | `string` | No | Statuses, comma-separated (case-insensitive). |
| `--from` | `string` | No | On or after this date. |
| `--to` | `string` | No | On or before this date. |
| `--sort` | `string` | No | `document_date` or `event_date`; prefix `-` to descend. |
| `--limit` | `integer` | No | Rows per page (1-200). |
| `--cursor` | `string` | No | `next_cursor` from the previous page. |

---

## Global flags

These flags are available on every command:

| Flag | Description |
|------|-------------|
| `--dry-run` | Print the HTTP request without sending it |
| `--json <JSON\|->` | Supply the request body as JSON (or `-` for stdin) |
| `--params <JSON>` | Merge extra parameters as JSON |
| `--format <json\|table\|yaml\|csv>` | Output format (default: `json`) |
| `--output <PATH>` | Write binary responses to a file |
| `--base-url <URL>` | Override the API base URL |
| `--no-extract` | Print the full response body instead of the `x-fern-sdk-return-value` extraction |
| `--no-retry` | Disable retries declared by `x-fern-retries`, including network errors |
| `-q, --quiet` | Suppress stdout on success |
| `-h, --help` | Print help |
| `-V, --version` | Print version |

Operations the spec describes how to page (via `x-fern-pagination` or a root `page_token` parameter) also accept:

| Flag | Description |
|------|-------------|
| `--page-all` | Auto-paginate and stream all results |
| `--page-limit <N>` | Max pages to fetch (default: `10`) |
| `--page-delay <MS>` | Delay between page fetches in milliseconds (default: `100`) |
| `--no-pager` | Disable the pager even on interactive terminals |

Operations the spec marks as streaming (via `x-fern-streaming`) also accept:

| Flag | Description |
|------|-------------|
| `--no-stream` | Buffer the streaming response and print it as a single value once complete |
