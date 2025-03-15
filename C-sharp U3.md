Certainly! I'll guide you step-by-step through each of the assignments in your Visual Programming using C# practical assignment(Unit-3). Let's start with the first one and proceed sequentially.

---

### **Assignment 1: User-Defined Function to Find Minimum Number**
Write a program that uses a user-defined function to find the minimum number out of two numbers.

#### Steps:
1. **Create a Console Application**:
   - Open Visual Studio.
   - Create a new project: `File -> New -> Project -> Console App (.NET Framework)`.
   - Name the project `FindMinimumNumber`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace FindMinimumNumber
{
    class Program
    {
        // User-defined function to find the minimum of two numbers
        static int FindMinimum(int num1, int num2)
        {
            return (num1 < num2) ? num1 : num2;
        }

        static void Main(string[] args)
        {
            Console.Write("Enter the first number: ");
            int number1 = Convert.ToInt32(Console.ReadLine());

            Console.Write("Enter the second number: ");
            int number2 = Convert.ToInt32(Console.ReadLine());

            int minimum = FindMinimum(number1, number2);
            Console.WriteLine($"The minimum number is: {minimum}");
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test the function.

---

### **Assignment 2: Implement a Class and Call Method Using Object**
Write a program to implement a class and call a method from the class using an object.

#### Steps:
1. **Create a Console Application**:
   - Create a new project named `ClassAndObject`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace ClassAndObject
{
    // Define a class
    class Calculator
    {
        // Method to add two numbers
        public int Add(int num1, int num2)
        {
            return num1 + num2;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Create an object of the Calculator class
            Calculator calc = new Calculator();

            Console.Write("Enter the first number: ");
            int number1 = Convert.ToInt32(Console.ReadLine());

            Console.Write("Enter the second number: ");
            int number2 = Convert.ToInt32(Console.ReadLine());

            // Call the Add method using the object
            int result = calc.Add(number1, number2);
            Console.WriteLine($"The sum is: {result}");
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test the class and method.

---

### **Assignment 3: Use of Constructor**
Write a program to show the use of a constructor and call the constructor.

#### Steps:
1. **Create a Console Application**:
   - Create a new project named `ConstructorExample`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace ConstructorExample
{
    // Define a class with a constructor
    class Person
    {
        public string Name { get; set; }
        public int Age { get; set; }

        // Constructor
        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }

        // Method to display person details
        public void DisplayDetails()
        {
            Console.WriteLine($"Name: {Name}, Age: {Age}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Create an object of the Person class and call the constructor
            Person person = new Person("John Doe", 25);

            // Call the method to display details
            person.DisplayDetails();
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test the constructor.

---

### **Assignment 4: Constructor Overloading**
Write a program to show the use of constructor overloading.

#### Steps:
1. **Create a Console Application**:
   - Create a new project named `ConstructorOverloading`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace ConstructorOverloading
{
    // Define a class with multiple constructors
    class Rectangle
    {
        public int Length { get; set; }
        public int Width { get; set; }

        // Default constructor
        public Rectangle()
        {
            Length = 0;
            Width = 0;
        }

        // Parameterized constructor
        public Rectangle(int length, int width)
        {
            Length = length;
            Width = width;
        }

        // Method to calculate area
        public int CalculateArea()
        {
            return Length * Width;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Create objects using different constructors
            Rectangle rect1 = new Rectangle();
            Rectangle rect2 = new Rectangle(10, 20);

            Console.WriteLine($"Area of rect1: {rect1.CalculateArea()}");
            Console.WriteLine($"Area of rect2: {rect2.CalculateArea()}");
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test constructor overloading.

---

### **Assignment 5: Function (Method) Overloading**
Write a program to implement function (method) overloading.

#### Steps:
1. **Create a Console Application**:
   - Create a new project named `MethodOverloading`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace MethodOverloading
{
    // Define a class with overloaded methods
    class Calculator
    {
        // Method to add two integers
        public int Add(int num1, int num2)
        {
            return num1 + num2;
        }

        // Method to add three integers
        public int Add(int num1, int num2, int num3)
        {
            return num1 + num2 + num3;
        }

        // Method to add two double values
        public double Add(double num1, double num2)
        {
            return num1 + num2;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Calculator calc = new Calculator();

            Console.WriteLine($"Sum of 5 and 10: {calc.Add(5, 10)}");
            Console.WriteLine($"Sum of 5, 10, and 15: {calc.Add(5, 10, 15)}");
            Console.WriteLine($"Sum of 5.5 and 10.5: {calc.Add(5.5, 10.5)}");
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test method overloading.

---

### **Assignment 6: Implement Inheritance**
Write a program to implement inheritance.

#### Steps:
1. **Create a Console Application**:
   - Create a new project named `InheritanceExample`.

2. **Write Code**:
   - Add the following code to the `Program.cs` file:

```csharp
using System;

namespace InheritanceExample
{
    // Base class
    class Animal
    {
        public void Eat()
        {
            Console.WriteLine("The animal is eating.");
        }
    }

    // Derived class
    class Dog : Animal
    {
        public void Bark()
        {
            Console.WriteLine("The dog is barking.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Create an object of the derived class
            Dog dog = new Dog();

            // Call methods from the base and derived class
            dog.Eat();
            dog.Bark();
        }
    }
}
```

3. **Run the Program**:
   - Press `F5` to run the program and test inheritance.

---

