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