# Project Documentation

## Project Overview
This project is a Java-based application for managing employee data and attendance records. The application connects to a MySQL database to perform CRUD operations on employee data and to track employee attendance. The application has two types of users: admin and regular employees. Admin users can manage employee data and view attendance reports, while regular employees can mark their attendance and view their attendance reports.

## Table of Contents
1. [Getting Started](#getting-started)
2. [Database Setup](#database-setup)
3. [Running the Application](#running-the-application)
4. [Application Features](#application-features)
    - [Admin Menu](#admin-menu)
    - [User Menu](#user-menu)
5. [Code Structure](#code-structure)
6. [Detailed Method Descriptions](#detailed-method-descriptions)
7. [Common Issues and Troubleshooting](#common-issues-and-troubleshooting)

## Getting Started

### Prerequisites
- Java Development Kit (JDK) 8 or higher
- MySQL database
- IDE such as NetBeans, IntelliJ IDEA, or Eclipse

### Installing
1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/yourrepository.git
   ```
2. **Open the project** in your preferred IDE.

### Database Setup
1. **Create a MySQL database** named `data_karyawan`.
2. **Run the following SQL script** to create the necessary tables:

```sql
CREATE DATABASE data_karyawan;

USE data_karyawan;

CREATE TABLE karyawan (
    id INT PRIMARY KEY,
    nama VARCHAR(50),
    yourusername VARCHAR(50),
    yourpassword VARCHAR(50)
);

CREATE TABLE absensi (
    karyawan_id INT,
    tanggal DATE,
    PRIMARY KEY (karyawan_id, tanggal),
    FOREIGN KEY (karyawan_id) REFERENCES karyawan(id)
);
```

3. **Update the database credentials** in the `getConnection` method in the `Main` class:
```java
con = DriverManager.getConnection("jdbc:mysql://localhost/data_karyawan", "yourusername", "yourpassword");
```

## Running the Application
1. **Compile and run** the `Main` class.
2. **Log in** with your username and password.

## Application Features

### Admin Menu
- **Input data karyawan**: Add a new employee to the database.
- **Edit data karyawan**: Modify existing employee data.
- **Laporan absensi**: View today's attendance report.
- **Rekap absensi**: View attendance report for a specific employee.
- **Hapus data karyawan**: Delete an employee from the database.
- **Exit**: Exit the application.

### User Menu
- **Presensi karyawan**: Mark attendance for the day.
- **Laporan absensi**: View today's attendance report.
- **Exit**: Exit the application.

## Code Structure
- **Main class**: Contains the main logic for the application, including user login, menu navigation, and database operations.
- **getConnection method**: Establishes a connection to the MySQL database.
- **login method**: Verifies user credentials and returns the user ID.
- **adminMenu method**: Provides options for admin users to manage employee data and view reports.
- **userMenu method**: Provides options for regular users to mark attendance and view reports.

## Detailed Method Descriptions

### getConnection
Establishes a connection to the MySQL database.
```java
public static Connection getConnection()
```

### login
Verifies the user credentials and returns the user ID if successful.
```java
static int login(String username, String password, Connection conn)
```

### adminMenu
Displays the admin menu and handles admin operations.
```java
static void adminMenu(Scanner scanner, Connection conn)
```

### userMenu
Displays the user menu and handles user operations.
```java
static void userMenu(Scanner scanner, Connection conn, int loggedInUserId)
```

### inputDataKaryawan
Allows the admin to add a new employee to the database.
```java
static void inputDataKaryawan(Scanner scanner, Connection conn)
```

### editDataKaryawan
Allows the admin to edit existing employee data.
```java
static void editDataKaryawan(Scanner scanner, Connection conn)
```

### laporanAbsensi
Generates a report of today's attendance.
```java
static void laporanAbsensi(Connection conn)
```

### rekapAbsensi
Generates a detailed attendance report for a specific employee.
```java
static void rekapAbsensi(Connection conn, int karyawanId)
```

### deleteKaryawan
Deletes an employee from the database.
```java
static void deleteKaryawan(Connection conn, int karyawanId)
```

### presensiKaryawan
Marks attendance for the logged-in user.
```java
static void presensiKaryawan(Scanner scanner, Connection conn, int loggedInUserId)
```

## Common Issues and Troubleshooting
- **Database connection issues**: Ensure the database credentials are correct and the MySQL server is running.
- **SQL exceptions**: Check the SQL syntax and ensure the tables exist in the database.
- **Null pointer exceptions**: Ensure all objects are properly initialized before use.

For further assistance, please refer to the [Java documentation](https://docs.oracle.com/en/java/) and [MySQL documentation](https://dev.mysql.com/doc/).
