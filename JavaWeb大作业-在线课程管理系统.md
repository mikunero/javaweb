# JavaWeb期末大作业-在线课程管理系统

## 用户手册
### 系统概述
- JavaWeb 在线课程管理系统是一款为学校或教育机构设计的在线教学管理平台，旨在方便教师管理课程、学生学习课程以及管理员进行系统管理和数据维护。本系统提供了丰富的功能，包括用户注册登录、课程管理、学生选课、课程日程安排、学生信息管理、教师信息管理等，同时支持多种用户角色（学生、教师、管理员），每个角色拥有不同的操作权限和功能界面。
### 注册与登录
- 注册
 - 打开系统登录页面，点击 “注册” 链接，进入注册页面。
 - 在注册页面中，填写用户名、密码、邮箱、姓名和身份（角色）等信息。用户名和密码为必填项，姓名应填写真实姓名。身份（角色）下拉框中提供了 “学生”“教师”“管理员” 三个选项，请根据实际情况选择。
 - 填写完成后，点击 “注册” 按钮。系统将对输入信息进行校验，如果信息填写不完整或不符合要求，将弹出相应的提示信息。例如，如果用户名已存在，系统会提示 “用户名已被注册，请重新选择”；如果密码过于简单，系统会提示 “密码强度不够，请重新设置”。
 - 注册成功后，系统将提示 “注册成功！请登录。”，并自动跳转到登录页面
- 登录
 - 在登录页面，输入已注册的用户名和密码，并选择对应的角色（学生、教师或管理员）。用户名和密码区分大小写。
 - 点击 “登录” 按钮，系统将验证用户身份信息。如果用户名、密码或角色不匹配，系统将提示 “用户名、密码或角色不匹配”。
 - 登录成功后，系统将根据用户角色跳转到相应的主页面。 
### 学生用户操作
- 学生主界面
 - 登录成功后，学生将进入学生主界面。主界面分为左侧导航栏和右侧内容区域。
 - 左侧导航栏包含 “课程表查看” 和 “退出登录” 两个功能链接。
 - 右侧内容区域显示欢迎语 “欢迎来到学生页面”，并提示学生选择左侧菜单中的功能。
- 课程表查看
 - 点击左侧导航栏中的 “课程表查看” 链接，进入课程表页面。
在课程表页面，学生需要输入自己的学生 ID，然后点击 “加载课程表” 按钮。
 - 如果学生ID输入正确且系统中存在该学生的课程安排，系统将从后端获取课程信息并展示在表格中。表格包含课程名称、课程描述、星期几、开始时间、结束时间、上课地点和教师等列。
 - 如果学生ID输入错误，系统将提示相应的错误信息，如 “请输入正确的学生ID”。
### 教师用户操作
- 教师主界面
 - 教师登录成功后，进入教师主界面。该界面同样由左侧导航栏和右侧内容区域组成。
 - 左侧导航栏提供了 “学生课程表查看”“课程管理与创建” 和 “退出登录” 三个功能链接。
 - 右侧内容区域显示欢迎语 “欢迎来到教师页面”，引导教师选择功能操作。
- 学生课程表查看
 - 点击 “学生课程表查看” 链接，教师可以查看所管理班级学生的课程安排情况。系统将展示学生的课程信息列表，包括课程名称、课程描述、星期几、开始时间、结束时间、上课地点和授课教师等。教师可以通过该功能了解学生的学习进度和课程分布，以便进行教学管理和辅导。
- 课程管理与创建
 - 点击 “课程管理与创建” 链接，进入课程管理页面。该页面包含 “添加新课程” 表单和 “所有课程” 列表展示区。
 - 在 “添加新课程” 表单中，教师需要填写课程标题和课程描述。课程标题和描述应准确反映课程内容。
 - 填写完成后，点击 “添加课程” 按钮。系统将向后端发送添加课程请求，添加成功后将提示 “课程添加成功”，并自动更新课程列表展示区；添加失败将提示 “添加课程失败”。
 - 在课程列表展示区，系统以表格形式展示所有课程信息，包括课程标题、课程描述等。教师可以在此查看已创建课程的详细信息。
### 管理员用户操作
- 管理员主界面
 - 管理员登录后进入管理员主界面，其布局与教师和学生主界面类似，左侧导航栏包含 “课程表查看”“教师信息查看”“学生信息查看” 和 “退出登录” 功能链接，右侧显示欢迎语和操作提示。
- 课程表查看
 -  操作方式与学生课程表查看类似，管理员可以查看系统中所有课程的安排情况，便于进行课程资源管理和调度。
- 教师信息查看
 - 点击 “教师信息查看” 链接，进入教师信息管理页面。该页面包括 “添加教师” 表单和 “教师列表” 展示区。
 - 在 “添加教师” 表单中，管理员需要填写用户 ID、职称、授课专业、管理班级 ID、姓名、邮箱和用户名等信息。其中用户 ID、职称、授课专业、管理班级 ID、姓名、邮箱和用户名必填。
 - 填写完成后，点击 “提交” 按钮。系统将根据输入信息添加教师记录，添加成功提示 “教师添加成功”，失败提示 “添加教师失败”。
 - 系统在教师列表展示区以表格形式展示所有教师信息，包括教师 ID、用户 ID、职称、授课专业、管理班级 ID、姓名、邮箱和用户名等列。管理员可以查看教师详细信息，并通过点击 “删除” 按钮删除教师记录。删除操作需谨慎，系统会提示确认信息，删除成功提示 “教师删除成功”，失败提示 “删除教师失败”。
- 学生信息查看
 - 点击 “学生信息查看” 链接，进入学生信息管理页面。该页面布局与教师信息管理页面类似，包含 “添加学生” 表单和 “学生列表” 展示区。
 - 在 “添加学生” 表单中，填写学号、专业、班级 ID、姓名、邮箱和用户名等必填信息。
 - 点击 “添加学生” 按钮，系统处理添加请求，成功提示 “学生添加成功”，失败提示 “添加学生失败”。
- 学生列表以表格形式展示学生信息，包括学号、姓名、邮箱、用户名、专业、班级 ID 等列。管理员可以查看学生详细信息，并通过点击 “删除” 按钮删除学生记录。删除操作需确认，成功提示 “学生删除成功”，失败提示 “删除学生失败”。
### 注意事项
- 请妥善保管好您的用户名和密码，不要将其透露给他人，以防账户被盗用。
- 在进行重要操作（如选课、添加课程、删除教师或学生信息等）前，请仔细核对输入信息，避免因误操作导致数据错误或丢失。
- 如果在使用过程中遇到任何问题或发现系统漏洞，请及时联系系统管理员或技术支持人员，我们将竭诚为您服务。

   
## 数据库设计（为统一设置，数据库插入的文字数据均为英文）
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
- 核心表之一，用于决定登录和注册用户的身份信息。

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
- 用于填写课程信息的基础信息，同时与教师表相关联。 

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
- 关于上课日程的信息，与课程表相关联。

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
- 该表是连接学生用户表和课程表的一个中间表，用于连接两个表使用。

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
-  该视图主要展示学生的相关信息，包括个人信息和学籍信息。

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
- 该视图的功能与学生细节信息是视图类似，主要记录教师的各类信息。
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
- 该视图主要展示了与课程相关的各种信息。

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
- 配置servlet，制造servlet环境
    ``` xml
    <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
        </dependency>
    
    ```
- 添加json相关依赖，用于传输文字类信息
  ``` xml
   <!-- https://mvnrepository.com/artifact/org.json/json -->
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20240303</version>
        </dependency>
  ```

## 基本类的实现

### 为所需的数据库表建造实体类
- 首先在model软件包中，创建一个User实体类用于存放user表中的各种数据，同时创建一个User方法，用于注册用户时使用
  ``` Java
  package org.example.course_system.model;
  import lombok.Getter;
  import lombok.Setter;
 
  @Getter@Setter
  public class User {
    private long id;

    private String username;

    private String password;

    private String email;

    private String name;

    private long roleId;



    public User(String username, String password, String email, String name, long roleId) {
        this.username = username;
        this.password = password;
        this.email = email;
        this.name = name;
        this.roleId = roleId;
    }


  }
  ```
- 其中role_id为外键要与role表关联，所以我们还需要创建一个Role实体类
  ``` Java
  package org.example.course_system.model;
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
  package org.example.course_system.model;
  import lombok.Getter;
  import lombok.Setter;
  @Getter@Setter
  public class Course {
    private long id;
    private String title;
    private String description;
    private long teacherId;
  }


  ```
- 创建Schedule实体类，包含该表的相关信息，同时给出一个创建日程表的方法
  ``` Java
  package org.example.course_system.model;
  import lombok.Setter;
  import lombok.Getter;

  @Setter@Getter
  public class schedule {
    private Long id;

    private  Long courseId;

    private String dayOfWeek;

    private String endTime;

    private String startTime;

    private String location;

    public schedule(long id, long courseId, String dayOfWeek, String startTime, String endTime, String location) {
        this.id = id;
        this.courseId = courseId;
        this.dayOfWeek = dayOfWeek;
        this.startTime = startTime;
        this.endTime = endTime;
        this.location = location;
    }

  }
  ```
- 创建student类，包含学生表的相关信息,同时给出一个无参的构造方法，用于后续的使用
``` Java
package org.example.course_system.model;
import lombok.Setter;
import lombok.Getter;

@Setter@Getter
public class Student {

    private long id;
    private String studentNumber;
    private String major;
    private long classId;
    private String name;
    private String email;
    private String username;



    public Student() {
    }
}

```
- 创建一个teacher实体类，包含教师表的各类信息
  ``` Java
  package org.example.course_system.model;
  import lombok.Getter;
  import lombok.Setter;
  @Getter@Setter

  public class Teacher {
    private long id;              
    private long userId;          
    private String teacherTitle;  
    private String teachingSubject; 
    private long managedClassId;  
    private String name;
    private String email;
    private String username;
  }
  ```
- 创建一个studentCourse实体类，还设置了一个通过学生和课程id来构造studentCourse类的方法·
  ``` Java
  package org.example.course_system.model;
  import lombok.Setter;
  import lombok.Getter;
  @Getter@Setter
  public class StudentCourse {
    private long id;
    private long studentId;
    private long courseId;

    //通过学生ID和课程ID构造StudentCourse
    public StudentCourse(long studentId, long courseId) {
        this.studentId = studentId;
        this.courseId = courseId;
    }
    
  }
  ```
  - 创建CourseSchedule实体类
    ``` Java
    package org.example.course_system.model;

    import lombok.Getter;
    import lombok.Setter;

    @Getter
    @Setter
    public class CourseSchedule {
    private String courseTitle;
    private String description;
    private String dayOfWeek;
    private String startTime;
    private String endTime;
    private String location;
    private String teacherName;

    // CourseSchedule 构造方法，初始化所有属性
    public CourseSchedule(String courseTitle, String description, String dayOfWeek,
                          String startTime, String endTime, String location, String teacherName) {
        this.courseTitle = courseTitle;
        this.description = description;
        this.dayOfWeek = dayOfWeek;
        this.startTime = startTime;
        this.endTime = endTime;
        this.location = location;
        this.teacherName = teacherName;
    }
    }
    ```
## 数据库连接类
- DBUtil数据库连接类
``` Java
package org.example.course_system.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DBUtil {
    private static final String URL = "jdbc:mysql://localhost:3306/onlinecoursemanagementsystem?serverTimezone=GMT&characterEncoding=UTF-8";
    private static final String USER = "root";
    private static final String PASSWORD = "20030530";

    static {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver"); // 加载驱动程序
        } catch (ClassNotFoundException e) {
            throw new RuntimeException("Failed to load MySQL driver", e);
        }
    }

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}

```
 - 配置连接参数：明确定义数据库 URL、用户名和密码等常量，涵盖数据库地址、端口、名称、时区、编码及用户登录凭据等信息。
 - 加载驱动：在静态块中加载 MySQL 驱动，确保程序与数据库通信，失败则抛RuntimeException并包含具体原因。
 - 获取连接：提供getConnection方法，依配置参数连接数据库，成功返回Connection对象用于后续操作，异常则抛给调用者。该类封装连接过程，提升代码维护性与扩展性，实现连接操作集中统一管理，便于其他类复用。
## 实现用户注册和登录功能
### 注册操作
- DAO类
``` Java
package org.example.course_system.dao;

import org.example.course_system.model.User;

import java.sql.*;

public class UserDAO {

    public boolean registerUser(User user) {
        String sql = "INSERT INTO user (username, password, email, name, roleId) VALUES (?, ?, ?, ?, ?)";
        try (Connection conn = DBUtil.getConnection();
             PreparedStatement st = conn.prepareStatement(sql)) {

            // 打印调试信息
            System.out.println("Executing SQL: " + sql);
            System.out.println("Parameters: " + user.getUsername() + ", " + user.getPassword() + ", " + user.getEmail() + ", " + user.getName() + ", " + user.getRoleId());

            st.setString(1, user.getUsername());
            st.setString(2, user.getPassword());
            st.setString(3, user.getEmail());
            st.setString(4, user.getName());
            st.setLong(5, user.getRoleId());

            return st.executeUpdate() > 0;
        } catch (SQLException e) {
            // 捕获 SQL 异常并打印详细信息
            System.err.println("SQL Error: " + e.getMessage());
            throw new RuntimeException("Failed to register user: " + e.getMessage(), e);
        }
    }

    public User login(String username, String password, long roleId) throws SQLException {
        String sql = "SELECT * FROM user WHERE username = ? AND password = ? AND roleId = ?";
        try (Connection conn = DBUtil.getConnection();
             PreparedStatement st = conn.prepareStatement(sql)) {
            st.setString(1, username);
            st.setString(2, password);
            st.setLong(3, roleId);

            ResultSet rs = st.executeQuery();
            if (rs.next()) {
                // 如果匹配成功，返回用户对象
                return new User(
                        rs.getString("username"),
                        rs.getString("password"),
                        rs.getString("email"),
                        rs.getString("name"),
                        rs.getLong("roleId")
                );
            }
        }
        return null; // 登录失败返回 null
    }

}
```
- DAO类（registerUser方法）
定义插入用户信息到数据库的 SQL 语句，然后获取数据库连接，创建PreparedStatement对象来执行 SQL。将传入User对象的属性值设置到PreparedStatement参数位置，通过executeUpdate执行插入操作，根据返回值判断插入是否成功，成功返回true，失败返回false。若出现SQLException异常，捕获并打印详细错误信息后抛出RuntimeException。

- Servlet类
  ``` Java
  package org.example.course_system.servlet;
  import org.example.course_system.dao.UserDAO;
  import org.example.course_system.model.User;
  import org.json.JSONObject;
  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.BufferedReader;
  import java.io.IOException;

   @WebServlet("/register")
  public class RegisterServlet extends HttpServlet {

    private final UserDAO userDAO = new UserDAO();

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        try {
            // 读取请求体内容
            BufferedReader reader = request.getReader();
            StringBuilder requestBody = new StringBuilder();
            String line;
            while ((line = reader.readLine()) != null) {
                requestBody.append(line);
            }

            System.out.println("Request Body: " + requestBody);

            // 解析 JSON 数据
            JSONObject json = new JSONObject(requestBody.toString());

            // 校验必填字段
            if (!json.has("username") || json.getString("username").isEmpty()) {
                response.setStatus(HttpServletResponse.SC_BAD_REQUEST);
                response.getWriter().write("{\"success\": false, \"message\": \"用户名不能为空\"}");
                return;
            }

            String username = json.getString("username");
            String password = json.getString("password");
            String email = json.getString("email");
            String name = json.getString("name");
            long roleId = json.getLong("roleId");

            User user = new User(username, password, email, name, roleId);


            // 调用 UserDAO 注册用户
            boolean success = userDAO.registerUser(user);


            // 返回注册结果
            if (success) {
                response.setStatus(HttpServletResponse.SC_OK);
                response.getWriter().write("{\"success\": true, \"message\": \"注册成功\"}");
            } else {
                response.setStatus(HttpServletResponse.SC_BAD_REQUEST);
                response.getWriter().write("{\"success\": false, \"message\": \"注册失败\"}");
            }
        } catch (Exception e) {
            e.printStackTrace();
            response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
            response.getWriter().write("{\"success\": false, \"message\": \"服务器内部错误\"}");
        }
    }
  }
  ```
  - Servlet类（RegisterServlet类的doPost方法）
处理POST请求，先设置响应的内容类型和字符编码，接着读取请求体内容拼成StringBuilder对象并打印调试。尝试将请求体解析为JSONObject，对其进行必填字段校验，不满足要求返回错误提示。校验通过则从JSONObject获取字段值创建User对象，调用userDAO.registerUser(user)在数据库注册用户，根据注册结果设置状态码和返回提示消息给前端。若出现其他异常，打印栈信息，设置相应状态码并返回服务器内部错误提示
  - 前端页面
    ``` html
    <html lang="zh">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>注册 - XX学校选课系统</title>
    <link rel="stylesheet" href="/css/register.css">
    </head>
    <body>
    <div class="container">
    <header>
    <h1>用户注册</h1>
    </header>

    <div class="auth-container">
    <h2>注册</h2>
    <form id="register-form">

      <label for="username">用户名</label>
      <input type="text" id="username" placeholder="请输入用户名" required>

      <label for="password">密码</label>
      <input type="password" id="password" placeholder="请输入密码" required>

      <label for="email">邮箱</label>
      <input type="email" id="email" placeholder="请输入邮箱" required>

      <label for="name">姓名</label>
      <input type="text" id="name" placeholder="请输入姓名" required>

      <label for="role">身份</label>
      <select id="role" required>
        <option value="1">学生</option>
        <option value="2">教师</option>
        <option value="3">管理员</option>
      </select>

      <button type="button" id="register-btn">注册</button>
    </form>
    <p>已有账户? <a href="/html/pages/login.html">登录</a></p>
    </div>
    </div>

    <script>
    document.getElementById('register-btn').addEventListener('click', async () => {
    // 获取输入字段的值
    const username = document.getElementById('username').value.trim();
    const password = document.getElementById('password').value.trim();
    const email = document.getElementById('email').value.trim();
    const name = document.getElementById('name').value.trim();
    const role = document.getElementById('role').value.trim(); // Role ID 从下拉框获取

    // 校验字段是否为空
    if (!username || !password || !email || !name || !role) {
      alert('请填写完整的注册信息');
      return;
    }

    try {
      // 构建请求的 JSON 数据
      const requestData = {
        username,
        password,
        email,
        name,
        roleId: role // 提供角色 ID
      };

      // 发送注册请求
      const response = await fetch('http://localhost:8080/register', {
        method: 'POST',
        headers: {
          'Content-Type': "application/json; charset=UTF-8",
        },
        body: JSON.stringify(requestData)
      });

      // 解析返回的响应
      const result = await response.json();

      // 根据响应显示结果
      if (result.success) {
        alert('注册成功！请登录。');
        window.location.href = '/html/pages/login.html';
      } else {
        alert(result.message || '注册失败，请稍后再试。');
      }
    } catch (error) {
      console.error('注册失败:', error);
      alert('注册失败，请检查网络或稍后再试。');
    }
    });
    </script>
 
    </body>
    </html>
    ```
- 前端页面
页面标题为 “用户注册”，form表单中有多个输入框和一个下拉框，用于收集用户名、密码、邮箱、姓名和身份（角色 ID）等信息，输入框有placeholder提示语和required属性。有 “注册” 按钮触发注册操作，页面下方提供已有账户用户跳转登录页面的链接。给 “注册” 按钮添加点击事件监听器，在处理函数中获取各输入框去除空格后的用户输入值，进行非空校验，有空值则提示并结束执行。输入完整则构建JSON格式requestData对象，用fetch函数向后端接口发POST请求，设置请求头并将requestData转字符串作请求体。后端响应后解析为JSON格式result对象，依success属性判断注册结果，成功则提示并跳转登录页，失败则弹出错误提示。


### 登录操作
- servlet类
  ``` Java
  package org.example.course_system.servlet;

  import org.example.course_system.dao.UserDAO;
  import org.example.course_system.model.User;
  import org.json.JSONObject;  // 使用 JSON 处理库

  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import javax.servlet.http.HttpSession;
  import java.io.BufferedReader;
  import java.io.IOException;
  import java.io.PrintWriter;

  @WebServlet("/login")
  public class LoginServlet extends HttpServlet {

    private final UserDAO userDAO = new UserDAO();  // 实例化 UserDAO

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // 设置响应头：允许跨域
        response.setHeader("Access-Control-Allow-Origin", "*");  // 允许所有来源
        response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE");  // 允许的方法
        response.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization"); // 允许的请求头

        // 设置响应类型为 JSON
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        // 读取请求体并解析 JSON
        StringBuilder requestBody = new StringBuilder();
        BufferedReader reader = request.getReader();
        String line;
        while ((line = reader.readLine()) != null) {
            requestBody.append(line);
        }

        // 解析请求体为 JSON 对象
        JSONObject json = new JSONObject(requestBody.toString());

        // 获取前端传递的用户名、密码和角色 ID
        String username = json.getString("username");
        String password = json.getString("password");
        long roleId = json.getLong("roleId");

        PrintWriter out = response.getWriter();

        try {
            // 调用 UserDAO 的 login 方法进行数据库查询
            User user = userDAO.login(username, password, roleId);

            if (user != null) {
                // 登录成功，返回用户信息
                response.setStatus(HttpServletResponse.SC_OK);  // 设置 HTTP 状态码 200
                out.println("{");
                out.println("\"status\": \"success\",");
                out.println("\"message\": \"登录成功\",");
                out.println("\"userId\": " + user.getId() + ",");
                out.println("\"roleId\": " + user.getRoleId());
                out.println("}");
            } else {
                // 用户名、密码或角色错误
                response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);  // 设置 HTTP 状态码 401
                out.println("{");
                out.println("\"status\": \"error\",");
                out.println("\"message\": \"用户名、密码或角色不匹配\"");  // 更具体的错误提示
                out.println("}");
            }
        } catch (Exception e) {
            e.printStackTrace();
            // 捕获异常并返回服务器错误信息
            response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);  // 设置 HTTP 状态码 500
            out.println("{");
            out.println("\"status\": \"error\",");
            out.println("\"message\": \"服务器内部错误，请稍后再试\"");  // 友好的错误提示
            out.println("}");
        }
    }
  } 
  ```
  - LoginServlet类的doPost方法主要负责处理登录请求，包括跨域设置以保障前端可正常访问接口，准备请求处理工作如设置响应格式和读取请求体并解析获取登录参数，接着进行用户验证，根据验证结果设置不同响应状态码并返回对应包含状态、消息、用户 ID 等信息的 JSON 数据，若出现异常则先打印异常栈信息再设置相应错误状态码及错误提示 JSON 数据。
- 前端页面
    ``` html
    <html lang="zh">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>登录 - XX学校选课系统</title>
    <link rel="stylesheet" href="/css/login.css">
    </head>
    <body>
    <div class="container">
    <header>
    <h1>欢迎登录</h1>
    </header>

    <div class="auth-container">
    <h2>登录</h2>
    <form id="login-form">
      <label for="username">用户名</label>
      <input type="text" id="username" placeholder="用户名" required>

      <label for="password">密码</label>
      <input type="password" id="password" placeholder="密码" required>

      <label for="roleId">角色ID</label>
      <input type="number" id="roleId" placeholder="ID (1=学生, 2=教师, 3=管理员)" min="1" max="3" required>

      <button type="button" id="login-btn">登录</button>
    </form>
    <p>没有账户? <a href="/html/pages/register.html">注册</a></p>
    </div>
    </div>

    <script>
    document.getElementById('login-btn').addEventListener('click', async function () {
    // 获取用户名、密码和角色ID
    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;
    const roleId = document.getElementById('roleId').value;

    // 验证输入是否为空
    if (username === '' || password === '' || roleId === '') {
      alert('用户名、密码和角色ID不能为空');
      return;
    }

    try {
      // 发送登录请求到后端
      const data = await fetch('http://localhost:8080/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          username: username, // 用户名
          password: password, // 密码
          roleId: parseInt(roleId) // 角色ID
        })
      }).then(response => response.json());

      // 处理返回的数据
      if (data.status === 'success') {
        alert('登录成功');
        // 根据角色跳转到不同页面
        switch (parseInt(roleId)) {
          case 1:
            window.location.href = "student-main.html";
            break;
          case 2:
            window.location.href = "teacher-main.html";
            break;
          case 3:
            window.location.href = "admin-main.html";
            break;
          default:
            alert('未知角色ID');
        }
      } else {
        alert(data.message); // 显示错误信息
      }
    } catch (error) {
      alert('登录失败，请稍后再试');
    }
    });
    </script>
    </body>
    </html>
    ```
  - 前端登录功能通过 HTML 页面和 JavaScript 交互实现。HTML 页面有明确标题、欢迎头部、带限制的登录表单及相关按钮链接。JavaScript 为登录按钮添加监听器，获取输入值并校验，非空则发 POST 请求（含正确格式数据），根据后端 JSON 格式响应中 status 判断登录结果，成功跳转对应页面，失败显示错误消息，出错则提示稍后再试。


## 不同用户登录后进入的主界面
### 学生主界面
``` html
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>学生首页</title>
  <link rel="stylesheet" href="/css/student-main.css">
</head>
<body>
<div class="main-container">
  <!-- 左侧导航栏 -->
  <nav class="sidebar">
    <ul>
      <li><a href="/html/pages/schedule.html">课程表查看</a></li>
      <li><a href="/html/pages/login.html">退出登录</a></li>
    </ul>
  </nav>

  <!-- 右侧内容区域 -->
  <div class="content">
    <header>
      <h1>欢迎来到学生页面</h1>
    </header>

    <div class="main-content">
      <p>请选择左侧菜单中的一个功能。</p>
    </div>
  </div>
</div>
</body>
</html>
```
- 该学生用户主界面主要提供了基础的页面布局与简单的功能导航。整体分为左侧导航栏和右侧内容区域两部分。
- 左侧导航栏：以列表形式呈现功能链接，包含 “课程表查看” 链接，点击可跳转至对应页面查看课程安排；还有 “退出登录” 链接，用于退出当前登录状态。
- 右侧内容区域：页面头部展示欢迎语 “欢迎来到学生页面”，主体部分提示用户选择左侧菜单中的功能，引导用户进行相应操作，整体界面布局清晰，方便学生快速找到所需功能入口。
  
### 教师主界面
``` html
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>教师首页</title>
  <link rel="stylesheet" href="/css/teacher-main.css">
</head>
<body>
<div class="main-container">
  <!-- 左侧导航栏 -->
  <nav class="sidebar">
    <ul>
      <li><a href="/html/pages/schedule.html">学生课程表查看</a></li>
      <li><a href="/html/pages/courses.html">课程管理与创建</a></li>
      <li><a href="/html/pages/login.html">退出登录</a></li>
    </ul>
  </nav>

  <!-- 右侧内容区域 -->
  <div class="content">
    <header>
      <h1>欢迎来到教师页面</h1>
    </header>

    <div class="main-content">
      <p>请选择左侧菜单中的一个功能。</p>
    </div>
  </div>
</div>
</body>
</html>
```
- 该教师用户主界面具备清晰的页面布局，主要由左侧导航栏与右侧内容区域构成，为教师提供了相应功能入口与操作引导。
- 左侧导航栏：以列表形式展示功能链接，包含 “学生课程表查看”，教师点击可查看学生的课程安排情况；“课程管理与创建”，能跳转至对应页面进行课程相关的管理操作以及创建新的课程；还有 “退出登录” 链接，用于结束当前登录状态。
- 右侧内容区域：页面头部显示欢迎语 “欢迎来到教师页面”，主体部分提示教师选择左侧菜单中的功能，引导教师按需操作，整体界面方便教师快速定位和使用各项功能。
  
### 管理员主界面
``` html
<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>管理员首页</title>
  <link rel="stylesheet" href="/css/student-main.css">
</head>
<body>
<div class="main-container">
  <!-- 左侧导航栏 -->
  <nav class="sidebar">
    <ul>
      <li><a href="/html/pages/schedule.html">课程表查看</a></li>
      <li><a href="/html/pages/teacher.html">教师信息查看</a></li>
      <li><a href="/html/pages/student.html">学生信息查看</a></li>
      <li><a href="/html/pages/login.html">退出登录</a></li>
    </ul>
  </nav>

  <!-- 右侧内容区域 -->
  <div class="content">
    <header>
      <h1>欢迎来到管理员页面</h1>
    </header>

    <div class="main-content">
      <p>请选择左侧菜单中的一个功能。</p>
    </div>
  </div>
</div>
</body>
</html>
```
- 该管理员用户主界面有着清晰的布局结构，主要分为左侧导航栏与右侧内容区域，为管理员提供了相应的功能操作入口及引导。
- 左侧导航栏：以列表形式呈现多个功能链接，包括 “课程表查看”，可供管理员查看课程安排相关情况；“教师信息查看”，点击可进入对应页面查看教师的各类信息；“学生信息查看”，能跳转至相应页面了解学生信息；还有 “退出登录” 链接，用于结束当前登录状态。
- 右侧内容区域：页面头部展示欢迎语 “欢迎来到管理员页面”，主体部分提示管理员选择左侧菜单中的功能，方便管理员按需操作，快速找到并使用各项管理功能。

## 开发课程创建和管理模块
- DAO类
  ``` Java
  package org.example.course_system.dao;

  import org.example.course_system.model.Course;

  import java.sql.*;
  import java.util.ArrayList;
  import java.util.List;

  public class CourseDAO {

    // 获取所有课程列表
    public List<Course> getAllCourses() {
        String sql = "SELECT * FROM course";
        List<Course> courses = new ArrayList<>();
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            ResultSet resultSet = statement.executeQuery();
            while (resultSet.next()) {
                Course course = new Course();
                course.setId(resultSet.getLong("id"));
                course.setTitle(resultSet.getString("title"));
                course.setDescription(resultSet.getString("description"));
                course.setTeacherId(resultSet.getLong("teacherId"));
                courses.add(course);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return courses;
    }

    // 添加新课程
    public boolean addCourse(Course course) {
        String sql = "INSERT INTO course (title, description, teacherId) VALUES (?, ?, ?)";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setString(1, course.getTitle());
            statement.setString(2, course.getDescription());
            statement.setLong(3, course.getTeacherId());
            return statement.executeUpdate() > 0;
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }
  }
  ```
 - courseDAO类
getAllCourses方法
定义查询课程表所有记录的 SQL 语句。通过DBUtil.getConnection()获取数据库连接，创建PreparedStatement执行预编译 SQL，获取ResultSet结果集。遍历结果集，为每条记录创建Course对象并设置属性值，添加到List<Course>集合。若查询过程出现SQLException异常，打印异常栈信息调试，最终返回包含所有课程信息的集合。
addCourse方法
定义插入新课程信息的 SQL 语句（含占位符）。同样获取数据库连接，创建PreparedStatement并设置参数值（来自传入Course对象属性）。执行executeUpdate判断插入是否成功（根据返回值），成功返回true，失败返回false。若出现SQLException异常，打印异常栈信
- Servlet类
  ``` Java
  package org.example.course_system.servlet;

  import org.example.course_system.dao.CourseDAO;
  import org.example.course_system.model.Course;
  import org.json.JSONArray;
  import org.json.JSONObject;

  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  import java.util.List;

  @WebServlet("/courses")
  public class CourseServlet extends HttpServlet {

    private CourseDAO courseDAO = new CourseDAO();  // 数据访问对象

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        try {
            // 获取所有课程
            List<Course> courses = courseDAO.getAllCourses();

            // 创建 JSON 数组存储课程数据
            JSONArray courseArray = new JSONArray();
            for (Course course : courses) {
                JSONObject courseJson = new JSONObject();
                courseJson.put("id", course.getId());
                courseJson.put("title", course.getTitle());
                courseJson.put("description", course.getDescription());
                courseJson.put("teacherId", course.getTeacherId());
                courseArray.put(courseJson);
            }

            // 设置响应头和响应内容类型
            response.setContentType("application/json");
            response.getWriter().write(courseArray.toString());  // 返回课程列表的 JSON 数据
        } catch (Exception e) {
            response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR, "获取课程列表时发生错误");
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        try {
            // 获取客户端传递的课程数据
            StringBuilder requestBody = new StringBuilder();
            String line;
            while ((line = request.getReader().readLine()) != null) {
                requestBody.append(line);
            }

            // 解析 JSON 数据
            JSONObject json = new JSONObject(requestBody.toString());
            String title = json.getString("title");
            String description = json.getString("description");

            // 创建新的课程对象
            Course newCourse = new Course();
            newCourse.setTitle(title);
            newCourse.setDescription(description);

            // 这里假设当前教师的 ID 可以从 session 或 token 获取 (简化处理)
            // 如果需要，可以从请求头或 session 获取教师ID
            // 假设使用默认教师ID 1
            newCourse.setTeacherId(1);

            // 将课程保存到数据库
            boolean success = courseDAO.addCourse(newCourse);

            if (success) {
                response.setStatus(HttpServletResponse.SC_OK);
                response.getWriter().write("{\"success\": true, \"message\": \"课程添加成功\"}");
            } else {
                response.setStatus(HttpServletResponse.SC_BAD_REQUEST);
                response.getWriter().write("{\"success\": false, \"message\": \"添加课程失败\"}");
            }

        } catch (Exception e) {
            e.printStackTrace();
            response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
            response.getWriter().write("{\"success\": false, \"message\": \"服务器错误\"}");
        }
    }
  }
   ```
 - 数据获取与处理
从请求体中读取数据并拼接成字符串，将其解析为JSONObject，从中获取课程的标题和描述信息，创建一个新的Course对象并设置其标题、描述和教师 ID（此处简化处理，假设教师 ID 为 1，实际应用中应从session或token等获取）。
 - 数据库操作与响应
调用CourseDAO的addCourse方法将新创建的课程保存到数据库，根据保存结果设置相应的响应状态码和消息。如果保存成功，设置状态码为HttpServletResponse.SC_OK，并返回成功消息；如果保存失败，设置状态码为HttpServletResponse.SC_BAD_REQUEST，并返回失败消息。若在整个过程中出现异常，打印异常栈信息，设置状态码为HttpServletResponse.SC_INTERNAL_SERVER_ERROR，并返回服务器错误消息。
- 前端html
``` html
  <!DOCTYPE html>
  <html lang="zh">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>教师课程管理</title>
    <link rel="stylesheet" href="/css/courses.css">
  </head>
  <body>

  <h1>教师课程管理</h1>

<!-- 添加课程的表单 -->
    <div id="add-course-section">
    <h2>添加新课程</h2>
    <form id="addCourseForm">
        <label for="title">课程标题：</label>
        <input type="text" id="title" name="title" required><br><br>

        <label for="description">课程描述：</label>
        <textarea id="description" name="description" required></textarea><br><br>

        <button type="submit">添加课程</button>
    </form>
    </div>

<!-- 课程列表 -->
    <div id="course-list-section">
    <h2>所有课程</h2>
    <table id="courseTable">
        <thead>
        <tr>
            <th>课程标题</th>
            <th>课程描述</th>
        </tr>
        </thead>
        <tbody>
        <!-- 课程信息将通过JavaScript动态加载 -->
        </tbody>
    </table>
    </div>

    <script>

    // 页面加载时获取课程信息
    window.onload = function () {
        getCourses();
    };

    // 获取课程信息
    function getCourses() {
        fetch(`http://localhost:8080/courses`, {
            method: "GET",
            headers: {
                "Content-Type": "application/json"
            }
        })
            .then(response => {
                if (!response.ok) {
                    throw new Error(`HTTP 错误: ${response.status}`);
                }
                return response.json();
            })
            .then(data => {
                renderCourses(data);  // 渲染课程数据
            })
            .catch(error => {
                console.error("获取课程数据失败:", error);
                alert("无法加载课程列表，请检查网络或稍后再试。");
            });
    }

    // 渲染课程数据到表格
    function renderCourses(courses) {
        const courseTable = document.getElementById("courseTable").getElementsByTagName("tbody")[0];
        courseTable.innerHTML = "";  // 清空当前表格内容
        courses.forEach(course => {
            const row = courseTable.insertRow();
            row.innerHTML = `
                <td>${course.title}</td>
                <td>${course.description}</td>
            `;
        });
    }

    // 提交添加课程表单
    document.getElementById('addCourseForm').addEventListener('submit', function(event) {
        event.preventDefault();  // 阻止默认表单提交

        const courseData = {
            title: document.getElementById('title').value,
            description: document.getElementById('description').value
        };

        const token = localStorage.getItem('token'); // 从 localStorage 获取 token

        fetch('http://localhost:8080/courses', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${token}`  // 将 token 放在请求头中
            },
            body: JSON.stringify(courseData)
        })
            .then(response => response.json())
            .then(data => {
                if (data.success) {
                    alert('课程添加成功');
                    getCourses();  // 更新课程列表
                } else {
                    alert('添加课程失败');
                }
            })
            .catch(error => console.error('添加课程时出错:', error));
    });

    </script>

    </body>
    </html>
```
 - 该前端代码用于教师课程管理与创建，包含页面结构与 JavaScript 功能。页面有标题及添加课程表单（含标题、描述输入框及提交按钮）和课程列表展示区（表格形式，初始空）。JavaScript 实现页面加载获取课程列表（发 GET 请求，依结果渲染或提示错误）、渲染课程数据（动态填充表格）及提交添加课程表单（阻止默认提交，发 POST 请求，依结果提示并更新列表或提示失败，出错打印错误）等功能，与后端交互实现完整课程管理体验。
   
## 课程日程表功能
- DAO类
``` Java
package org.example.course_system.dao;
import org.example.course_system.model.CourseSchedule;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class StudentCourseDAO {
    public List<CourseSchedule> getStudentSchedule(long studentId) {
        List<CourseSchedule> courses = new ArrayList<>();
        String query = "SELECT c.title, c.description, s.dayOfWeek, s.startTime, s.endTime, s.location, u.name AS teacherName " +
                "FROM course c " +
                "JOIN studentCourse sc ON c.id = sc.courseId " +
                "JOIN schedule s ON c.id = s.courseId " +
                "JOIN user u ON c.teacherId = u.id " +
                "WHERE sc.studentId = ?";

        try (Connection connection = DBUtil.getConnection();
             PreparedStatement stmt = connection.prepareStatement(query)) {

            // 设置查询参数
            stmt.setLong(1, studentId);

            try (ResultSet rs = stmt.executeQuery()) {
                while (rs.next()) {
                    // 结果集中的数据映射到 CourseSchedule 对象
                    CourseSchedule course = new CourseSchedule(
                            rs.getString("title"),
                            rs.getString("description"),
                            rs.getString("dayOfWeek"),
                            rs.getString("startTime"),
                            rs.getString("endTime"),
                            rs.getString("location"),
                            rs.getString("teacherName")
                    );
                    courses.add(course);
                }
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }

        return courses;
    }

}
```
 - getStudentSchedule方法：
构建复杂的 SQL 查询语句，通过多表连接（course表、studentCourse表、schedule表和user表）来获取学生所选课程的详细信息，包括课程标题、描述、上课星期几、开始时间、结束时间、上课地点以及授课教师姓名，查询条件为传入的学生 ID。
 - 使用DBUtil.getConnection获取数据库连接，创建PreparedStatement并设置学生 ID 参数，执行查询操作获取ResultSet结果集。
 - 遍历结果集，将每行数据映射到CourseSchedule对象中，包含从结果集中获取的各项课程相关信息，然后将CourseSchedule对象添加到列表中。
 - 若在数据库操作过程中出现SQLException异常，打印异常栈信息，最后返回包含学生课程日程信息的CourseSchedule对象列表，若查询无结果则返回空列表。通过该方法，为获取学生课程日程提供了数据访问层的支持，方便在其他业务逻辑中调用以展示学生课程安排。
- Servlet类
  ``` Java
  package org.example.course_system.servlet;

  import org.example.course_system.dao.StudentCourseDAO;
  import org.example.course_system.model.CourseSchedule;
  import org.example.course_system.model.StudentCourse;
  import org.json.JSONArray;
  import org.json.JSONObject;

  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.BufferedReader;
  import java.io.IOException;
  import java.util.List;

  @WebServlet("/schedule-course")
  public class ScheduleCourseServlet extends HttpServlet {

    private final StudentCourseDAO studentCourseDAO = new StudentCourseDAO();

    // 处理 GET 请求，返回学生的课程表
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        try {
            String studentIdParam = request.getParameter("studentId");
            if (studentIdParam == null || studentIdParam.isEmpty()) {
                response.setStatus(HttpServletResponse.SC_BAD_REQUEST);
                response.getWriter().write("{\"success\": false, \"message\": \"学生ID不能为空\"}");
                return;
            }

            long studentId = Long.parseLong(studentIdParam);

            // 查询学生的课程表，假设 studentCourseDAO.getStudentSchedule 返回的是课程信息
            List<CourseSchedule> courses = studentCourseDAO.getStudentSchedule(studentId);

            // 如果学生没有课程，返回空数组
            if (courses.isEmpty()) {
                response.getWriter().write("[]");
                return;
            }

            // 将课程信息转换为 JSON 格式
            JSONArray courseArray = new JSONArray();
            for (CourseSchedule schedule : courses) {
                // 创建一个 JSON 对象，并填充 CourseSchedule 的数据
                JSONObject courseJson = new JSONObject();
                courseJson.put("courseTitle", schedule.getCourseTitle());
                courseJson.put("description", schedule.getDescription());
                courseJson.put("dayOfWeek", schedule.getDayOfWeek());
                courseJson.put("startTime", schedule.getStartTime());
                courseJson.put("endTime", schedule.getEndTime());
                courseJson.put("location", schedule.getLocation());
                courseJson.put("teacherName", schedule.getTeacherName());

                // 将该课程的 JSON 对象加入课程数组
                courseArray.put(courseJson);
            }

            // 返回课程表的 JSON 数据
            response.getWriter().write(courseArray.toString());
        } catch (Exception e) {
            e.printStackTrace();
            response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);
            response.getWriter().write("{\"success\": false, \"message\": \"服务器内部错误\"}");
        }
    }

  }
  ```
  - 请求处理准备
设置响应的内容类型为application/json以及字符编码为UTF-8，确保与前端进行正确的数据交互格式。
获取学生 ID 并校验
从HttpServletRequest中获取名为studentId的参数值，若该值为空或空字符串，说明学生 ID 未提供，设置响应状态码为HttpServletResponse.SC_BAD_REQUEST（400 错误），并向响应体写入包含错误状态（success: false）和提示消息（“学生 ID 不能为空”）的 JSON 数据，然后结束方法执行。若获取到学生 ID，则将其转换为long类型。
 - 查询学生课程表
调用studentCourseDAO.getStudentSchedule方法，传入获取到的学生 ID，获取该学生的课程信息列表（假设返回的是CourseSchedule对象列表）。
 - 处理查询结果
若查询到的课程列表为空（即学生没有课程），直接向响应体写入空数组（[]），表示没有课程数据。若课程列表不为空，遍历该列表，将每个CourseSchedule对象的属性（课程标题、描述、星期几、开始时间、结束时间、地点、教师姓名）提取出来，构建一个JSONObject，并添加到JSONArray中。
 - 返回课程表数据
将包含所有课程信息的JSONArray转换为字符串，写入响应体，返回给前端，使前端能够获取并展示学生的课程表信息。若在整个过程中出现异常，打印异常栈信息，设置响应状态码为HttpServletResponse.SC_INTERNAL_SERVER_ERROR（500 错误），并向响应体写入包含错误状态和提示服务器内部错误的 JSON 数据。通过这个方法，实现了从后端获取学生课程表数据并以 JSON 格式响应给前端的功能，为前端展示学生课程表提供了数据支持。
- 前端html
  ``` html
  <!DOCTYPE html>
  <html lang="zh">
  <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>学生课程表</title>
  <link rel="stylesheet" href="/css/schedule.css"> <!-- 引入 CSS 样式文件 -->
  </head>
  <body>

  <div class="container">
  <h1>学生课程表</h1>

  <!-- 学生ID -->
  <label for="studentId">学生ID: </label>
  <input type="number" id="studentId" placeholder="请输入学生ID" />

  <!-- 加载课程表按钮 -->
  <button onclick="loadStudentSchedule()">加载课程表</button>

  <!-- 课程表 -->
  <table id="schedule-table">
    <thead>
    <tr>
      <th>课程名称</th>
      <th>课程描述</th>
      <th>星期几</th>
      <th>开始时间</th>
      <th>结束时间</th>
      <th>上课地点</th>
      <th>教师</th>
    </tr>
    </thead>
    <tbody>
    <!-- 动态加载课程表内容 -->
    </tbody>
  </table>

  <!-- 加载失败或其他提示 -->
  <div id="message"></div>
  </div>
 
  <script>
  // 加载学生课程表
  async function loadStudentSchedule() {
    const studentId = document.getElementById("studentId").value;
    if (!studentId) {
      alert("请输入学生ID！");
      return;
    }

    try {
      // 向后台请求学生的课程表
      const response = await fetch(`/schedule-course?studentId=${studentId}`);
      if (!response.ok) throw new Error('加载课程表失败');

      // 获取课程表数据（假设返回的是 JSON 格式）
      const courses = await response.json();

      // 获取表格的 tbody 元素
      const tableBody = document.querySelector('#schedule-table tbody');
      tableBody.innerHTML = '';  // 清空之前的内容

      // 遍历课程并填充表格
      if (courses.length === 0) {
        tableBody.innerHTML = '<tr><td colspan="7">没有找到课程。</td></tr>';
      } else {
        courses.forEach(course => {
          const row = document.createElement('tr');
          row.innerHTML = `
              <td>${course.courseTitle}</td>
              <td>${course.description}</td>
              <td>${course.dayOfWeek}</td>
              <td>${course.startTime}</td>
              <td>${course.endTime}</td>
              <td>${course.location}</td>
              <td>${course.teacherName}</td>
            `;
          tableBody.appendChild(row);
        });
      }
    } catch (error) {
      console.error('加载课程表出错:', error);
      alert('加载课程表失败，请稍后再试');
    }
  }
  </script>

  </body>
  </html>
  ```
  - 此前端页面用于学生课程表展示与交互。页面布局清晰，在container div内有明确标题，含学生 ID 输入框、加载按钮、多列表头的课程表（tbody动态加载数据）及提示区。loadStudentSchedule函数校验 ID 输入，向/schedule-course发请求获取数据，依结果清空tbody后填充课程信息或显示无课程提示，报错则控制台打印并告知用户，与后端协同实现课程表查看功能，增强用户体验。
    
## 查看学生信息
- DAO类
   ``` Java
   package org.example.course_system.dao;

  import org.example.course_system.model.Student;
  import org.example.course_system.dao.DBUtil;

  import java.sql.*;
  import java.util.ArrayList;
  import java.util.List;

  public class StudentDAO {

    // 添加学生
    public boolean addStudent(Student student) {
        String sql = "INSERT INTO student (studentNumber, major, classId, name, email, username) VALUES (?, ?, ?, ?, ?, ?)";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setString(1, student.getStudentNumber());
            statement.setString(2, student.getMajor());
            statement.setLong(3, student.getClassId());
            statement.setString(4, student.getName());
            statement.setString(5, student.getEmail());
            statement.setString(6, student.getUsername());
            int rowsInserted = statement.executeUpdate();
            return rowsInserted > 0;
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }

    // 获取所有学生信息
    public List<Student> getAllStudents() {
        List<Student> students = new ArrayList<>();
        String sql = "SELECT * FROM student";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql);
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                Student student = new Student();
                student.setId(resultSet.getLong("id"));
                student.setStudentNumber(resultSet.getString("studentNumber"));
                student.setMajor(resultSet.getString("major"));
                student.setClassId(resultSet.getLong("classId"));
                student.setName(resultSet.getString("name"));
                student.setEmail(resultSet.getString("email"));
                student.setUsername(resultSet.getString("username"));
                students.add(student);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return students;
    }

    // 删除学生
    public boolean deleteStudent(long studentId) {
        String sql = "DELETE FROM student WHERE id = ?";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setLong(1, studentId);
            int rowsDeleted = statement.executeUpdate();
            return rowsDeleted > 0;
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }
  }

   ```
   - addStudent方法：
负责将学生信息插入数据库，接收一个Student对象，构建对应的INSERT语句，通过DBUtil.getConnection获取数据库连接并创建PreparedStatement，将Student对象各属性值设置到语句参数中，执行executeUpdate操作，根据插入的行数判断是否添加成功（大于 0 则成功，返回true，否则返回false），若出现SQLException异常则打印栈信息。
   - getAllStudents方法：
用于获取所有学生的信息，执行查询数据库中student表所有记录的SELECT语句，通过数据库连接获取PreparedStatement并执行查询得到ResultSet，遍历结果集，将每条记录对应的数据封装成Student对象（设置其各属性值），添加到List<Student>集合中，若出现异常同样打印栈信息，最后返回包含所有学生信息的集合。
   - deleteStudent方法：
依据传入的学生 ID 删除对应学生记录，构建DELETE语句，按流程获取连接、创建PreparedStatement并设置学生 ID 参数，执行更新操作，根据删除的行数判断是否删除成功（大于 0 返回true，否则返回false），异常时打印栈信息。

- Servlet类
  ``` Java
  package org.example.course_system.servlet;

  import org.example.course_system.dao.StudentDAO;
  import org.example.course_system.model.Student;
  import org.json.JSONArray;
  import org.json.JSONObject;

  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.BufferedReader;
  import java.io.IOException;
  import java.util.HashMap;
  import java.util.List;
  import java.util.Map;

  @WebServlet("/student")
  public class StudentServlet extends HttpServlet {

    private final StudentDAO studentDAO = new StudentDAO();

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获取所有学生信息
        List<Student> students = studentDAO.getAllStudents();

        // 构建 JSON 数组
        JSONArray jsonArray = new JSONArray();
        for (Student student : students) {
            JSONObject jsonObject = new JSONObject();
            jsonObject.put("id", student.getId());
            jsonObject.put("studentNumber", student.getStudentNumber());
            jsonObject.put("major", student.getMajor());
            jsonObject.put("classId", student.getClassId());
            jsonObject.put("name", student.getName());
            jsonObject.put("email", student.getEmail());
            jsonObject.put("username", student.getUsername());
            jsonArray.put(jsonObject);
        }

        // 设置响应
        resp.setContentType("application/json");
        resp.setCharacterEncoding("UTF-8");
        resp.getWriter().write(jsonArray.toString());
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 读取请求体并解析为 JSON 对象
        StringBuilder jsonBody = new StringBuilder();
        try (BufferedReader reader = req.getReader()) {
            String line;
            while ((line = reader.readLine()) != null) {
                jsonBody.append(line);
            }
        }
        JSONObject jsonObject = new JSONObject(jsonBody.toString());

        // 构建 Student 对象
        Student student = new Student();
        student.setStudentNumber(jsonObject.getString("studentNumber"));
        student.setMajor(jsonObject.getString("major"));
        student.setClassId(jsonObject.getLong("classId"));
        student.setName(jsonObject.getString("name"));
        student.setEmail(jsonObject.getString("email"));
        student.setUsername(jsonObject.getString("username"));

        // 添加学生到数据库
        boolean success = studentDAO.addStudent(student);

        // 构建响应 JSON 对象
        JSONObject result = new JSONObject();
        result.put("success", success);

        // 设置响应
        resp.setContentType("application/json");
        resp.setCharacterEncoding("UTF-8");
        resp.getWriter().write(result.toString());
    }

    @Override
    protected void doDelete(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 获取学生 ID 参数
        String idParam = req.getParameter("id");
        boolean success = false;

        if (idParam != null) {
            long studentId = Long.parseLong(idParam);
            success = studentDAO.deleteStudent(studentId);
        }

        // 构建响应 JSON 对象
        JSONObject result = new JSONObject();
        result.put("success", success);

        // 设置响应
        resp.setContentType("application/json");
        resp.setCharacterEncoding("UTF-8");
        resp.getWriter().write(result.toString());
    }
    }
  ```
  - doGet方法：
处理GET请求，调用studentDAO.getAllStudents获取所有学生信息，将这些信息逐个转换为JSONObject（包含学生的id、studentNumber、major、classId、name、email、username等属性）并添加到JSONArray中，最后设置响应头为application/json及合适字符编码，将JSONArray内容以字符串形式写入响应，向前端返回所有学生信息的 JSON 数据。
  - doPost方法：
处理POST请求，先读取请求体内容并解析为JSONObject，从其中获取各项学生信息构建Student对象，调用studentDAO.addStudent将该学生添加到数据库，根据添加结果构建JSONObject（含success属性表示添加是否成功），设置响应相关属性后把结果的 JSON 字符串写入响应返回给前端，告知添加操作的情况。
  - doDelete方法：
处理DELETE请求，从请求参数中获取学生 ID，若获取到则调用studentDAO.deleteStudent尝试删除学生，依据删除结果构建JSONObject（含success属性），设置响应后将 JSON 字符串写入响应返回前端，反馈删除操作的成败情况。

- 前端html
``` html
  <!DOCTYPE html>
  <html lang="zh">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>学生信息管理</title>
    <link rel="stylesheet" href="/css/style.css">
  </head>
  <body>
  <h1>学生信息管理</h1>

<!-- 添加学生的表单 -->
    <form id="addStudentForm">
    <h2>添加学生</h2>
    <label for="studentNumber">学号</label>
    <input type="text" id="studentNumber" name="studentNumber" required><br><br>

    <label for="major">专业</label>
    <input type="text" id="major" name="major" required><br><br>

    <label for="classId">班级 ID</label>
    <input type="number" id="classId" name="classId" required><br><br>

    <label for="name">姓名</label>
    <input type="text" id="name" name="name" required><br><br>

    <label for="email">邮箱</label>
    <input type="email" id="email" name="email" required><br><br>

    <label for="username">用户名</label>
    <input type="text" id="username" name="username" required><br><br>

    <button type="submit">添加学生</button>
    </form>

    <hr>

<!-- 学生信息展示 -->
    <h2>学生列表</h2>
    <table id="studentTable">
    <thead>
    <tr>
        <th>学号</th>
        <th>姓名</th>
        <th>邮箱</th>
        <th>用户名</th>
        <th>专业</th>
        <th>班级 ID</th>
        <th>操作</th>
    </tr>
    </thead>
    <tbody>

    </tbody>
    </table>

    <script>
    // 页面加载时获取所有学生信息
    window.onload = function() {
        getStudents();
    };

    // 获取学生信息并填充到表格中
    function getStudents() {
        fetch('http://localhost:8080/student')  // 访问后端 Servlet 获取学生数据
            .then(response => response.json())
            .then(data => {
                const studentTable = document.getElementById('studentTable').getElementsByTagName('tbody')[0];
                studentTable.innerHTML = ''; // 清空现有的表格行
                data.forEach(student => {
                    const row = studentTable.insertRow();
                    row.innerHTML = `
                    <td>${student.studentNumber}</td>
                    <td>${student.name}</td>
                    <td>${student.email}</td>
                    <td>${student.username}</td>
                    <td>${student.major}</td>
                    <td>${student.classId}</td>
                    <td>
                        <button onclick="deleteStudent(${student.id})">删除</button>
                    </td>
                `;
                });
            })
            .catch(error => console.error('Error fetching student data:', error));
    }

    // 提交添加学生表单
    document.getElementById('addStudentForm').addEventListener('submit', function(event) {
        event.preventDefault();

        const studentData = {
            studentNumber: document.getElementById('studentNumber').value,
            major: document.getElementById('major').value,
            classId: parseInt(document.getElementById('classId').value),
            name: document.getElementById('name').value,
            email: document.getElementById('email').value,
            username: document.getElementById('username').value,
        };

        fetch('http://localhost:8080/student', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(studentData)
        })
            .then(response => response.json())
            .then(data => {
                if (data.success) {
                    alert('学生添加成功');
                    getStudents();  // 更新学生列表
                } else {
                    alert('添加学生失败');
                }
            })
            .catch(error => console.error('Error adding student:', error));
    });

    // 删除学生
    function deleteStudent(studentId) {
        fetch(`/student?id=${studentId}`, { method: 'DELETE' })
            .then(response => response.json())
            .then(data => {
                if (data.success) {
                    alert('学生删除成功');
                    getStudents();  // 更新学生列表
                } else {
                    alert('删除学生失败');
                }
            })
            .catch(error => console.error('Error deleting student:', error));
    }

    </script>
    </body>
    </html>
```
 - 页面结构上，标题为 “学生信息管理”，含 “添加学生” 表单（有学号、专业等多个必填输入框及提交按钮）和展示学生信息的表格（表头含多列，主体为空待动态加载）。
 - JavaScript 交互功能涵盖：页面加载时调用getStudents函数发请求获取数据，解析后清空表格并插入行展示信息、添加删除按钮（关联deleteStudent函数），出错打印错误；为表单添加监听器，阻止默认提交，构建数据对象发POST请求，依后端success属性判断添加结果并相应提示、更新列表，出错打印；deleteStudent函数接收学生 ID 发DELETE请求，依后端success属性判断删除结果并相应提示、更新列表，出错打印。整体实现学生信息的添加、展示与删除交互功能。

## 查看教师信息
- DAO类
  ``` Java
  package org.example.course_system.dao;

  import org.example.course_system.model.Teacher;
  import org.example.course_system.dao.DBUtil;

  import java.sql.*;
  import java.util.ArrayList;
  import java.util.List;

  public class TeacherDAO {

    // 获取所有教师信息
    public List<Teacher> getAllTeachers() {
        List<Teacher> teachers = new ArrayList<>();
        String sql = "SELECT * FROM teacher";

        try (Connection connection = DBUtil.getConnection();
             Statement statement = connection.createStatement();
             ResultSet resultSet = statement.executeQuery(sql)) {

            while (resultSet.next()) {
                Teacher teacher = new Teacher();
                teacher.setId(resultSet.getLong("id"));
                teacher.setUserId(resultSet.getLong("userId"));
                teacher.setTeacherTitle(resultSet.getString("teacherTitle"));
                teacher.setTeachingSubject(resultSet.getString("teachingSubject"));
                teacher.setManagedClassId(resultSet.getLong("managedClassId"));
                teacher.setName(resultSet.getString("name"));
                teacher.setEmail(resultSet.getString("email"));
                teacher.setUsername(resultSet.getString("username"));
                teachers.add(teacher);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return teachers;
    }

    // 添加教师信息
    public boolean addTeacher(Teacher teacher) {
        String sql = "INSERT INTO teacher (userId, teacherTitle, teachingSubject, managedClassId, name, email, username) VALUES (?, ?, ?, ?, ?, ?, ?)";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setLong(1, teacher.getUserId());
            statement.setString(2, teacher.getTeacherTitle());
            statement.setString(3, teacher.getTeachingSubject());
            statement.setLong(4, teacher.getManagedClassId());
            statement.setString(5, teacher.getName());
            statement.setString(6, teacher.getEmail());
            statement.setString(7, teacher.getUsername());

            int rowsInserted = statement.executeUpdate();
            return rowsInserted > 0;
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }

    // 删除教师信息
    public boolean deleteTeacher(long teacherId) {
        String sql = "DELETE FROM teacher WHERE id = ?";
        try (Connection connection = DBUtil.getConnection();
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setLong(1, teacherId);
            int rowsDeleted = statement.executeUpdate();
            return rowsDeleted > 0;
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return false;
    }
    }
  ```
  - getAllTeachers方法：通过执行查询teacher表所有记录的SELECT语句，利用DBUtil.getConnection获取数据库连接，创建Statement并执行查询得到ResultSet。遍历结果集，将每条记录的数据封装成Teacher对象（设置如id、userId、teacherTitle等各属性值），添加到List<Teacher>集合中，出现SQLException异常时打印栈信息，最终返回包含所有教师信息的集合，用于获取全部教师数据。
  - addTeacher方法：负责将教师信息插入数据库，接收Teacher对象，构建对应的INSERT语句，获取数据库连接后创建PreparedStatement，将Teacher对象各属性值设置到语句参数中，执行executeUpdate操作，依据插入的行数判断添加是否成功（大于 0 则成功，返回true，否则返回false），若出现异常则打印栈信息。
  - deleteTeacher方法：依据传入的教师 ID 删除对应教师记录，构建DELETE语句，按流程获取连接、创建PreparedStatement并设置教师 ID 参数，执行更新操作，根据删除的行数判断是否删除成功（大于 0 返回true，否则返回false），异常时打印栈信息。
    
- Servlet类
  ``` Java
  package org.example.course_system.servlet;

  import org.example.course_system.dao.TeacherDAO;
  import org.example.course_system.model.Teacher;

  import javax.servlet.ServletException;
  import javax.servlet.annotation.WebServlet;
  import javax.servlet.http.*;
  import java.io.IOException;
  import java.io.PrintWriter;
  import java.util.List;

  import org.json.JSONArray;
  import org.json.JSONObject;
 
  @WebServlet("/teacher")
  public class TeacherServlet extends HttpServlet {

    private TeacherDAO teacherDAO;

    @Override
    public void init() throws ServletException {
        teacherDAO = new TeacherDAO();
    }

    // 处理 GET 请求，获取所有教师信息
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        List<Teacher> teachers = teacherDAO.getAllTeachers();

        // 转换教师列表为 JSON 格式
        JSONArray teacherJsonArray = new JSONArray();
        for (Teacher teacher : teachers) {
            JSONObject teacherJson = new JSONObject();
            teacherJson.put("id", teacher.getId());
            teacherJson.put("userId", teacher.getUserId());
            teacherJson.put("teacherTitle", teacher.getTeacherTitle());
            teacherJson.put("teachingSubject", teacher.getTeachingSubject());
            teacherJson.put("managedClassId", teacher.getManagedClassId());
            teacherJson.put("name", teacher.getName());
            teacherJson.put("email", teacher.getEmail());
            teacherJson.put("username", teacher.getUsername());
            teacherJsonArray.put(teacherJson);
        }

        // 设置响应类型为 JSON
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        // 返回教师列表 JSON 数据
        PrintWriter out = response.getWriter();
        out.print(teacherJsonArray.toString());
    }

    // 处理 POST 请求，添加教师信息
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        StringBuilder sb = new StringBuilder();
        String line;
        while ((line = request.getReader().readLine()) != null) {
            sb.append(line);
        }

        // 将 JSON 字符串转为 JSONObject
        JSONObject jsonObject = new JSONObject(sb.toString());

        // 创建 Teacher 对象并填充数据
        Teacher teacher = new Teacher();
        teacher.setId(jsonObject.optLong("teacherId"));  // 获取 teacherId（可以为空）
        teacher.setUserId(jsonObject.getLong("userId"));
        teacher.setTeacherTitle(jsonObject.getString("teacherTitle"));
        teacher.setTeachingSubject(jsonObject.getString("teachingSubject"));
        teacher.setManagedClassId(jsonObject.getLong("managedClassId"));
        teacher.setName(jsonObject.getString("name"));
        teacher.setEmail(jsonObject.getString("email"));
        teacher.setUsername(jsonObject.getString("username"));

        // 调用 DAO 类添加教师
        boolean success = teacherDAO.addTeacher(teacher);

        // 设置响应内容类型和编码
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        // 返回 JSON 格式的响应
        PrintWriter out = response.getWriter();
        JSONObject responseJson = new JSONObject();
        responseJson.put("success", success);
        out.print(responseJson.toString());
    }

    // 处理 DELETE 请求，删除教师信息
    @Override
    protected void doDelete(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        long teacherId = Long.parseLong(request.getParameter("id"));

        // 调用 DAO 类删除教师
        boolean success = teacherDAO.deleteTeacher(teacherId);

        // 设置响应内容类型和编码
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");

        // 返回 JSON 格式的响应
        PrintWriter out = response.getWriter();
        JSONObject responseJson = new JSONObject();
        responseJson.put("success", success);
        out.print(responseJson.toString());
    }
  }
  ```
  - doGet方法：处理GET请求，调用teacherDAO.getAllTeachers获取所有教师信息，把这些教师信息逐个转换为JSONObject（包含id、userId等多个属性）并添加到JSONArray中。接着设置响应类型为application/json及字符编码为UTF-8，将JSONArray内容以字符串形式写入响应，向前端返回所有教师信息的 JSON 数据，实现教师信息查询功能。
  - doPost方法：处理POST请求，先读取请求体内容并拼接成字符串，再将其转换为JSONObject，从中获取各项教师信息构建Teacher对象，调用teacherDAO.addTeacher将该教师信息添加到数据库，根据添加结果构建含success属性的JSONObject，设置响应相关属性后把结果的 JSON 字符串写入响应返回给前端，告知添加操作情况。
  - doDelete方法：处理DELETE请求，从请求参数中获取教师 ID，调用teacherDAO.deleteTeacher尝试删除教师，依据删除结果构建含success属性的JSONObject，设置响应后将 JSON 字符串写入响应返回前端，反馈删除操作的成败情况。

- 前端html
  ``` html
      <!DOCTYPE html>
    <html lang="zh">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>教师信息管理</title>
        <link rel="stylesheet" href="/css/style.css">
    </head>
    <body>
    <h1>教师信息管理</h1>

    <!-- 添加教师的表单 -->
    <h2>添加教师</h2>
    <form id="addTeacherForm">
        <label for="teacherId">教师ID：</label>
        <input type="number" id="teacherId" name="teacherId"><br><br>

        <label for="userId">用户ID：</label>
        <input type="number" id="userId" name="userId" required><br><br>

        <label for="teacherTitle">职称：</label>
        <input type="text" id="teacherTitle" name="teacherTitle" required><br><br>

        <label for="teachingSubject">授课专业：</label>
        <input type="text" id="teachingSubject" name="teachingSubject" required><br><br>

        <label for="managedClassId">管理班级ID：</label>
        <input type="number" id="managedClassId" name="managedClassId" required><br><br>

        <label for="name">姓名：</label>
        <input type="text" id="name" name="name" required><br><br>

        <label for="email">邮箱：</label>
        <input type="email" id="email" name="email" required><br><br>

        <label for="username">用户名：</label>
        <input type="text" id="username" name="username" required><br><br>

        <button type="submit">提交</button>
    </form>

    <hr>

    <!-- 教师信息展示 -->
    <h2>教师列表</h2>
    <table id="teacherTable">
        <thead>
        <tr>
            <th>教师ID</th>
            <th>用户ID</th>
            <th>职称</th>
            <th>授课专业</th>
            <th>管理班级ID</th>
            <th>姓名</th>
            <th>邮箱</th>
            <th>用户名</th>
            <th>操作</th>
        </tr>
        </thead>
        <tbody>
        <!-- 教师信息会通过JavaScript动态加载 -->
        </tbody>
    </table>

    <script>
        // 页面加载时获取所有教师信息
        window.onload = function() {
            getTeachers();
        };

        // 获取教师信息并填充到表格中
        function getTeachers() {
            fetch('http://localhost:8080/teacher')  // 访问后端 Servlet 获取教师数据
                .then(response => response.json())
                .then(data => {
                    const teacherTable = document.getElementById('teacherTable').getElementsByTagName('tbody')[0];
                    teacherTable.innerHTML = ''; // 清空现有的表格行
                    data.forEach(teacher => {
                        const row = teacherTable.insertRow();
                        row.innerHTML = `
                                <td>${teacher.id}</td>
                                <td>${teacher.userId}</td>
                                <td>${teacher.teacherTitle}</td>
                                <td>${teacher.teachingSubject}</td>
                                <td>${teacher.managedClassId}</td>
                                <td>${teacher.name}</td>
                                <td>${teacher.email}</td>
                                <td>${teacher.username}</td>
                                <td>
                                    <button onclick="deleteTeacher(${teacher.id})">删除</button>
                                </td>
                            `;
                    });
                })
                .catch(error => console.error('Error fetching teacher data:', error));
        }

        // 提交添加教师表单
        document.getElementById('addTeacherForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const teacherData = {
                teacherId: document.getElementById('teacherId').value,
                userId: document.getElementById('userId').value,
                teacherTitle: document.getElementById('teacherTitle').value,
                teachingSubject: document.getElementById('teachingSubject').value,
                managedClassId: document.getElementById('managedClassId').value,
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                username: document.getElementById('username').value
            };

            fetch('http://localhost:8080/teacher', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(teacherData)
            })
                .then(response => response.json())
                .then(data => {
                    if (data.success) {
                        alert('教师添加成功');
                        getTeachers();  // 更新教师列表
                    } else {
                        alert('添加教师失败');
                    }
                })
                .catch(error => console.error('Error adding teacher:', error));
        });

        // 删除教师
        function deleteTeacher(teacherId) {
            fetch(`/teacher?id=${teacherId}`, { method: 'DELETE' })
                .then(response => response.json())
                .then(data => {
                    if (data.success) {
                        alert('教师删除成功');
                        getTeachers();  // 更新教师列表
                    } else {
                        alert('删除教师失败');
                    }
                })
                .catch(error => console.error('Error deleting teacher:', error));
        }
    </script>
    </body>
    </html>
  ```
  - 页面布局上，标题为 “教师信息管理”，含 “添加教师” 表单（有多个输入框，部分必填）与 “提交” 按钮，还有展示教师信息的表格（表头含多列及操作列，主体为空待动态加载）。
  - JavaScript 交互功能涵盖：页面加载时调用getTeachers函数发请求获取教师数据，解析后清空表格、插入行展示信息并添加删除按钮（关联deleteTeacher函数），出错打印错误；为表单添加监听器，阻止默认提交，构建数据对象发POST请求，依后端success属性判断添加结果并相应提示、更新列表，出错打印；deleteTeacher函数接收教师 ID 发DELETE请求，依后端success属性判断删除结果并相应提示、更新列表，出错打印，以此实现教师信息的添加、展示与删除交互功能。
 
## 优化设计
### 系统安全优化设计
- 密码加密：在用户注册和密码修改时，使用安全的加密算法（如 MD5、SHA 等）对密码进行加密处理后再存储到数据库中，确保密码在数据库中以密文形式保存，防止密码泄露。
- 输入校验
前端校验：在前端页面对特殊字符进行过滤，防止用户输入恶意脚本或 SQL 语句。
后端校验：在后端业务逻辑层再次对用户输入进行校验，确保数据的合法性和安全性。
### 系统性能优化设计
- 数据库优化
 - 索引优化：根据数据库查询语句的频繁程度和条件字段，为经常查询的字段建立合适的索引，如在 user 表的 username 字段建立唯一索引，提高用户登录时的查询速度；在 studentCourse 表的 studentId 和 courseId 字段建立联合索引，优化学生选课和查看课程表时的查询操作。
 - 查询优化：分析和优化查询语句，避免使用复杂的子查询和全表扫描，合理使用连接查询、索引覆盖等技术，提高查询效率。例如在获取学生课程日程安排时，通过多表连接查询代替多次单表查询，减少数据库操作次数。
 - 连接池配置：使用数据库连接池管理数据库连接，合理配置连接池参数，如最大连接数、最小连接数、连接超时时间等，提高连接的复用率，减少连接创建和销毁的开销，提升数据库操作性能。
- 缓存机制
 - 页面缓存：对不经常变动的页面（如系统首页、帮助页面等）进行缓存，当用户再次访问时直接返回缓存页面，减少服务器处理时间。可以使用服务器端缓存技术（如 Redis）或浏览器缓存机制（设置合适的缓存头）来实现页面缓存。
 - 数据缓存：对于频繁查询但数据更新不频繁。

## 功能拓展设计
- 为教师提供更丰富的教学工具，如在线课堂互动功能（实时提问、投票、抢答等），方便教师更好地掌握学生学习情况，提高教学效果。
- 为学生打造个性化学习空间，根据学生的学习历史、课程偏好和学习进度，推荐适合的课程和学习资源，实现个性化学习路径规划。
- 增加课程评价与反馈功能，学生可以对所学课程进行评价，教师和管理员可以根据反馈信息改进教学内容和管理策略










  
