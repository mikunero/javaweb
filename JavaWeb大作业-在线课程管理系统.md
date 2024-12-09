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
  - ![image](https://github.com/user-attachments/assets/10694541-5271-4196-9169-645b126ffe00)
  


## 不同用户登录后进入的主界面
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
  
  ```


