# Entities

## Departments

| departments | Data Type    | Attributes         |
| ----------- | ------------ | ------------------ |
| id          | tinyint      | PK, auto_increment |
| name        | varchar(100) | notnull, unique    |
| email       | varchar(50)  | notnull, unique    |
| phone       | char(12)     | null               |
| address     | varchar(50)  | notnull            |

## Graduate Courses

| graduate_courses | Data Type   | Attributes         |
| ---------------- | ----------- | ------------------ |
| id               | smallint    | PK, auto_increment |
| department_id    | tinyint     | FK                 |
| name             | varchar(50) | notnull            |
| lenght           | tinyint     | notnull            |
| tot_cfu          | varchar(3)  | notnull            |
| language         | varchar(30) | notnull            |
| location         | varchar(50) | notnull            |

## Courses

| courses         | Data Type   | Attributes         |
| --------------- | ----------- | ------------------ |
| id              | smallint    | PK, auto_increment |
| name            | varchar(30) | notnull            |
| lenght          | smallint    | notnull            |
| cfu             | tinyint     | notnull            |
| teaching_period | varchar(25) | notnull            |
| frequency       | varchar(20) | notnull            |

## Teachers

| teachers  | Data Type   | Attributes         |
| --------- | ----------- | ------------------ |
| id        | smallint    | PK, auto_increment |
| firstname | varchar(50) | notnull            |
| lastname  | varchar(50) | notnull            |
| email     | varchar(50) | notnull, unique    |

## Students

| students           | Data Type   | Attributes         |
| ------------------ | ----------- | ------------------ |
| serial_number      | int         | PK, auto_increment |
| graduate_course_id | smallint    | FK                 |
| firstname          | varchar(50) | notnull            |
| lastname           | varchar(50) | notnull            |
| email              | varchar(50) | notnull, unique    |
| accumulated_cfu    | varchar(3)  | notnull            |
| tax                | smallint    | notnull            |

## Exam Appeals

| exam_appeals | Data Type | Attributes         |
| ------------ | --------- | ------------------ |
| id           | smallint  | PK, auto_increment |
| course_id    | smallint  | FK                 |
| date         | date      | notnull            |
| timetable    | time      | notnull            |

## Graduate Course_Course

| graduate_course_course | Data Type | Attributes |
| ---------------------- | --------- | ---------- |
| graduate_course_id     | smallint  | FK         |
| course_id              | smallint  | FK         |

## Course_Teacher

| course_teacher | Data Type | Attributes |
| -------------- | --------- | ---------- |
| course_id      | smallint  | FK         |
| teacher_id     | smallint  | FK         |

## Exam Appeal_Student

| exam_appeal_student   | Data Type | Attributes |
| --------------------- | --------- | ---------- |
| exam_appeal_id        | smallint  | FK         |
| student_serial_number | smallint  | FK         |
| evaluation            | tinyint   | notnull    |
