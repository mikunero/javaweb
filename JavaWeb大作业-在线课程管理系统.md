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
- 数据库访问层（UserDAO 类）
registerUser方法先定义插入用户信息到数据库的SQL语句，接着获取数据库连接并创建PreparedStatement对象用于执行该语句，随后把传入User对象的各属性值设置到PreparedStatement相应参数位置，再通过executeUpdate方法执行插入操作，依据返回值判断插入是否成功（大于 0 为成功，返回true，否则返回false），若出现SQLException异常，会捕获、打印详细错误信息并抛出RuntimeException。
- 服务层（RegisterServlet 类）
doPost方法主要处理POST请求，先是设置响应的内容类型与字符编码以保证与前端正确交互数据格式，接着读取请求体内容拼成StringBuilder对象并打印用于调试，然后尝试解析为JSONObject，对其进行必填字段校验，不满足要求就返回对应错误提示。若校验通过，从JSONObject获取各字段值创建User对象，调用userDAO.registerUser(user)在数据库注册用户，依据注册结果设置相应状态码和返回对应提示消息给前端，若出现其他异常，则打印栈信息，设置对应状态码并返回服务器内部错误提示。
- HTML 页面：
页面整体有标题显示 “用户注册”，在form表单中包含了多个输入框和一个下拉框，用于收集用户的用户名、密码、邮箱、姓名以及身份（通过下拉框选择学生、教师、管理员对应的角色 ID）等信息，每个输入框都设置了相应的placeholder提示语以及required属性来确保用户必须输入对应的值，还有一个 “注册” 按钮用于触发注册操作，同时页面下方提供了已有账户的用户可点击链接跳转到登录页面的提示。
- JavaScript：
给 “注册” 按钮添加点击事件监听器，在其处理函数中，先获取各输入框去除空格后的用户输入值，进行非空校验，若有空值则提示并结束执行；若输入完整，构建含用户信息的JSON格式requestData对象，用fetch函数向指定后端接口发POST请求，设置相应请求头并将requestData转字符串作请求体。待后端响应后，解析为JSON格式的result对象，依success属性判断注册结果，成功则提示并跳转登录页，失败则弹出对应错误提示。

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
  - 设置跨域相关响应头以保障跨域环境下登录接口可正常访问，接着准备请求处理工作，设置响应内容类型与字符编码，并读取、解析请求体获取登录参数。之后进行用户验证及响应返回，通过调用UserDAO的login方法验证用户，根据返回结果分情况处理，登录成功设状态码为 200 并返回相应成功信息，登录失败设状态码为 401 返回对应错误提示，出现异常则设状态码为 500 并返回服务器错误提示，同时会打印异常栈信息辅助调试。


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
getAllCourses方法：
首先定义了查询课程表所有记录的SQL语句"SELECT * FROM course"，用于获取全部课程信息。
通过DBUtil.getConnection()获取数据库连接，并基于此连接创建PreparedStatement对象来执行预编译的SQL语句。
执行executeQuery方法获取查询结果集ResultSet，然后遍历该结果集，对于每一条记录，创建一个Course对象，将从结果集中获取到的课程的id、title、description、teacherId等属性值分别设置到Course对象对应的属性上，最后将该Course对象添加到List<Course>集合中。若在查询过程中出现SQLException异常，会打印异常栈信息用于调试。最终返回包含所有课程信息的List<Course>集合，即获取到所有课程列表。
addCourse方法：
定义插入新课程信息到课程表的SQL语句"INSERT INTO course (title, description, teacherId) VALUES (?,?,?)"，其中使用占位符?来表示待传入的参数。
同样通过DBUtil.getConnection()获取数据库连接，创建PreparedStatement对象并将传入的Course对象中的title、description、teacherId属性值依次设置到PreparedStatement对应的参数位置上。
执行executeUpdate方法来执行插入操作，根据其返回值是否大于0判断插入是否成功，大于0表示成功插入了至少一行数据，返回true，否则返回false。若出现SQLException异常，会打印异常栈信息。

## 开发课程日程表功能


