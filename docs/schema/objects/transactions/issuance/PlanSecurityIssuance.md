:house: [Documentation Home](/README.md)

---

### Object - Plan Security Issuance Transaction

`https://opencaptablecoalition.com/schema/objects/transactions/issuance/PlanSecurityIssuance.schema.json`

**Description:** _Object describing securities issuance transaction from a plan by the issuer and held by a stakeholder_

**Data Type:** `OCF Object - TX_PLAN_SECURITY_ISSUANCE`

**Composed From:**

- [schema/primitives/BaseObject](/docs/schema/primitives/BaseObject.md)
- [schema/primitives/transactions/BaseTransaction](/docs/schema/primitives/transactions/BaseTransaction.md)
- [schema/primitives/transactions/BaseSecurityTransaction](/docs/schema/primitives/transactions/BaseSecurityTransaction.md)
- [schema/primitives/transactions/issuance/BaseIssuance](/docs/schema/primitives/transactions/issuance/BaseIssuance.md)

**Properties:**

| Property                     | Type                                                                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Required   |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| id                           | `STRING`                                                                                                                                           | Identifier for the object                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | `REQUIRED` |
| comments                     | [`STRING`]                                                                                                                                         | Unstructured text comments related to and stored for the object                                                                                                                                                                                                                                                                                                                                                                                                                                             | -          |
| object_type                  | **Constant:** `TX_PLAN_SECURITY_ISSUANCE`</br>_Defined in [schema/enums/ObjectType](/docs/schema/enums/ObjectType.md)_                             | Object type field                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `REQUIRED` |
| date                         | [schema/types/Date](/docs/schema/types/Date.md)                                                                                                    | Date on which the transaction occurred                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | `REQUIRED` |
| security_id                  | `STRING`                                                                                                                                           | Identifier for the security (stock, plan security, warrant, or convertible) by which it can be referenced by other transaction objects. Note that while this identifier is created with an issuance object, it should be different than the issuance object's `id` field which identifies the issuance transaction object itself. All future transactions on the security (e.g. acceptance, transfer, cancel, etc.) must reference this `security_id` to qualify which security the transaction applies to. | `REQUIRED` |
| custom_id                    | `STRING`                                                                                                                                           | A custom ID for this security (e.g. CN-1.)                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `REQUIRED` |
| stakeholder_id               | `STRING`                                                                                                                                           | Identifier for the stakeholder that holds legal title to this security                                                                                                                                                                                                                                                                                                                                                                                                                                      | `REQUIRED` |
| board_approval_date          | [schema/types/Date](/docs/schema/types/Date.md)                                                                                                    | Date of board approval for the security                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `REQUIRED` |
| consideration                | [schema/types/Monetary](/docs/schema/types/Monetary.md)                                                                                            | Consideration for the security                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | `REQUIRED` |
| security_law_exemptions      | [ [schema/types/SecurityExemption](/docs/schema/types/SecurityExemption.md) ]                                                                      | List of security law exemptions (and applicable jurisdictions) for this security                                                                                                                                                                                                                                                                                                                                                                                                                            | `REQUIRED` |
| stock_plan_id                | `STRING`                                                                                                                                           | Identifier of StockPlan the PlanSecurities were issued from                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `REQUIRED` |
| compensation_type            | `Enum - Compensation Type`</br></br>_Description:_ Enumeration of stock compensation types</br></br>**ONE OF:** </br>&bull; OPTION </br>&bull; RSU | If the plan security is compensation, what kind?                                                                                                                                                                                                                                                                                                                                                                                                                                                            | `REQUIRED` |
| option_grant_type            | `Enum - Option Type`</br></br>_Description:_ Enumeration of option types</br></br>**ONE OF:** </br>&bull; NSO </br>&bull; ISO </br>&bull; INTL     | If the plan security is an option, what kind?                                                                                                                                                                                                                                                                                                                                                                                                                                                               | -          |
| quantity                     | [schema/types/Numeric](/docs/schema/types/Numeric.md)                                                                                              | How many shares are subject to this plan security?                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `REQUIRED` |
| exercise_price               | [schema/types/Monetary](/docs/schema/types/Monetary.md)                                                                                            | What is the exercise price?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `REQUIRED` |
| vesting_rules                | [schema/types/VestingRules](/docs/schema/types/VestingRules.md)                                                                                    | What vesting applies to this plan security?                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `REQUIRED` |
| expiration_date              | **ONE OF the Following Types/Objs:**</br>&bull; `NULL` _()_</br>&bull; [schema/types/Date](/docs/schema/types/Date.md)                             | Expiration date of the plan security                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `REQUIRED` |
| termination_exercise_windows | [ [schema/types/TerminationWindow](/docs/schema/types/TerminationWindow.md) ]                                                                      | Exercise periods applicable to plan security after a termination for a given, enumerated reason                                                                                                                                                                                                                                                                                                                                                                                                             | `REQUIRED` |

**Source Code:** [schema/objects/transactions/issuance/PlanSecurityIssuance](/schema/objects/transactions/issuance/PlanSecurityIssuance.schema.json)

**Examples:**

```json
[
  {
    "object_type": "TX_PLAN_SECURITY_ISSUANCE",
    "id": "test-plan-security-issuance-minimal",
    "security_id": "test-security-id",
    "date": "2019-12-12",
    "security_law_exemptions": [
      {
        "description": "Exemption",
        "jurisdiction": "CA"
      }
    ],
    "board_approval_date": "2021-01-21",
    "stakeholder_id": "test-stakeholder-id",
    "consideration": {
      "amount": "1.00",
      "currency": "USD"
    },
    "custom_id": "CA-1",
    "stock_plan_id": "test-stock-plan-id",
    "compensation_type": "RSU",
    "quantity": "50",
    "exercise_price": {
      "amount": "50.00",
      "currency": "USD"
    },
    "vesting_rules": {
      "vesting_type": "SCHEDULE_DRIVEN_ONLY"
    },
    "expiration_date": "2031-01-20",
    "termination_exercise_windows": [
      {
        "reason": "CAUSE",
        "period": 1,
        "period_type": "DAYS"
      }
    ]
  },
  {
    "object_type": "TX_PLAN_SECURITY_ISSUANCE",
    "id": "test-plan-security-issuance-any-of-block-for-compensation-type-option",
    "security_id": "test-security-id",
    "date": "2019-12-12",
    "security_law_exemptions": [
      {
        "description": "Exemption",
        "jurisdiction": "CA"
      }
    ],
    "board_approval_date": "2021-01-21",
    "stakeholder_id": "test-stakeholder-id",
    "consideration": {
      "amount": "1.00",
      "currency": "USD"
    },
    "custom_id": "CA-1",
    "stock_plan_id": "test-stock-plan-id",
    "compensation_type": "OPTION",
    "option_grant_type": "ISO",
    "quantity": "50",
    "exercise_price": {
      "amount": "50.00",
      "currency": "USD"
    },
    "vesting_rules": {
      "vesting_type": "SCHEDULE_DRIVEN_ONLY"
    },
    "expiration_date": "2031-01-20",
    "termination_exercise_windows": [
      {
        "reason": "CAUSE",
        "period": 1,
        "period_type": "DAYS"
      }
    ]
  },
  {
    "object_type": "TX_PLAN_SECURITY_ISSUANCE",
    "id": "test-plan-security-issuance-full-fields",
    "security_id": "test-security-id",
    "date": "2019-12-12",
    "security_law_exemptions": [
      {
        "description": "Exemption",
        "jurisdiction": "CA"
      },
      {
        "description": "Extra special exemption",
        "jurisdiction": "CA"
      }
    ],
    "board_approval_date": "2021-01-21",
    "stakeholder_id": "test-stakeholder-id",
    "consideration": {
      "amount": "1.00",
      "currency": "CAD"
    },
    "custom_id": "CA-1",
    "stock_plan_id": "test-stock-plan-id",
    "compensation_type": "RSU",
    "quantity": "100",
    "exercise_price": {
      "amount": "50.00",
      "currency": "CAD"
    },
    "vesting_rules": {
      "vesting_type": "SCHEDULE_DRIVEN_ONLY",
      "vesting_schedule_id": "test-vesting-schedule-id",
      "vesting_start_date": "2021-01-10",
      "vesting_conditions": [
        {
          "amount_numerator": 1,
          "amount_denominator": 4,
          "period_length": 1,
          "period_type": "YEARS",
          "priority": 1,
          "dependent_vesting": []
        }
      ],
      "custom_vesting_tranches": [
        {
          "vest_date": "2021-01-11",
          "vest_quantity": "100"
        }
      ],
      "custom_vesting_description": "100% up front due to custom vesting tranche"
    },
    "expiration_date": "2031-01-20",
    "termination_exercise_windows": [
      {
        "reason": "CAUSE",
        "period": 0,
        "period_type": "DAYS"
      },
      {
        "reason": "VOLUNTARY",
        "period": 3,
        "period_type": "MONTHS"
      },
      {
        "reason": "INVOLUNTARY",
        "period": 14,
        "period_type": "DAYS"
      },
      {
        "reason": "DEATH",
        "period": 3,
        "period_type": "YEARS"
      },
      {
        "reason": "DISABILITY",
        "period": 3,
        "period_type": "YEARS"
      },
      {
        "reason": "RETIREMENT",
        "period": 1,
        "period_type": "MONTHS"
      }
    ],
    "comments": [
      "comment 1",
      "comment 2",
      "a third comment"
    ]
  }
]
```