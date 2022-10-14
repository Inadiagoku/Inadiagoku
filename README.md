PRACTICAL NO. 1: Implement the following Simple Servlet applications. Q.1.a. Create a simple calculator application using servlet. 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form method="post" action="CalcServlet"> 
            Enter no. 1: <input type="text" name="n1"><br><br>             Enter no. 2: <input type="text" name="n2"><br><br> 
              
                  <input type="submit" value="+" name="btn"> 
            <input type="submit" value="-" name="btn"> 
            <input type="submit" value="*" name="btn"> 
            <input type="submit" value="/" name="btn"> 
        </form> 
    </body> 
</html> 
CalcServlet.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {         response.setContentType("text/html;charset=UTF-8");         PrintWriter out = response.getWriter();           int a= Integer.parseInt(request.getParameter("n1")); 
        int b= Integer.parseInt(request.getParameter("n2")); 
        int c=0; 
        String op=request.getParameter("btn");         if(op.equals("+"))             c=a+b;         else if(op.equals("-"))             c=a-b;         else if(op.equals("*"))             c=a*b;         else if(op.equals("/"))             c=a/b; 
        out.println("<b>"+a +op+ b+" = "+ c+"<b>"); 
    } 
 
 
 
Q.1.b. Create a servlet for a login page. If the username and password are correct then it says message “Hello <username>” else a message “login failed” 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form method="post" action="LoginServlet"> 
            Enter Username: <input type="text" name="uname"><br><br> 
            Enter Password: <input type="password" name="pwd"><br><br> 
            <input type="submit" value="Login"> 
        </form> 
    </body> 
</html> 
LoginServlet.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {         response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
         
        String username=request.getParameter("uname"); 
        String password=request.getParameter("pwd"); 
         
        String msg=""; 
         
        if(username.equals("admin") && password.equals("123")){             msg="Hello "+username;             out.println(msg); 
        }         else{ msg="Login Failed."; 
            out.println(msg); 
    }    
 } 
 
 
Q.1.c. Create a simple calculator application using servlet. 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form method="post" action="RegistrationServlet"> 
            Enter Username: <input type="text" name="uname"><br><br> 
            Enter Password: <input type="password" name="pwd"><br><br> 
            Enter Email: <input type="email" name="email"><br><br> 
Enter Country: <select name="coun"> 
                <option>India</option> 
                <option>USA</option> 
                <option>China</option> 
            </select><br><br> 
            <input type="submit" value="Register"> 
        </form> 
    </body> 
</html> 
RegistrationServlet.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {         response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
         
        Connection con=null; 
        PreparedStatement ps=null; 
         
        String username=request.getParameter("uname"); 
        String password=request.getParameter("pwd"); 
        String email=request.getParameter("email"); 
        String country=request.getParameter("coun"); 
                 try { 
            Class.forName("com.mysql.jdbc.Driver");             con=DriverManager.getConnection("jdbc:mysql://localhost:3306/registration", "root", "root");             out.println("Connection done successfully"); 
 
            ps=con.prepareStatement("Insert into untitled values(?,?,?,?)");             ps.setString(1, username);             ps.setString(2, password);             ps.setString(3, email);             ps.setString(4, country);             ps.execute();             out.println("Data inserted successfully"); 
         }  
         
        catch (ClassNotFoundException | SQLException e) { 
            out.println(e);             out.println("<b>"+"<b>"); 
        } 
    } 
 
 
PRACTICAL NO. 2: Implement the following Servlet applications with Cookies and Sessions. 
Q.2.a. Using Request Dispatcher Interface create a Servlet which will validate the password entered by the user, if the user has entered "Servlet" as password, then he will be forwarded to Welcome Servlet else the user will stay on the index.html page and an error message will be displayed. 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form method="post" action="ValidateServlet"> 
            Enter Username: <input type="text" name="uname"><br><br> 
            Enter Password: <input type="password" name="pwd"><br><br> 
            <input type="submit" value="Login"> 
        </form> 
    </body> 
</html> 
ValidateServlet.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {         response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
         
        String username=request.getParameter("uname"); 
        String password=request.getParameter("pwd"); 
         
        if(password.equals("admin")) 
        { 
            request.setAttribute("u1", username);             request.setAttribute("p1", password); 
             
            RequestDispatcher rd=request.getRequestDispatcher("/WelcomeServlet");             rd.forward(request, response); 
        }         else{ 
            out.println("Incorrect Credentials!<br>Try again."); 
            RequestDispatcher rd=request.getRequestDispatcher("/index.html");             rd.include(request, response); 
        } 
    } 
WelcomeServlet.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {         response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
         
        String u2=(String)request.getAttribute("u1");         String p2=(String)request.getAttribute("p1"); 
         
        out.println("Welcome "+u2); 
    } 
 
Output 
 
Q.2.b. Create a servlet that uses Cookies to store the number of times a user has visited servlet. 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form action="CookieServlet"> 
        </form> 
    </body> 
</html> 
 
 
 
CookieServlet.java 
(Initialize the variable private int i=1 inside the particular main class) 
@Override protected void doGet(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException {          response.setContentType("text/html;charset=UTF-8"); 
         PrintWriter out = response.getWriter(); 
          
         String k=String.valueOf(i);          Cookie c=new Cookie("visit",k);          response.addCookie(c);          int j=Integer.parseInt(c.getValue()); 
          
         if(j==1){ 
             out.println("YOU ARE VISITING THE PAGE FOR THE FIRST TIME"); 
         }          else { 
             synchronized(CookieServlet.this){                  out.println("YOU VISITED THIS PAGE FOR "+i+" TIMES"); 
             }          }          i++; 
    } 
Output 
 
 Q.2.c. Create a servlet demonstrating the use of session creation and destruction.  Also check whether the user has visited this page first time or has visited earlier also using sessions. 
index.html 
<html> 
    <head> 
        <title>TODO supply a title</title> 
        <meta charset="UTF-8"> 
        <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    </head> 
    <body> 
        <form action="SessionServlet" > 
        </form> 
    </body> 
</html> 
SessionServlet.java 
(Initialize the variable private int counter=1 inside the main class) 
@Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
 
response.setContentType("text/html;charset=UTF-8");  
 
        HttpSession session=request.getSession(true);  if(session.isNew()) 
        {  
out.println("THIS IS THE FIRST TIME YOU ARE VISITING THIS PAGE");  
            ++counter;  
        }  
else 
        {  
synchronized(SessionServlet.this) 
            {  
if(counter==10)  
                {  
session.invalidate();  counter=0;  request.getSession(false);  
                }  
else out.println("YOU HAVE VISITED THIS PAGE" +(++counter)+ "times");    
            }  
        }  
    } 
Output 
  
 
 
 
 
 
 
 
 
 
PRACTICAL NO. 3: Implement the Servlet IO and File applications. Q.3.a. Create a Servlet application to upload a file. 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<form action="FileUploadServlet" method="post" enctype="multipart/form-data"> 
            Select file to upload: <input type="file" name="file" id="file"> 
Destination:<input type="text" value="/tmp" name="destination"> 
<input type="submit" value="Upload File" name="upload" id="upload"> 
</form> 
</body> 
</html> 
FileUpload.Servlet 
@MultipartConfig @Override protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { response.setContentType("text/html;charset=UTF-8");         PrintWriter out = response.getWriter(); 
        String path=request.getParameter("destination"); 
        Part filePart=request.getPart("file"); 
        String sfilePart=request.getPart("file").toString(); out.println("<br>filePart: "+sfilePart); 
        String filename = filePart.getSubmittedFileName().toString(); out.print("<br><br><hr>file name: "+filename); 
        OutputStream os=null; 
        InputStream is=null; 
 
try 
        { 
os=new FileOutputStream(new File(path+File.separator+filename)); is=filePart.getInputStream(); int read=0; byte[]b=new byte[1024]; while((read=is.read(b))!=-1) 
            { 
os.write(b,0,read); 
            } 
out.println("FILE UPLOADED SUCCESSFULLY.....!!!"); 
        } 
 
catch(FileNotFoundException e) 
        { 
out.print(e); 
        } 
    } 
Output 
  
 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<form action="FileDownloadAppServlet"> 
<h1>FILE DOWNLOAD APPLICATION</h1> 
        Click<a href="FileDownloadAppServlet?filename=BatchD.docx">TYIT 2</a> 
<br/><br/> 
</form> 
</body> 
</html> 
FileDownloadAppServlet 
@Override     protected void doGet(HttpServletRequest request, HttpServletResponse response)             throws ServletException, IOException { 
            String filename = request.getParameter("filename"); 
            ServletContext context = getServletContext(); 
            InputStream is = context.getResourceAsStream("/" + filename);             ServletOutputStream os = response.getOutputStream();             response.setHeader("Content-Disposition","attachment;filename=\"" + filename + "\""); 
             int i; 
            byte b[]=new byte[1024];             while ((i=is.read(b)) != -1) 
            { 
                os.write(b); 
            }             is.close();             os.close();     } 
 
Q.3.d. Create simple Servlet application to demonstrate Non-Blocking Read Operation. index.html 
<html> 
<head> 
<title>FILE DOWNLOAD PAGE</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<a href="NonBlockingServlet">Non Blocking Read Application </a> 
</body> 
</html> 
ReadingListener.java 
package nonblkapp; public class ReadingListener implements ReadListener { privateServletInputStream input = null; privateAsyncContext ac = null; 
ReadingListener(ServletInputStream in, AsyncContext c){ input = in; ac = c; 
    } 
    @Override public void onDataAvailable() throws IOException { 
    } 
    @Override public void onAllDataRead() throws IOException { ac.complete(); 
    } 
    @Override public void onError(Throwable t) { ac.complete(); 
t.printStackTrace(); 
    } 
} 
ReadingNonblockingservlet.java 
package nonblkapp; 
@WebServlet(name = "ReadingNonBlockingServlet", urlPatterns=("/ReadingNonBlockingServlet"),asyncSupported= true) public class ReadingNonBlockingServlet extends HttpServlet { 
    @Override protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{ response.setContentType("text/html"); 
AsyncContext ac = request.startAsync(); ServletInputStream in = request.getInputStream(); in.setReadListener(new ReadingListener(in,ac)); 
    } 
} 
NonBlockingServlet.java 
package nonblkapp; 
@WebServlet(name = "NonBlockingServlet", urlPatterns={"/NonBlockingServlet"}) public class NonBlockingServlet extends HttpServlet { 
@Override 
protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{ response.setContentType("text/html"); 
PrintWriter out = response.getWriter(); 
         String filename ="booklist.txt"; 
ServletContext c= getServletContext(); 
InputStream is = c.getResourceAsStream("/"+filename); 
         String path="http://"+request.getServerName()+":"+request.getServerPort()+ request.getContextPath()+"/ReadingNonBlockingServlet"; out.println("<h1>File Reader</h1>"); out.flush(); 
         URL url= new URL(path); 
HttpURLConnectionhc = (HttpURLConnection)url.openConnection(); hc.setChunkedStreamingMode(2); hc.setDoOutput(true); hc.connect(); 
InputStreamReaderisr = new InputStreamReader(is); 
BufferedReaderbr = new BufferedReader(isr); 
 String text = ""; 
System.out.println("Reading started..."); 
BufferedWriterbw = new BufferedWriter(new OutputStreamWriter(hc.getOutputStream())); while ((text = br.readLine()) != null)  
 { 
bw.write(text); bw.flush(); out.println(text+"<br>"); out.flush(); try 
 { 
Thread.sleep(1000); 
 } 
catch (Exception ex)  
 { 
out.print(ex); 
 } 
 } 
bw.write("Reading completed..."); bw.flush(); bw.close(); 
 } 
} 
 
PRACTICAL NO. 4: Implement the following JSP application. 
Q.4.a. Develop a simple JSP application to display values obtained from the use of intrinsicobjects of various types. 
index.jsp 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<form action="implicitObjectEx.jsp"> 
 ENTER YOUR NAME: <input type="text" name="myname"><br> 
 ENTER YOUR EMAIL ID: <input type="text" name="mymailid"><br> 
<input type="submit" value="submit"> 
</form></body></html> 
 
implicitObjectEx.jsp 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>USE OF INTRINSIC OBJECT</h1> 
<br> 
<h1>REQUEST OBJECTs</h1> 
 Query String <%=request.getQueryString()%><br> 
 Context Path <%=request.getContextPath()%><br> 
 Remote host <%=request.getRemoteHost()%><br> 
<h2>Response Object</h2> 
 Character Encoding Type <%=request.getCharacterEncoding()%><br> 
 Locale <%=response.getLocale()%><br> 
<h1>SESSION OBJECT</h1> 
 Id <%=session.getId()%><br> 
 Creation Time <%=new java.util.Date(session.getCreationTime())%><br> last access Time <%=new java.util.Date(session.getLastAccessedTime())%><br> </body></html> 
Output  
 
Q.4.b. Create a registration and login JSP application to register and authenticate the user based on username and password using JDBC. 
index.html 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-
</head> 
<body> 
<form action="Registration1.jsp"> 
<center><h1>NEW USER REGISTRATION</h1></center> 
                Enter Username: <input type="text" name="txtName"><br> 
                Enter Password: <input type="password" name="txtPass1"><br> 
                Re-enter Password: <input type="password" name="txtPass2"><br> 
                Enter Email: <input type="email" name="txtEmail"><br> 
                Enter Country: <select name="txtCon"> 
<option>India</option> 
<option>France</option> 
<option>England</option> 
<option>Argentina</option> 
</select><br> 
<input type="submit" value="Register"><input type="reset"> 
</form> 
</body> 
</html> 
Registration1.jsp 
<%@page import="java.sql.PreparedStatement"%> 
<%@page import="java.sql.DriverManager"%> 
<%@page import="java.sql.Connection"%> 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
 
<% 
            String uname=request.getParameter("txtName"); 
            String pass1=request.getParameter("txtPass1"); 
            String pass2=request.getParameter("txtPass2"); 
            String email=request.getParameter("txtEmail"); 
            String ctry=request.getParameter("txtCon"); if(pass2.equals(pass1)){ try{ 
Class.forName("com.mysql.jdbc.Driver"); 
                    Connection 
con=DriverManager.getConnection("jdbc:mysql://localhost:3306/logindb","root","root");                     PreparedStatement stmt=con.prepareStatement("insert into userpass values(?,?,?,?)"); stmt.setString(1,uname); stmt.setString(2,pass1); stmt.setString(3,email); stmt.setString(4,ctry); int row=stmt.executeUpdate(); if(row==1){ out.println("Registration Successful"); 
                    } 
else{ out.println("Registration Failed"); 
    %> 
<jsp:include page="ndex.html"></jsp:include> 
<% 
                    } 
                } 
catch(Exception e){ out.println(e); 
                } 
             } 
else{ 
out.println("<h1>PASSWORD MISMATCH<h1>"); 
    %> 
<jsp:include page="ndex.html"></jsp:include> 
<% 
                       } 
         %> 
 
 
 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<h1>LOGIN PAGE</h1> 
<form action="Login.jsp"> 
            Enter Username: <input type="text" name="txtName"><br> 
            Enter Password: <input type="password" name="txtPass"><br> 
<input type="submit" value="Login"><input type="reset"> 
</form> 
</body> 
</html> 
Login.jsp 
<%@page import="java.sql.Connection"%> 
<%@page import="java.sql.Statement"%> 
<%@page import="java.sql.DriverManager"%> 
<%@page import="java.sql.ResultSet"%> 
 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>Login JSP Page</h1> 
<% 
            String uname=request.getParameter("txtName"); 
            String pass=request.getParameter("txtPass");             ResultSet rs=null; try{ 
Class.forName("com.mysql.jdbc.Driver"); 
                Connection 
con=DriverManager.getConnection("jdbc:mysql://localhost:3306/logindb","root","root");                 Statement stmt=con.createStatement(); rs=stmt.executeQuery("select password from userpass where username='"+uname+"'"); 
rs.next(); if(pass.equals(rs.getString(1))){ out.println("<h1>LOGIN SUCCESSFULL<h1>"); 
                } 
else{ 
out.println("<h1>PASSWORD DOES NOT MATCH!<h1>"); 
    %> 
<jsp:include page="ndex.html"></jsp:include> 
<% 
                 } 
             } 
catch(Exception e){ out.println("<h1>USER DOES NOT EXIST<h1>"); 
    %> 
<jsp:include page="ndex.html"></jsp:include> 
<% 
                       } 
         %> 
</body> 
</html> 
Output 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
PRACTICAL NO. 5: Implement the following JSP and EL applications. 
Q.5.a. Create a html page with fields, eno, name, age, desg, salary. Now on submit this data to a JSP pagewhich will update the employee table of database with matching eno. 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<form method="post" action="UpdateEmp.jsp"> 
            Enter Employee Number: <input type="text" name="txtEno"><br><br> 
            Enter Employee Salary: <input type="text" name="txtSal"><br><br> 
<input type="reset"><input type="submit"> 
</form> 
</body> 
</html> 
UpdateEmp.jsp 
<%@page import="java.sql.ResultSet"%> 
<%@page import="java.sql.PreparedStatement"%> 
<%@page import="java.sql.DriverManager"%> 
<%@page import="java.sql.Connection"%> 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>UPDATING EMPLOYEE RECORD</h1> 
<% 
            String eno=request.getParameter("txtEno"); 
            String sal=request.getParameter("txtSal"); try 
            { 
Class.forName("com.mysql.jdbc.Driver"); 
                Connection 
con=DriverManager.getConnection("jdbc:mysql://localhost:3306/empbatchd","root","root");                 PreparedStatement stmt=con.prepareStatement("select * from emp where eno=?"); stmt.setString(1,eno); 
                ResultSet rs=stmt.executeQuery(); if(rs.next()) 
                { 
out.println("<h1>Employee"+rs.getString(1)+" Exists<h1><br>"); 
                    PreparedStatement pst=con.prepareStatement("update emp set sal=? where eno=?"); pst.setString(1,eno); pst.setString(2,sal); pst.executeUpdate(); out.println("<h1>EMPLOYEE RECORD UPDATED<br>"); 
                } 
else 
                { 
out.println("<h1>EMPLOYEE RECORD DOES NOT EXIST"); 
                } 
            } 
catch(Exception e) 
            { 
out.println(e); 
            } 
    %> 
</body> 
</html> 
 
Q.5.b. Create a JSP application to demonstrate the use of expression language (EL). 
index.jsp 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>Welcome to index.jsp</h1> 
<% session.setAttribute("user","Admin"); 
    %> 
<%  
            Cookie ck=new Cookie("name","mycookie"); response.addCookie(ck); 
    %> 
<form action="ExpressionLanguage.jsp"> 
        Enter Name: <input type="text" name="name"><br><br> 
<input type="submit" value="submit"> 
</form> 
</body> 
</html> 
ExpressionLanguage.jsp 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
        Welcome, ${param.name}<br> 
        Session value is ${sessionScope.user}<br> 
        Cookie name is ${cookie.name.value} 
</body> 
</html> 
Output 
 
ELArithmeticOperator.jsp 
<body> 
        5*5+4: ${5*5+4}<br> 
1.4E4+1.4: ${1.4E4+1.4}<br> 
10 mod 4: ${10 mod 4}<br> 
15 div 3: ${15 div 3}<br> 
</body> 
 
 
ELLogicalOperator.jsp 
<body> true and true: ${true and true} <br> true&& false: ${true && false} <br> true or true: ${true or true} <br> true || false: ${true || false} <br> not true: ${not true} <br> 
        !false: ${!false}<br> 
</body> 
Output 
 
<body> 
        10.0==10: ${10.0==10}<br> 
        10.0 eq 10: ${10.0 eq 10}<br> 
        ((20*10)!=200):${((20*10)!=200)} <br> 
3	ne 3: ${3 ne 3}<br> 
        3.2>=2: ${3.2>=2}<br> 
        3.2 ge 2: ${3.2 ge 2}<br> 
4	le 2: ${4 le 2}<br> 
</body> 
Output 
 
ELConditionalOperator.jsp 
<body> 
        THE RESULT OF 10>2 IS:  "${(10>1)?'greater':'lesser'}" 
</body> 
Output 
 
EmptyOperator.jsp 
<body> 
        The value for empty operator is:: ${empty "txxt"} 
</body> 
Output 
 
 
 
Q.5.c. Create a JSP application to demonstrate the use of JSTL (JSP standard tag library). index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 	 
<body> 
<a href="setDemo.jsp">setDemo</a> 
<a href="ForeachDemo.jsp">ForeachDemo</a> 
<a href="outDemo.jsp">outDemo</a> 
<a href="URLDemo.jsp">URLDemo</a> 
<a href="choose_when_otherwise.jsp">choose_when_otherwise</a> 
</body> 
</html> 
Output 
  
setDemo.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<c:set var="pageTitle" scope="application" value="THIS IS MY JSTL PRACTICAL"/> 
        ${pageTitle} 
</body> 
</html> 
Output 
 
ForeachDemo.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%> 
<c:forEach begin="1" end="10" var="i"> 
            THE SQUARE OF<c:out value= "${i}=${i*i}"/><br> 
</c:forEach> 
</body> 
</html> 
 
 
 
Output 
 
outDemo.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%> 
<c:set var="name" value="TYIT"/> 
MY NAME IS :<c:out value= "${name}"/> 
</body> 
</html> 
 
URLDemo.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<c:url value="/index.html"/> 
</body> </html> 
 
choose_when_otherwise.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<c:set var="income" value="${4000*4}"/> 
       YOUR INCOME IS:<c:out value="${income}"/> 
<c:choose> 
<c:when test ="${income <=1000}"> 
               INCOME IS NOT GOOD 
</c:when> 
<c:when test ="${income>10000}"> 
               INCOME IS VERY GOOD 
</c:when> 
<c:otherwise> 
                   INCOME UNDETERMINED 
</c:otherwise> 
</c:choose> 
</body> 
</html> 
 
 
 
 
 
 
PRACTICAL NO. 6: Implement the following EJB applications. Q.6.a. Create a Currency Converter application using EJB. 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<form action="CCServlet"> 
            ENTER AMOUNT: <input type="text" name="amt"><br><br> 
            SELECT CONVERSION TYPE: <br><input type="radio" name="type" value="r2d" checked/>RUPEES TO DOLLAR<br> 
<input type="radio" name="type" value="d2r"/>DOLLAR TO RUPEES<br> 
<input type="reset"> 
<input type="submit" name="Convert"><br> 
</form> 
</body> 
</html> 
CCBean.java 
package mybeans; import javax.ejb.Stateless; 
 
@Stateless public class CCBean implements CCBeanLocal { 
    @Override public Double r2Dollar(double r) { return r/79.96; 
    } 
 
    @Override public Double d2Rupees(double d) { return d*79.96; 
    } 
CCServlet.java 
@Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
 
double amt=Double.parseDouble(request.getParameter("amt")); if(request.getParameter("type").equals("r2d")) 
        { 
out.println("<h1>"+amt+" Rupees = "+cCBean.r2Dollar(amt)+" Dollars<h1>"); 
        } 
 
if(request.getParameter("type").equals("d2r")) 
        { 
out.println("<h1>"+amt+" Dollars = "+cCBean.d2Rupees(amt)+" Rupees<h1>"); 
        } 
    } 
 
 
 
Output 
 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
</head> 
<body> 
<form method="post" action="RoomClientServlet"> 
<br>No. of rooms<input type="text" name="t1"> 
<br><input type="submit" name="btn" value="CheckIN"> 
<br><input type="submit" name="btn" value="CheckOUT"> 
</form> 
</body> 
</html> 
 
RoomClientServlet.java 
package servlet; 
 
importejb.RoomBeanLocal; importjava.io.IOException; importjava.io.PrintWriter; importjavax.ejb.EJB; importjavax.servlet.ServletException; importjavax.servlet.annotation.WebServlet; importjavax.servlet.http.HttpServlet; importjavax.servlet.http.HttpServletRequest; importjavax.servlet.http.HttpServletResponse; 
@WebServlet(name = "RoomClientServlet", urlPatterns = {"/RoomClientServlet"}) public class RoomClientServlet extends HttpServlet { 
    @EJB RoomBeanLocalobj; 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response) throwsServletException, IOException { response.setContentType("text/html"); PrintWriter out = response.getWriter(); 
try { 
int no=Integer.parseInt(request.getParameter("t1"));      String b=request.getParameter("btn"); int res=0; if(b.equals("CheckIN")) 
 { 
res=obj.checkin(no); if (res==1) out.println(no + " rooms check-in"); 
 } 
if(b.equals("CheckOUT")) 
 { 
res=obj.checkout(no); if (res==1) out.println(no + " rooms check-out"); 
 } 
if(res==0) out.println("Not possible to do Check IN / OUT"); out.println("<br><br><a href=index.html>Back</a>"); 
 } finally { out.close(); 
 } 
 }  
 } 
RoomBean.java 
packageejb; importjavax.ejb.Stateless; importjava.sql.*; @Stateless public class RoomBean implements RoomBeanLocal {     @Override publicintcheckin(int no) { try 
 { 
Class.forName("com.mysql.jdbc.Driver"); 
     Connection con=DriverManager.getConnection("jdbc:mysql://localhost/hoteldb","root","root"); 
 
     String sql1 = "select * from room"; 
     Statement st= con.createStatement(); ResultSetrs = st.executeQuery(sql1); rs.next(); int total=rs.getInt(1); intocc=rs.getInt(2); int free=total-occ; 
System.out.println(total); System.out.println(free); if (free>=no) 
     { 
         String sql2="update room set occ=?"; 
PreparedStatementps=con.prepareStatement(sql2); ps.setInt(1, occ+no); int res=ps.executeUpdate(); return res; 
 } 
else return 0; 
 } 
catch(ClassNotFoundException | SQLException e) 
 { 
return 0; 
 } 
    } 
    @Override publicint checkout(int no) { try 
{ Class.forName("com.mysql.jdbc.Driver");  Connection con=DriverManager.getConnection("jdbc:mysql://localhost/hoteldb","root","root"); 
 String sql1 = "select * from room"; 
 Statement st= con.createStatement(); ResultSetrs=st.executeQuery(sql1); rs.next(); int total=rs.getInt(1); intocc=rs.getInt(2); if (occ>=no) 
 { 
 String sql2="update room set occ=?"; 
PreparedStatementps=con.prepareStatement(sql2); ps.setInt(1, occ-no); int res=ps.executeUpdate(); return res; 
 } 
else return 0; 
 } 
catch(ClassNotFoundException | SQLException e) 
 { 
return 0; 
 } 
 }  
} 
 
 
 
PRACTICAL NO. 7: Implement the following EJB applications with different types of beans. 
Q.7.a. Develop simple EJB application to demonstrate Servlet Hit count using SingletonSession Beans. 
index.html 
<html> 
<head> 
<title>TODO supply a title</title> 
<meta charset="UTF-8"> 
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
<meta http-equiv="Refresh" content="0; URL=ServletClient"> 
</head> 
<body></body> 
</html> 
CountServletHitBean.java 
package mybeans; import javax.ejb.Singleton; 
@Singleton public class CountServletHitBean { private int hitCount; public synchronized int getCount() 
    { 
return hitCount++; 
    } 
} 
ServletClient.java 
@Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { response.setContentType("text/html;charset=UTF-8"); 
        PrintWriter out = response.getWriter(); 
out.println("<b>NUMBER OF TIMES THE SERVLET IS ACCESSED : </b>"+countServletHitBean.getCount()); 
    } 
 
Q.7.b. Develop simple Marks Entry Application to demonstrate accessing Database usingEJB. 
QuesAnsDBServlet.java 
package dbapp; 
@WebServlet(name = "QuesAnsDB", urlPatterns = {"/QuesAnsDB"}) public class QuesAnsDB extends HttpServlet { 
@Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throwsServletException, IOException { response.setContentType("text/html"); PrintWriter out = response.getWriter(); try 
 { 
out.print("<html><body><br>"); out.println("<form method='post' action='Marks'>"); 
Class.forName("com.mysql.jdbc.Driver"); 
 Connection con=DriverManager.getConnection("jdbc:mysql://localhost/queansdb1","root","root"); 
 Statement st = con.createStatement(); 
 String sql="select * from queans"; 
ResultSet rs = st.executeQuery(sql); 
Inti=0; 
out.print("<center>Online Exam</center>"); while(rs.next()) 
 { 
i++; out.print("<br><br><hr>"+rs.getInt(1)+" "); out.print(rs.getString(2)); out.print("<br><input type=radio name="+i+" value=1>"+rs.getString(3)); out.print("<br><input type=radio name="+i+" value=2>"+rs.getString(4)); out.print("<br><input type=radio name="+i+" value=3>"+rs.getString(5)); out.print("<br><input type=radio name="+i+" value=4>"+rs.getString(6));  String ans="ans"+i; out.println("<br><input type=hidden name="+ans+" value="+rs.getString(7)+">"); 
 } 
out.println("<br><input type=hidden name=total value="+i+">"); out.println("<input type=submit value=submit>"); out.println("</form>"); out.print("</body></html>"); 
 } 
catch(Exception e) 
 { 
out.println("ERROR "+e.getMessage()); 
 } 
    } 
} 
Marks.java 
@Override protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
{ response.setContentType("text/html"); PrintWriter out = response.getWriter(); try 
{ out.print("<html><body>"); int total=Integer.parseInt(request.getParameter("total")); int marks=0; for(inti=1; i<=total; i++) 
 { 
 String sel=request.getParameter(new Integer(i).toString());  String ans=request.getParameter("ans"+i); if (sel.equals(ans)) marks++; 
 } 
out.println("Total Marks : "+marks); out.print("</body></html>"); 
 } 
catch(Exception e) 
 { 
out.println("ERROR "+e.getMessage()); 
 } 
 } 
} 
Output: 
 
 
 
 
PRACTICAL NO. 8:Implement Validation and Shopping Cart application using EJB. Q.8.a. Develop simple shopping cart application using EJB [Stateful Session Bean]. index.jsp 
<%@page import="java.util.Iterator"%> 
<%@page import="java.util.List"%> 
<%@page import="javax.naming.InitialContext"%> 
<%@page import="ejb.ShoppingCart"%> 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPE html> 
<%! 
private static ShoppingCart cart; 
 
public void jspInit() { try { 
InitialContextic = new InitialContext(); cart = (ShoppingCart) ic.lookup("java:global/batchD_8A/ShoppingCart"); 
        } catch (Exception ex) { 
System.out.println("Could not create cart bean." + ex.getMessage()); 
        } 
    } 
%> <% if (request.getParameter("txtCustomerName") != null) { cart.initialize(request.getParameter("txtCustomerName")); 
    } else { cart.initialize("Guest"); 
    } 
if (request.getParameter("btnRmvBook") != null) {         String books[] = request.getParameterValues("chkBook"); if (books != null) { for (int i = 0; i<books.length; i++) { cart.removeBook(books[i]); 
            } 
        } 
    } 
if (request.getParameter("btnAddBook") != null) {         String books[] = request.getParameterValues("chkBook"); if (books != null) { for (int i = 0; i<books.length; i++) { cart.addBook(books[i]); 
            } 
        } 
    } 
%> 
} 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>Shopping Cart</title> 
</head> 
<body style="background-color: blueviolet;"> 
<h1 style="text-align: center;">Books For Sale</h1><br> 
<form method="post"> 
                              Customer Name: <input type="text" name="txtCustomerName" value=<%=request.getParameter("txtCustomerName")%> /><br> 
<b>Book Titles</b><br> 
<input type="checkbox" name="chkBook" value="The life of SahilJadhav">The life of SahilJadhav<br> 
<input type="checkbox" name="chkBook" value="Chronicles of Mihir">Chronicles of Mihir<br> 
<input type="checkbox" name="chkBook" value="60 days of Gayatri">60 days of Gayatri<br> 
<input type="checkbox" name="chkBook" value="lIFE LESSON FROM cHINMAYpEDNEKAr">lIFE LESSON 
FROM cHINMAYpEDNEKAr<br> 
<br> 
<input type='submit' value='Add To My Basket' name='btnAddBook'> 
<input type='submit' value='Remove From My Basket'  name='btnRmvBook'><br><br><br> 
<% 
if (cart != null) { 
out.print("<b>Basket</b><br>"); 
                    List<String>bookList = cart.getContents();                     Iterator iterator = bookList.iterator(); while (iterator.hasNext()) { 
                        String title = (String) iterator.next(); 
            %> 
<%= title%><br> 
<% 
                    } 
                } 
            %> 
</form> 
</body> 
</html> 
ShoppingCart.java 
package ejb; import java.sql.Connection; import java.sql.DriverManager; import java.sql.ResultSet; import java.sql.SQLException; import java.sql.Statement; import java.util.ArrayList; import java.util.List; import javax.ejb.Remove; import javax.ejb.Stateful; 
 
@Stateful public class ShoppingCart { 
 
    List<String> contents;     String customerName; private Connection conn = null; privateResultSetrs; private Statement stmt = null; private String query = null; public void initialize(String person) throws SQLException { if (person != null) { 
customerName = person; 
try { 
Class.forName("com.mysql.jdbc.Driver").newInstance(); conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/cartdb3", "root", "root"); 
            } catch (ClassNotFoundException | IllegalAccessException | InstantiationException e) { System.err.println("Sorry failed to connect to the Database." + e.getMessage()); 
            } 
        } 
contents = new ArrayList<>(); 
    } 
 
public void addBook(String title) { try { 
stmt = (Statement) conn.createStatement(); query = "INSERT INTO cart VALUES('" + customerName + "','" + title + "')"; stmt.executeUpdate(query); 
        } catch (SQLException e) { 
System.err.println("Sorry failed to insert values from the database table. " + e.getMessage()); 
        } 
    } 
 
public void removeBook(String title) { 
try { 
stmt = (Statement) conn.createStatement(); 
            query = "DELETE FROM cart WHERE UserName='" + customerName + "' AND ItemName='" + title 
+ "'"; 
stmt.executeUpdate(query); 
        } catch (SQLException e) { 
System.err.println("Sorry failed to delete values from the database table. " + e.getMessage()); 
        } 
    } 
 
public List<String>getContents() { 
try { 
stmt = (Statement) conn.createStatement();             query = "SELECT * FROM cart WHERE UserName='" + customerName + "'"; rs = stmt.executeQuery(query); while (rs.next()) { contents.add(rs.getString("ItemName")); 
            } 
        } catch (SQLException e) { 
System.err.println("Sorry failed to select values from the database table. " + e.getMessage()); 
        } 
return contents; 
    } 
@Remove() 
public void remove() { contents = null; 
    } 
} 
Output 
  
  
 
Q.8.b. Develop a simple JSP application to pass values from one page to another with validations.(Nametxt, age-txt, hobbies-checkbox, email-txt, gender-radio button). 
index.jsp 
<html> 
<body> 
<form action="Validate.jsp"> 
            Enter Your Name <input type="text" name="name"><br> 
            Enter Your Age <input type="text" name="age"><br> 
            Select Hobbies <input type="checkbox" name="hob" value="Singing">Singing  
<input type="checkbox" name="hob" value="Reading">Reading Books  
<input type="checkbox" name="hob" value="Football">Playing Football<br> 
            Enter E-mail<input type="text" name="email"><br> 
            Select Gender <input type="radio" name="gender" value="male">Male  
<input type="radio" name="gender" value="female">Female  
<input type="radio" name="gender" value="other">Other<br> 
<input type="hidden" name="error" value=""> 
<input type="submit" value="Submit Form"> 
</form > 
</body> 
</html> 
Successful.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8"%> 
<!DOCTYPEhtml> 
<html> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>DATA VALIDATED SUCCESSFULLY</h1> 
</body> 
</html> 
 
Validate.jsp 
<%@page contentType="text/html" pageEncoding="UTF-8" import="mypack.*"%> <html> 
<head> 
<title>JSP Page</title> 
</head> 
<body> 
<h1>Validation Page</h1> 
<jsp:useBean id="obj" scope="request" class="mypack.CheckerBean" > 
<jsp:setProperty name="obj" property="*"/> 
</jsp:useBean> 
<%if (obj.validate()) {%> 
<jsp:forward page="Successful.jsp"/> 
<% } else {%> 
<jsp:include page="index.html"/> 
<%}%> 
<%=obj.getError()%> 
</body> 
</html> 
CheckerBean.java 
package mypack; public class CheckerBean { 
 
    String name, hob, email, gender, error; int age; 
 
public CheckerBean() { name = ""; 
hob = ""; email = ""; gender = ""; error = ""; age = 0; 
    } 
 
public void setName(String n) 
        { 
name=n; 
} 
public String getName() 
{ 
return name; 
} 
public void setAge(int a) 
{ 
age=a; 
} 
public int getAge() 
{ 
return age; 
} 
public void setHob(String h) 
{ 
hob=h; 
} 
public String getHob() 
{ 
return hob; 
} 
public void setEmail(String e) 
{ 
email=e; 
} 
public String getEmail() 
{ 
return email; 
} 
public void setGender(String g) 
{ 
gender=g; 
} 
public String getGender() 
{ 
return gender; 
} 
public String getError() 
        { 
return error; 
} 
public boolean validate() 
{ 
boolean res=true; if(name.trim().equals("")) 
{ 
error+="<br>Enter First Name"; res=false; 
} 
if(age<0||age>99) 
{ 
error+="<br>Age Invalid"; res=false; 
} 
String emailregex="^[_A-Za-z0-9-]+(\\.[_A-Za-z0-9-]+)*@[A-Za-z0-9-]+(\\.[A-Za-z0-9-]+)*(\\.[A-Zaz]{2,})$"; 
Boolean b=email.matches(emailregex); 
if(!b) 
{ 
error+="<br>email Invalid"; res=false; 
} 
return res; 
} 
} 
 
 
 
 
 
 
 
 
Output
