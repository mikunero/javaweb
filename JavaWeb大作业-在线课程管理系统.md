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
    role_id BIGINT,                              -- 角色ID（外键关联到 role 表）
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 用户注册时间
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,  -- 更新时间
    CONSTRAINT fk_role FOREIGN KEY (role_id) REFERENCES role(id)  -- 外键关联角色表
);
```

- role(角色表)
```Mysql
CREATE TABLE role (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 角色ID
    name VARCHAR(255) NOT NULL UNIQUE             -- 角色名称（如：学生、教师、管理员）
);
```
- course(课程表)
``` Mysql
CREATE TABLE course (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 课程ID
    title VARCHAR(255) NOT NULL,                  -- 课程标题
    description TEXT,                             -- 课程描述
    teacher_id BIGINT,                            -- 教师ID（外键关联到 user 表）
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 创建时间
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,  -- 更新时间
    CONSTRAINT fk_teacher FOREIGN KEY (teacher_id) REFERENCES user(id)  -- 外键关联教师
);
```

- grade(成绩表)
```Mysql
CREATE TABLE grade (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 成绩ID
    student_id BIGINT,                           -- 学生ID（外键关联到 user 表）
    course_id BIGINT,                            -- 课程ID（外键关联到 course 表）
    score DOUBLE,                                -- 成绩（如：0 - 100）
    term VARCHAR(255),                           -- 学期（如：2024年春季学期）
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 记录创建时间
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,  -- 更新时间
    CONSTRAINT fk_student FOREIGN KEY (student_id) REFERENCES user(id),  -- 外键关联学生
    CONSTRAINT fk_course FOREIGN KEY (course_id) REFERENCES course(id)   -- 外键关联课程
);
```
- schedule(课程日程表)
``` Mysql
CREATE TABLE schedule (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,        -- 日程ID
    course_id BIGINT,                            -- 课程ID（外键关联到 course 表）
    day_of_week VARCHAR(20),                     -- 上课星期几（如：Monday, Tuesday）
    start_time TIME,                             -- 上课开始时间
    end_time TIME,                               -- 上课结束时间
    location VARCHAR(255),                       -- 上课地点
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,  -- 记录创建时间
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,  -- 更新时间
    CONSTRAINT fk_course_schedule FOREIGN KEY (course_id) REFERENCES course(id)  -- 外键关联课程
);

```
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


