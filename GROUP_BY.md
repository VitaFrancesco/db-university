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
GROUP BY `office_address`;
```

### Calcolare la media dei voti di ogni appello d'esame

```SQL
SELECT `exam_id`, AVG(`vote`) AS 'avg_votes'
FROM `exam_student`
GROUP BY `exam_id`;
```

### Contare quanti corsi di laurea ci sono per ogni dipartimento

```SQL
SELECT `department_id`, COUNT(*)
FROM `degrees`
GROUP BY `department_id`;
```