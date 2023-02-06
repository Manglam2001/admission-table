# admission-table
--parent table of studentPage for course--
CREATE TABLE Course
(
CourseId CHAR(4),
CourseName VARCHAR(50) Primary key,
PriceDetails NUMERIC(10,2) NOT NULL,
Duration tinyint NOT NULL
)


CREATE TABLE StudentDetails
(
StudentId CHAR(4) PRIMARY KEY,
StudentName VARCHAR(50) NOT NULL,
InitialAmount NUMERIC(10,2) check (InitialAmount >10000) NOT NULL,
CourseName VARCHAR(50)
FOREIGN KEY REFERENCES Course(CourseName)
check(CourseName In ('Electrical Engineering','Electrical and Electronics Engineering',
'Mechanical Engineering','Civil Engineering','Computer Science','Information Technology',
'Electronics and Communication Engineering'))
)



--contactdetails must match with student id

CREATE TABLE ContactDetails
(
StudentID CHAR(4) FOREIGN KEY REFERENCES StudentDetails(StudentId),
EmailId VARCHAR(30) NOT NULL,
ContactNumber CHAR(10) NOT NULL,
StudentAddress VARCHAR(150) NOT NULL
)


--Customer details will be linked with exact student id--

CREATE TABLE CustomerDetails
(
StudentId CHAR(4) FOREIGN KEY REFERENCES StudentDetails(StudentId),
CustomerName VARCHAR(50)
)


-----------------------------------------------
SELECT * FROM Course

SELECT * FROM StudentDetails

SELECT * FROM ContactDetails

SELECT * FROM CustomerDetails
------------------------------------------------

ALTER TABLE Course
DROP COLUMN CourseId

/*(
CourseId CHAR(4),
CourseName VARCHAR(50) Primary key,
PriceDetails NUMERIC(10,2) NOT NULL,
Duration tinyint NOT NULL
)*/

INSERT Course
VALUES('EE--','Electrical Engineering',25000,4),
('EEE-','Electrical and Electronics Engineering',27000,4),
('ME--','Mechanical Engineering',10000,4),
('CE--','Civil Engineering',12000,4.5),
('CS--','Computer Science',112000,5),
('IT--','Information Technology',75000,4.5),
('ECE-','Electronics and Communication Engineering',35000,4)



/*

(
StudentId CHAR(4) PRIMARY KEY,
StudentName VARCHAR(50) NOT NULL,
InitialAmount NUMERIC(10,2) check (InitialAmount >10000) NOT NULL,
CourseName VARCHAR(50)
FOREIGN KEY REFERENCES Course(CourseName)
check(CourseName In ('Electrical Engineering','Electrical and Electronics Engineering',
'Mechanical Engineering','Civil Engineering','Computer Science','Information Technology',
'Electronics and Communication Engineering'))
)

*/
--inserting data into studentdetails

INSERT StudentDetails
VALUES('A101','Bal Krishna','11000','Mechanical Engineering'),
('A102','Humza Khan','50000','Electrical and Electronics Engineering')

INSERT StudentDetails
VALUES('A103','Narayan Murthy','110000','Information Technology'),
('A104','Alisha Singh','80000','Electronics and Communication Engineering')

--JOINING Student Details and respective course
SELECT sd.StudentName,sd.InitialAmount,c.PriceDetails,c.Duration,sd.CourseName FROM StudentDetails sd
JOIN Course c
ON sd.CourseName = c.CourseName
ORDER BY PriceDetails


/*CREATE TABLE ContactDetails
(
StudentID CHAR(4) FOREIGN KEY REFERENCES StudentDetails(StudentId),
EmailId VARCHAR(30) NOT NULL,
ContactNumber CHAR(10) NOT NULL,
StudentAddress VARCHAR(150) NOT NULL
)*/

--inserting info in contact details
INSERT ContactDetails
VALUES ('A101','BalKrishna@gmail.com','9988997667','45/A C-Block Ambala'),
('A102','HumzaKhan@gmail.com','9988127667','45/123 Gol Chakar D-Park Noida'),
('A103','NarayanMurthy@gmail.com','9981237667','plot 6 sector 23A Dehradun'),
('A104','AlishaSingh@gmail.com','9944337667','Plot 6 Chanakyapuri New Delhi')


--Joining Course details student details and contact details together--

SELECT sd.StudentName,sd.InitialAmount,c.PriceDetails,c.Duration,sd.CourseName,
cd.EmailId,cd.ContactNumber,cd.StudentAddress
FROM StudentDetails sd
JOIN Course c
ON sd.CourseName = c.CourseName
JOIN ContactDetails cd
ON sd.StudentId = cd.StudentId

INSERT CustomerDetails
VALUES('A101','Rupali Bind'),
('A102','Raj Nayak')



SELECT sd.StudentName,sd.InitialAmount,c.PriceDetails,c.Duration,sd.CourseName,
cd.EmailId,cd.ContactNumber,cd.StudentAddress,
cud.CustomerName
FROM StudentDetails sd
JOIN Course c
ON sd.CourseName = c.CourseName
JOIN ContactDetails cd
ON sd.StudentId = cd.StudentId
LEFT JOIN CustomerDetails cud
ON sd.StudentId = cud.StudentId




BEGIN TRANSACTION t2
   UPDATE CustomerDetails
   SET CustomerName = 'Divya Singh'
   WHERE StudentId = 'A102'
--COMMIT means that the transaction has been recorded to the log file
COMMIT TRANSACTION t2


ROLLBACK TRANSACTION t2




select * from Customer 
