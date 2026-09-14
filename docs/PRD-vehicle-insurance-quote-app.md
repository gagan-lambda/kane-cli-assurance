# PRD — Vehicle Insurance Quote Application

**Application under test:** https://sampleapp.tricentis.com/101/index.php
**Document owner:** Gagan — Principal Solution Architect
**Version:** 0.1 (draft)
**Date:** 14 Sep 2026
**Status:** For review

---

## 1. Purpose

This PRD describes the expected behaviour of the Vehicle Insurance Quote application and defines the **minimum scenario coverage** required to certify a release. It is written to be consumable both by a human reviewer and by an AI test authoring agent (KaneAI / Kane CLI), so requirements are stated as testable assertions rather than prose.

The application is a publicly hosted demo. It is used here as a stand-in for an insurance carrier's online quote journey.

---

## 2. Product overview

A prospective customer lands on the site, picks a vehicle category, completes a five-step quote wizard, chooses a price tier and submits the quote. On submission the system generates a quote PDF and sends it to the customer by e-mail.

**Journey:**

`Select vehicle category → Enter Vehicle Data → Enter Insurant Data → Enter Product Data → Select Price Option → Send Quote → Confirmation`

**Vehicle categories:** Automobile, Truck, Motorcycle, Camper.

---

## 3. Scope

**In scope**
- The four quote journeys (one per vehicle category)
- Field-level validation on all five wizard steps
- Forward and backward navigation within the wizard
- Price tier selection and quote submission
- Quote PDF generation and the e-mail confirmation dialog
- Cross-browser, responsive, visual and accessibility behaviour of the above

**Out of scope**
- Policy binding, payment, or any post-quote servicing (not implemented in the app)
- Marketing links in the site footer and external Tricentis destinations
- Underwriting/premium calculation correctness against an actuarial model — premiums are treated as opaque values; only *consistency* is asserted
- Load and performance characterisation (tracked separately; the app is a shared public demo and is not a valid load target)

---

## 4. Functional requirements

### 4.1 Landing page

| ID | Requirement |
|---|---|
| FR-1.1 | The landing page presents four vehicle categories: Automobile, Truck, Motorcycle, Camper. |
| FR-1.2 | Selecting a category opens Step 1 (Enter Vehicle Data) with the form variant for that category. |
| FR-1.3 | The active category is visually indicated in the navigation. |
| FR-1.4 | Switching category mid-journey resets the wizard to Step 1 for the newly selected category. |

### 4.2 Step 1 — Enter Vehicle Data

| Field | Locator id | Control | Notes |
|---|---|---|---|
| Make | `make` | Select | e.g. Audi, BMW, Fiat, Honda, Jeep, Nissan, Porsche, Renault, Tesla, Volkswagen |
| Engine Performance (kW) | `engineperformance` | Numeric text | |
| Date of Manufacture | `dateofmanufacture` | Date (MM/DD/YYYY) | Must be in the past |
| Number of Seats | `numberofseats` | Select | |
| Fuel Type | `fuel` | Select | Petrol, Diesel, Other |
| List Price | `listprice` | Numeric text | |
| Licence Plate Number | `licenseplatenumber` | Text | Optional |
| Annual Mileage | `annualmileage` | Numeric text | |

Category variants: **Truck** and **Camper** additionally capture payload, total weight and right-hand-drive; **Motorcycle** omits fuel type and seat-count options that do not apply. The exact variant field set must be confirmed against the live app before scripting.

| ID | Requirement |
|---|---|
| FR-2.1 | Mandatory fields are marked and block progression when empty. |
| FR-2.2 | Numeric fields reject non-numeric input or surface a validation message. |
| FR-2.3 | `Next »` advances to Step 2 only when the step is valid. |
| FR-2.4 | Entered values persist when the user returns to this step. |

### 4.3 Step 2 — Enter Insurant Data

| Field | Locator id | Control |
|---|---|---|
| First Name | `firstname` | Text |
| Last Name | `lastname` | Text |
| Date of Birth | `birthdate` | Date (MM/DD/YYYY) |
| Gender | `gendermale` / `genderfemale` | Radio |
| Street Address | `streetaddress` | Text |
| Country | `country` | Select |
| Zip Code | `zipcode` | Text |
| City | `city` | Text |
| Occupation | `occupation` | Select |
| Hobbies | checkbox group | Multi-select (incl. Speeding, Cliff Diving, Skydiving, Bungee Jumping, Other) |
| Picture upload | file input | Optional file upload |

| ID | Requirement |
|---|---|
| FR-3.1 | Date of Birth must be a valid past date and must satisfy the minimum-age rule. |
| FR-3.2 | Gender is a single-choice control; selecting one clears the other. |
| FR-3.3 | Hobbies accept zero, one or many selections. |
| FR-3.4 | The picture upload accepts a supported image type and displays the chosen filename. |
| FR-3.5 | `« Back` returns to Step 1 with vehicle data intact. |

### 4.4 Step 3 — Enter Product Data

| Field | Control | Notes |
|---|---|---|
| Start Date | Date | Must be at least ~2 months in the future (confirm exact rule) |
| Insurance Sum | Select | e.g. up to 15,000,000.00 |
| Merit Rating | Select | Bonus/Malus scale |
| Damage Insurance | Select | No coverage / Partial coverage / Full coverage |
| Optional Products | Checkboxes | Euro Protection, Legal Defense Insurance |
| Courtesy Car | Select | Yes / No |

| ID | Requirement |
|---|---|
| FR-4.1 | A start date earlier than the minimum permitted date is rejected with a clear message. |
| FR-4.2 | Optional products are independently selectable and deselectable. |
| FR-4.3 | `Next »` advances to the price options only when the step is valid. |

### 4.5 Step 4 — Select Price Option

| ID | Requirement |
|---|---|
| FR-5.1 | Four tiers are presented: Silver, Gold, Platinum, Ultimate. |
| FR-5.2 | Each tier displays a price and its included benefits. |
| FR-5.3 | Exactly one tier can be selected at a time. |
| FR-5.4 | Prices are consistent for identical input across repeated runs on the same day. |
| FR-5.5 | Prices increase monotonically from Silver through Ultimate. |

### 4.6 Step 5 — Send Quote

| Field | Control |
|---|---|
| E-Mail | Text |
| Phone | Text |
| Username | Text |
| Password / Confirm Password | Password |
| Comments | Textarea |

| ID | Requirement |
|---|---|
| FR-6.1 | E-Mail must be in a valid format. |
| FR-6.2 | Password and Confirm Password must match; a mismatch blocks submission. |
| FR-6.3 | `« Send »` submits the quote and returns a success confirmation dialog. |
| FR-6.4 | Submission triggers generation of a quote PDF (`/101/tcpdf/pdfs/quote.php`). |
| FR-6.5 | Dismissing the confirmation returns the user to a usable state. |

---

## 5. Non-functional requirements

| ID | Requirement |
|---|---|
| NFR-1 | The full journey works on the latest two versions of Chrome, Edge, Firefox and Safari. |
| NFR-2 | The journey is usable at mobile (≤480px), tablet and desktop viewports. |
| NFR-3 | No unintended visual regression on any of the six screens against an approved baseline. |
| NFR-4 | No new critical or serious WCAG 2.1 AA violations on any wizard step. |
| NFR-5 | Each wizard step renders within 3s on a standard broadband profile. |

---

## 6. Minimum scenario coverage

The set below is the floor for a release to be considered tested. **P0 must pass for every build**; P1 is required before a release.

### 6.1 Smoke — P0

| ID | Scenario | Expected result |
|---|---|---|
| SMK-01 | Landing page loads and shows all four vehicle categories | All four tiles/tabs render; no console errors |
| SMK-02 | Automobile happy path, end to end, Silver tier | Quote submitted; success confirmation displayed |
| SMK-03 | Navigate forward through all five steps without submitting | Each step renders with its expected field set |

### 6.2 End-to-end functional — P0

| ID | Scenario | Expected result |
|---|---|---|
| E2E-01 | Automobile — full journey, Platinum tier, both optional products selected | Success confirmation; PDF generated |
| E2E-02 | Truck — full journey, Gold tier | Success confirmation; truck-specific fields accepted |
| E2E-03 | Motorcycle — full journey, Silver tier | Success confirmation |
| E2E-04 | Camper — full journey, Ultimate tier | Success confirmation |
| E2E-05 | Journey with picture upload on Step 2 | Filename displayed; journey completes |
| E2E-06 | Journey with no optional products and no courtesy car | Success confirmation; lower premium than E2E-01 for same inputs |

### 6.3 Navigation and state — P0

| ID | Scenario | Expected result |
|---|---|---|
| NAV-01 | Back from Step 2 to Step 1 | Vehicle data retained |
| NAV-02 | Back from Step 4 to Step 3, change Damage Insurance, forward again | Price options recalculated |
| NAV-03 | Switch vehicle category mid-journey | Wizard resets to Step 1 for the new category |
| NAV-04 | Browser refresh on Step 3 | Documented behaviour (reset vs. retain) is consistent |

### 6.4 Validation and negative — P0/P1

| ID | Scenario | Priority | Expected result |
|---|---|---|---|
| VAL-01 | Submit Step 1 with all fields empty | P0 | Progression blocked; mandatory fields flagged |
| VAL-02 | Alphabetic input in Engine Performance | P1 | Rejected or flagged invalid |
| VAL-03 | Date of Manufacture set in the future | P1 | Rejected with message |
| VAL-04 | Date of Birth set in the future | P0 | Rejected with message |
| VAL-05 | Date of Birth below minimum insurable age | P1 | Rejected with message |
| VAL-06 | Start Date inside the minimum notice window | P0 | Rejected with message |
| VAL-07 | Malformed e-mail on Step 5 | P0 | Submission blocked |
| VAL-08 | Password and Confirm Password mismatch | P0 | Submission blocked |
| VAL-09 | Boundary values on List Price and Annual Mileage (0, max, max+1) | P1 | Handled per rule; no unhandled error |
| VAL-10 | Special characters and 255-char strings in name/address fields | P1 | Accepted or rejected cleanly; no page break |

### 6.5 Price logic — P1

| ID | Scenario | Expected result |
|---|---|---|
| PRC-01 | Same inputs run twice in a session | Identical prices on both runs |
| PRC-02 | Tier ordering check | Silver < Gold < Platinum < Ultimate |
| PRC-03 | Raise Insurance Sum, hold all else constant | Premium does not decrease |
| PRC-04 | Toggle Euro Protection on | Premium does not decrease |

### 6.6 Output verification — P1

| ID | Scenario | Expected result |
|---|---|---|
| OUT-01 | Quote PDF retrieved after submission | PDF opens and is not zero-byte |
| OUT-02 | PDF contents vs. entered data | Insurant name, vehicle make and selected tier match the journey inputs |
| OUT-03 | Confirmation dialog dismissal | App returns to a usable state |

### 6.7 Cross-browser and responsive — P1

| ID | Scenario | Expected result |
|---|---|---|
| XB-01 | E2E-01 on Chrome, Edge, Firefox, Safari (latest two versions) | Passes on all |
| XB-02 | E2E-01 on Android Chrome and iOS Safari, real devices | Passes on both |
| XB-03 | Wizard at 375px, 768px and 1440px viewports | No overlap, clipping or unreachable controls |

### 6.8 Visual and accessibility — P1

| ID | Scenario | Expected result |
|---|---|---|
| VIS-01 | Visual baseline on all six screens, two viewports | No unapproved diffs |
| VIS-02 | Visual check of validation-error states | Error styling renders consistently |
| A11Y-01 | Automated WCAG 2.1 AA scan on each wizard step | No new critical or serious violations |
| A11Y-02 | Keyboard-only traversal of the full journey | Every control reachable; focus order logical; visible focus indicator |
| A11Y-03 | Form labels and error messages announced | Each input has a programmatic label; errors are associated with their field |

---

## 7. Coverage summary

| Area | Scenarios | P0 |
|---|---|---|
| Smoke | 3 | 3 |
| End-to-end functional | 6 | 6 |
| Navigation and state | 4 | 4 |
| Validation and negative | 10 | 6 |
| Price logic | 4 | 0 |
| Output verification | 3 | 0 |
| Cross-browser and responsive | 3 | 0 |
| Visual and accessibility | 5 | 0 |
| **Total** | **38** | **19** |

---

## 8. Test data

| Set | Purpose |
|---|---|
| TD-01 | Valid automobile profile — Audi, 110 kW, 5 seats, Petrol, list price 30,000, mileage 10,000 |
| TD-02 | Valid insurant — adult, Germany, Employee, one hobby selected |
| TD-03 | Valid product data — start date at today + 90 days, mid-range insurance sum |
| TD-04 | Boundary set — min/max numeric values for each numeric field |
| TD-05 | Invalid set — future manufacture date, future DOB, malformed e-mail, mismatched passwords |
| TD-06 | Unicode/special-character names and addresses |

Start dates must be generated relative to the run date, never hard-coded — a fixed future date will silently fail the notice-period rule once it passes.

---

## 9. Entry and exit criteria

**Entry:** application reachable; test data sets prepared; baselines approved for visual checks.

**Exit:**
- 100% of P0 scenarios pass
- ≥95% of P1 scenarios pass, with every failure triaged and either fixed or accepted
- No open critical or high defects
- No unreviewed visual diffs and no new critical/serious accessibility violations

---

## 10. Assumptions, risks and open questions

**Assumptions**
- Field inventory and locator ids above are drawn from Tricentis' published documentation and community automation examples. The live app blocks automated crawling, so **every field list and validation rule must be confirmed against the running application before scripting.**
- The app is stateless between sessions; no login or persisted account is required.

**Risks**
- Shared public demo environment — availability, data resets and app updates are outside our control. Do not treat failures as product defects without re-running.
- Premium calculation is undocumented, so price scenarios assert relationships and consistency, not absolute values.
- The confirmation on submit is a native-style dialog; handling differs across drivers and must be scripted per framework.

**Open questions**
1. What is the exact minimum notice period for Start Date, and is it calendar days or months?
2. Is there a minimum insurable age, and does it differ by vehicle category?
3. What is the precise additional field set for Truck and Camper?
4. Are file uploads on Step 2 restricted by type and size?
5. Is refresh-on-step expected to preserve state or reset the wizard?
