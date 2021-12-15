# 1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(`id`) as `numero_iscrizioni`, YEAR(`enrolment_date`) as `anno_iscrizione`
FROM `students`
GROUP BY YEAR(`enrolment_date`)

# 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) as `numero_insegnanti` , `office_address` as `indirizzo_ufficio`
FROM `teachers`
GROUP BY `office_address`

# 3. Calcolare la media dei voti di ogni appello d'esame
SELECT COUNT(`id`), `exams`.`id`, `exams`.`date`,  AVG(`exam_student`.`vote`)
FROM `exams`
INNER JOIN `exam_student` ON `exams`.`id` = `exam_student`.`exam_id`
GROUP BY `exams`.`id`

# 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(`degrees`.`id`), `departments`.`name`
FROM `degrees`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
GROUP BY `departments`.`id`

# 5. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT *
FROM `degrees`
INNER JOIN `students` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` LIKE "Corso di Laurea in Economia"

# 6. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze
SELECT * 
FROM `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` LIKE "%neuroscienze%"

# 7. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT * 
FROM `teachers`
INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44

# 8. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `students`.`surname`, `students`.`name`, `degrees`.`name`, `departments`.`name`
FROM `students`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`  
ORDER BY `students`.`surname`  ASC
# 9. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`, `teachers`.`surname`
FROM `degrees`
INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
ORDER BY `degrees`.`name`
# 10. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`
FROM `teachers`
INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` LIKE "%matematica%"
ORDER BY `teachers`.`name`

# 11. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami