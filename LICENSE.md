# This sql statement holds Customer Accounts and tracks,Name,Service address,Phone,Email,the customer's electricity utility,the customer's utility's alphanumeric account number, the current status of the account #
#The code runs on MySQL 5.5#

#Deliverable #1#
CREATE TABLE Customer_Accounts 
(id int UNIQUE NOT NULL,
Customer_name varchar(100) NOT NULL,
Service_address varchar(260) NOT NULL,
phone_num INTEGER,
email varchar(260),
customer_electricity_utility varchar(100) NOT NULL,
customers_account_number varchar(50) NOT NULL PRIMARY KEY,
account_status TEXT CHECK (account_status = "Pending" or "Rejected" or "Accepted" or "Closed")
);
 
INSERT INTO Customer_Accounts VALUES (1,"Davy","31 OLD BONIFANT ROAD","240547","sheri4_umbc.edu", "1234","2333334","pending");




#Deliverable #1: Table Structures, The Two tables below hold the uniques ID's of customers that enrolled , their names, market channel, and enrollment date in "Enrollment_Attempt"#
CREATE TABLE Enrollment_Attempt
(Enrollment_id int UNIQUE,
Customer_Attempt_Name TEXT(100) NOT NULL,
Marketing_Channel TEXT  NOT NULL CHECK (Marketing_Channel IN ("Mail" or "Telemarketing" or "Web")),
Enrollment_date DATE NOT NULL,
PRIMARY KEY(Enrollment_id));
#This table holds similar information as above excepts that this tracks customers that renrolled#

CREATE TABLE Renrollment_Attempt
(Customer_id int UNIQUE NOT NULL,
Renrollment_id int NOT NULL,
Customer_Attempt_Name TEXT(100) NOT NULL,
Marketing_Channel TEXT  NOT NULL CHECK (Marketing_Channel IN ("Mail" or "Telemarketing" or "Web")),
Renrollment_date DATE NOT NULL,
PRIMARY KEY(Customer_id),
FOREIGN KEY(Renrollment_id)REFERENCES Enrollment_Attempt(Enrollment_id));

INSERT INTO Enrollment_Attempt VALUES(1,"SHERIFF TAIWO","Mail","2015-1-10");
INSERT INTO Renrollment_Attempt VALUES(1,1,"SHERIFF TAIWO","Mail","2015-1-10");



QUERIES 
SELECT * FROM Enrollment_Attempt;
SELECT * FROM Renrollment_Attempt;
SELECT * FROM Customer_Accounts 

#deliverable #2#
SELECT Enrollment_Attempt.Enrollment_id, Enrollment_Attempt.Enrollment_date, Enrollment_Attempt.Marketing_Channel, Renrollment_Attempt.Renrollment_date,Renrollment_Attempt.Marketing_Channel
Inner join Renrollment_Attempt

#deliverable #3#
SELECT Enrollment_date, Marketing_Channel, COUNT(*) 
FROM Enrollment_Attempt
Group By Enrollment_date ;

#deliverable #4#
SELECT customer_electricity_utility FROM Customer_Accounts;
SELECT Marketing_channel, COUNT(*) FROM Enrollment_Attempt;
