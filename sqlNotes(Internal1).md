# 1 Company DB.
dept number, dept name, location, est date, total sal

// having clause
Q1) Retrieve dept's name having salary greater than 3k (select deptname, sum(sal) from department group by deptname having sum(sal) > 3k);
### group by
select location from department group by location (show you locations)
### order by
select deptname from department order by deptname (civil, ise, cse etc)

// aggregate commands
Q2) Count and display the number of department's whose salary are above 4k
select count(sal) from departments where sal > 4k;
select max(sal), min(sal), avg(sal), from department;

// in clause
Q3) Retrieve department details where deptno in (1,3,5)
select * from department where deptno in (1,3,5); (shows deptno 1 3 5 data)

### any clause
select sal from department where sal > any (select sal from department where deptname = 'ise'); {shows all salary except 1 ise(lowest)}

### all clause
select sal from department where sal > all (select sal from department where deptname = 'ise');  {shows all except ise completely}


# 2 Hospital DB.
doctor id, doctor name, hospital number, salary, years of exp, speciality

// basic queries
### displaying number of doctors in same speciality.
select count(did), speciality from doctor 
group by speciality having count(did) > 1; [COUNT more than 1 -> should be clubbed together] # answer

### order by
select docName from doctor order by docName desc;

### group by
select speciality from doctor groupy by speciality; (cardio, neuro, obgyn, sr nurse) [NOT COUNT]

// all
select * from doctor where did > all (select did from doctor where speciality = 'neuro'); prints 4 5 6

### any
select * from doctor where did > any (select did from doctor where speciality = 'neuro'); prints 2 3 4 5 6 (skips 1)


# 3 College database.
faculty id, faculty name, designation, salary, years of exp, subject name, department number

### order by 
select * from faculty order by fname desc;

### group by + having

select count(yearsOfExp) from faculty group by yearsOfExp having yearsOfExp = 2;

### in
select * from faculty where deptNo in (4,2);

### any
select fname from faculty where salary > any (select salary from faculty where yearsOfExp = 2); // prints all except the lowest val of yearsOfExp = 2

### all
select fname from faculty where salary > all (select salary from faculty where yearsOfExp = 2); // prints all except yearsOfExp = 2 salaries.

# 4 Train DB.
Train number, train name, soruce, destination, regularity, departure, farePer50KM

### update
update train set regularity = 'no' where trainNumber = 5;

### having
select trainName, sum(fare) from train group by trainName having sum(fare) > 1600; // shows name of the trains whose fairs are > 1.6k.

### any
select trainName from train where fare > any (select fare from train where departure = 7.56);

### all
select trainName from train where fare > all (select fare from train where departure = 7.56);

# 5 Patient DB.
patient id, patient name, age, gender, disease, doctor name, hospital number, fees amount.

Q1 -> retrieve patient's name having fare greater than 500
select patientName, sum(fair) from patient group by having sum(fair) > 500;

Q2 -> count and display number of patient's whose age are above 40.
select count(age) from patient where age >= 40; // where can't be used which aggregate commands, having should be used.

### any
select patientName from patient where fare > ANY (select fare from patient where gender = 'female');

### all
select patientName from patient where fare > ALL (select fare from patient where gender = 'female');

# 6 Employee DB.
employee id, employee name, age, designation, dept, address, salary.

Q1 -> Retrieve name of employee whose salary is greater than salary of all the employees in dept no 11
select empName from employee where salary > ALL(select salary from employee where deptNo = 11);

## MUST
Q2 -> Retrieve name of employee who works for more than one department
select count(empID), empName from employee group by empName having count(empID) > 1 order by empName; // IMPORTANT.

# 7 Student DB.

usn, name, age, dept, address, fee.

11 		abc             26 	    ise       Bengaluru       10000
12 		def             27 	    cse       mangaluru       20000
13 		mno             28      ece       mysuru          30000
14 		xyz             28      ece       mysuru          30000
15 		xyz1            29      ise       mysuru          30000

Q1 -> retrieve name of student who belongs to more than one dept.
select count(usn), department from students group by department having count(usn) > 1 order by department;

COUNT(USN)     DEP
----------     ----
         2 		ece
         2 		ise

Q2 -> Retrieve name of student who is paying more fee than ISE department students.
select name from students where fee > ANY (select fee from students where department = 'ise');

Q3 -> Retrieve name of student who is paying more fee than cse department students.
select name from students where fee > ALL (select fee from students where department = 'cse');

## random
select * from student4 where usn in (10,11,12);

       USN NAME       AGE      DEP   ADDRESS           FEE
---------- ------- ----------  ---- ----------    --------
        11  abc       26 	   ise    Bengaluru       10000
        12  def       27       cse    Mangaluru       20000
