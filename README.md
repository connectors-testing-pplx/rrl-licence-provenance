# ACMA RRL per-licensee row artifacts

This repository publishes per-licensee row artifacts extracted from the **official ACMA Register of
Radiocommunications Licences (RRL) current data download**, with full source provenance, for
organisational-licence provenance research.

## Provenance

- **Official ACMA source URL:** https://web.acma.gov.au/rrl-updates/spectra_rrl.zip
  (HTTP 301 → https://cdn.acma.gov.au/rrl/spectra_rrl.zip)
- **ACMA download page:** https://www.acma.gov.au/radiocomms-licence-data — "The download contains a
  complete data set current for that day." (RRL data is regenerated every few hours.)
- **Data vintage / archive date:** retrieved 19 August 2026 (UTC); HTTP `Last-Modified` of the zip:
  `Wed, 19 Aug 2026 20:47:27 GMT`; archive date 2026-08-19.
- **ZIP SHA-256:** `0697874595e8f70f034b2a20db0e71b955b19efb09e6aeecf4d4bc3581c07230`
- **Files used:** `client.csv` (licensee records, incl. `CLIENT_TYPE_ID` and `ABN`), `licence.csv`
  (licence records), plus reference tables `client_type.csv`, `licence_service.csv`,
  `licence_status.csv` — all inside `spectra_rrl.zip`.

## Client classification

`client_type.csv` (verbatim, from the zip):

```
TYPE_ID,NAME
1,Commonwealth Department
2,Other Commonwealth Agency
3,State Government
4,Local Government
5,Company
6,Community or Volunteer Group
7,Person
```

Only organisational licensees are included here (`CLIENT_TYPE_ID` 1–6). `CLIENT_TYPE_ID=7` ("Person",
natural-person licensees) is out of scope and excluded.

## Service buckets

Artifacts are grouped by RRL service (`licence_service.csv`):

| Bucket directory | SV_ID | SV_NAME |
|---|---|---|
| `fixed_public_network` | 2 | Fixed |
| `spectrum_public_network` | 85 | Spectrum |
| `broadcasting` | 1 | Broadcasting |
| `aeronautical_services` | 8 | Aeronautical |
| `maritime_coast` | 5 | Maritime Coast |
| `public_safety_land_mobile` | 3 | Land Mobile |

## Artifact format

Each file `artifacts/<service_bucket>/<ABN>.json` is a plain-text/JSON row artifact naming:

- the official ACMA source URL, data vintage / archive date, and zip checksum;
- the `client.csv` locator (`CLIENT_NO`) and `licence.csv` locator (`LICENCE_NO`);
- the `CLIENT_TYPE_ID` organisational (non-natural-person) client classification;
- the organisation name and ABN;
- the licence number, licence type/category, and licence status;
- the verbatim `client.csv` and `licence.csv` rows as extracted (only postal/contact address
  columns of `client.csv` are redacted, as contact details are out of scope);
- the service bucket the licence belongs to.

All licence rows shown have `STATUS=1 (Granted)` in the snapshot.
