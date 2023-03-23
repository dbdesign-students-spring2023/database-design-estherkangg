# Data Normalization and Entity-Relationship Diagramming  
   
  
## _Original Data Set_  
  
| assignment_id | student_id | due_date | professor | assignment_topic                | classroom | grade | relevant_reading    | professor_email   |
| :------------ | :--------- | :------- | :-------- | :------------------------------ | :-------- | :---- | :------------------ | :---------------- |
| 1             | 1          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 80    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 2             | 7          | 18.11.21 | Logston   | Single table queries            | 60FA 314  | 25    | Dümmlers Chapter 11 | e.logston@foo.edu |
| 1             | 4          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 75    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 5             | 2          | 05.05.21 | Logston   | Python and pandas               | 60FA 314  | 92    | Dümmlers Chapter 14 | e.logston@foo.edu |
| 4             | 2          | 04.07.21 | Nevarez   | Spreadsheet aggregate functions | WWH 201   | 65    | Zehnder Page 87     | i.nevarez@foo.edu |
| ...           | ...        | ...      | ...       | ...                             | ...       | ...   | ...                 | ...               |  
  
### Explanation  
  
The original data set is not compliant with 4NF's rules because it contains multi-valued dependencies. For example, the _assignment_topic_ column is dependent on the _assignment_id_ column, but it is also dependent on the _professor_ column. In other words, it fails to satisfy one of the assumptions that each course can be taught by multiple professors in different sections. As long as multi-valued dependencies like this exist, the data set fails to meet 4NF standards. 
  
  

## _4NF Tables_  
  

**Table 1: Courses**

course_id | course_name
------- | -------
1 | data normalization |
2 | single table queries |
3 | python and pandas |
4 | spreadsheet aggregate functions |  
  
Primary key: course_id  

**Table 2: Professors**  
    
professor_id | professor_name | email
---------|----------|---------
 1 | Melvin | l.melvin@foo.edu
 2 | Longston | e.longston@foo.edu
 3 | Nevarez | i.nevarez@foo.edu  
   
Primary key: professor_id  

**Table 3: Sections**  
  
section_id | course_id | professor_id | classroom
------- | ------- | ------- | -------
1 | 1 | 1 | WWH 101
2 | 2 | 2 | 60FA 314
3 | 3 | 2 | 60FA 314
4 | 4 | 3 | WWH 201  

Primary key: section_id  
Foreign keys: course_id, professor_id  


**Table 4: Assignments**  
  
assignment_id | section_id | assignment_topic | due_date | relevant reading |
------- | ------- | ------- | ------- | ------- |
1 | 1 | data normalization | 23.02.21 | deumlich chapter 3
2 | 2 | single table queries | 18.11.21 | dummlers chapter 11
3 | 3 | python and pandas | 05.05.21 | dummlers chapter 14
4 | 4 | spreadsheet aggregate functions | 04.07.21 | zehnder page 87 
  
Primary key: assignment_id  
Foreign key: section_id  

**Table 5: Students**
     
student_id | student_name
------- | -------
1 | john
2 | jane
3 | bob
4 | alice
5 | joe   

Primary key: student_id  

**Table 6: Grades**

assignment_id | student_id | grade
------- | ------- | -------
1 | 1 | 80
2 | 5 | 25
3 | 2 | 92
4 | 2 | 65

Primary key: assignment_id, student_id  
Foreign keys: assignment_id, student_id  

**Table 7: Readings**

reading_id | assignment_id | reading
------- | ------- | -------
1 | 1 | deumlich chapter 3
2 | 2 | dummlers chapter 11
3 | 3 | dummlers chapter 14
4 | 4 | zehnder page 87  

Primary key: reading_id  
Foreign key: assignment_id  
  
### Changes I Made & Why it's 4NF Compliant  
  
After multiple revisions, I have reached this final design, where I have eliminated the redundant data and achieved 4NF by splitting the original Assignments table into two tables, and the original Readings table into one table. I also added a new table for professors' assignments to satisfy the requirement that professors can give the same assignment to different sections of the same course, but with different due dates.  
  
This new tables meets all of the assumptions provided. It allows for courses to be taught by multiple professors in different sections, and for professors to teach multiple sections of the same course. Each section is associated with a specific classroom and professor, and different sections of the same course can meet in different classrooms. Professors give assignments with specific due dates and readings that are relevant to the assignments. They can give the same assignment to different sections of the same course with different due dates, and students complete assignments and receive grades. The new design also allows for the flexibility to have multiple rows of data in each table.  
  
### ER Diagram  
  
The changes in the table can also be seen in this entity-relationship diagram as follows:  
  

![Diagram](./images/entity.svg)  
  
_Worked with Justin Chu_


  
