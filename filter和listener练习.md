#Filter练习

## 登录验证流程

- 用户访问首页 `index.html` `IndexServlet，Filter` 负责判断用户是否登录。

- 如果已登录，显示 `welcome.html` 页面。

- 如果未登录，进入 `login.html` 页面，用户输入用户名和密码。

- 登录后，LoginServlet 负责处理登录信息，验证用户名和密码。

- 验证成功，跳转到 `welcome.html` 显示用户信息。

- 验证失败，返回 `login.html` 提示用户名或密码错误。

- 用户可以通过 button `logout` `LogoutServlet` 进行退出登录。

- 代码实现
### IndexServlet类
```java
package org.example.filter_1;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/index")
public class IndexServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // 访问首页逻辑
        request.getRequestDispatcher("/index.html").forward(request, response);
    }
}
```
### LoginFilter类
```java
package org.example.filter_1;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

@WebFilter("/*")
public class LoginFilter implements Filter {

    // 排除列表，包含不需要登录的资源路径
    private static final List<String> EXCLUDED_URLS = Arrays.asList("/login", "/register", "/public", "/login.html");

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        // 初始化过滤器时执行的逻辑
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {

        HttpServletRequest httpRequest = (HttpServletRequest) request;
        HttpServletResponse httpResponse = (HttpServletResponse) response;
        HttpSession session = httpRequest.getSession(false);

        String requestURI = httpRequest.getRequestURI();

        // 检查是否为排除的URL
        if (isExcluded(requestURI)) {
            System.out.println("访问公共页面: " + requestURI);  // 访问公共页面的提示
            chain.doFilter(request, response);
            return;
        }

        // 检查用户是否已登录
        if (session != null && session.getAttribute("user") != null) {
            System.out.println("用户已登录，访问受保护资源: " + requestURI);
            chain.doFilter(request, response);
        } else {
            // 用户未登录
            System.out.println("用户未登录，尝试访问受保护资源: " + requestURI + "，重定向到登录页面");
            httpResponse.sendRedirect(httpRequest.getContextPath() + "/login.html");
        }
    }

    @Override
    public void destroy() {
        // 销毁过滤器时执行的逻辑
    }

    // 判断当前请求的URI是否在排除的URL列表中
    private boolean isExcluded(String requestURI) {
        for (String url : EXCLUDED_URLS) {
            if (requestURI.contains(url)) {
                return true;
            }
        }
        return false;
    }
}
```
- 排除列表 EXCLUDED_URLS:

这是一个 List，包含不需要进行登录验证的 URL 路径，比如 /login、/register、/public 等等。

- isExcluded 方法：

该方法用于检查当前请求的 URI 是否在排除列表中。如果请求的 URI 包含排除列表中的任意路径段，就认为该请求属于无需登录验证的请求，返回 true，并允许请求通过。

- doFilter 方法的逻辑：

当请求到达时，首先检查该请求的路径是否在排除列表中：
- 如果是排除路径（登录、注册、公共资源等），则调用 chain.doFilter(request, response) 放行，不进行任何登录验证。
  
- 如果请求不在排除列表中，接着检查当前 session 中是否有表示用户已登录的 user 属性：
  
- 如果用户已登录（session.getAttribute("user") != null），则放行该请求。
  
- 如果用户未登录，将用户重定向到登录页面（/login.html）

### LoginServlet类
```java
package org.example.filter_1;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

@WebServlet("/login")
public class LoginServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        response.setCharacterEncoding("UTF-8");

        // 获取登录表单中的用户名和密码
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        // 假设用户名和密码是"admin"和"password"，这里可以连接数据库进行验证
        if ("admin".equals(username) && "1234".equals(password)) {
            // 登录成功，创建 session，并将用户信息存入 session
            HttpSession session = request.getSession();
            session.setAttribute("user", username);

            // 输出成功登录信息到 IDEA 控制台
            System.out.println("用户 " + username + " 登录成功");

            // 重定向到欢迎页面
            response.sendRedirect("welcome.html");
        } else {
            // 登录失败，输出失败信息到控制台
            System.out.println("用户 " + username + " 登录失败，用户名或密码错误");

            // 登录失败，重定向回登录页面并显示错误信息
            response.sendRedirect("login.html");
        }
    }
}

```
### LogoutServlet类
```java
package org.example.filter_1;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

@WebServlet("/logout")
public class LogoutServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        response.setCharacterEncoding("UTF-8");

        // 获取当前的 session，如果存在的话
        HttpSession session = request.getSession(false);

        if (session != null) {
            // 获取用户信息
            String username = (String) session.getAttribute("user");

            // 销毁 session
            session.invalidate();

            // 输出登出信息到控制台
            System.out.println("用户 " + username + " 已成功登出");
        }

        // 重定向到登录页面
        response.sendRedirect("login.html");
    }
}

```
### index页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Index Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            text-align: center;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }
        h1 {
            color: #333;
        }
        a {
            text-decoration: none;
            color: #007bff;
            margin: 10px;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Welcome to the Website</h1>
    <p>This is the index page. Please login to access more features.</p>

    <!-- 链接到登录页面 -->
    <a href="login.html">Login</a>

    <!-- 链接到欢迎页面，未登录的用户将会被重定向到登录页面 -->
    <a href="welcome.html">Welcome Page</a>
</div>
</body>
</html>
```
- 代码解释：

- 结构：

 h1：显示网站的主标题 "Welcome to the Website"。

 p：说明用户需要登录才能访问更多功能。

- <a> 标签：

 第一个链接指向 login.html 页面，用于登录。

 第二个链接指向 welcome.html，登录后可以访问欢迎页面，未登录用户点击后会被过滤器重定向到登录页面。

- 样式：

 使用 flexbox 来让页面内容在浏览器中居中显示，整体风格简洁。

 a:hover 添加了一个简单的悬停效果，用户体验更友好
 
- 功能：

 用户可以从首页导航到登录页面，登录成功后可以访问欢迎页面。

 如果用户尝试在未登录状态下直接访问 welcome.html，LoginFilter 会重定向用户到 login.html。

### login页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Login</title>
</head>
<body>
<h1>Login</h1>
<form method="post" action="login">
  <label for="username">Username:</label>
  <input type="text" id="username" name="username"><br>
  <label for="password">Password:</label>
  <input type="password" id="password" name="password"><br>
  <input type="submit" value="Login">
</form>

</body>
</html>

```
![image](https://github.com/user-attachments/assets/3b41415c-1f31-438d-8d42-0fa5b3305aaa)

### welcome页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome Page</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      text-align: center;
      background-color: #fff;
      padding: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
    }
    h1 {
      color: #333;
    }
    a {
      text-decoration: none;
      color: #007bff;
      margin: 10px;
    }
    a:hover {
      text-decoration: underline;
    }
    .button {
      display: inline-block;
      margin: 15px;
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border-radius: 5px;
      text-decoration: none;
    }
    .button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
<div class="container">
  <h1>Welcome, User!</h1>
  <p>You have successfully logged in.</p>

  <!-- 提供返回网站首页的链接 -->
  <a href="index.html" class="button">Go to Homepage</a>

  <!-- 提供登出链接，登出后重定向到登录页面 -->
  <a href="logout" class="button">Logout</a>
</div>
</body>
</html>
```
![image](https://github.com/user-attachments/assets/899f7fdf-04ae-4f41-85ea-3d41404504cc)

- 代码解释：
  
- h1 和 p：

 显示用户登录成功后的欢迎信息，如“Welcome, User!”。
  
 说明用户已经成功登录。
  
- a 标签：

 返回首页按钮：链接到 index.html，用户点击后可以返回网站首页。
  
 登出按钮：链接到 logout，通过 LogoutServlet 处理登出操作，点击后用户会被重定向到 login.html。
  
- 样式：

 使用 flexbox 将页面内容居中显示，整体设计简洁、直观。
  
 按钮使用了 a 标签，通过 CSS 设置为按钮样式，增加了用户体验。
  
 button:hover 添加了悬停效果，当用户鼠标悬停时按钮颜色会发生变化，增强了交互性。
  
- 页面逻辑：
  
 登录成功后，用户可以通过此欢迎页面：
  
 进入网站：点击 "Go to Homepage" 返回首页 index.html。
  
 退出登录：点击 "Logout"，触发登出请求，LogoutServlet 会处理登出并将用户重定向到登录页面。

 ![image](https://github.com/user-attachments/assets/1de6d9f8-613a-483b-a7d3-bf0e3a6e38a8)

  

#listner练习
## 核心功能

- `ServletRequestListener` 用于监听请求的创建和销毁事件。
- 使用 `System.currentTimeMillis()` 来记录请求的开始和结束时间，从而计算处理时间。

首先，我们实现 `ServletRequestListener`，这个类会监听请求的开始和结束，并在这两个事件中分别记录相关信息。在 `RequestLoggingListener` 中，我们使用 `ServletContext` 来存储一个共享的日志列表，并在每次请求时将日志追加到这个列表中。

### 类 `RequestLoggingListener`

```java
package org.example.listener;
import javax.servlet.ServletRequestEvent;
import javax.servlet.ServletRequestListener;
import javax.servlet.annotation.WebListener;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.ServletContext;
import java.util.List;
import java.util.ArrayList;
import java.util.logging.Logger;

@WebListener
public class RequestLoggingListener implements ServletRequestListener {    
    private static final Logger logger = Logger.getLogger(RequestLoggingListener.class.getName());

    @Override
    public void requestInitialized(ServletRequestEvent sre) {
        HttpServletRequest request = (HttpServletRequest) sre.getServletRequest();
        long startTime = System.currentTimeMillis();
        request.setAttribute("startTime", startTime);

        String clientIp = request.getRemoteAddr();
        String method = request.getMethod();
        String requestUri = request.getRequestURI();
        String queryString = request.getQueryString();
        String userAgent = request.getHeader("User-Agent");

        // 使用中文记录日志
        String logMessage = "客户端 IP: " + clientIp +
                            " 请求方法: " + method +
                            " 请求 URI: " + requestUri +
                            " 查询字符串: " + (queryString == null ? "" : queryString) +
                            " 用户代理: " + userAgent +
                            " 请求开始时间: " + startTime;
        logger.info(logMessage);

        // 获取ServletContext并将日志存储在其中
        ServletContext context = sre.getServletContext();
        List<String> logs = (List<String>) context.getAttribute("requestLogs");
        if (logs == null) {
            logs = new ArrayList<>();
            context.setAttribute("requestLogs", logs);
        }
        logs.add(logMessage);  // 将日志信息存储到共享列表中
    }

    @Override
    public void requestDestroyed(ServletRequestEvent sre) {
        HttpServletRequest request = (HttpServletRequest) sre.getServletRequest();
        long startTime = (Long) request.getAttribute("startTime");
        long endTime = System.currentTimeMillis();
        long duration = endTime - startTime;

        // 使用中文记录处理时间日志
        String logMessage = "请求 URI: " + request.getRequestURI() + 
                            " 处理时间: " + duration + " 毫秒";
        logger.info(logMessage);

        // 同样将处理时间的日志也加入到日志列表中
        ServletContext context = sre.getServletContext();
        List<String> logs = (List<String>) context.getAttribute("requestLogs");
        if (logs != null) {
            logs.add(logMessage);
        }
    }
}
```
## 日志解释

### `requestInitialized`
在请求开始时被调用，我们记录了以下信息：

- **客户端的 IP 地址**：`getRemoteAddr()`
- **请求方法**：`getMethod()`
- **请求的 URI 和查询字符串**：`getRequestURI()` 和 `getQueryString()`
- **User-Agent**：客户端代理（如浏览器类型）
- **请求的开始时间**：将其存入请求属性中，供后续使用。

### `requestDestroyed`
在请求结束时被调用，我们取出在开始时记录的开始时间，并计算出请求的处理时间（单位为毫秒），最后记录请求的结束日志：

- **处理时间**：通过请求开始和结束时间计算，单位为毫秒。
## 创建测试 Servlet

这个 `Servlet` 将从 `ServletContext` 中读取日志，并将它们输出到网页上。用户可以通过访问这个 `Servlet` 页面来查看请求的日志。

### 代码示例

```java
package org.example.listener;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.ServletContext;
import java.io.IOException;
import java.util.List;

@WebServlet("/viewLogs")
public class ViewLogsServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");

        // 获取ServletContext中的日志
        ServletContext context = getServletContext();
        List<String> logs = (List<String>) context.getAttribute("requestLogs");

        // 输出中文页面
        response.getWriter().write("<html><head><title>请求日志</title></head><body>");
        response.getWriter().write("<h1>请求日志</h1>");
        if (logs == null || logs.isEmpty()) {
            response.getWriter().write("<p>没有日志可显示。</p>");
        } else {
            response.getWriter().write("<ul>");
            for (String log : logs) {
                response.getWriter().write("<li>" + log + "</li>");
            }
            response.getWriter().write("</ul>");
        }
        response.getWriter().write("</body></html>");
    }
}
```
## 设置页面显示页面

```html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="refresh" content="0; URL=viewLogs" />
  <title>Redirecting to Logs</title>
</head>
<body>
  <p>Redirecting to logs page...</p>
</body>
</html>
```
### 这个页面将直接显示我们得到的信息

![image](https://github.com/user-attachments/assets/6d1aa482-27fb-44b0-a2e7-6592c21fb119)

