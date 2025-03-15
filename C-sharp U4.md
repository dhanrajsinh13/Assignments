Certainly! I'll guide you step-by-step through each of the assignments in your Visual Programming using C# practical assignment. These assignments involve database connectivity and Windows Forms. Let's start with the first one and proceed sequentially.

---

### **Assignment 1: Display City Names in ComboBox Using Database Connectivity**
Design a form that displays city names in a `ComboBox` control. The city names should be fetched from a database.

#### Steps:
1. **Create a Database**:
   - Use SQL Server or any other database (e.g., SQLite, MySQL).
   - Create a table named `City` with columns `CityCode` (int) and `CityName` (varchar).
   - Insert some sample data into the `City` table.

2. **Create a Windows Forms Application**:
   - Open Visual Studio.
   - Create a new project: `File -> New -> Project -> Windows Forms App (.NET Framework)`.
   - Name the project `CityComboBoxDB`.

3. **Add Database Connectivity**:
   - Install the required NuGet package for database connectivity (e.g., `System.Data.SqlClient` for SQL Server).
   - Add a connection string to your `App.config` file.

4. **Design the Interface**:
   - Add a `ComboBox` control to the form.
   - Set the `Name` property of the `ComboBox` to `cmbCities`.

5. **Write Code**:
   - Add the following code to load city names from the database into the `ComboBox`:

```csharp
using System;
using System.Data.SqlClient;
using System.Windows.Forms;

namespace CityComboBoxDB
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            LoadCities();
        }

        private void LoadCities()
        {
            string connectionString = "YourConnectionStringHere"; // Replace with your connection string
            string query = "SELECT CityName FROM City";

            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                SqlCommand command = new SqlCommand(query, connection);
                connection.Open();
                SqlDataReader reader = command.ExecuteReader();

                while (reader.Read())
                {
                    cmbCities.Items.Add(reader["CityName"].ToString());
                }
            }
        }
    }
}
```

6. **Run the Program**:
   - Press `F5` to run the program and test the `ComboBox`.

---

### **Assignment 2: Database Application with Record Navigation**
Write a program to develop a database application with record navigation (Next, Previous, First, Last) for a `Books` table.

#### Steps:
1. **Create a Database**:
   - Create a table named `Books` with columns `BookID`, `BookName`, `Qty`, `UnitPrice`, and `TotalPrice`.

2. **Create a Windows Forms Application**:
   - Create a new project named `BookNavigation`.

3. **Design the Interface**:
   - Add `TextBox` controls for `BookID`, `BookName`, `Qty`, `UnitPrice`, and `TotalPrice`.
   - Add `Button` controls for `Next`, `Previous`, `First`, and `Last`.

4. **Write Code**:
   - Add the following code to implement navigation:

```csharp
using System;
using System.Data.SqlClient;
using System.Windows.Forms;

namespace BookNavigation
{
    public partial class Form1 : Form
    {
        private SqlConnection connection;
        private SqlDataReader reader;

        public Form1()
        {
            InitializeComponent();
            connection = new SqlConnection("YourConnectionStringHere"); // Replace with your connection string
            LoadFirstRecord();
        }

        private void LoadFirstRecord()
        {
            string query = "SELECT TOP 1 * FROM Books";
            SqlCommand command = new SqlCommand(query, connection);
            connection.Open();
            reader = command.ExecuteReader();
            ReadRecord();
        }

        private void ReadRecord()
        {
            if (reader.Read())
            {
                txtBookID.Text = reader["BookID"].ToString();
                txtBookName.Text = reader["BookName"].ToString();
                txtQty.Text = reader["Qty"].ToString();
                txtUnitPrice.Text = reader["UnitPrice"].ToString();
                txtTotalPrice.Text = reader["TotalPrice"].ToString();
            }
        }

        private void btnNext_Click(object sender, EventArgs e)
        {
            ReadRecord();
        }

        private void btnPrevious_Click(object sender, EventArgs e)
        {
            // Implement logic to move to the previous record
        }

        private void btnFirst_Click(object sender, EventArgs e)
        {
            LoadFirstRecord();
        }

        private void btnLast_Click(object sender, EventArgs e)
        {
            // Implement logic to move to the last record
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test navigation.

---

### **Assignment 3: CRUD Operations on City Table**
Create a table `City` and provide Insert, Update, Select, and Delete operations using database connectivity.

#### Steps:
1. **Create a Database**:
   - Create a table named `City` with columns `CityCode` and `CityName`.

2. **Create a Windows Forms Application**:
   - Create a new project named `CityCRUD`.

3. **Design the Interface**:
   - Add `TextBox` controls for `CityCode` and `CityName`.
   - Add `Button` controls for `Insert`, `Update`, `Delete`, and `Select`.

4. **Write Code**:
   - Add the following code to perform CRUD operations:

```csharp
using System;
using System.Data.SqlClient;
using System.Windows.Forms;

namespace CityCRUD
{
    public partial class Form1 : Form
    {
        private SqlConnection connection;

        public Form1()
        {
            InitializeComponent();
            connection = new SqlConnection("YourConnectionStringHere"); // Replace with your connection string
        }

        private void btnInsert_Click(object sender, EventArgs e)
        {
            string query = "INSERT INTO City (CityCode, CityName) VALUES (@CityCode, @CityName)";
            SqlCommand command = new SqlCommand(query, connection);
            command.Parameters.AddWithValue("@CityCode", txtCityCode.Text);
            command.Parameters.AddWithValue("@CityName", txtCityName.Text);

            connection.Open();
            command.ExecuteNonQuery();
            connection.Close();
            MessageBox.Show("Record inserted successfully.");
        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {
            string query = "UPDATE City SET CityName = @CityName WHERE CityCode = @CityCode";
            SqlCommand command = new SqlCommand(query, connection);
            command.Parameters.AddWithValue("@CityCode", txtCityCode.Text);
            command.Parameters.AddWithValue("@CityName", txtCityName.Text);

            connection.Open();
            command.ExecuteNonQuery();
            connection.Close();
            MessageBox.Show("Record updated successfully.");
        }

        private void btnDelete_Click(object sender, EventArgs e)
        {
            string query = "DELETE FROM City WHERE CityCode = @CityCode";
            SqlCommand command = new SqlCommand(query, connection);
            command.Parameters.AddWithValue("@CityCode", txtCityCode.Text);

            connection.Open();
            command.ExecuteNonQuery();
            connection.Close();
            MessageBox.Show("Record deleted successfully.");
        }

        private void btnSelect_Click(object sender, EventArgs e)
        {
            string query = "SELECT * FROM City WHERE CityCode = @CityCode";
            SqlCommand command = new SqlCommand(query, connection);
            command.Parameters.AddWithValue("@CityCode", txtCityCode.Text);

            connection.Open();
            SqlDataReader reader = command.ExecuteReader();
            if (reader.Read())
            {
                txtCityName.Text = reader["CityName"].ToString();
            }
            connection.Close();
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test CRUD operations.

---

### **Assignment 4: CRUD Operations on Employee Table**
Create a table `Employee` and design a form to perform Insert, Update, and Delete operations.

#### Steps:
1. **Create a Database**:
   - Create a table named `Employee` with columns `Eno`, `Ename`, `Salary`, and `Designation`.

2. **Create a Windows Forms Application**:
   - Create a new project named `EmployeeCRUD`.

3. **Design the Interface**:
   - Add `TextBox` controls for `Eno`, `Ename`, `Salary`, and `Designation`.
   - Add `Button` controls for `Insert`, `Update`, and `Delete`.

4. **Write Code**:
   - Use similar CRUD logic as in Assignment 3.

---

### **Assignment 5: Book Table with Navigation**
Design a table `Book` in Access and provide Add, Update, Delete, Next, First, Last, and Previous functionalities.

#### Steps:
1. **Create an Access Database**:
   - Create a table named `Book` with columns `Bookcode`, `Bookpublisher`, `Bookauther`, `Bookpage`, and `Bprice`.

2. **Create a Windows Forms Application**:
   - Create a new project named `BookNavigationAccess`.

3. **Design the Interface**:
   - Add `TextBox` controls for each column.
   - Add `Button` controls for navigation and CRUD operations.

4. **Write Code**:
   - Use `OleDbConnection` for Access database connectivity.
   - Implement similar logic as in Assignment 2 and 3.

---

### **Assignment 6: Generate Report Using Report Viewer**
Generate a report using Report Viewer to show data from a database table.

#### Steps:
1. **Install Report Viewer**:
   - Install the `Microsoft.Reporting.WinForms` NuGet package.

2. **Create a Windows Forms Application**:
   - Create a new project named `ReportViewerExample`.

3. **Add a Report**:
   - Add a new Report (`.rdlc`) file to the project.
   - Design the report using the Report Designer.

4. **Write Code**:
   - Bind the report to data from the database.

```csharp
using System;
using System.Data.SqlClient;
using Microsoft.Reporting.WinForms;

namespace ReportViewerExample
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string connectionString = "YourConnectionStringHere"; // Replace with your connection string
            string query = "SELECT * FROM YourTable"; // Replace with your table name

            SqlConnection connection = new SqlConnection(connectionString);
            SqlDataAdapter adapter = new SqlDataAdapter(query, connection);
            System.Data.DataTable dt = new System.Data.DataTable();
            adapter.Fill(dt);

            ReportDataSource reportDataSource = new ReportDataSource("DataSet1", dt); // Replace "DataSet1" with your dataset name
            reportViewer1.LocalReport.DataSources.Add(reportDataSource);
            reportViewer1.RefreshReport();
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and view the report.

---

