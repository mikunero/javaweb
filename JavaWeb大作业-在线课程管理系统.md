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
- 本项目采用的IDE环境为IDEA2024，Mysql使用8.0版本，使用SpringBoot进行开发
  
- 配置Mysql驱动，让项目能与Mysql连接
  - ![image](https://github.com/user-attachments/assets/5c4bed2e-8dcb-4a28-b1e3-414f859005a3)
  - ![image](https://github.com/user-attachments/assets/09051a67-5f23-4ca3-ba71-261fcfcf7d28)

- 配置MyBatis，以简化数据库操作
  - ![image](https://github.com/user-attachments/assets/a6758b92-6ed7-41df-9e96-c3418115c2a7)


## 实现用户注册和登录功能

### 为所需的数据库表建造实体类
- 首先在model软件包中，创建一个User实体类用于存放user表中的各种数据
  - ![image](https://github.com/user-attachments/assets/03317f1a-ca3a-4f50-8f8b-e9bac0f55859)
- 其中role_id为外键要与role表关联，所以我们还需要创建一个Role实体类
  - ![image](https://github.com/user-attachments/assets/180c0643-64e1-4496-b8af-c6ee98081d44)
- 创建Course实体类
  - ![image](https://github.com/user-attachments/assets/b101ced5-f6cf-4920-8df5-6554146b06ba)
- 创建Grade实体类
  - ![image](https://github.com/user-attachments/assets/df80500d-a7ec-4d86-8b31-f51dc401754e)
- 创建Schedule实体类
  - ![image](https://github.com/user-attachments/assets/9fee916c-8347-4d8f-812a-7befe963a548)



 
## 创建个人信息管理界面

## 开发课程创建和管理模块

## 实现课程内容上传功能

## 创建学生选课系统

## 实现成绩管理和查询功能

## 开发课程日程表功能


