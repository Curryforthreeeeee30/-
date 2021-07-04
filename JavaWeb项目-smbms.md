# JavaWeb项目-smbms

# 超市订单管理系统



**项目结构图：**

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020072518535846.png)

## 项目搭建

1. 搭建一个maven web项目

2. 配置Tomcat

3. 测试项目是否能够跑起来

4. 导入项目中会遇到的jar包(maven依赖)

   jsp、servlet、mysql驱动、jstl、stardand核心库

5. 创建包结构

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-24_105702.png)

各个包的作用：

- dao：与数据库打交道
- filter：处理一些登录拦截的事情以及处理乱码
- pojo：实体类
- service：处理业务，主要是调dao层的方法
- servlet：接收前端请求、调业务层写的方法以及视图跳转
- util：主要是一些工具类，比如项目中用到的参数以及一些页面支持的与web本身关系不大的一些事情。

6、编写实体类

 ORM映射：表-类映射

7、编写基础公共类

1. 数据库配置文件

   ```
   driver=com.mysql.jdbc.Driver
   url=jdbc:mysql://localhost:3306/smbms?useSSL=true&useUnicode=true&characterEncoding=utf-8
   username=root
   password=123456
   ```

2. 编写数据库公共类

   ```
   package com.wyqian.dao;
   
   import java.io.IOException;
   import java.io.InputStream;
   import java.sql.*;
   import java.util.Properties;
   
   //操作数据库的公共类
   public class BaseDao {
       //四个参数：driver,url,username,password，用来接收db.properties里的参数
       public static String driver = null;
       public static String url = null;
       public static String username = null;
       public static String password = null;
   
       //静态代码块，类加载的时候就会运行
       static{
           Properties properties = new Properties();
           //通过类加载器读取对应的资源
           InputStream is = BaseDao.class.getClassLoader().getResourceAsStream("db.properties");
   
           try {
               //加载db.properties资源文件
               properties.load(is);
               driver = properties.getProperty("driver");
               url = properties.getProperty("url");
               username = properties.getProperty("username");
               password = properties.getProperty("password");
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   
       //加载驱动、连接数据库
       public static Connection getConnection(){
           Connection connection = null;
           try {
               Class.forName(driver);
               connection = DriverManager.getConnection(url, username, password);
           } catch (ClassNotFoundException | SQLException e) {
               e.printStackTrace();
           }
           return connection;
       }
   
       //编写公共查询方法
       public static ResultSet execute(Connection connection, PreparedStatement preparedStatement, ResultSet resultSet,  String sql, Object[] params) throws SQLException {
           preparedStatement = connection.prepareStatement(sql);
           for(int i=0; i < params.length; i++){
               preparedStatement.setObject(i+1, params[i]);
           }
           resultSet = preparedStatement.executeQuery();
           return resultSet;
       }
   
       //编写公共增删改方法----重载
       public static int execute(Connection connection, PreparedStatement preparedStatement, String sql, Object[] params) throws SQLException {
           preparedStatement = connection.prepareStatement(sql);
           for(int i=0; i < params.length; i++){
               preparedStatement.setObject(i+1, params[i]);
           }
           int updateRows = preparedStatement.executeUpdate();
           return updateRows;
       }
   
       //释放资源
       public static boolean closeResource(Connection connection, PreparedStatement preparedStatement, ResultSet resultSet){
           boolean flag = true;
   
           if(connection != null){
               try {
                   connection.close();
                   //GC回收
                   connection = null;
               } catch (SQLException throwables) {
                   flag = false;
                   throwables.printStackTrace();
               }
           }
   
           if(preparedStatement != null){
               try {
                   preparedStatement.close();
                   //GC回收
               } catch (SQLException throwables) {
                   flag = false;
                   throwables.printStackTrace();
               }
           }
   
           if(resultSet != null){
               try {
                   resultSet.close();
                   //GC回收
                   resultSet = null;
               } catch (SQLException throwables) {
                   flag = false;
                   throwables.printStackTrace();
               }
           }
   
           return flag;
       }
   }
   ```

3. 编写字符编码过滤器并注册

   ```
   package com.wyqian.filter;
   
   import javax.servlet.*;
   import java.io.IOException;
   
   public class characterEncodingFilter implements Filter {
       @Override
       public void init(FilterConfig filterConfig) throws ServletException {
   
       }
   
       @Override
       public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
           servletRequest.setCharacterEncoding("utf-8");
           servletResponse.setCharacterEncoding("utf-8");
   
           filterChain.doFilter(servletRequest, servletResponse);
       }
   
       @Override
       public void destroy() {
   
       }
   }
   ```

   ```
   <!--字符编码过滤器-->
   <filter>
       <filter-name>characterEncodingFilter</filter-name>
       <filter-class>com.wyqian.filter.characterEncodingFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>characterEncodingFilter</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
   ```

## 登录功能实现

### 编写前端页面

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>系统登录 - 超市订单管理系统</title>
    <link type="text/css" rel="stylesheet" href="${pageContext.request.contextPath }/css/style.css" />
    <script type="text/javascript">
	/* if(top.location!=self.location){
	      top.location=self.location;
	 } */
    </script>
</head>
<body class="login_bg">
    <section class="loginBox">
        <header class="loginHeader">
            <h1>超市订单管理系统</h1>
        </header>
        <section class="loginCont">
	        <form class="loginForm" action="${pageContext.request.contextPath }/login.do"  name="actionForm" id="actionForm"  method="post" >
				<div class="info">${error }</div>
				<div class="inputbox">
                    <label for="userCode">用户名：</label>
					<input type="text" class="input-text" id="userCode" name="userCode" placeholder="请输入用户名" required/>
				</div>	
				<div class="inputbox">
                    <label for="userPassword">密码：</label>
                    <input type="password" id="userPassword" name="userPassword" placeholder="请输入密码" required/>
                </div>	
				<div class="subBtn">
					
                    <input type="submit" value="登录"/>
                    <input type="reset" value="重置"/>
                </div>	
			</form>
        </section>
    </section>
</body>
</html>
```

### 设置首页

```
<!--设置欢迎页面-->
<welcome-file-list>
    <welcome-file>login.jsp</welcome-file>
</welcome-file-list>
```

### 编写dao层接口

```
//获得登陆的用户
public User getLoginUser(Connection connection, String userCode) throws SQLException;
```

### 编写dao层实现类

```
@Override
public User getLoginUser(Connection connection, String userCode) throws SQLException {
    PreparedStatement preparedStatement = null;
    ResultSet rs = null;
    User user = null;

    if(connection != null){
        String sql = "select * from smbms_user where userCode = ?";
        Object[] params = {userCode};

        rs = BaseDao.execute(connection, preparedStatement, rs, sql, params);

        if(rs.next()){
            user = new User();
            user.setId(rs.getInt("id"));
            user.setUserCode(rs.getString("userCode"));
            user.setUserName(rs.getString("userName"));
            user.setUserPassword(rs.getString("userPassword"));
            user.setGender(rs.getInt("gender"));
            user.setBirthday(rs.getDate("birthday"));
            user.setPhone(rs.getString("phone"));
            user.setAddress(rs.getString("address"));
            user.setUserRole(rs.getInt("userRole"));
            user.setCreatedBy(rs.getInt("createdBy"));
            user.setCreationDate(rs.getDate("creationDate"));
            user.setModifyBy(rs.getInt("modifyBy"));
            user.setModifyDate(rs.getDate("modifyDate"));
        }
        BaseDao.closeResource(null, preparedStatement, rs);
    }
    return user;
}
```

### 编写service层接口

```
//用户登录
public User login(String userCode, String password);
```

### 编写service层实现类

```
@Override
public User login(String userCode, String password) {
    Connection connection = null;
    User admin = null;

    try {
        connection = BaseDao.getConnection();
        admin = userDao.getLoginUser(connection, userCode);
    } catch (SQLException throwables) {
        throwables.printStackTrace();
    }finally {
        BaseDao.closeResource(connection, null, null);
    }
    return admin;
}
```

### 编写servlet

```
package com.wyqian.servlet.user;

import com.wyqian.pojo.User;
import com.wyqian.service.user.UserServiceImpl;
import com.wyqian.util.Constant;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LoginServlet extends HttpServlet {
    //控制层：调用业务层代码

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String userCode = req.getParameter("userCode");
        String userPassword = req.getParameter("userPassword");

        UserServiceImpl userService = new UserServiceImpl();
        User login = userService.login(userCode, userPassword);

        if(login != null && login.getUserPassword().equals(userPassword)){
            //查出来的用户存在，并且密码验证成功，才可以走正常登陆~

            //将用户信息放入Session中
            req.getSession().setAttribute(Constant.USER_SESSION, login);
            //跳转到主页
            resp.sendRedirect("jsp/frame.jsp");
        }else{
            //否则，转发至login.jsp

            //请求转发可以携带信息，后端将提示信息放入error中，供前端读取
            req.setAttribute("error", "用户名或者密码错误！");
            //请求转发至登陆页面
            req.getRequestDispatcher("login.jsp").forward(req, resp);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### 注册servlet

```
<!--配置LoginServlet-->
<servlet>
    <servlet-name>LoginServlet</servlet-name>
    <servlet-class>com.wyqian.servlet.user.LoginServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>
    <url-pattern>/login.do</url-pattern>
</servlet-mapping>
```

## 登录功能优化

***移除Session\***

```
package com.wyqian.servlet.user;

import com.wyqian.util.Constant;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LogoutServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.getSession().removeAttribute(Constant.USER_SESSION);
        resp.sendRedirect(req.getContextPath() + "/login.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

***注册xml\***

```
<!--配置LogoutServlet-->
<servlet>
    <servlet-name>LogoutServlet</servlet-name>
    <servlet-class>com.wyqian.servlet.user.LogoutServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>LogoutServlet</servlet-name>
    <url-pattern>/jsp/logout.do</url-pattern>
</servlet-mapping>
```

***还需要使用Filter实现登录拦截\***

```
package com.wyqian.filter;

import com.wyqian.pojo.User;
import com.wyqian.util.Constant;

import javax.servlet.*;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class sysFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest req = (HttpServletRequest) servletRequest;
        HttpServletResponse resp = (HttpServletResponse) servletResponse;

        User user = (User) req.getSession().getAttribute(Constant.USER_SESSION);
        if(user == null) {
            resp.sendRedirect("/smbms/error.jsp");
        }
        filterChain.doFilter(servletRequest, servletResponse);
    }

    @Override
    public void destroy() {

    }
}
<!--配置权限拦截过滤器-->
<filter>
    <filter-name>sysFilter</filter-name>
    <filter-class>com.wyqian.filter.sysFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>sysFilter</filter-name>
    <url-pattern>/jsp/*</url-pattern>
</filter-mapping>
```

## 密码修改

### 导入前端素材

common文件夹下的head.jsp、foot.jsp以及pwdmodify.jsp，在这里展示的是pwdmodify.jsp:

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@include file="/jsp/common/head.jsp"%>

<div class="right">
    <div class="location">
        <strong>你现在所在的位置是:</strong>
        <span>密码修改页面</span>
    </div>
    <div class="providerAdd">
        <form id="userForm" name="userForm" method="post" action="${pageContext.request.contextPath }/jsp/user.do">
            <input type="hidden" name="method" value="savepwd">
            <!--div的class 为error是验证错误，ok是验证成功-->
            <div class="info">${message}</div>
            <div class="">
                <label for="oldPassword">旧密码：</label>
                <input type="password" name="oldpassword" id="oldpassword" value="">
                <font color="red"></font>
            </div>
            <div>
                <label for="newpassword">新密码：</label>
                <input type="password" name="newpassword" id="newpassword" value=""> 
                <font color="red"></font>
            </div>
            <div>
                <label for="rnewpassword">确认新密码：</label>
                <input type="password" name="rnewpassword" id="rnewpassword" value="">
                <font color="red"></font>
            </div>
            <div class="providerAddBtn">
                <!--<a href="#">保存</a>-->
                <input type="button" name="save" id="save" value="保存" class="input-button">
            </div>
        </form>
    </div>
</div>
</section>
<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/pwdmodify.js"></script>
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020072518544849.png)

### 编写dao层接口

```
//修改密码
public int updatePwd(Connection connection, int id, String password);
```

### 编写dao层实现类

```
@Override
public int updatePwd(Connection connection, int id, String password) {
    PreparedStatement pstm = null;
    int execute = 0;
    if (connection!=null){
        String sql = "update smbms_user set userPassword = ? where id = ?";
        Object params[] = {password,id};
        try {
            execute = BaseDao.execute(connection, pstm, sql, params);
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }
        BaseDao.closeResource(null,pstm,null);
    }
    System.out.println("进入Dao层");
    return execute;
}
```

### 编写service层接口

```
//修改用户密码
public boolean updatePwd(int id, String password);
```

### 编写service层实现类

```
@Override
public boolean updatePwd(int id, String password) {
    Connection connection = null;
    boolean flag = false;
    //修改密码
    try {
        connection = BaseDao.getConnection();
        if (userDao.updatePwd(connection,id,password)>0){
            flag = true;
        }
    } catch (Exception e) {
        e.printStackTrace();
    }finally {
        BaseDao.closeResource(connection,null,null);
    }
    System.out.println("进入业务层");
    return flag;
}
```

### 编写servlet

```
private void updatePwd(HttpServletRequest req, HttpServletResponse resp){
    //从Session中拿id
    Object o = req.getSession().getAttribute(Constant.USER_SESSION);
    String newpassword = req.getParameter("newpassword");

    boolean flag = false;

    if(o != null && newpassword != null){
        UserServiceImpl userService = new UserServiceImpl();
        User user = (User) o;
        flag = userService.updatePwd(user.getId(), newpassword);

        if(flag){
            req.setAttribute("message","修改密码成功！请退出，使用新密码登录！");
            //密码修改成功，移除当前Session
            req.removeAttribute(Constant.USER_SESSION);
        }else{
            req.setAttribute("message", "对不起，密码修改失败！");
        }
    }else{
        req.setAttribute("message","新密码有问题！");
    }
    try {
        req.getRequestDispatcher("pwdmodify.jsp").forward(req,resp);
    } catch (ServletException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### 注册servlet

```
<!--配置UserServlet-->
<servlet>
    <servlet-name>UserServlet</servlet-name>
    <servlet-class>com.wyqian.servlet.user.UserServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>UserServlet</servlet-name>
    <url-pattern>/jsp/user.do</url-pattern>
</servlet-mapping>
```

### 验证旧密码

使用的是Ajax，前后端交互的主流技术~

使用阿里巴巴的fastjson

```
<!--阿里巴巴封装的fastjson库依赖-->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.4</version>
</dependency>
//验证旧密码
private void pwdModify(HttpServletRequest req, HttpServletResponse resp) {
    //从Session中拿id
    Object o = req.getSession().getAttribute(Constant.USER_SESSION);
    String oldpassword = req.getParameter("oldpassword");

    //万能的Map
    HashMap<String, String> map = new HashMap<>();
    if(o == null){
        //当前Session过期，传一个sessionerror过去
        map.put("result", "sessionerror");
    }else if(StringUtils.isNullOrEmpty(oldpassword)){
        //旧密码为空，传一个error过去
        map.put("result", "error");
    }else{
        User user = (User) o;
        if(oldpassword.equals(user.getUserPassword())){
            //旧密码输入正确
            map.put("result", "true");
        }else{
            //旧密码输入错误
            map.put("result","false");
        }
    }
    resp.setContentType("application/json");
    /*
        阿里巴巴JSON工具类：JSONArray, 转换格式，需引入fastjson的maven依赖
         */
    try {
        PrintWriter writer = resp.getWriter();
        writer.write(JSONArray.toJSONString(map));

        writer.flush();
        writer.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

## 用户管理实现

思路：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/20200725185504444.png)

### 导入用户分页的工具类

```
package com.wyqian.util;

public class PageSupport {
    //当前页码-来自于用户输入
    private int currentPageNo = 1;

    //总数量（表）
    private int totalCount = 0;

    //页面容量
    private int pageSize = 0;

    //总页数-totalCount/pageSize（+1）
    private int totalPageCount = 1;

    public int getCurrentPageNo() {
        return currentPageNo;
    }

    public void setCurrentPageNo(int currentPageNo) {
        if(currentPageNo > 0){
            this.currentPageNo = currentPageNo;
        }
    }

    public int getTotalCount() {
        return totalCount;
    }

    public void setTotalCount(int totalCount) {
        if(totalCount > 0){
            this.totalCount = totalCount;
            //设置总页数
            this.setTotalPageCountByRs();
        }
    }
    public int getPageSize() {
        return pageSize;
    }

    public void setPageSize(int pageSize) {
        if(pageSize > 0){
            this.pageSize = pageSize;
        }
    }

    public int getTotalPageCount() {
        return totalPageCount;
    }

    public void setTotalPageCount(int totalPageCount) {
        this.totalPageCount = totalPageCount;
    }

    public void setTotalPageCountByRs(){
        if(this.totalCount % this.pageSize == 0){
            this.totalPageCount = this.totalCount / this.pageSize;
        }else if(this.totalCount % this.pageSize > 0){
            this.totalPageCount = this.totalCount / this.pageSize + 1;
        }else{
            this.totalPageCount = 0;
        }
    }

}
```

### 导入用户列表页面

***userlist.jsp和rollpage.jsp\***

**userlist.jsp**

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@include file="/jsp/common/head.jsp"%>
        <div class="right">
            <div class="location">
                <strong>你现在所在的位置是:</strong>
                <span>用户管理页面</span>
            </div>
            <div class="search">
           		<form method="get" action="${pageContext.request.contextPath }/jsp/user.do">
					<input name="method" value="query" class="input-text" type="hidden">
					 <span>用户名：</span>
					 <input name="queryname" class="input-text"	type="text" value="${queryUserName }">
					 
					 <span>用户角色：</span>
					 <select name="queryUserRole">
						<c:if test="${roleList != null }">
						   <option value="0">--请选择--</option>
						   <c:forEach var="role" items="${roleList}">
						   		<option <c:if test="${role.id == queryUserRole}">selected="selected"</c:if>
						   		value="${role.id}">${role.roleName}</option>
						   </c:forEach>
						</c:if>
	        		</select>
					 
					 <input type="hidden" name="pageIndex" value="1"/>
					 <input	value="查 询" type="submit" id="searchbutton">
					 <a href="${pageContext.request.contextPath}/jsp/useradd.jsp">添加用户</a>
				</form>
            </div>
            <!--用户-->
            <table class="providerTable" cellpadding="0" cellspacing="0">
                <tr class="firstTr">
                    <th width="10%">用户编码</th>
                    <th width="20%">用户名称</th>
                    <th width="10%">性别</th>
                    <th width="10%">年龄</th>
                    <th width="10%">电话</th>
                    <th width="10%">用户角色</th>
                    <th width="30%">操作</th>
                </tr>
                   <c:forEach var="user" items="${userList }" varStatus="status">
					<tr>
						<td>
						<span>${user.userCode }</span>
						</td>
						<td>
						<span>${user.userName }</span>
						</td>
						<td>
							<span>
								<c:if test="${user.gender==1}">男</c:if>
								<c:if test="${user.gender==2}">女</c:if>
							</span>
						</td>
						<td>
						<span>${user.age}</span>
						</td>
						<td>
						<span>${user.phone}</span>
						</td>
						<td>
							<span>${user.userRoleName}</span>
						</td>
						<td>
						<span><a class="viewUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/images/read.png" alt="查看" title="查看"/></a></span>
						<span><a class="modifyUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/images/xiugai.png" alt="修改" title="修改"/></a></span>
						<span><a class="deleteUser" href="javascript:;" userid=${user.id } username=${user.userName }><img src="${pageContext.request.contextPath }/images/schu.png" alt="删除" title="删除"/></a></span>
						</td>
					</tr>
				</c:forEach>
			</table>
			<input type="hidden" id="totalPageCount" value="${totalPageCount}"/>
		  	<c:import url="rollpage.jsp">
	          	<c:param name="totalCount" value="${totalCount}"/>
	          	<c:param name="currentPageNo" value="${currentPageNo}"/>
	          	<c:param name="totalPageCount" value="${totalPageCount}"/>
          	</c:import>
        </div>
    </section>

<!--点击删除按钮后弹出的页面-->
<div class="zhezhao"></div>
<div class="remove" id="removeUse">
    <div class="removerChid">
        <h2>提示</h2>
        <div class="removeMain">
            <p>你确定要删除该用户吗？</p>
            <a href="#" id="yes">确定</a>
            <a href="#" id="no">取消</a>
        </div>
    </div>
</div>

<%@include file="/jsp/common/foot.jsp" %>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/userlist.js"></script>
```

**rollpage.jsp**

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<script type="text/javascript">
	
</script>
</head>
<body>
 		<div class="page-bar">
			<ul class="page-num-ul clearfix">
				<li>共${param.totalCount }条记录&nbsp;&nbsp; ${param.currentPageNo }/${param.totalPageCount }页</li>
				<c:if test="${param.currentPageNo > 1}">
					<a href="javascript:page_nav(document.forms[0],1);">首页</a>
					<a href="javascript:page_nav(document.forms[0],${param.currentPageNo-1});">上一页</a>
				</c:if>
				<c:if test="${param.currentPageNo < param.totalPageCount }">
					<a href="javascript:page_nav(document.forms[0],${param.currentPageNo+1 });">下一页</a>
					<a href="javascript:page_nav(document.forms[0],${param.totalPageCount });">最后一页</a>
				</c:if>
				&nbsp;&nbsp;
			</ul>
		 <span class="page-go-form"><label>跳转至</label>
	     <input type="text" name="inputPage" id="inputPage" class="page-key" />页
	     <button type="button" class="page-btn" onClick='jump_to(document.forms[0],document.getElementById("inputPage").value)'>GO</button>
		</span>
		</div> 
</body>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/rollpage.js"></script>
</html>
```

### 获取用户总数

#### dao层接口

```
//根据用户名或者角色查询用户总数
public int getUserCount(Connection connection, String username, int userRole);
```

#### dao层实现类

```
@Override
public int getUserCount(Connection connection, String username, int userRole) {
    PreparedStatement preparedStatement = null;
    ResultSet rs = null;
    int count = 0;

    if(connection != null){
        StringBuffer sql = new StringBuffer();
        sql.append("select count(1) as count from smbms_user as u, smbms_role as r where u.userRole = r.id");

        ArrayList<Object> list = new ArrayList<Object>();
        if(!StringUtils.isNullOrEmpty(username)){
            sql.append(" and u.userName like ?");
            list.add("%" + username + "%");//index：0
        }
        if(userRole > 0){
            sql.append(" and userRole = ?");
            list.add(userRole);//index：1
        }

        //把list转换成数组
        Object [] params = list.toArray();
        try {
            rs = BaseDao.execute(connection, preparedStatement, rs, sql.toString(), params);
            if(rs.next()){
                count = rs.getInt("count");//从结果集中获取最终的参数
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            BaseDao.closeResource(null,preparedStatement,rs);
        }

    }
    return count;

}
```

#### service层接口

```
//查询记录数
public int getUserCount(String username, int userRole);
```

#### service层实现类

```
@Override
public int getUserCount(String username, int userRole) {
    Connection connection = null;
    connection = BaseDao.getConnection();
    int count = userDao.getUserCount(connection, username, userRole);
    BaseDao.closeResource(connection, null, null);
    return count;
}
```

### 获取用户列表

#### dao层接口

```
//查询用户列表
public List<User> getUserList(Connection connection, String username, int userRole, int currentPageNo, int pageSize);
```

#### dao层实现类

```
@Override
public List<User> getUserList(Connection connection, String username, int userRole, int currentPageNo, int pageSize) {
    PreparedStatement preparedStatement = null;
    ResultSet rs = null;
    ArrayList<User> userList = new ArrayList<>();

    StringBuilder sql = new StringBuilder();
    sql.append("select u.*, r.roleName from smbms_user as u, smbms_role as r where u.userRole = r.id");

    ArrayList<Object> list = new ArrayList<>();
    if(!StringUtils.isNullOrEmpty(username)){
        sql.append(" and u.userName like ?");
        list.add("%" + username + "%");
    }
    if(userRole > 0){
        sql.append(" and userRole = ?");
        list.add(userRole);
    }
    sql.append(" order by creationDate DESC limit ?,?");
    currentPageNo = (currentPageNo - 1) * pageSize;
    list.add(currentPageNo);
    list.add(pageSize);

    Object [] params = list.toArray();
    System.out.println("UserDaoImpl-->sql:" + sql.toString());
    try {
        rs = BaseDao.execute(connection, preparedStatement, rs, sql.toString(), params);
        while(rs.next()){
            User _user = new User();
            _user.setId(rs.getInt("id"));
            _user.setUserCode(rs.getString("userCode"));
            _user.setUserName(rs.getString("userName"));
            _user.setGender(rs.getInt("gender"));
            _user.setBirthday(rs.getDate("birthday"));
            _user.setPhone(rs.getString("phone"));
            _user.setUserRole(rs.getInt("userRole"));
            _user.setUserRoleName(rs.getString("RoleName"));
            _user.setAge(rs.getDate("birthday"));
            userList.add(_user);
        }
    } catch (SQLException throwables) {
        throwables.printStackTrace();
    }finally {
        BaseDao.closeResource(null,preparedStatement,rs);
    }
    return userList;
}
```

#### service层接口

```
//查询用户列表
public List<User> getUserList(String username, int userRole, int currentPageNo, int pageSize);
```

#### service层实现类

```
@Override
public List<User> getUserList(String username, int userRole, int currentPageNo, int pageSize) {
    Connection connection = null;
    List<User> userList = new ArrayList<User>();
    connection = BaseDao.getConnection();

    userList = userDao.getUserList(connection, username, userRole, currentPageNo,pageSize);
    BaseDao.closeResource(connection, null, null);
    return userList;
}
```

### 获取角色操作

这里为了与user操作分清楚，我们将角色的操作放在另一个包，如下图所示：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-24_134024.png)

#### dao层接口

```
//获取角色列表
public List<Role> getRoleList(Connection connection);
```

#### dao层实现类

```
@Override
public List<Role> getRoleList(Connection connection) {
    PreparedStatement preparedStatement = null;
    ResultSet rs = null;
    List<Role> roleList = new ArrayList<Role>();

    String sql = "select * from smbms_role";
    Object[] params = {};

    try {
        rs = BaseDao.execute(connection, preparedStatement, rs, sql, params);
        while(rs.next()){
            Role _role = new Role();
            _role.setId(rs.getInt("id"));
            _role.setRoleCode(rs.getString("roleCode"));
            _role.setRoleName(rs.getString("roleName"));
            roleList.add(_role);
        }
    } catch (SQLException throwables) {
        throwables.printStackTrace();
    }finally {
        BaseDao.closeResource(null, preparedStatement, rs);
    }
    return roleList;
}
```

#### service层接口

```
//获取用户列表
public List<Role> getRoleList();
```

#### service层实现类

```
@Override
public List<Role> getRoleList() {
    Connection connection = null;
    connection = BaseDao.getConnection();

    List<Role> roleList = roleDao.getRoleList(connection);

    BaseDao.closeResource(connection, null, null);
    return roleList;
}
```

### 编写servlet（重难点）

```
//query方法
private void query(HttpServletRequest req, HttpServletResponse resp){
    //从前端获取数据
    String queryUserName = req.getParameter("queryname");
    String temp = req.getParameter("queryUserRole");
    String pageIndex = req.getParameter("pageIndex");

    int queryUserRole = 0;//默认为0是因为正常不选择的时候是展示全部页面，这里和Dao层保持一致

    //处理分页问题
    int currentPageNo = 1;
    int pageSize = 5;//这里其实可以写进配置文件，方便用户修改
    if(queryUserName == null){
        queryUserName = "";
    }
    if(temp != null && !temp.equals("")){
        queryUserRole = Integer.parseInt(temp);
    }
    if(pageIndex != null){
        currentPageNo = Integer.parseInt(pageIndex);
    }

    UserServiceImpl userService = new UserServiceImpl();
    //获得用户的总数
    int totalCount = userService.getUserCount(queryUserName, queryUserRole);

    //总页数支持
    PageSupport pageSupport = new PageSupport();

    pageSupport.setCurrentPageNo(currentPageNo);
    pageSupport.setPageSize(pageSize);
    pageSupport.setTotalCount(totalCount);

    int tmp = totalCount % pageSize;
    int totalPageCount = (tmp == 0) ? (totalCount / pageSize) : (totalCount / pageSize)+1;

    //控制首页和尾页
    if(currentPageNo < 1){
        currentPageNo = 1;
    }
    if(currentPageNo > totalPageCount){
        currentPageNo = totalPageCount;
    }
    //获取用户列表展示
    List<User> userList = userService.getUserList(queryUserName, queryUserRole, currentPageNo, pageSize);

    RoleServiceImpl roleService = new RoleServiceImpl();
    List<Role> roleList = roleService.getRoleList();

    req.setAttribute("userList", userList);
    req.setAttribute("roleList", roleList);
    req.setAttribute("currentPageNo", currentPageNo);
    req.setAttribute("totalPageCount", totalPageCount);
    req.setAttribute("totalCount",totalCount);

    req.setAttribute("queryUserName", queryUserName);
    req.setAttribute("queryUserRole", queryUserRole);

    //返回前端
    try {
        req.getRequestDispatcher("userlist.jsp").forward(req, resp);
    } catch (ServletException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

## 添加用户

## 删除用户

## 修改用户

这三个操作的代码与上面代码类似，都是走一条线走一遍，这里就不写了，挂一个链接，里面有这三部分的代码：https://blog.csdn.net/qq_45879460/article/details/107583127

