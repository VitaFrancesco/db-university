### Contare quanti iscritti ci sono stati ogni anno

```SQL
SELECT YEAR(`enrolment_date`) AS 'year', COUNT(*) AS 'n_registered'
FROM `students`
GROUP BY `year`
ORDER BY `year` ASC;
```