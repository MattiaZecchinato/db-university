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
