### Fakten
Es stehen folgende Fakten zur Verfügung: 

| Name / key | Typ           | Erklärung |
|------------|---------------|-----------| 
| gender     | "male", "female", "other" | Geschlecht des Patienten |
| age        | integer       | Alter des Patienten, in kompletten Jahren |
| age_in_months| integer, NULL       | Alter des Patienten, in kompletten Monaten, wenn age <= 2 |
| vXXX_last_dose| integer, NULL | Zeitdauer in Tagen seit letzter Dosis der Impfung |
| vXXX_completed| "TRUE", "FALSE" | Wurde die Impfung komplettisiert? |
| dXXX_last_dose| integer, NULL | Zeitdauer in Tagen seit letzter Dosis der Impfung zur Zielerkrankung |
| dXXX_completed| "TRUE", "FALSE" | Wurde die Impfung zur Zielerkrankung komplettisiert? |
| dXXX_number_of_doses| integer, NULL | Wurde die Impfung zur Zielerkrankung komplettisiert? |
| rXXX_risk| "TRUE", "FALSE" | Trifft das Risiko für den\*die Patient\*in zu? |

### Regeln
Wie die Regeln aufgebaut sein können, ist bei [stugna-es](https://www.npmjs.com/package/stugna-es#ruleadd) dokumentiert.
Reservierte Wörter sind: `TRUE`, `FALSE`, `AND`, `OR`, `NOT`, und `LIKE` (alle case sensitive). Diese können nicht für Variablennamen verwendet werden.
Erforderlich sind folgende Properties, was die minimale Regel wie folgt definiert:
``` typescript
interface rule
  {
    condition: string      // describe condition for adding new fact to system
    factName: string,      // name of new fact, which will be added if condition is met. no spaces allowed.
    factValue: string | number | boolean //  value of new fact, which will be added if condition is met
    description?: string    // short fact description for logging
    priority?: number      // rule priority, number, optional, default value is 1. low numbers are processed first
    missing? string,       // optional field with default values for missing facts. not working with precondition
    precondition?: string, // option string field with the same syntax as condition.
    factNameElse?: string   // name of new fact, which will be added if condition is not met. no spaces allowed. needs factValueElse if present.
    factValueElse?: string | number | boolean // value of new fact, which will be added if condition is not met. needs factNameElse if present.
    final?: 1 | 2 | 3      // Each value dictates when to halt the evaluation of subsequent rules as documented in the link above
    isTrigger?: boolean    // after new rule adding, rules check procedure starts automatically (default: true)

  }
```

