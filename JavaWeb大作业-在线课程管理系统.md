# JavaWeb期末大作业-在线课程管理系统
## 需求分析和系统设计

## 数据库设计

- user(用户表)
``` Mysql
CREATE TABLE user (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,       -- 用户ID
    username VARCHAR(255) NOT NULL UNIQUE,       -- 用户名
    password VARCHAR(255) NOT NULL,              -- 密码
    email VARCHAR(255),                          -- 邮箱
    name VARCHAR(255),                           -- 姓名
    roleId BIGINT,                              -- 角色ID（外键关联到 role 表）
    CONSTRAINT fk_role FOREIGN KEY (roleId) REFERENCES role(id)  -- 外键关联角色表
);
INSERT INTO user (id, username, password, email, name, roleId) VALUES
(1, 'john_doe', 'pass123', 'john.doe@example.com', 'John Doe', 2),
(2, 'jane_smith', 'pass456', 'jane.smith@example.com', 'Jane Smith', 3),
(3, 'robert_brown', 'pass789', 'robert.b@example.com', 'Robert Brown', 2),
(4, 'emily_jones', 'passabc', 'emily.j@example.com', 'Emily Jones', 1);
```
![image](https://github.com/user-attachments/assets/6ddf03b2-4e8d-427f-a72c-cfd1131b2237)
- user表是核心表，用于存储系统中的所有用户的基本信息，与 role 表的外键关联（roleId），user 表能够实现用户角色的分类管理。

- student(学生表)
``` Mysql
CREATE TABLE student (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,       -- 学生ID
    userId BIGINT,                              -- 关联的用户ID（外键关联到 user 表）
    studentNumber VARCHAR(20) NOT NULL UNIQUE,   -- 学号
    major VARCHAR(255),                          -- 专业
    classId BIGINT,                              -- 班级ID（外键关联到 class 表）
    CONSTRAINT fk_user_student FOREIGN KEY (userId) REFERENCES user(id),  -- 外键关联到 user 表
    CONSTRAINT fk_class_student FOREIGN KEY (classId) REFERENCES `class`(id) -- 外键关联班级
);
ALTER TABLE student 
ADD COLUMN name VARCHAR(100) NOT NULL,
ADD COLUMN email VARCHAR(100) NOT NULL,
ADD COLUMN username VARCHAR(50) NOT NULL;
INSERT INTO student (id, userId, studentNumber, major, classId, name, email, username) VALUES
(1, 1, 'S1001', 'Computer Science', 1, 'John Doe', 'john.doe@example.com', 'john_doe'),
(2, 4, 'S1002', 'Electrical Eng.', 2, 'Emily Jones', 'emily.j@example.com', 'emily_jones');

```
![image](https://github.com/user-attachments/assets/4fea59ee-4ce0-4a7b-8a80-8a99048f5644)
- student 表存储学生的特定属性，与 user 表中的属性（如用户名、密码）进行区分，包括学号，专业，班级，这样可以更加细致地记录学生的信息。还与其他表有所联系。

- teacher(教师表)
``` Mysql
CREATE TABLE teacher (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,       -- 教师ID
    userId BIGINT,                              -- 关联的用户ID（外键关联到 user 表）
    teacherTitle VARCHAR(255),                   -- 职称
    teachingSubject VARCHAR(255),                -- 授课专业
    managedClassId BIGINT,                       -- 教师管理的班级ID（外键关联到 class 表）
    CONSTRAINT fk_user_teacher FOREIGN KEY (userId) REFERENCES user(id),  -- 外键关联到 user 表
    CONSTRAINT fk_class_teacher FOREIGN KEY (managedClassId) REFERENCES `class`(id) -- 外键关联班级
);
ALTER TABLE teacher
ADD COLUMN name VARCHAR(100) NOT NULL,
ADD COLUMN email VARCHAR(100) NOT NULL,
ADD COLUMN username VARCHAR(50) NOT NULL;
INSERT INTO teacher (id, userId, teacherTitle, teachingSubject, managedClassId, name, email, username) VALUES
(1, 2, 'Associate Prof.', 'Computer Science', 1, 'Jane Smith', 'jane.smith@example.com', 'jane_smith'),
(2, 3, 'Professor', 'Mathematics', 2, 'Robert Brown', 'robert.b@example.com', 'robert_brown');
```
![image](https://github.com/user-attachments/assets/fcf179ac-417d-4c55-a317-bb655017d472)
- 与学生表作用类似，与学生表相对应。

- class(班级表)
``` Mysql
CREATE TABLE class (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,       -- 班级ID
    name VARCHAR(255) NOT NULL UNIQUE,           -- 班级名称（如：计算机科学1班）
    major VARCHAR(255),                          -- 专业（如：计算机科学）
    year INT,                                    -- 入学年份
    teacherId BIGINT,                            -- 班级负责人（教师ID，外键关联到 user 表）
    CONSTRAINT fk_teacher_class FOREIGN KEY (teacherId) REFERENCES user(id)  -- 外键关联教师
);
INSERT INTO class (id, name, major, year, teacherId) VALUES
(1, 'CS Class 1', 'Computer Science', 2023, 2),
(2, 'EE Class 1', 'Electrical Eng.', 2023, 3);
```
![image](https://github.com/user-attachments/assets/c727856a-f8af-46c2-a926-9dca92d9ff3b)
- class表在系统中作为班级管理的核心，用于连接学生、教师和课程等模块，为教学管理提供支持

- role(角色表)
``` Mysql
CREATE TABLE role (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 角色ID
    name VARCHAR(255) NOT NULL UNIQUE             -- 角色名称（如：学生、教师、管理员）
);
INSERT INTO role (id, name) VALUES
(1, 'Student'),
(2, 'Teacher'),
(3, 'Admin');
```
![image](https://github.com/user-attachments/assets/e017d498-8ead-4b7d-9536-5fe9973b2f6b)
- 

- course(课程表)
``` Mysql
CREATE TABLE course (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 课程ID
    title VARCHAR(255) NOT NULL,                  -- 课程标题
    description TEXT,                             -- 课程描述
    teacherId BIGINT,                            -- 教师ID（外键关联到 user 表）
    CONSTRAINT fk_teacher FOREIGN KEY (teacherId) REFERENCES user(id)  -- 外键关联教师
);
INSERT INTO course (id, title, description, teacherId) VALUES
(1, 'Introduction to Java', 'Learn Java basics and object-oriented programming.', 2),
(2, 'Advanced Mathematics', 'Explore calculus, algebra, and geometry.', 3);
```
![image](https://github.com/user-attachments/assets/5d801bbc-c5d2-4a94-b657-8b254a213258)

- schedule(课程日程表)
``` Mysql
CREATE TABLE schedule (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 日程ID
    courseId BIGINT,                            -- 课程ID（外键关联到 course 表）
    dayOfWeek VARCHAR(20),                     -- 上课星期几（如：Monday, Tuesday）
    startTime VARCHAR(255),                             -- 上课开始时间
    endTime VARCHAR(255),                               -- 上课结束时间
    location VARCHAR(255),                       -- 上课地点
    CONSTRAINT fk_course_schedule FOREIGN KEY (courseId) REFERENCES course(id)  -- 外键关联课程
);
INSERT INTO schedule (id, courseId, dayOfWeek, startTime, endTime, location) VALUES
(1, 1, 'Monday', '09:00 AM', '11:00 AM', 'Room 101'),
(2, 2, 'Wednesday', '02:00 PM', '04:00 PM', 'Room 202');
```
![image](https://github.com/user-attachments/assets/b2426e1b-12f8-45de-b456-dceec97b245d)

- studentCourse（学生课程表）
``` Mysql
CREATE TABLE studentCourse (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,  -- 记录ID
    studentId BIGINT,                      -- 学生ID（外键关联到 user 表）
    courseId BIGINT,                       -- 课程ID（外键关联到 course 表）
    CONSTRAINT fk_student2 FOREIGN KEY (studentId) REFERENCES user(id),
    CONSTRAINT fk_course2 FOREIGN KEY (courseId) REFERENCES course(id)
);
INSERT INTO studentCourse (id, studentId, courseId) VALUES
(1, 1, 1),
(2, 2, 2);
```
![image](https://github.com/user-attachments/assets/c0d18bf0-9096-45af-98d9-47d4f8b90e61)

- student_details_view(学生信息细节视图)
``` Mysql
CREATE VIEW student_details_view AS
SELECT 
    s.id AS student_id,
    u.username AS username,
    CONCAT(u.name, ' (', u.email, ')') AS student_info,
    s.studentNumber AS student_number,
    s.major AS major,
    c.name AS class_name,
    c.major AS class_major,
    c.year AS enrollment_year
FROM 
    student s
JOIN 
    user u ON s.userId = u.id
JOIN 
    class c ON s.classId = c.id;
```
![image](https://github.com/user-attachments/assets/b53ce377-7841-4899-bf77-e65bda89b858)

- teacher_details_view(教师信息细节视图)
``` Mysql
 CREATE VIEW teacher_details_view AS
SELECT 
    t.id AS teacher_id,
    u.username AS username,
    CONCAT(u.name, ' (', u.email, ')') AS teacher_info,
    t.teacherTitle AS title,
    t.teachingSubject AS teaching_subject,
    c.name AS managed_class_name,
    c.major AS class_major
FROM 
    teacher t
JOIN 
    user u ON t.userId = u.id
LEFT JOIN 
    class c ON t.managedClassId = c.id;
```
![image](https://github.com/user-attachments/assets/edf42515-1526-4dd2-a774-23472a8786b9)

- course_details_view（课程信息细节视图）
``` Mysql
CREATE VIEW course_details_view AS
SELECT 
    c.id AS course_id,
    c.title AS course_title,
    c.description AS course_description,
    CONCAT(u.name, ' (', u.email, ')') AS teacher_info,
    s.dayOfWeek AS class_day,
    s.startTime AS class_start_time,
    s.endTime AS class_end_time,
    s.location AS class_location
FROM 
    course c
JOIN 
    user u ON c.teacherId = u.id
LEFT JOIN 
    schedule s ON c.id = s.courseId;
```
![image](https://github.com/user-attachments/assets/390023a1-4686-4203-b2cc-679c51497f36)

## 配置开发环境
- 本项目采用的IDE环境为IDEA2024，Mysql使用8.0版本，使用Jakarta进行开发
  
- 配置Mysql驱动，让项目能与Mysql连接
  ``` xml
   <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.0.33</version>
        </dependency>
  ```

- 配置lombok，以简化实体类的get和set操作
  ``` xml
   <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.34</version>
        </dependency>
  ```
- 配置servlet
    ``` xml
    <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
        </dependency>
    
    ```
- 添加DButils依赖
  ``` xml
  <dependency>
    <groupId>commons-dbutils</groupId>
    <artifactId>commons-dbutils</artifactId>
    <version>1.8.1</version>
  </dependency>
  ```

## 基本类的实现

### 为所需的数据库表建造实体类
- 首先在model软件包中，创建一个User实体类用于存放user表中的各种数据
  ``` Java
  package model;
  import lombok.Getter;
  import lombok.Setter;
  import java.util.Date;
  @Getter@Setter
  public class User {
    private Long id;

    private String username;

    private String password;

    private String email;

    private String name;

    private Long role_id;

    private Date created_at;

    private Date updated_at;
  }
  ```
- 其中role_id为外键要与role表关联，所以我们还需要创建一个Role实体类
  ``` Java
  package model;
  import lombok.Setter;
  import lombok.Getter;
  @Getter@Setter
  public class Role {

    private Long id;

    private String name;

  }
  ```
- 创建Course实体类
  ``` Java
  package model;
  import java.util.Date;
  import lombok.Getter;
  import lombok.Setter;
  @Getter@Setter
  public class Course {
    private Long id;

    private String title;

    private String description;

    private Long teacher_id; // 外键，关联到 User 表

    private Date created_at;

    private Date updated_at;
  }
  ```
- 创建Grade实体类
  ``` Java
  package model;

  import java.util.Date;
  import lombok.Setter;
  import lombok.Getter;
  @Setter@Getter
  public class Grade {

    private Long id;

    private Long student_id; // 外键，关联到 User 表

    private Long course_id;  // 外键，关联到 Course 表

    private Double score;

    private String term;

    private Date created_at;

    private Date updated_at;
  }

  ```
- 创建Schedule实体类
  ``` Java
   package model;
  import lombok.Setter;
  import lombok.Getter;
  import java.util.Date;
  @Setter@Getter
  public class schedule {
    private Long id;

    private  Long course_id;

    private String day_of_week;

    private String end_time;

    private String start_time;

    private String location;

    private Date created_at;

    private Date updated_at;
  }
  ```

## 实现用户注册和登录功能

### 注册操作时的数据操作代码
``` Java
package org.example.course_system;

import model.User;
import org.example.course_system.DatabaseUtils;
import java.sql.*;
//注册时，插入数据操作
public class UserDAO {
    public boolean registerUser(User user) throws SQLException {
        String sql = "INSERT INTO user (username, password, email, name, role_id) VALUES (?, ?, ?, ?, ?)";
        try (Connection conn = DatabaseUtils.getConnection();
             PreparedStatement st = conn.prepareStatement(sql)) {
            st.setString(1, user.getUsername());
            st.setString(2, user.getPassword());
            st.setString(3, user.getEmail());
            st.setString(4, user.getName());
            st.setLong(5, user.getRole_id());
            return st.executeUpdate() > 0;
        }catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    public User login(String username, String password) throws SQLException {
        String sql = "SELECT * FROM user WHERE username = ? AND password = ?";
        try (Connection conn = DatabaseUtils.getConnection();
             PreparedStatement st = conn.prepareStatement(sql)) {
            st.setString(1, username);
            st.setString(2, password);
            ResultSet rs = st.executeQuery();
            if (rs.next()) {
                return new User(rs.getLong("id"), rs.getString("username"), rs.getString("name"), rs.getLong("role_id"));
            }
            return null;
        }
    }
}
```
- 使用JDBC来实现与数据库的连接以及操作，首先实现的是注册时的插入操作，user里的构函数由lombok帮助我们生成
- 用查找的sql语句来搜索数据库中是否有该user的username和password，来实现登录操作
## 创建个人信息管理界面

## 开发课程创建和管理模块

## 实现课程内容上传功能

## 创建学生选课系统

## 实现成绩管理和查询功能

## 开发课程日程表功能


