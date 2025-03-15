Certainly! I'll guide you step-by-step through each of the assignments in your Visual Programming using C# practical assignment. Let's start with the first one and proceed sequentially.

---

### **Assignment 1: Arithmetic Calculator**
Design an interface and implement functionalities for an arithmetic calculator with Addition, Multiplication, Subtraction, Division, and Clear functionalities.

#### Steps:
1. **Create a Windows Forms Application**:
   - Open Visual Studio.
   - Create a new project: `File -> New -> Project -> Windows Forms App (.NET Framework)`.
   - Name the project `ArithmeticCalculator`.

2. **Design the Interface**:
   - Drag and drop the following controls onto the form:
     - `TextBox` (for input and display).
     - `Buttons` for `+`, `-`, `*`, `/`, `=`, and `Clear`.
     - Label (optional for displaying the result).

3. **Set Properties**:
   - Set the `Text` property of buttons to `+`, `-`, `*`, `/`, `=`, and `Clear`.
   - Set the `Name` property of the `TextBox` to `txtDisplay`.

4. **Write Code**:
   - Double-click each button to generate the `Click` event handler.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace ArithmeticCalculator
{
    public partial class Form1 : Form
    {
        private double result = 0;
        private string operation = "";
        private bool isOperationPerformed = false;

        public Form1()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, EventArgs e)
        {
            if ((txtDisplay.Text == "0") || (isOperationPerformed))
                txtDisplay.Clear();

            isOperationPerformed = false;
            Button button = (Button)sender;
            txtDisplay.Text = txtDisplay.Text + button.Text;
        }

        private void Operator_Click(object sender, EventArgs e)
        {
            Button button = (Button)sender;
            operation = button.Text;
            result = Double.Parse(txtDisplay.Text);
            isOperationPerformed = true;
        }

        private void ButtonEquals_Click(object sender, EventArgs e)
        {
            switch (operation)
            {
                case "+":
                    txtDisplay.Text = (result + Double.Parse(txtDisplay.Text)).ToString();
                    break;
                case "-":
                    txtDisplay.Text = (result - Double.Parse(txtDisplay.Text)).ToString();
                    break;
                case "*":
                    txtDisplay.Text = (result * Double.Parse(txtDisplay.Text)).ToString();
                    break;
                case "/":
                    txtDisplay.Text = (result / Double.Parse(txtDisplay.Text)).ToString();
                    break;
            }
        }

        private void ButtonClear_Click(object sender, EventArgs e)
        {
            txtDisplay.Text = "0";
            result = 0;
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test the calculator.

---

### **Assignment 2: Scrollbars for Background Color**
Write a program that takes three scrollbars and three textboxes. Based on the combined value of the scrollbars, change the background color of a label and display each scrollbar's current value in a textbox.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `ScrollbarColorChanger`.

2. **Design the Interface**:
   - Add three `HScrollBar` controls (for Red, Green, Blue).
   - Add three `TextBox` controls to display the scrollbar values.
   - Add a `Label` to display the background color.

3. **Set Properties**:
   - Set the `Maximum` property of each scrollbar to `255` (RGB range).
   - Set the `Name` property of the scrollbars to `hScrollBarRed`, `hScrollBarGreen`, and `hScrollBarBlue`.
   - Set the `Name` property of the textboxes to `txtRed`, `txtGreen`, and `txtBlue`.

4. **Write Code**:
   - Double-click each scrollbar to generate the `Scroll` event handler.
   - Add the following code:

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace ScrollbarColorChanger
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void UpdateColor()
        {
            int red = hScrollBarRed.Value;
            int green = hScrollBarGreen.Value;
            int blue = hScrollBarBlue.Value;

            txtRed.Text = red.ToString();
            txtGreen.Text = green.ToString();
            txtBlue.Text = blue.ToString();

            label1.BackColor = Color.FromArgb(red, green, blue);
        }

        private void hScrollBarRed_Scroll(object sender, ScrollEventArgs e)
        {
            UpdateColor();
        }

        private void hScrollBarGreen_Scroll(object sender, ScrollEventArgs e)
        {
            UpdateColor();
        }

        private void hScrollBarBlue_Scroll(object sender, ScrollEventArgs e)
        {
            UpdateColor();
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test the scrollbars.

---

### **Assignment 3: Radio Buttons for Label Color**
Design a form with eight radio buttons. When the user selects any radio button, the label's background color will change based on the selected color.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `RadioButtonColorChanger`.

2. **Design the Interface**:
   - Add eight `RadioButton` controls (for colors like Red, Green, Blue, Yellow, etc.).
   - Add a `Label` to display the background color.

3. **Set Properties**:
   - Set the `Text` property of each radio button to the color name (e.g., "Red", "Green").
   - Set the `Name` property of the label to `lblColor`.

4. **Write Code**:
   - Double-click each radio button to generate the `CheckedChanged` event handler.
   - Add the following code:

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace RadioButtonColorChanger
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void RadioButton_CheckedChanged(object sender, EventArgs e)
        {
            RadioButton radioButton = (RadioButton)sender;
            if (radioButton.Checked)
            {
                switch (radioButton.Text)
                {
                    case "Red":
                        lblColor.BackColor = Color.Red;
                        break;
                    case "Green":
                        lblColor.BackColor = Color.Green;
                        break;
                    case "Blue":
                        lblColor.BackColor = Color.Blue;
                        break;
                    case "Yellow":
                        lblColor.BackColor = Color.Yellow;
                        break;
                    // Add more cases for other colors
                }
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test the radio buttons.

---

### **Assignment 4: Checkboxes for Font Style**
Design an application with three checkboxes for Bold, Italic, and Underline. Based on the selection, change the font style of the label text.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `FontStyleChanger`.

2. **Design the Interface**:
   - Add three `CheckBox` controls (for Bold, Italic, Underline).
   - Add a `Label` to display the text.

3. **Set Properties**:
   - Set the `Text` property of the checkboxes to "Bold", "Italic", and "Underline".
   - Set the `Name` property of the label to `lblText`.

4. **Write Code**:
   - Double-click each checkbox to generate the `CheckedChanged` event handler.
   - Add the following code:

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleChanger
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void UpdateFontStyle()
        {
            FontStyle style = FontStyle.Regular;

            if (checkBoxBold.Checked)
                style |= FontStyle.Bold;
            if (checkBoxItalic.Checked)
                style |= FontStyle.Italic;
            if (checkBoxUnderline.Checked)
                style |= FontStyle.Underline;

            lblText.Font = new Font(lblText.Font, style);
        }

        private void checkBoxBold_CheckedChanged(object sender, EventArgs e)
        {
            UpdateFontStyle();
        }

        private void checkBoxItalic_CheckedChanged(object sender, EventArgs e)
        {
            UpdateFontStyle();
        }

        private void checkBoxUnderline_CheckedChanged(object sender, EventArgs e)
        {
            UpdateFontStyle();
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and test the checkboxes.

---

### **Assignment 5: Progress Bar with Timer**
Write a program that uses a progress bar and a timer control to generate output.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `ProgressBarTimer`.

2. **Design the Interface**:
   - Add a `ProgressBar` control.
   - Add a `Timer` control from the toolbox.

3. **Set Properties**:
   - Set the `Maximum` property of the progress bar to `100`.
   - Set the `Interval` property of the timer to `100` (milliseconds).

4. **Write Code**:
   - Double-click the form to generate the `Load` event handler.
   - Double-click the timer to generate the `Tick` event handler.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace ProgressBarTimer
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            timer1.Start();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (progressBar1.Value < progressBar1.Maximum)
                progressBar1.Value++;
            else
                timer1.Stop();
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program and observe the progress bar filling up.

---

### **Assignment 6: PictureBox with File Dialog**
Write a program that uses a PictureBox, TextBox, and Button. Provide a runtime file open dialog to select an image and display it in the PictureBox, along with the image path in the TextBox.

#### Steps:
1. **Create a Windows Forms Application**:
   - Create a new project named `PictureBoxFileDialog`.

2. **Design the Interface**:
   - Add a `PictureBox` control.
   - Add a `TextBox` control.
   - Add a `Button` control.
   - Add an `OpenFileDialog` control from the toolbox.

3. **Set Properties**:
   - Set the `Name` property of the button to `btnLoadImage`.
   - Set the `Name` property of the textbox to `txtImagePath`.

4. **Write Code**:
   - Double-click the button to generate the `Click` event handler.
   - Add the following code:

```csharp
using System;
using System.Windows.Forms;

namespace PictureBoxFileDialog
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnLoadImage_Click(object sender, EventArgs e)
        {
            openFileDialog1.Filter = "Image Files|*.jpg;*.jpeg;*.png;*.bmp";
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                txtImagePath.Text = openFileDialog1.FileName;
                pictureBox1.ImageLocation = openFileDialog1.FileName;
            }
        }
    }
}
```

5. **Run the Program**:
   - Press `F5` to run the program, click the button, and select an image to display.

---
