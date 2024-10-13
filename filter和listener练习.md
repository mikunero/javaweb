#Filter练习



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

