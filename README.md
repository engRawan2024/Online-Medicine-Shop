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
...
