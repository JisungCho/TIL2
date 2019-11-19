# 2019-11-18(Listener API)

- 여러 가지 서블릿 관련 Listener API

  - HttpSessionListener 이용해 로그인 접속자수 표시

    세션 객체의 생성/소멸 이벤트 발생 시 처리

    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>로그인창</title>
    </head>
    <body>
    	<form name="frmLogin" action="Login3" method = "post">
    		아이디 : <input type="text" name = "user_id"><br>
    		비밀번호 : <input type="password" name = user_pw><br>
    		<input type="submit" value="로그인"><input type = "reset" value="다시 입력">
    	</form>
    </body>
    </html>
    ```

    ```java
    package sec04.ex02;
    
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.util.ArrayList;
    import java.util.List;
    
    import javax.servlet.ServletContext;
    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import javax.servlet.http.HttpSession;
    
    /**
     * Servlet implementation class LoginTest
     */
    @WebServlet("/Login3")
    public class LoginTest extends HttpServlet {
    	ServletContext context = null;
    	List user_list = new ArrayList(); // 로그인한 접속자 ID를 저장하는 ArrayList입니다.
    	/**
    	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
    	 */
    	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		request.setCharacterEncoding("utf-8");
    		response.setContentType("text/html;charset=utf-8");
    		context = getServletContext(); //웹 애플리케이션  접근수준
    		//브라우저에 상관없이 접속한 아이디를 보기위해서 선언
    		
    		PrintWriter out = response.getWriter();
    		HttpSession session = request.getSession();
    		//현재 세션이 존재하면 기존 세션 리턴 , 없으면 새로 생성한 세션 리턴 (LoginImpl의 sessionCreated 메서드 호출)
    		
    		
    		String user_id = request.getParameter("user_id"); 
    		String user_pw = request.getParameter("user_pw");
    		// Login3.html에서 user_id와 user_pw의 value를 가져와 저장
    
    		
    		LoginImpl loginUser = new LoginImpl(user_id, user_pw);
    		//핸들러 객체 생성
    		
    
    		if(session.isNew()) {
    			session.setAttribute("loginUser", loginUser);
    			
    			
    			user_list.add(user_id);
    			context.setAttribute("user_list", user_list);
    			//접속자 아이디를 ArrayList인 user_list에 저장 후 다시 context객체에 user_list로 바인딩
    		}
    		out.print("<html>");
    		out.print("<head>");
    		out.print("<script type='text/javascript'>");
    		out.print("</script></head>");
    		out.print("<body>");
    		out.print("아이디는 : "+loginUser.user_id+"<br>");
    		out.print("총접속자수는 : "+LoginImpl.total_user+"<br><br>");
    		out.print("접속 아이디 : <br>");
    		
    		List list = (List) context.getAttribute("user_list");
    		//유저 리스트를 가져옴
    		for(int i=0;i<list.size();i++) {
    			out.print(list.get(i)+"<br>");
    		}
    		//유저를 출력
    		
    		out.print("<a href= 'Logout?user_id="+user_id+"'>로그아웃</a>");
    		out.print("</body></html>");
    	}
    
    }
    
    ```

    ```java
    package sec04.ex02;
    
    import javax.servlet.annotation.WebListener;
    import javax.servlet.http.HttpSessionEvent;
    import javax.servlet.http.HttpSessionListener;
    
    /**
     * Application Lifecycle Listener implementation class LoginImpl
     *
     */
    @WebListener
    public class LoginImpl implements HttpSessionListener { // 세션 객체의 생성or소멸 이벤트 발생시 처리
    	String user_id;
    	String user_pw;
    	static int total_user=0;
        /**
         * Default constructor. 
         */
        public LoginImpl() {
        }
        public LoginImpl(String user_id,String user_pw) {
        	this.user_id = user_id;
        	this.user_pw = user_pw;
        }
    	/**
         * @see HttpSessionListener#sessionCreated(HttpSessionEvent)
         */
        public void sessionCreated(HttpSessionEvent se)  { 
            System.out.println("세션 생성");
            total_user++;
        }
    
    	/**
         * @see HttpSessionListener#sessionDestroyed(HttpSessionEvent)
         */
        public void sessionDestroyed(HttpSessionEvent se)  { 
        	System.out.println("세션 소멸");
        	total_user--;
        }
    	
    }
    
    ```

    ```java
    package sec04.ex02;
    
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.util.List;
    
    import javax.servlet.ServletContext;
    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import javax.servlet.http.HttpSession;
    
    /**
     * Servlet implementation class LogoutTest
     */
    @WebServlet("/Logout")
    public class LogoutTest extends HttpServlet {
    	private static final long serialVersionUID = 1L;
    	ServletContext context;
    	/**
    	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
    	 */
    	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		doHandle(request, response);
    	}
    
    	/**
    	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
    	 */
    	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		doHandle(request, response);
    	}
    
    	private void doHandle(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		request.setCharacterEncoding("utf-8");
    		response.setContentType("text/html;charset=utf-8");
    		context = getServletContext();
    		PrintWriter out = response.getWriter();
    		HttpSession session = request.getSession();
    		
    		
    		String user_id =request.getParameter("user_id");
    		
    		session.invalidate(); 
    		//LoginImpl의 sessionDestroyed호출
    		
    		List user_list = (List) context.getAttribute("user_list");
    		user_list.remove(user_id);
    		
    		context.removeAttribute("user_list");
    		context.setAttribute("user_list", user_list);
    		//user_list 제거후 다시 갱신한 리스트를 저장
    	
    		out.print("<br>로그아웃했습니다.");
    	}
    }
    
    ```

