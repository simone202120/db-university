                QUERY SELECT


1. Selezionare tutti gli studenti nati nel 1990 (160)
    SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
    SELECT * FROM `courses` WHERE CFU > 10 

3. Selezionare tutti gli studenti che hanno più di 30 anni
    SELECT * FROM `students` WHERE year(`date_of_birth`)<1992 

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
    SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = 1 

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
    SELECT * FROM `exams` WHERE `date` = "2020-06-20" AND `hour`>= "14:00:00" 

6. Selezionare tutti i corsi di laurea magistrale (38)
    SELECT * FROM `degrees` WHERE `level` = "magistrale" 

7. Da quanti dipartimenti è composta l'università? (12)
    SELECT COUNT(*) FROM departments

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
    SELECT * FROM `teachers` WHERE `phone` IS null 



                    QUERY GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
    SELECT COUNT(*), YEAR(`enrolment_date`) FROM `students` GROUP BY YEAR (`enrolment_date`)

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
    SELECT COUNT(*), `office_adress` FROM `teachers` GROUP BY `office_adress`

3. Calcolare la media dei voti di ogni appello d'esame
    SELECT AVG (`vote`) FROM `exam_student` GROUP BY `exam_id` 

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
    SELECT COUNT(*), `degree_id` FROM `courses` GROUP BY `degree_id`




                        QUERY JOIN


1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
    SELECT `students`.`name`, `students`.surname, `students`.`registration_number` FROM `students` JOIN `degrees`.`id` WHERE `degrees`.`name` = "Corso di Laurea in Economia"

2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze
    SELECT `departments`. `name`, `degrees`. `name`  FROM `departments` JOIN `degrees` ON `departments` .`id` = `degrees`. `departments_id` WHERE `departments`.`name` = "Dipartimento di Neuroscienze"

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    SELECT `teachers`.`id` AS "ID_insegnate", `courses`.`name`, `courses`.`description`  FROM `courses`
     JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`  JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`  WHERE `teachers`.`name` ="Fulvio"  AND `teachers` . `surname` = "Amato"

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome
    SELECT `students`.`name` AS "Nome_Studente", `students`.`surname` AS "Cognome_Studente", `students`.`registration_number`, `degrees`.`name` AS "Nome_Laurea", `departments`.`name`  FROM `students`  JOIN `degrees` ON `students`. `degrees_id` = `degrees`.`id`  JOIN `departments` ON `departments`.`id`= `degrees`.`departments_id`  ORDER BY `students`. `surname`, `students` . `name`;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
    SELECT `degrees`.`name`, `courses`.`name`,`teachers`.`surname`  FROM `degrees`  JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`  JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`  JOIN `teachers` ON `teachers` .`id` = `course_teacher` . `teacher_id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
    SELECT `degrees`.`name`, `courses`.`name`,`teachers`.`surname`  FROM `degrees`  JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`  JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`  JOIN `teachers` ON `teachers` .`id` = `course_teacher` . `teacher_id` JOIN `departments` ON `departments`.`id` = `degrees`.`departments_id`;

