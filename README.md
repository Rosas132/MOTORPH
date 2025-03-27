import java.util.Scanner;

public class Payrollsystem {

    // Employee class to store employee information
    static class Employee {
        String employeeNumber;
        String name;
        String birthday;
        int hoursWorked;
        double hourlyRate;
        double deductionsPercentage;

        // Constructor to initialize employee data
        public Employee(String employeeNumber, String name, String birthday, int hoursWorked, double hourlyRate, double deductionsPercentage) {
            this.employeeNumber = employeeNumber;
            this.name = name;
            this.birthday = birthday;
            this.hoursWorked = hoursWorked;
            this.hourlyRate = hourlyRate;
            this.deductionsPercentage = deductionsPercentage;
        }

        // Method to calculate the gross salary
        public double calculateGrossSalary() {
            return this.hoursWorked * this.hourlyRate;
        }

        // Method to calculate deductions
        public double calculateDeductions(double grossSalary) {
            return grossSalary * this.deductionsPercentage;
        }

        // Method to calculate the net salary
        public double calculateNetSalary(double grossSalary, double deductions) {
            return grossSalary - deductions;
        }

        // Method to display employee details and salary calculations
        public void displayEmployeeDetails() {
            double grossSalary = calculateGrossSalary();
            double deductions = calculateDeductions(grossSalary);
            double netSalary = calculateNetSalary(grossSalary, deductions);

            System.out.println("---------------------------------------------------------");
            System.out.println("Employee Number: " + this.employeeNumber);
            System.out.println("Employee Name: " + this.name);
            System.out.println("Birthday: " + this.birthday);
            System.out.println("---------------------------------------------------------");
            System.out.println("Gross Salary: $" + String.format("%.2f", grossSalary));
            System.out.println("Deductions: $" + String.format("%.2f", deductions));
            System.out.println("Net Salary: $" + String.format("%.2f", netSalary));
            System.out.println("---------------------------------------------------------");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Getting employee details from the user
        System.out.println("Enter Employee Number: ");
        String employeeNumber = scanner.nextLine();

        System.out.println("Enter Employee Name: ");
        String name = scanner.nextLine();

        System.out.println("Enter Employee Birthday (MM/DD/YYYY): ");
        String birthday = scanner.nextLine();

        System.out.println("Enter Hours Worked in a Week: ");
        int hoursWorked = scanner.nextInt();

        System.out.println("Enter Hourly Rate: ");
        double hourlyRate = scanner.nextDouble();

        System.out.println("Enter Deductions Percentage (e.g., 0.10 for 10%): ");
        double deductionsPercentage = scanner.nextDouble();

        // Create an Employee object
        Employee employee = new Employee(employeeNumber, name, birthday, hoursWorked, hourlyRate, deductionsPercentage);

        // Display employee details and calculate salary
        employee.displayEmployeeDetails();

        scanner.close();
    }
}
