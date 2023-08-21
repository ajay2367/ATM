# ATM
To connect Java to a SQL database, you typically use Java Database Connectivity (JDBC), which is a Java-based API that provides a standard way to interact with databases. Here are the general steps to connect Java to an SQL database using JDBC:

1. **Load the JDBC Driver**: JDBC drivers are specific to each database management system (DBMS). You need to load the appropriate driver class for the database you're using. This step is essential as it registers the driver with the DriverManager.

2. **Establish a Connection**: Use the DriverManager class to establish a connection to the database. You need to provide the database URL, username, and password as parameters to the `getConnection` method.

3. **Create a Statement or PreparedStatement**: Once you have a connection, you can create a Statement or PreparedStatement object. Statements are used to execute simple SQL queries, while PreparedStatements are used for executing parameterized queries.

4. **Execute SQL Queries**: Use the created Statement or PreparedStatement to execute SQL queries against the database. You can use methods like `executeQuery` for SELECT statements and `executeUpdate` for INSERT, UPDATE, DELETE statements.

5. **Retrieve Results**: If you're executing a SELECT query, you'll receive a ResultSet object. You can iterate through this object to retrieve the results of your query.

6. **Close Resources**: After you're done using the database connection and any related resources (such as statements and result sets), make sure to close them properly. This helps release resources and prevent memory leaks.

Here's a basic example of connecting Java to an SQL database using JDBC and performing a SELECT query:

```java
import java.sql.*;

public class JDBCTutorial {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database";
        String username = "your_username";
        String password = "your_password";

        try {
            // Load the JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Establish a connection
            Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

            // Create a statement
            Statement statement = connection.createStatement();

            // Execute a SELECT query
            String sqlQuery = "SELECT * FROM your_table";
            ResultSet resultSet = statement.executeQuery(sqlQuery);

            // Process the result set
            while (resultSet.next()) {
                String columnValue = resultSet.getString("column_name");
                System.out.println("Value: " + columnValue);
            }

            // Close resources
            resultSet.close();
            statement.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Remember to replace `your_database`, `your_username`, `your_password`, `your_table`, and `column_name` with your actual database information.

Also, note that handling exceptions and resource management is crucial in real-world applications. Consider using try-with-resources to ensure resources are properly closed even in case of exceptions.
