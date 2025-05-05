# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
University Database

## ER Diagram:

![Screenshot (161)](https://github.com/user-attachments/assets/3d6efac2-a00b-4234-b60e-f9784807d39f)


## Entities and Attributes:
# Student:

 1. StudentID (Primary Key)
    
 2. FirstName
 
 3. Admission no
    
 4. DateOfBirth
 
 5. Email
 
 6. PhoneNumber
  
 7. gender
 
 8. Address


# course:

 1. CourseID (Primary Key)
   
 2. CourseName

 3.Credits

 4. DepartmentID


# Instructor:

 1.instructor id
 
 2.Name
 
 3.phoneno
 
 4.department
 
 5.email



 # class:
 
 1.class id
 
 2.year 
 
 3.schedule
 
 4.semester
 
# department:
 
 1.department id 
 
 2.department name
 
 3.head of the department
 
## Relationships and Constraints:
 Student- course:
 
 1. Relationship-enrollment
    
 2. A student can enroll to many course.

 course-instructor:
 
 1.relationship "faculty"
 
 2. instructor can teach one course.

course-department:

1.relationship-"offered"

2. A course isoffered by one department.

3. A department can offer multiple courses.

Class- Course

 1. "teaches" Relationship
   
 2. A class is based on one course.
    
 3. A course can have multiple classes.
  
## Extension (Prerequisite / Billing):
- Explain how you modeled prerequisites or billing.

## Design Choices:
Brief explanation of why you chose certain entities, relationships, and assumptions

## RESULT:
Thus,the Er diagram was suucessfully designed.
