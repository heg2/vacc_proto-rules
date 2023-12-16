Es stehen folgende Fakten zur Verfügung: 

| Name / key | Typ           | Erklärung |
|------------|---------------|-----------| 
| gender     | "male", "female", "other" | Geschlecht des Patienten |
| age        | integer       | Alter des Patienten, in kompletten Jahren |
| age_in_months| integer       | Alter des Patienten, in kompletten Monaten, wenn age <= 2 |
| vXXX_last_dose| integer, NULL | Zeitdauer in Tagen seit letzter Dosis der Impfung |
| vXXX_completed| "TRUE", "FALSE" | Wurde die Impfung komplettisiert? |
| dXXX_last_dose| integer, NULL | Zeitdauer in Tagen seit letzter Dosis der Impfung zur Zielerkrankung |
| dXXX_completed| "TRUE", "FALSE" | Wurde die Impfung zur Zielerkrankung komplettisiert? |
| dXXX_number_of_doses| "TRUE", "FALSE" | Wurde die Impfung zur Zielerkrankung komplettisiert? |
| rXXX_risk| "TRUE", "FALSE" | Trifft das Risiko für den\*die Patient\*in zu? |
