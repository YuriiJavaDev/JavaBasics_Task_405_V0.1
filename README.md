# Student Management System: Foundational Blueprint (JavaBasics_Task_405_V0.1)

## 📖 Description
The first step in building a robust management system is defining the core entities. This project establishes the **Basic Class Structure** for a student record. By creating a public class, we ensure that the student blueprint is accessible to other components of the application. At this initial stage, the class focuses on a single responsibility: holding the student's name. This serves as the fundamental building block upon which more complex features (like grades, attendance, or IDs) will be constructed in future iterations.

## 📋 Requirements Compliance
- **Class Visibility**: Declared the class as `public` for global accessibility within the project.
- **Meaningful Naming**: Applied "Clean Code" standards by using the descriptive identifier `studentName` instead of generic names like "s" or "val".
- **Encapsulation Preparation**: Set up a basic class structure that can be easily extended with methods and further fields.
- **File Consistency**: Ensured the class name matches the file name (`Student.java`) for successful compilation.

## 🚀 Architectural Stack
- Java 8+ (OOP Basics)

## 🏗️ Implementation Details
- **Student**: The primary model class representing an individual learner.

## 📋 Expected result
```
The project compiles successfully, providing a valid `Student` type for use in other parts of the system.
```

## 💻 Code Example

Project Structure:

    JavaBasics_Task_405/
    ├── src/
    │   └── com/yurii/pavlenko/
    │                 └── school/
    │                     └── models/
    │                         └── Student.java
    ├── LICENSE
    ├── TASK.md
    ├── THEORY.md
    └── README.md

Code
```java
package com.yurii.pavlenko.school.models;

public class Student {
    public String studentName;
}
```

## ⚖️ License
This project is licensed under the **MIT License**.

Copyright (c) 2026 Yurii Pavlenko

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files...

License: [MIT](LICENSE)
