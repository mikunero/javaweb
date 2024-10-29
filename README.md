#JDBC练习
##插入数据
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
