# my-sql-practice-syntax
my sql practice syntax


show databases;
use office;
create table  department(deptno int not null ,dname varchar (50) not null, location varchar (50) not null );
insert into department values (10,"accounting","new york"),(20,"research","daallas"),(30,"sales","chicago"),(40,"operations","boston");
select * from department;
update department set location  = "dallas" where deptno = 20;

alter table department add primary key (deptno);
desc department;

create table emp(empno int unique  not null ,ename varchar (20) not null,job varchar (20) not null,mgr varchar (10),hiredate datetime ,
sal float (8,2),comm varchar (6),deptno int (6),grade int ,foreign key (deptno) references department(deptno));
desc emp;
alter table emp modify column empno int(4)UNSIGNED ZEROFILL unique not null;
alter table emp modify column hiredate date;
update emp set job = "salesman"  where job = "saleman";
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES("7369","smith","clerk","7902","1980-12-17","800",20,2);
insert into emp value (7499,"allen","salesman",7698,"1981-02-20",1600,300,30,1);
insert into emp value( 7521,"ward","saleman",7698,"1981-02-22",1250,500,30,1);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7566,'jones','manager',7839,'1981-04-02',2975,20,5);
insert into emp values (7654,"martin","salesman",7698,"1981-09-28",1250,1400,30,1);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7698,"blake","manager",7839,"1981-05-01",2850,30,4);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7782,"clerk",'manager',7839,"1981-06-09",2450,10,4);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7788,'scott','analyst',7566,"1982-12-09",3000,20,3);
insert into emp (EMPNO, ENAME, JOB,HIREDATE,SAL,DEPTNO,grade) VALUES (7839,'king','president','1981-11-17',5000,10,5);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,comm,DEPTNO,grade) VALUES (7844,'turner','salesman',7698,"1981-09-08",1500,0,30,1);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7876,'adams','clerk',7788,"1983-01-03",1100,20,2);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7900,'james','clerk',7698,'1981-12-03',950,30,2);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7902,'ford','analyst',7566,'1981-12-03',3000,20,3);
insert into emp (EMPNO, ENAME, JOB,MGR,HIREDATE,SAL,DEPTNO,grade) VALUES (7934,'miller','clerk',7782,"1982-01-23",1300,10,2);
select * from emp;

#1. Display all the information of the emp table?
select * from emp;

#2. Display unique jobs from emp table?
select distinct job from emp;

#3.list the emps in the asc order of thier salaries?
select * from emp order by sal asc;

#4.list the detail of the emps in asc order of the dptnos and desc of jobs ?
select * from emp order by deptno asc ,job desc;

#5. display all the unique job groups in the descending order?
select distinct job from emp order by job desc;

#6.Display all the details of all "mgrs"?
select * from emp where empno in (select mgr from emp);

#7.list the emps who joined before 1981?
select * from emp where hiredate <"1981-01-01";

#8 list the empno,ename,sal,daily sal of all emps  in the emps in the asc order of annsal?
select empno,ename,sal,sal/30,12*sal annsal from emp order by annsal asc;

#9. display the empno,ename,job,hiredate ,exp of all mgrs?
SELECT empno, ename, job, hiredate, TIMESTAMPDIFF(MONTH, hiredate, CURDATE()) AS exp
FROM emp
WHERE empno IN (SELECT DISTINCT mgr FROM emp WHERE mgr IS NOT NULL);

#10 list the empno,ename,sal,exp of all emps working for mgr 7369.
select empno,ename,sal,Timestampdiff (month,hiredate,curdate())as exp from emp where mgr = 7369;

#11 display all the details of the emps whose comm. is more than their sal?
select * from emp where comm>sal;

#12 list the emps in the asc order of designations of those joined after the second half of 1981?
select * from emp where hiredate >"1981-07-01" order by job asc;

#13 list the emps along with their exp and daily sal is more than 100 ?
select * from emp  where (sal/30)>100  ;

#14 list the emps who are either 'clerk' or 'analyst' in the desc order?
SELECT *
FROM emp
WHERE job = 'clerk' OR job = 'analyst'
ORDER BY job DESC;

#15 list the emps who join on  "01-05-1981","3-12-1981",'17-12-1981','19-01-1980' in asc order of seniority.
select * from emp where hiredate in ("1981-05-01",'1981-12-03','1981-12-17','1980-01-19')order by hiredate asc;

#16 list the emp who are working for the deptno 10 or 20?
select * from emp where deptno ='10' or deptno = '20';

#17 list the emps who are join in year 1981?
select * from emp where hiredate between "1981-01-01" and "1981-12-31";

#18 list the emps who are joined in the month oh aug 1980?
select * from emp where hiredate between "1980-08-01" and "1980-08-31"; 

#19 list the emps who annual sal ranging from 22000 and 45000?
select * from emp where 12*sal between 22000 and 45000;

#20 list the emp who have five characters in their names ?
select * from emp where length(ename)=5;

#21 list the enames those are starting with 's' and with five characters?
select * from emp where ename like "s%" and length(ename) = 5;

#22 list the emps those are having four chars and third character must be "r"?
select * from emp where ename like "__r%" and length(ename)=4;

#23 list the five character names starting with "s" and ending with "h"?
select * from emp where ename like "s%h" and length(ename) = 5;

#24 list the emps who joined in january?
SELECT * FROM emp WHERE MONTH(hiredate) = 1;

#25 list the emps who joined in the month of which second character is "a"?


#26 list the emps whose sal is four digit number ending with zero?
select * from emp where length(sal) = 4 and sal like "%0";

#27 list the emps whose name having a character set "ll" together?
select * from emp where ename like "%ll%" ;

#28 list the emps those who joined in 80s?
select * from emp where hiredate between ("1980-01-01") and ("1980-12-31");

#29 list the emps who does not belong to deptno 20?
select * from emp where deptno not in (20);

#30 list all the emps except "president" & "mgr" in asc order of salaries?
select * from emp where job not in ("president" , "manager") order by sal asc;

#31 list all the emps who joined before or after 1981?
select * from emp where year(hiredate) not in ("1981");

#32 list the emps whose empno not starting with digit  78?
select * from emp where empno not like "78%";

#33 list the emps  who are working under "mgr"?

#34 list the emps who joined in any year but not belongs to the month of march?
SELECT * FROM emp WHERE EXTRACT(MONTH FROM hiredate) <> 3;

#35 list all the clerks of depno 20?
select * from emp where job = "clerk" and deptno = "20";

#36 list the emps of depno 30 or 10 joined in the year 1981?
select * from emp where (deptno = "30" or deptno ="10") and year(hiredate) = 1981; 

#37 display the details of "smith"?
select * from emp where ename like "smith";

#38 display the location of smith?
select location from emp e, department d where e.ename = "smith" and e.deptno = d.deptno;

#39 list the total information of emp table along with dname and location of all the emps working under "accounting" & "research" in the asc deptno?
select * from emp e,department d where (d.dname ="accounting" or d.dname =  "research")and e.deptno = d.deptno order by e.deptno asc;

#40 list the empno, ename,sal,dname,of all the "mgr" and "analyst" working in new york, dallas with an exp more than 7 years without
# receiving the comm asc order of location?

# 41 display the empno,ename,sal,dname,location,deptno,job of all emps working at cicago or working for accounting dept with ann sal>28000,
# but the sal should not be = 3000 or 2800 who doesn't belongs to the mgr and whose no is having a digit '7' or '8' in 3rd in 3rd position in 
# the asc order of deptno and desc of job?

#42 display the total information of the emps along with grades in the asc order?
select * from emp order by grade asc;

#43 list all the grade 2 and grade 3 emps?
select * from emp where grade = 2 or grade = 3;

#44 display all grade 4,5 analyst and mgr?
SELECT * FROM emp WHERE (grade = 4 OR grade = 5) AND (job = 'analyst' OR job = 'manager');

#45 list the empno, ename,sal dname,grade ,exp and annual salary of emps working for dept 10 or 20?

#46 

#47 list the details of the depts along with empno, ename or without the emps?
SELECT *  FROM emp e LEFT JOIN department d ON e.deptno = d.deptno;

#48 list the details of the emps whose salaries more than the employee blake?
select * from emp where sal > (select sal from emp where ename = "blake") ;

#49 list the emps whose jobs are same as allen?
select * from emp where job = (select job from emp where ename = "allen");

#50 list the emps who are senior to king ?
select * from emp where hiredate >(select hiredate from emp where ename = 'king');

#51 list the emps who are senior to their manager?
select * from emp where hiredate <(select hiredate from emp where job = "manager");

#52 list the emps of deptno 20 whose jobs are same as deptno 10?
SELECT e.* FROM emp e WHERE e.deptno = 20 AND e.job IN (SELECT DISTINCT d1.job FROM emp d1 JOIN emp d2 ON d1.job = d2.job
WHERE d1.deptno = 10 AND d2.deptno = 10);

#53 list the emp whose sal is same as ford or smith in desc order of sal?
select * from emp where sal in (select sal from emp where (ename = "smith" or ename = "ford")) order by sal desc;

#54 list the emps whose jobs are same as miller or sal is more than allen?
select * from emp where job = (select job from emp where ename = "miller") or sal>(select sal from emp where ename = "allen");

#55 list  the emps whose sal is > the total remuneration of the salesman?
SELECT * 
FROM emp 
WHERE sal > (
  SELECT SUM(IFNULL(comm, sal + COALESCE(comm, 0)))
  FROM emp
  WHERE job = 'salesman'
);

#56 list the emp who are senior to blake working at chicago & boston?
select * from emp e, department d where d.location in ('chicago','boston') and e.deptno = d.deptno and e.hiredate 
<(select e.hiredate from emp e where e.ename ="blake");

#57 list the emps of grade 3,4 belongs to the dept accounting and research whose sal is more than smith in the asc order of exp?

SELECT * 
FROM emp e
WHERE e.deptno IN (
  SELECT d.deptno
  FROM department d
  WHERE d.dname IN ('accounting', 'research')
)
AND e.sal > (
  SELECT sal
  FROM emp
  WHERE ename = 'allen'
)
AND e.hiredate < (
  SELECT hiredate
  FROM emp
  WHERE ename = 'smith'
)
AND e.grade IN (3, 4);

#58 list the emps whose jobs are same as smith or allen.
select * from emp where job in (select job from emp where ename in ('smith','allen'));

#60 any jobs of deptno 10 those that are not found in deptno 20?
select e.job from emp e where e.deptno = 10 and e.job not in (select job from emp where deptno = 20);

#62 find the highest sal of emp table ?
select max(sal)from emp;

#63 find details of highest paid employee? 
select * from emp where sal in (select max(sal) from emp);

#64 find the highest paid employee of sales department?
select * from emp where sal in (select max(sal) from emp where deptno in (select d.deptno from department d where d.dname = "sales"));

#65 list the most recently hired emp of grade3 belongs to location chicago?
SELECT empno, ename, hiredate
FROM emp
WHERE grade = 3 AND deptno IN (SELECT deptno FROM department WHERE location = 'Chicago')
ORDER BY hiredate DESC
LIMIT 1;

#66 list the employee who are senior to most recently hired employee working under king?
select * from emp where hiredate < (select max(hiredate) from emp where mgr in (select empno from emp where ename = "king"));

#67 

#68 list the details of the senior employee belongs to 1981?
select * from emp where hiredate in (select min(hiredate) from emp where year(hiredate) = "1981");

#69 list the employees who joined in 1981 with the job same as the most senior person of the year 1981?
SELECT * FROM emp WHERE job IN (SELECT job FROM emp WHERE hiredate IN (SELECT MIN(hiredate)FROM emp WHERE YEAR(hiredate) = 1981));

#70 list the most senior employ working under the king and grade is more than 3?
SELECT *
FROM emp
WHERE mgr = 'king' AND grade > 3
ORDER BY hiredate ASC
LIMIT 1;

#71 find the total sal given to the manager?
select sum(sal) from emp where job = "manager";
select sum(sal) from emp where empno in (select mgr from emp);

# 72 find the total annual sal to distribut job wise in the year 1981?
select job ,sum(12*sal)from emp where year(hiredate) = "1981" group by job;

# 73 display total sal employee belonging to grade 3?



#74 display the avg salaries of all the clerk?
select avg(sal) from emp where job = "clerk";

#75 list the employee in dept 20 whose sal is > the average sal of dept 10 emps?
select * from emp where deptno = 20 and sal >(select avg(sal) from emp where deptno = 10);

#76 display the number of employee for each job group deptno wise?
select deptno ,job,count(*) from emp group by deptno,job; 

#77 list the manager and the number of employees working for those mgrs in the ascending mgrno?
select w.mgr,count(*) from emp w,emp m where w.mgr = m.empno group by w.mgr order by w.mgr asc;

#78 list the department, detail where at least two emps are working ?
select deptno , count(*) from emp group by deptno having count(*) >=2;

#79 dispaly the grade, number of emps and max sal of each grade?
select grade, count(*) ,max(sal) from emp e ;

# 80 display dname,grade ,no of emps where at least two emps are clerks ?
SELECT d.dname, e.grade, COUNT(*) AS num_of_emps FROM department d JOIN emp e ON d.deptno = e.deptno WHERE e.job = 'clerk'
GROUP BY d.dname, e.grade HAVING COUNT(*) >= 2;

#81 list the details of the department where maximun number of emps are working?
SELECT * FROM departmentn WHERE deptno IN (SELECT deptno FROM emp GROUP BY deptno HAVING COUNT(*) = (SELECT MAX(emp_count)
FROM (SELECT COUNT(*) as emp_count FROM emp GROUP BY deptno) AS dept_counts));

#82 dispaly the emp whose manager name is jones?
select * from emp where mgr in (select empno from emp  where ename = "jones");

#83 list the employees whose salary is more than 3000 after giving 20% increment?
select * from emp where (1.2*sal) >3000;

#84 list the emps with dept names?
select e.empno, e.ename,e.job,e.mgr,e.hiredate,e.sal,e.sal,e.comm,e.deptno,d.dname from emp e ,department d where e.deptno = d.deptno;

#85 list the emps who are not working in sales dept?
SELECT emp.empno, emp.ename, emp.job, emp.deptno FROM emp LEFT JOIN department ON emp.deptno = department.deptno
WHERE department.dname != 'Sales' OR department.dname IS NULL;

#86 list the emps name, dept, sal and comm.for those salary is between 2000 and 5000 while location is chicago?
select e.ename,e.deptno,e.sal,e.comm from emp e,department d where e.deptno = d.deptno and d.location ="chicago" and e.sal between 2000 and 5000;

#87 list the emps whose sal is greater than his managers salary?
select * from emp e,emp m where e.mgr = m.empno and e.sal>m.sal;

#88 list the grade, emp name for the deptno 10 or deptno 30 but sal grade is not 4 while they joined the company before "31-dec-1982"?
SELECT emp.grade, emp.ename
FROM emp
JOIN department ON emp.deptno = department.deptno
WHERE (emp.deptno = 10 OR emp.deptno = 30)
  AND emp.grade <> 4
  AND emp.hiredate < '1982-12-31';
