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
    first_name VARCHAR(255),                     -- 姓名
    last_name VARCHAR(255),                      -- 姓氏
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

## 实现用户注册和登录功能

## 创建个人信息管理界面

## 开发课程创建和管理模块

## 实现课程内容上传功能

## 创建学生选课系统

## 实现成绩管理和查询功能

## 开发课程日程表功能


