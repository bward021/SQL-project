```sql
CREATE SCHEMA `sql_final_project` ;

-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema my_sql_final
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema my_sql_final
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `my_sql_final` DEFAULT CHARACTER SET utf8 ;
USE `my_sql_final` ;

-- -----------------------------------------------------
-- Table `my_sql_final`.`Students`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `my_sql_final`.`Students` (
  `idStudents` INT NOT NULL AUTO_INCREMENT,
  `students_firstname` VARCHAR(45) NULL,
  `students_lastname` VARCHAR(45) NULL,
  PRIMARY KEY (`idStudents`),
  UNIQUE INDEX `idStudents_UNIQUE` (`idStudents` ASC) VISIBLE)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `my_sql_final`.`professors`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `my_sql_final`.`professors` (
  `idprofessors` INT NOT NULL AUTO_INCREMENT,
  `professors_name` VARCHAR(45) NULL,
  PRIMARY KEY (`idprofessors`),
  UNIQUE INDEX `idprofessors_UNIQUE` (`idprofessors` ASC) VISIBLE)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `my_sql_final`.`courses`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `my_sql_final`.`courses` (
  `idcourses` INT NOT NULL AUTO_INCREMENT,
  `courses_name` VARCHAR(45) NULL,
  `professors_idprofessors` INT NOT NULL,
  PRIMARY KEY (`idcourses`, `professors_idprofessors`),
  UNIQUE INDEX `idcourses_UNIQUE` (`idcourses` ASC) VISIBLE,
  INDEX `fk_courses_professors1_idx` (`professors_idprofessors` ASC) VISIBLE,
  CONSTRAINT `fk_courses_professors1`
    FOREIGN KEY (`professors_idprofessors`)
    REFERENCES `my_sql_final`.`professors` (`idprofessors`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `my_sql_final`.`grades`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `my_sql_final`.`grades` (
  `idgrades` INT NOT NULL AUTO_INCREMENT,
  `grades_letter` VARCHAR(45) NULL,
  `Students_idStudents` INT NOT NULL,
  `courses_idcourses` INT NOT NULL,
  PRIMARY KEY (`idgrades`, `Students_idStudents`, `courses_idcourses`),
  UNIQUE INDEX `idgrades_UNIQUE` (`idgrades` ASC) VISIBLE,
  INDEX `fk_grades_Students1_idx` (`Students_idStudents` ASC) VISIBLE,
  INDEX `fk_grades_courses1_idx` (`courses_idcourses` ASC) VISIBLE,
  CONSTRAINT `fk_grades_Students1`
    FOREIGN KEY (`Students_idStudents`)
    REFERENCES `my_sql_final`.`Students` (`idStudents`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_grades_courses1`
    FOREIGN KEY (`courses_idcourses`)
    REFERENCES `my_sql_final`.`courses` (`idcourses`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;


-- inserting data

INSERT INTO students (students_firstname, students_lastname)
VALUES ('Brandon', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Nate', 'Bradshaw');
INSERT into students(students_firstname, students_lastname)
VALUES('Colton', 'Gallegos');
INSERT into students(students_firstname, students_lastname)
VALUES('Kat', 'Ramos');
INSERT into students(students_firstname, students_lastname)
VALUES('Trevor', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Wesley', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Jaden', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Heather', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Jeffrey', 'Ward');
INSERT into students(students_firstname, students_lastname)
VALUES('Jaden', 'Harris');
INSERT into students(students_firstname, students_lastname)
VALUES('Bryana', 'Searcy');
INSERT into students(students_firstname, students_lastname)
VALUES('Ariana', 'Anderson');

INSERT INTO professors (professors_name)
VALUES ('Rebecca Tindle');
INSERT INTO professors (professors_name)
VALUES ('Katie Baldwin');

INSERT INTO courses (courses_name, professors_idprofessors)
VALUES ('Math 1050', 1);
INSERT INTO courses (courses_name, professors_idprofessors)
VALUES ('CS 360', 2);
INSERT INTO courses (courses_name, professors_idprofessors)
VALUES ('English 1010', 1);

INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('c', 1, 2);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('b', 2, 3);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('a', 3, 1);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('b', 4, 2);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('a', 5, 3);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('f', 6, 1);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('d', 7, 2);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('c', 8, 3);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('b', 9, 1);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('a', 10, 2);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('c', 11, 3);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('b', 12, 1);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('a', 1, 2);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('c', 2, 3);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('b', 3, 1);
INSERT INTO grades (grades_letter, Students_idStudents, courses_idcourses)
VALUES ('a', 4, 2);


CREATE temporary table alldata
SELECT 
    CASE
		WHEN grades_letter = 'a' THEN 4
		WHEN grades_letter = 'b' THEN 3
        WHEN grades_letter = 'c' THEn 2
        WHEN grades_letter = 'd' THEN 1
        WHEN grades_letter = 'f' THEN 0
        END AS NumberGrade,
	S.idStudents,
    S.Students_firstname,
    S.students_lastname,
    G.idgrades,
    G.grades_letter,
    G.Students_idstudents,
    G.courses_idcourses,
    C.idcourses,
    C.courses_name,
    C.professors_idprofessors,
    p.idprofessors,
    p.professors_name
FROM
	students s
	JOIN grades g ON G.students_idstudents = idStudents 
    JOIN Courses AS C ON g.courses_idcourses = c.idcourses
    JOIN professors AS p ON c.professors_idprofessors = p.idprofessors
limit 1000;

select avg(NumberGrade), idprofessors, professors_name
FROM alldata
GROUP BY idprofessors, professors_name ;

SELECT max(grades_letter), idStudents, students_firstname, students_lastname
FROM alldata
group by idStudents, students_firstname, students_lastname;


SELECT min(grades_letter), idStudents, students_firstname, students_lastname
FROM alldata
group by idStudents, students_firstname, students_lastname;

SELECT students_firstname, students_lastname, courses_name
FROM alldata;

SELECT AVG(NumberGrade) as average_grade, courses_name
FROM alldata
group by courses_name ORDER BY average_grade DESC;

SELECT COUNT(idcourses) as course, students_firstname, students_lastname, professors_name
FROM alldata
group by students_firstname, students_lastname, professors_name ORDER BY course DESC
LIMIT 1;
    

```