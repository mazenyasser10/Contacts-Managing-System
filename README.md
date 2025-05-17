# Contact-Management-System-Java
This project is a Contact Management System developed using Java and MySQL. The application enables users to add, view, and delete contacts with a simple graphical user interface (GUI) built using Java Swing. Data persistence is handled via a MySQL database connection using JDBC.
## Objectives
    • Create a Java-based application to store and manage contacts information.
    • Implement CRUD (Create, Read, Update, Delete) operations.
    • To demonstrate integration between a Java Swing GUI and a MySQL database.
    • Store contact data in a database for persistence.
    • To apply exception handling and input validation techniques.
    • Ensure data validation and error handling
## Algorithm and external libraries
### *Main Algorithms Used:*
    •  On application start, MainFrame calls loadContacts() to fetch all records from the database and display them in a JTable.
    • AddContactFrame allows users to enter contact information, which is then validated and inserted into the MySQL database using an SQL INSERT query.
    •  Upon selection and confirmation, a contact is deleted using a SQL DELETE query through the deleteSelectedContact() method in MainFrame.
### *External Libraries:*
#### 1. javax.swing: Java’s built-in Swing library is used for creating the graphical user interface (GUI)
    JFrame, JPanel: Windows and panels to organize the layout.
    JTable: To display tabular contact data.
    JButton: Interactive buttons for user actions.
    JScrollPane: To provide scrollable views for large tables.
    JOptionPane: For dialog boxes (confirmation, alerts)
#### 2. java.sql: provides classes and interfaces for accessing and processing data stored in a relational database using SQL, To perform database operations such as querying, inserting, and deleting contacts.
    Connection: Establishes connection with the MySQL database.
    PreparedStatement: Prepares and executes SQL queries safely, avoiding SQL injection.
    ResultSet: Holds the results of SQL SELECT queries.
    Statement: (if used) Executes simple SQL commands.
#### 3. JDBC (Java Database Connectivity):  is an API (Application Programming Interface) that enables Java applications to connect and execute SQL statements with databases like MySQL.
    provides the core functionality to connect Java applications with MySQL databases. 
    It allows opening database connections, executing SQL queries safely using PreparedStatements, and handles transactions and errors to ensure smooth, efficient communication between the Java app and the database.
## GUI and Database Usage
  GUI (Graphical User Interface) : is developed using Java Swing, part of the javax.swing package, which provides components for building desktop applications.
### *Main Window (MainFrame):*
    • Displays contacts in a JTable named tableClients. The table shows four columns: Name, Phone, E-Mail, and Address.
    • The table supports automatic row sorting and has a customized appearance with a dark background and highlighted text for better readability.
    • Two buttons below the table allow the user to manage contacts (AddContactFrame) and (Delete Contact)
             
**Layout Details:** The main window uses a JPanel with a GroupLayout for arranging components vertically: label at the top, buttons in the middle, and the scrollable JTable at the bottom. The GUI uses consistent coloring for an aesthetic look and enhanced usability.
### *Database Usage*
#### 1•  Database System: 
  MySQL database accessed via JDBC for storing contact information persistently.
#### 2•  Connection Management:
    • Uses a separate class DBConnection (not shown here) to manage connections via DriverManager.getConnection().
    • Database operations use PreparedStatements to securely run SQL queries and avoid SQL injection.

#### The project works with a database table (assumed name: contacts) with the following columns:
     Coloumn Name        Data Type       Description
       
         Name             VARCHAR      Contact's full name
         Phone            VARCHAR      Contact's phone number
         E-mail           VARCHAR      Contact's email addrss
         Address          VARCHAR      Contact's physical address
#### 3•  Database operations:
Loading contacts: On app start, loadContacts() runs a SELECT query to fetch all contacts and populate the JTable ,Adding contacts: New contacts entered in AddContactFrame are inserted into the contacts table via an INSERT query, Deleting contacts: Selected contact is deleted by running a DELETE query matching the name and phone number.
## Code Explaining
### *Explaination ofJava Swing GUI + JDBC (Database)*
    This code is a GUI application for managing contacts (Add, View, Delete) using:
         • Java Swing :for building the graphical user interface (GUI).
         • JDBC : for connecting and interacting with a MySQL database.
         • OOP concepts :classes, methods, encapsulation.
 
#### 1• Classes: MainFrame
    Shows the list of contacts in a table, Lets the user add or delete a contact.
 
#### 2• Constructor: public MainFrame()
    Initializes GUI components (initComponents()), Sets the background color of the table scroll pane.
    Calls loadContacts() to show data from the database.
 
#### 3• Key GUI Components
      Component        ​ Purpose
      
      tableClients​      Displays contacts in rows (Name, Phone, Email, Address)
      btnAdd​            Opens a new window to add a contact
      btnDelete​         Deletes selected contact from table + database
 
#### 4• initComponents(): This method (auto-generated) builds the layout, Adds a label, table, scroll pane, and buttons to the panel. 
    Handles GUI setup using Swing layout managers.
 
#### 5• Button Actions 
    1. btnAddActionPerformed()  :Opens a new AddContactFrame (a new window for adding a contact).
    2. btnDeleteActionPerformed() :Calls deleteSelectedContact().
 
#### 6• deleteSelectedContact()
    Gets selected row data (Name + Phone),Asks for confirmation,  Deletes that contact from the contacts table in MySQL using JDBC,Calls loadContacts() again to refresh the table.
 
#### 7• loadContacts() 
    Connects to the MySQL database, Executes: SELECT Name, Phone, E-Mail, Address FROM contacts, Reads each row from result set, Adds it to tableClients.
    

### *Explanation of AddContactFrame.java*
    The AddContactFrame class is part of a Java Swing-based contact management system. It provides a GUI for users to enter and save new contact details (Name, Phone, Email, and Address).
#### 1• GUI Elements:
    • Four JTextFields for input: tfName, tfPhone, tfEmail, and tfAddress.
    • Two JButtons: btnAdd2 (to add the contact) and btnClear (to reset fields).
    • Labels and layout defined using Swing’s GroupLayout and JPanel.
#### 2• Add Button Functionality (btnAdd2ActionPerformed): When the "Add" button is clicked
    1. Input data is retrieved from the text fields
    2. Input is validated to ensure no field is empty.
    3. Phone number is checked to ensure it contains only digits.
    4. If valid:
                o The contact is added to the main table (MainFrame.AddRowToTable()).
                o A connection to the MySQL database is established via DBConnection.getConnection().
                o A PreparedStatement is used to insert the contact into the contacts table.
                o Fields are cleared and the form window is closed using dispose().
#### 4• Clear Button Functionality (btnClearActionPerformed): 
    Resets all input fields to blank.
#### 5• Form Initialization (initComponents()):
    This method, auto-generated by the NetBeans GUI editor, builds the layout and connects event listeners for the form.
#### 6• Main Method:
    Runs the form as a standalone window by calling new AddContactFrame().setVisible(true).
### *Explanation of DBConnection.java*
  #### 1. It manages connecting your Java program to a MySQL database.
  #### 2. package contactsmanagingsystem:Specifies that this class is part of the contactsmanagingsystem package.
  #### 3. private static final String URL = "jdbc:mysql://localhost:3306/contactsdb";:This is the database URL:
  #### 4. jdbc:mysql:// means you're using MySQL.
  #### 5. localhost:3306 means the database server is on your local machine at port 3306 (default MySQL port). contactsdb is the name of your database.
  #### 6. private static final String USER = "root";:The username for your MySQL database login.
  #### 7. private static final String PASSWORD = "";:The password for the MySQL user (empty string here).
  #### 8. public static Connection getConnection() throws SQLException:This method returns a Connection object, which is used to interact with the database.
  #### 9. It uses DriverManager.getConnection(URL, USER, PASSWORD) to open the connection.
  #### 10. It can throw an SQLException if something goes wrong (e.g., wrong credentials or database not available).
## Results
![WhatsApp Image 2025-05-17 at 12 38 32_996621a2](https://github.com/user-attachments/assets/fd52cc33-22df-4a1d-9a1f-d93d58f55af7)
![WhatsApp Image 2025-05-17 at 12 38 32_16b8495b](https://github.com/user-attachments/assets/9038337f-0d08-40b3-9c36-5fa2a4ff1f03)
![WhatsApp Image 2025-05-17 at 12 38 32_3cf12454](https://github.com/user-attachments/assets/23b432e1-facb-4f0e-941d-3948d9abadde)
![WhatsApp Image 2025-05-17 at 12 38 33_5fda5f35](https://github.com/user-attachments/assets/3c850836-be35-4065-9b4c-6ad64a10608c)
![WhatsApp Image 2025-05-17 at 12 38 33_37230e1f](https://github.com/user-attachments/assets/15696951-762a-4e1b-b9a8-c08ac135d0ee)
![WhatsApp Image 2025-05-17 at 12 38 33_0562e63f](https://github.com/user-attachments/assets/43d6dea0-1591-4b95-a305-e08f21fa4bc1)

## Acknowledgments
This project is part of the university Ptograming II course, supervised by Dr.Ahmed El Anany, Eng. Dina Magdy and Eng. Hussien Mostafa
### Credits to team members
    Team Member            Responsibility
    
    1. Mazen Yasser           ​GUI Design
    2. Jana​ M.Badry           Database Integration +Report
    3. Jasmine Ali            DBconnection class+invalidation
    4. Habiba Fekry           GitHub
    5. Sandy Atef             GUI design+Powerpoint











