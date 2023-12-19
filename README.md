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
| rXXX | "TRUE", "FALSE" | Trifft das Risiko für den\*die Patient\*in zu? |

`vXXX` steht für Impfungen, wobei XXX durch den Wert des coding.code erstetzt werden muss. Analog für `dXXX` für Zielerkrankungen und `rXXX` für Risiken.

### Regeln
Wie die Regeln aufgebaut sein können, ist bei [stugna-es](https://www.npmjs.com/package/stugna-es#ruleadd) dokumentiert.
Reservierte Wörter sind: `TRUE`, `FALSE`, `AND`, `OR`, `NOT`, und `LIKE` (alle case sensitive). Diese können nicht für Variablennamen verwendet werden.
Erforderlich sind folgende Properties, was die minimale Regel wie folgt definiert:
``` typescript
interface rule
  {
    // describe condition for adding new fact to system
    condition: string      
    // name of new fact, which will be added if condition is met. no spaces allowed.
    factName: string,      
    // value of new fact, which will be added if condition is met
    factValue: string | number | boolean 
    // short fact description for logging
    description?: string
    // rule priority, number, optional, default value is 1. low numbers are processed first
    priority?: number      
    // optional field with default values for missing facts. not working with precondition
    missing? string,      
    // option string field with the same syntax as condition. 
    precondition?: string, 
     // name of new fact, which will be added if condition is not met. no spaces allowed. needs factValueElse if present.
    factNameElse?: string  
    // value of new fact, which will be added if condition is not met. needs factNameElse if present.
    factValueElse?: string | number | boolean 
    // Each value dictates when to halt the evaluation of subsequent rules as documented in the link above
    final?: 1 | 2 | 3      
    // after new rule adding, rules check procedure starts automatically (default: true)
    isTrigger?: boolean    
  }
```

*Vorsicht:* 
- Fehlende Fakten werden per default als "TRUE" angenommen. Möchte man das nicht, muss man in der Regel den Parameter `missing: "FALSE"` setzen.
- Abgekürzte Schreibweisen gehen nicht: `fact1 OR fact2` ist nicht das selbe wie `fact1 = TRUE OR fact2 = TRUE`.

Konvention für "Helferfakten", die nicht im Endergebnis aufscheinen sollen: Deren Faktnamen beginnen mit einem `x_`, und werden so bei der Anzeige ausgefiltert.
