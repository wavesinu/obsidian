### Shell 1
- 기존 코드
```MySQL
create table STUDENT
(
    Name           varchar(20) not null,
    Student_number int         not null,
    Class          varchar(20) not null,
    Major          varchar(20) not null,
    PRIMARY KEY (Student_number)
);

create table COURSE
(
    Course_name   varchar(20) not null,
    Course_number varchar(20) not null,
    Credit_hours  int         not null,
    Department    varchar(20) not null,
    PRIMARY KEY (Course_number)
);

create table SECTION
(
    Section_identifier int         not null,
    Course_number      varchar(20) not null,
    Semester           varchar(20) not null,
    Year               int         not null,
    Instructor         varchar(20) not null,
    FOREIGN KEY (Course_number) REFERENCES COURSE (Course_number),
    PRIMARY KEY (Section_identifier)
);

create table GRADE_REPORT
(
    Student_number     int         not null,
    Section_identifier int         not null,
    Grade              varchar(20) not null,
    FOREIGN KEY (Student_number) REFERENCES STUDENT (Student_number),
    FOREIGN KEY (Section_identifier) REFERENCES SECTION (Section_identifier),
    PRIMARY KEY (Student_number, Section_identifier)
);

);

create table PREREQUISITE
(
    Course_number       varchar(20) not null,
    Prerequisite_number varchar(20) not null,
    FOREIGN KEY (Course_number) REFERENCES COURSE (Course_number),
    PRIMARY KEY (Course_number, Prerequisite_number)
);
```

- 수정 코드
```MySQL
CREATE TABLE STUDENT
(
    Name           VARCHAR(20) NOT NULL,
    Student_number INT NOT NULL,
    Class          VARCHAR(20) NOT NULL,
    Major          VARCHAR(20) NOT NULL,
    PRIMARY KEY (Student_number)
);

CREATE TABLE COURSE
(
    Course_name   VARCHAR(20) NOT NULL,
    Course_number VARCHAR(20) NOT NULL,
    Credit_hours  INT NOT NULL,
    Department    VARCHAR(20) NOT NULL,
    PRIMARY KEY (Course_number)
);

CREATE TABLE SECTION
(
    Section_identifier INT NOT NULL,
    Course_number      VARCHAR(20) NOT NULL,
    Semester           ENUM('Spring', 'Summer', 'Fall', 'Winter') NOT NULL,
    Year               INT NOT NULL,
    Instructor         VARCHAR(20) NOT NULL,
    FOREIGN KEY (Course_number) REFERENCES COURSE (Course_number)
        ON DELETE RESTRICT ON UPDATE CASCADE,
    PRIMARY KEY (Section_identifier)
);

CREATE TABLE GRADE_REPORT
(
    Student_number     INT NOT NULL,
    Section_identifier INT NOT NULL,
    Grade              ENUM('A', 'B', 'C', 'D', 'F') NOT NULL,
    FOREIGN KEY (Student_number) REFERENCES STUDENT (Student_number)
        ON DELETE CASCADE ON UPDATE CASCADE,
    FOREIGN KEY (Section_identifier) REFERENCES SECTION (Section_identifier)
        ON DELETE CASCADE ON UPDATE CASCADE,
    PRIMARY KEY (Student_number, Section_identifier)
);

CREATE TABLE PREREQUISITE
(
    Course_number       VARCHAR(20) NOT NULL,
    Prerequisite_number VARCHAR(20) NOT NULL,
    FOREIGN KEY (Course_number) REFERENCES COURSE (Course_number)
        ON DELETE CASCADE ON UPDATE CASCADE,
    PRIMARY KEY (Course_number, Prerequisite_number)
);
```
### Shell 2
```MySQL
-- insert data into STUDENT table
insert into STUDENT (Name, Student_number, Class, Major) values ('Smith', '17', '1', 'CS');
insert into STUDENT (Name, Student_number, Class, Major) values ('Brown', '8', '2', 'CS');

-- insert data into COURSE table
insert into COURSE (Course_name, Course_number, Credit_hours, Department) values ('Intro to Computer Science', 'CS1310', '4', 'CS');
insert into COURSE (Course_name, Course_number, Credit_hours, Department) values ('Data Structures', 'CS3320', '4', 'CS');
insert into COURSE (Course_name, Course_number, Credit_hours, Department) values ('Discrete Mathematics', 'MATH2410', '3', 'MATH');
insert into COURSE (Course_name, Course_number, Credit_hours, Department) values ('Database', 'CS3380', '3', 'CS');

-- insert data into SECTION table
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('85', 'MATH2410', 'Fall', '07', 'King');
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('92', 'CS1310', 'Fall', '07', 'Anderson');
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('102', 'CS3320', 'Spring', '08', 'Knuth');
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('112', 'MATH2410', 'Fall', '08', 'Chang');
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('119', 'CS1310', 'Fall', '08', 'Anderson');
insert into SECTION (Section_identifier, Course_number, Semester, Year, Instructor) values ('135', 'CS3380', 'Fall', '08', 'Stone');

-- insert data into GRADE_REPORT table
```