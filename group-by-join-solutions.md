# Query solutions

# GROUP BY

## 1. Contare quanti iscritti ci sono stati ogni anno

```
SELECT
    COUNT(*), YEAR(`enrolment_date`)
FROM
    `students`
GROUP BY YEAR(`enrolment_date`);
```

## 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```
SELECT
    COUNT(*), office_address
FROM
    `teachers`
GROUP BY `office_address`;
```

## 3. Calcolare la media dei voti di ogni appello d'esame

```
SELECT
    `exam_id`, AVG(vote)
FROM
    `exam_student`
GROUP BY `exam_id`;
```

```
SELECT
    `exam_student`.`exam_id`, `courses`.`name`, AVG(vote)
FROM
    `exam_student`
        JOIN
    `exams` ON `exam_student`.`exam_id` = `exams`.`id`
        JOIN
    `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `exam_id`;
```

## 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```
SELECT
    COUNT(*), `departments`.`name`
FROM
    `departments`
        JOIN
    `degrees` ON `departments`.`id` = `degrees`.`department_id`
GROUP BY `departments`.`name`;
```

# JOIN

## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```
SELECT
    `degrees`.`name`, `students`.*
FROM
    `degrees`
        JOIN
    `students` ON `degrees`.`id` = `students`.`degree_id`
WHERE
    `degrees`.`name` = 'Corso di Laurea in Economia';
```

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```
SELECT
    *
FROM
    `departments`
        JOIN
    `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE
    `degrees`.`level` = 'magistrale'
        AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT
    `teachers`.`id`,
    `teachers`.`name`,
    `teachers`.`surname`,
    `courses`.*
FROM
    `course_teacher`
        JOIN
    `courses` ON `course_teacher`.`course_id` = `courses`.`id`
        JOIN
    `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE
    `teachers`.`id` = 44;
```

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```
SELECT
    `students`.`name`,
    `students`.`surname`,
    `students`.`registration_number`,
    `degrees`.*,
    `departments`.*
FROM
    `departments`
        JOIN
    `degrees` ON `departments`.`id` = `degrees`.`department_id`
        JOIN
    `students` ON `degrees`.`id` = `students`.`degree_id`
ORDER BY `students`.`surname` , `students`.`name`;
```

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```
SELECT
    `degrees`.`name`, `courses`.*, `teachers`.*
FROM
    `degrees`
        JOIN
    `courses` ON `degrees`.`id` = `courses`.`degree_id`
        JOIN
    `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
        JOIN
    `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`name`;
```

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```
SELECT DISTINCT
    `departments`.`name`, `teachers`.*
FROM
    `departments`
        JOIN
    `degrees` ON `departments`.`id` = `degrees`.`department_id`
        JOIN
    `courses` ON `degrees`.`id` = `courses`.`degree_id`
        JOIN
    `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
        JOIN
    `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE
    `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY teachers.id;
```

## 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

Parte 1

```
SELECT
    `students`.`name`,
    `students`.`surname`,
    `students`.`registration_number`,
    `courses`.`name`,
    COUNT(`exam_student`.`exam_id`) AS `attempts`,
    MAX(`exam_student`.`vote`) AS `highest_score`
FROM
    `students`
        JOIN
    `exam_student` ON `students`.`id` = `exam_student`.`student_id`
        JOIN
    `exams` ON `exam_student`.`exam_id` = `exams`.`id`
        JOIN
    `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`name` , `students`.`surname` , `students`.`registration_number` , `courses`.`name`
ORDER BY `students`.`surname` , `students`.`name`;
```

Parte 2

```
SELECT
    `students`.`name`,
    `students`.`surname`,
    `students`.`registration_number`,
    `courses`.`name`,
    COUNT(`exam_student`.`exam_id`) AS `attempts`,
    MAX(`exam_student`.`vote`) AS `highest_score`
FROM
    `students`
        JOIN
    `exam_student` ON `students`.`id` = `exam_student`.`student_id`
        JOIN
    `exams` ON `exam_student`.`exam_id` = `exams`.`id`
        JOIN
    `courses` ON `exams`.`course_id` = `courses`.`id`
WHERE
    `exam_student`.`vote` >= 18
GROUP BY `students`.`name` , `students`.`surname` , `students`.`registration_number` , `courses`.`name`
ORDER BY `students`.`surname` , `students`.`name`;
```
