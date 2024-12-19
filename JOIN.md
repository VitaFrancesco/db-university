### Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```SQL
SELECT `students`.*, `degrees`.`name`
FROM `students`
JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

### Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```SQL
SELECT *
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'Magistrale';
```

### Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```SQL
SELECT *
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `course_teacher`.`teacher_id` = 44;
```

Unendo anche la tabella teachers

```SQL
SELECT *
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;
```

### Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```SQL
SELECT *
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`;
```

Uguale a scrivere
```SQL
SELECT *
FROM `departments`
JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`
JOIN `students`
ON `degrees`.`id` = `students`.`degree_id`;
```

### Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```SQL
SELECT `degrees`.`name` AS 'Corso di laurea', `courses`.`name` AS 'Corso', CONCAT(`teachers`.`name`,' ',`teachers`.`surname`) AS 'Insegnante'
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`;
```

### Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```SQL
SELECT DISTINCT CONCAT(`teachers`.`name`,' ',`teachers`.`surname`) AS 'Insegnante'
FROM `departments`
JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';
```

### BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo.

```SQL
SELECT CONCAT(`students`.`name`,' ',`students`.`surname`) AS 'students', `courses`.`name` AS 'courses', COUNT(*) AS 'attemps', MAX(`exam_student`.`vote`) AS 'vote_max'
FROM `students`
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses`
ON `courses`.`id` = `exams`.`course_id`
GROUP BY `students`.`id`, `courses`.`id`;
```

Filtrare i tentativi con voto minimo 18.

```SQL
SELECT CONCAT(`students`.`name`,' ',`students`.`surname`) AS 'students', MAX(`exam_student`.`vote`) AS 'passed_vote'
FROM `students`
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses`
ON `courses`.`id` = `exams`.`course_id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `students`.`id`, `courses`.`id`;
```