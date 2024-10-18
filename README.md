# Online-Medicine-Shop
The Online Medicine Shop is a web application developed in Java JSP MySQL that aims to streamline the drug supply process for pharmaceutical companies. It provides a platform for distributors and customers to interact, manage orders, and access relevant information.
## System Architecture :
The Online Medicine Shop Project in JSP MySQL is a web application developed to manage sales reporting and inventory in the pharmaceutical industry. The system has the following major components:

1. **Login Pages**:
   - Vendor Login
   - Customer Login

2. **Registration Page**: Allows users to register for the system.

3. **Customer Homepage**: Landing page for customers after login.

4. **Vendor Homepage**: Landing page for vendors after login.

5. **Buy Page**: Enables customers to make purchases.

6. **Vendor Restock Page**: Allows vendors to manage their inventory.

7. **Home Page**: Main dashboard for the application.

8. **Products**: Displays available products.

9. **Add Product**: Functionality to add new products to the system.

10. **Purchase Medicine**: Allows customers to purchase medicines.

11. **View Order**: Enables users to view their orders.

### System Components, Modules and Interactions

#### 1. **Frontend Components**:
   - **HTML Pages**: Responsible for the layout and structure of the web application.
   - **CSS Styling**: Provides the visual design elements and styles to enhance user interface.
   - **JavaScript**: Handles client-side validation tasks and interactive components.
   - **JSP (JavaServer Pages)**: Contains front-end logic and dynamic content generation.

#### 2. **Backend Components**:
   - **Java Classes**: Implement business logic and server-side operations.
   - **Servlets**: Handle HTTP requests, interact with databases, and manage application flow.
   - **MySQL Database**: Stores data related to products, users, orders, etc.

#### 3. **Core Modules**:

##### a. **User Authentication**:
   - **Vendor Login**: Allows vendors to access their accounts securely.
   - **Customer Login**: Grants customers access to the system with authentication.

##### b. **Product Management**:
   - **Add Product**: Enables vendors to add new products with details like ID, name, manufacturer, etc.
   - **View Products**: Displays available products for customers to browse and purchase.

##### c. **Order Processing**:
   - **Purchase Medicine**: Facilitates customers to place orders for medicines.
   - **View Order**: Allows users to track their orders and view order history.

##### d. **Inventory Management**:
   - **Vendor Restock Page**: Provides a platform for vendors to manage their inventory levels and restock items.

#### 4. **Interactions**:

- **User Interaction**:
  - Customers interact with the application to browse and purchase medicines.
  - Vendors interact to manage inventory and add new products.

- **Database Interaction**:
  - Java classes and servlets interact with the MySQL database for storing and retrieving data.
  - User authentication, product management, and order processing modules interact with the database to perform necessary operations.

- **Frontend-Backend Communication**:
  - HTML, CSS, and JavaScript in JSP pages communicate with Java classes and servlets to render dynamic content and handle user interactions.
  - Data submitted through frontend forms is processed by backend components for validation and storage.

- **Module Integration**:
  - The frontend and backend components are integrated to provide a seamless user experience.
  - Modules like user authentication, product management, order processing, and inventory management work together to ensure the smooth functioning of the online medicine shop application.

### Code Snippet Example:
#### 1. User Login Servlet
```java
		conn=DriverManager.getConnection("jdbc:mysql://localhost:3306/drugdatabase","root","1234");
		if(u==2)
		{ 
			ps=conn.prepareStatement(query2);
			ps.setString(1,uid1);
		}	
		else if(u==1)
		{ 
			ps=conn.prepareStatement(query1);
			ps.setString(1,uid1);
		}
		rs=ps.executeQuery();
		if(rs.next())
		{
			if((rs.getString(2)).equals(pass1))
			{
				if(u==1) 
					response.sendRedirect("Homepage.jsp");
				else 
					if(u==2) 
						response.sendRedirect("SellerHomepage.jsp");
			}
			else
			{
			response.sendRedirect("LoginError1.html");
			}
		}
		else
			response.sendRedirect("LoginError2.html");
	}
```
#### 2. Add Product JSP Form
	
	try {
		Class.forName("com.mysql.jdbc.Driver");
		conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/drugdatabase", "root", "1234");
		ps1 = conn.prepareStatement(query1);
		ps1.setString(1, prid);
		rs = ps1.executeQuery();
		if (!rs.next()) {
			ps2 = conn.prepareStatement(query2);
			ps2.setString(1, prid);
			ps2.setString(2, prname);
			ps2.setString(3, mfname);
			ps2.setString(4, mdate);
			ps2.setString(5, edate);
			ps2.setInt(6, price);
			int i = ps2.executeUpdate();
			ps3 = conn.prepareStatement(query3);
			ps3.setString(1, prid);
			ps3.setString(2, prname);
			ps3.setString(3, guid);
			ps3.setInt(4, quantity);
			int j = ps3.executeUpdate();
			response.sendRedirect("AddInventory.jsp");
		} else {
			response.sendRedirect("AddProductError.html");
		}
	} catch (Exception e) {
		response.sendRedirect("AddProductError2.html");
	}
	
### 4. Product Listing 
div class="active">
	<%@ page import="java.sql.*" %>
	<%@ page import="javax.sql.*" %>
	<%
	HttpSession httpSession = request.getSession();
    String uid=(String)httpSession.getAttribute("currentuser");
    %>
    
    <div class="filler"></div>
    
    <%
    int flag=0;
	ResultSet rs=null;
	PreparedStatement ps=null;
	java.sql.Connection conn=null;
	String query="select p.pname,p.pid,p.manufacturer,p.mfg,p.price,i.quantity from product p,inventory i where p.pid=i.pid";
	
	try{
		Class.forName("com.mysql.jdbc.Driver");
		conn=DriverManager.getConnection("jdbc:mysql://localhost:3306/drugdatabase","root","1234");
		ps=conn.prepareStatement(query);
		rs=ps.executeQuery();
		%><div class="filler2"></div>
				<div class="block">
				<%
		while(rs.next())
		{
			if(flag==4)
				{
				flag=1;
				%></div><div class="filler2"></div><%
				}
			else
			flag++;
		%>
			<div class="row">
 				<div class="column">
    				<div class="card">
    				<img src="images/pills.png" width=180 height=200>
  					<h1><%=rs.getString("pname") %></h1>
  					<p><b>ID: </b><%=rs.getString("pid") %></p>
					<p><b>Manufacturer: </b><%=rs.getString("manufacturer") %></p>
					<p><b>Mfg Date: </b><%=rs.getDate("mfg") %></p>
					<p><b>Stock: </b><%=rs.getInt("quantity") %></p>
					<p><b>Price: </b><%=rs.getInt("price") %></p>
					<%if (rs.getInt("quantity")>0) 
					{
					%>
  					<form action="PlaceOrder.jsp" method="post">
  					<input type="number" name="orderquantity" onkeypress="return event.charCode>= 48 && event.charCode<= 57" placeholder="Enter quantity" max="<%=rs.getInt("quantity") %>" required >
  					<input type="hidden" name="pid" value="<%=rs.getString("pid") %>">
  					<p></p>
  					<button>Buy</button></form></div>
  					<%
  					}
  					else	
  						{
  						%>
  					
  					<button>Out Of Stock</button></div>
  					<% 
  						} 
  					%>
  				</div>
  				<%
  				}
				%>
			</div>
		<%
	}
	catch(Exception e)
	{
		out.println("error: "+e);
	}
	finally {
	    try { if (rs != null) rs.close(); } catch (Exception e) {};
	    try { if (ps != null) ps.close(); } catch (Exception e) {};
	    try { if (conn != null) conn.close(); } catch (Exception e) {};
}
	%>

