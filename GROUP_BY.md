### Contare quanti iscritti ci sono stati ogni anno

```SQL
SELECT YEAR(`enrolment_date`) AS 'year', COUNT(*) AS 'n_registered'
FROM `students`
GROUP BY `year`
ORDER BY `year` ASC;
```

### Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```SQL
SELECT `office_address`, COUNT(*) AS 'n_teachers'
FROM `teachers`
GROUP BY `office_address`
```