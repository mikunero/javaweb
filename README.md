# JDBC练习
## 插入数据
```java
import java.sql.*;
public class jdbc_demo_insert {
    private static  final String URL = "jdbc:mysql://localhost:3306/jdbc_test_teacher?serverTimezone=GMT&characterEncoding=UTF-8";
    private static  final String USER = "root";
    private static  final String PASSWORD = "20030530";

    public static void main(String[] args) {
        String sql1 = "INSERT INTO teacher (id,name,course,birthday) VALUES (?,?,?,?)";
        String sql2 = "SELECT * FROM teacher";
        String sql3 = "UPDATE teacher SET name = ? WHERE id = ?";
        //与数据库建立连接
        try (Connection conn = DriverManager.getConnection(URL,USER,PASSWORD);){
            conn.setAutoCommit(false);//设置自动提交模式为false
            //插入数据
            try(PreparedStatement ps = conn.prepareStatement(sql1)){
                //设置参数
                ps.setInt(1,1);
                ps.setString(2,"张三");
                ps.setString(3,"数学");
                ps.setDate(4, Date.valueOf("2000-1-1"));
                //执行插入
                ps.executeUpdate();//
                conn.commit();//提交事务
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

}
```
-- 运行后效果
-- ![image](https://github.com/user-attachments/assets/bfbf35e0-f3fd-498a-8c6d-a53afb56392f)


## 查询数据
```java
import java.sql.*;
public class jdbc_demo_select {
    private static final String URL = "jdbc:mysql://localhost:3306/jdbc_test_teacher?serverTimezone=GMT&characterEncoding=UTF-8";
    private static final String USER = "root";
    private static final String PASSWORD = "20030530";

    public static void main(String[] args) {
        String sql1 = "INSERT INTO teacher (id,name,course,birthday) VALUES (?,?,?,?)";
        String sql2 = "SELECT * FROM teacher";
        String sql3 = "UPDATE teacher SET name = ? WHERE id = ?";
        //与数据库建立连接
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);) {
            conn.setAutoCommit(false);//设置自动提交模式为false

            //查询数据

            try (PreparedStatement ps = conn.prepareStatement(sql2)) {
                try (ResultSet rs = ps.executeQuery()) {
                    while (rs.next()) {
                        System.out.println(rs.getInt(1) + " " + rs.getString(2) + " " + rs.getString(3) + " " + rs.getDate(4));
                    }
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }

        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```
## 更新数据
```java
import java.sql.*;
public class jdbc_demo_update {
    private static final String URL = "jdbc:mysql://localhost:3306/jdbc_test_teacher?serverTimezone=GMT&characterEncoding=UTF-8";
    private static final String USER = "root";
    private static final String PASSWORD = "20030530";

    public static void main(String[] args) {
        String sql3 = "UPDATE teacher SET name = ? WHERE id = ?";
        //与数据库建立连接
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);) {
            conn.setAutoCommit(false);//设置自动提交模式为false
            //更新数据
            try (PreparedStatement ps = conn.prepareStatement(sql3)) {
                //设置参数
                ps.setString(1, "李四");
                ps.setInt(2,1);
                //执行更新
                ps.executeUpdate();
                conn.commit();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```
## 删除数据
```java
import java.sql.*;
public class jdbc_demo_delete {
    private static final String URL = "jdbc:mysql://localhost:3306/jdbc_test_teacher?serverTimezone=GMT&characterEncoding=UTF-8";
    private static final String USER = "root";
    private static final String PASSWORD = "20030530";

    public static void main(String[] args) {
        String sql4 = "DELETE FROM teacher WHERE id = ?";
        //与数据库建立连接
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);) {
            conn.setAutoCommit(false);//设置自动提交模式为false
            //更新数据
            try (PreparedStatement ps = conn.prepareStatement(sql4)) {
                //设置参数
                ps.setInt(1,1);
                //执行更新
                ps.executeUpdate();
                conn.commit();
            } catch (SQLException e) {
                conn.rollback();
                e.printStackTrace();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
## 教师表多数插入与查看结果集练习
```java
import java.sql.*;

public class jdbc_demo_teacher {
    private static final String URL = "jdbc:mysql://localhost:3306/jdbc_test_teacher?serverTimezone=GMT&characterEncoding=UTF-8";
    private static final String USER = "root";
    private static final String PASSWORD = "20030530";

    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD)) {
            // 1. 清空表
            clearTeacherTable(conn);

            // 2. 批量插入500个教师
            insertTeachers(conn);

            // 3. 查看结果集中倒数第2条数据
            getSecondLastTeacher(conn);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void clearTeacherTable(Connection conn) {
        String clearSQL = "DELETE FROM teacher";
        try (PreparedStatement ps = conn.prepareStatement(clearSQL)) {
            ps.executeUpdate();
        } catch (SQLException e) {
            throw new RuntimeException();
        }
    }

    private static void insertTeachers(Connection conn) throws Exception {
        String insertSQL = "INSERT INTO teacher (id, name, course, birthday) VALUES (?, ?, ?, ?) " +
                "ON DUPLICATE KEY UPDATE name=VALUES(name), course=VALUES(course), birthday=VALUES(birthday)";
        try (PreparedStatement ps = conn.prepareStatement(insertSQL)) {
            for (int i = 1; i <= 500; i++) {
                ps.setInt(1, i);
                ps.setString(2, "教师" + i);
                ps.setString(3, "课程" + (i % 5 + 1)); // 5种课程
                ps.setDate(4, java.sql.Date.valueOf("1980-01-01")); // 固定生日

                ps.addBatch();

                // 每100条提交一次
                if (i % 100 == 0) {
                    ps.executeBatch();
                }
            }
            // 提交剩余的条目
            ps.executeBatch();
        } catch (SQLException e) {
            System.err.println("Batch insert failed: " + e.getMessage());
        }
    }

    private static void getSecondLastTeacher(Connection conn) throws Exception {
        String querySQL = "SELECT * FROM teacher ORDER BY id DESC LIMIT 2";
        try (PreparedStatement pstmt = conn.prepareStatement(querySQL, ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY)) {
            ResultSet rs = pstmt.executeQuery();
            if (rs.last()) {
                // 倒数第二条记录
                rs.previous();
                System.out.println("倒数第二条教师记录：");
                System.out.println("ID: " + rs.getInt("id"));
                System.out.println("姓名: " + rs.getString("name"));
                System.out.println("课程: " + rs.getString("course"));
                System.out.println("生日: " + rs.getDate("birthday"));
            }
        }
    }
}
```

