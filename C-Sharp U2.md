Certainly! I'll guide you step-by-step through each of the assignments in your Visual Programming using C# practical assignment (Unit-2). Let's start with the first one and proceed sequentially.

---

### **Assignment 1: Add and Remove Cities from ComboBox**
Design a form that allows the user to add a city from a `TextBox` to a `ComboBox`. If the city already exists in the `ComboBox`, show a message using a `MessageBox`. Also, allow the user to remove a city dynamically from the `ComboBox`.

#### Steps:
1. **Create a Windows Forms Application**:
   - Open Visual Studio.
   - Create a new project: `File -> New -> Project -> Windows Forms App (.NET Framework)`.
   - Name the project `CityComboBox`.

2. **Design the Interface**:
   - Drag and drop the following controls onto the form:
     - `TextBox` (for entering the city name).
     - `ComboBox` (to display the list of cities).
     - `Button` (for adding a city).
     - `Button` (for removing a city).

3. **Set Properties**:
   - Set the `Name` property of the `TextBox` to `txtCity`.
   - Set the `Name` property of the `ComboBox` to `cmbCities`.
   - Set the `Text` property of the buttons to `Add City` and `Remove City`.

4. **Write Code**:
   - Double-click the `Add City` button to generate the `Click` event handler.
   - Double-click the `Remove City` button to generate the `Click` event handler.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace CityComboBox
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnAddCity_Click(object sender, EventArgs e)
        {
            string city = txtCity.Text.Trim();
            if (string.IsNullOrEmpty(city))
            {
                MessageBox.Show("Please enter a city name.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                return;
            }

            if (cmbCities.Items.Contains(city))
            {
                MessageBox.Show("City already exists in the list.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            }
            else
            {
                cmbCities.Items.Add(city);
                txtCity.Clear();
            }
        }

        private void btnRemoveCity_Click(object sender, EventArgs e)
        {
            if (cmbCities.SelectedIndex != -1)
            {
                cmbCities.Items.RemoveAt(cmbCities.SelectedIndex);
            }
            else
            {
                MessageBox.Show("Please select a city to remove.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test adding/removing cities.

---

### **Assignment 2: State Names in ComboBox and ListBox**
Design a form with a `ComboBox` containing state names. When the user selects a state, store it in a `ListBox`. If the state already exists in the `ListBox`, display an appropriate message.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `StateListBox`.

2. **Design the Interface**:
   - Add a `ComboBox` (for state names).
   - Add a `ListBox` (to display selected states).

3. **Set Properties**:
   - Set the `Name` property of the `ComboBox` to `cmbStates`.
   - Set the `Name` property of the `ListBox` to `lstStates`.

4. **Write Code**:
   - Double-click the `ComboBox` to generate the `SelectedIndexChanged` event handler.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace StateListBox
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            // Add some states to the ComboBox
            cmbStates.Items.AddRange(new string[] { "California", "Texas", "New York", "Florida", "Illinois" });
        }

        private void cmbStates_SelectedIndexChanged(object sender, EventArgs e)
        {
            string selectedState = cmbStates.SelectedItem.ToString();
            if (lstStates.Items.Contains(selectedState))
            {
                MessageBox.Show("State already exists in the list.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            }
            else
            {
                lstStates.Items.Add(selectedState);
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test selecting states.

---

### **Assignment 3: Transfer Items Between ListBoxes**
Write a program to transfer one or more car names from one `ListBox` to another and vice versa.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `ListBoxTransfer`.

2. **Design the Interface**:
   - Add two `ListBox` controls (for car names).
   - Add two `Button` controls (for transferring items).

3. **Set Properties**:
   - Set the `Name` property of the `ListBox` controls to `lstCars1` and `lstCars2`.
   - Set the `Text` property of the buttons to `>>` and `<<`.

4. **Write Code**:
   - Double-click the buttons to generate the `Click` event handlers.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace ListBoxTransfer
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            // Add some car names to the first ListBox
            lstCars1.Items.AddRange(new string[] { "Toyota", "Honda", "Ford", "Chevrolet", "BMW" });
        }

        private void btnMoveRight_Click(object sender, EventArgs e)
        {
            MoveItems(lstCars1, lstCars2);
        }

        private void btnMoveLeft_Click(object sender, EventArgs e)
        {
            MoveItems(lstCars2, lstCars1);
        }

        private void MoveItems(ListBox source, ListBox destination)
        {
            if (source.SelectedItems.Count > 0)
            {
                foreach (var item in source.SelectedItems)
                {
                    destination.Items.Add(item);
                }
                while (source.SelectedItems.Count > 0)
                {
                    source.Items.Remove(source.SelectedItems[0]);
                }
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test transferring items.

---

### **Assignment 4: Textpad Application**
Implement a Textpad application using a `RichTextBox`. Create menus like `File` (New, Close, Close All, Exit), `Window` (Maximize, Minimize, Normal), and `Tile` (Horizontal, Vertical, Cascade). Use common dialog controls and implement functionalities.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `TextpadApp`.

2. **Design the Interface**:
   - Add a `RichTextBox` control.
   - Add a `MenuStrip` control.
   - Add `OpenFileDialog`, `SaveFileDialog`, and `FontDialog` controls.

3. **Set Properties**:
   - Set the `Dock` property of the `RichTextBox` to `Fill`.
   - Add menu items to the `MenuStrip`:
     - `File` -> `New`, `Open`, `Save`, `Close`, `Close All`, `Exit`.
     - `Window` -> `Maximize`, `Minimize`, `Normal`.
     - `Tile` -> `Horizontal`, `Vertical`, `Cascade`.

4. **Write Code**:
   - Double-click each menu item to generate the `Click` event handler.
   - Add the following code:

```csharp
using System;
using System.IO;
using System.Windows.Forms;

namespace TextpadApp
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void NewToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.Clear();
        }

        private void OpenToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                richTextBox1.LoadFile(openFileDialog1.FileName, RichTextBoxStreamType.PlainText);
            }
        }

        private void SaveToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                richTextBox1.SaveFile(saveFileDialog1.FileName, RichTextBoxStreamType.PlainText);
            }
        }

        private void CloseToolStripMenuItem_Click(object sender, EventArgs e)
        {
            richTextBox1.Clear();
        }

        private void ExitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        private void MaximizeToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.WindowState = FormWindowState.Maximized;
        }

        private void MinimizeToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.WindowState = FormWindowState.Minimized;
        }

        private void NormalToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.WindowState = FormWindowState.Normal;
        }

        private void HorizontalToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.LayoutMdi(MdiLayout.TileHorizontal);
        }

        private void VerticalToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.LayoutMdi(MdiLayout.TileVertical);
        }

        private void CascadeToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.LayoutMdi(MdiLayout.Cascade);
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test the Textpad application.

---

### **Assignment 5: Read and Write Text File**
Write a program that provides read and write functionality with a text file.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `TextFileReadWrite`.

2. **Design the Interface**:
   - Add a `RichTextBox` control.
   - Add two `Button` controls (for reading and writing).

3. **Set Properties**:
   - Set the `Text` property of the buttons to `Read` and `Write`.

4. **Write Code**:
   - Double-click the buttons to generate the `Click` event handlers.
   - Add the following code:

```csharp
using System;
using System.IO;
using System.Windows.Forms;

namespace TextFileReadWrite
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnRead_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                richTextBox1.Text = File.ReadAllText(openFileDialog1.FileName);
            }
        }

        private void btnWrite_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                File.WriteAllText(saveFileDialog1.FileName, richTextBox1.Text);
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test reading/writing text files.

---

### **Assignment 6: Read and Write Binary File**
Write a program that provides read and write functionality with a binary file.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `BinaryFileReadWrite`.

2. **Design the Interface**:
   - Add a `RichTextBox` control.
   - Add two `Button` controls (for reading and writing).

3. **Set Properties**:
   - Set the `Text` property of the buttons to `Read` and `Write`.

4. **Write Code**:
   - Double-click the buttons to generate the `Click` event handlers.
   - Add the following code:

```csharp
using System;
using System.IO;
using System.Windows.Forms;

namespace BinaryFileReadWrite
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnRead_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                using (BinaryReader reader = new BinaryReader(File.Open(openFileDialog1.FileName, FileMode.Open)))
                {
                    richTextBox1.Text = reader.ReadString();
                }
            }
        }

        private void btnWrite_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                using (BinaryWriter writer = new BinaryWriter(File.Open(saveFileDialog1.FileName, FileMode.Create)))
                {
                    writer.Write(richTextBox1.Text);
                }
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test reading/writing binary files.

---
