import java.util.Scanner;

public class PayrollSystem {

    // Employee class to store employee information
    static class Employee {
        String employeeNumber;
        String name;
        String birthday;
        String position;
        int hoursWorked;
        double hourlyRate;

        // Fixed deductions
        static final double SSS_DEDUCTION = 1125;
        static final double PHILHEALTH_DEDUCTION = 375;
        static final double PAG_IBIG_DEDUCTION = 100;
        static final double TAX_EXEMPTION = 20833; // Taxable income limit

        // Constructor
        public Employee(String employeeNumber, String name, String birthday, String position, int hoursWorked, double hourlyRate) {
            this.employeeNumber = employeeNumber;
            this.name = name;
            this.birthday = birthday;
            this.position = position;
            this.hoursWorked = hoursWorked;
            this.hourlyRate = hourlyRate;
        }

        // Calculate Gross Salary
        public double calculateGrossSalary() {
            return this.hoursWorked * this.hourlyRate;
        }

        // Total Deductions
        public double calculateTotalDeductions() {
            return SSS_DEDUCTION + PHILHEALTH_DEDUCTION + PAG_IBIG_DEDUCTION;
        }

        // Taxable Income
        public double calculateTaxableIncome(double grossSalary) {
            return grossSalary - calculateTotalDeductions();
        }

        // Withholding Tax (20% in excess of ₱20,833)
        public double calculateWithholdingTax(double taxableIncome) {
            if (taxableIncome > TAX_EXEMPTION) {
                return (taxableIncome - TAX_EXEMPTION) * 0.20;
            } else {
                return 0;
            }
        }

        // Calculate Net Salary
        public double calculateNetSalary(double grossSalary, double totalDeductions, double withholdingTax) {
            return grossSalary - totalDeductions - withholdingTax;
        }

        // Display Employee Details
        public void displayEmployeeDetails() {
            double grossSalary = calculateGrossSalary();
            double totalDeductions = calculateTotalDeductions();
            double taxableIncome = calculateTaxableIncome(grossSalary);
            double withholdingTax = calculateWithholdingTax(taxableIncome);
            double netSalary = calculateNetSalary(grossSalary, totalDeductions, withholdingTax);

            System.out.println("\n==================== EMPLOYEE PAYROLL SUMMARY ====================");
            System.out.println("Employee Number: " + this.employeeNumber);
            System.out.println("Employee Name  : " + this.name);
            System.out.println("Position       : " + this.position);
            System.out.println("Birthday       : " + this.birthday);
            System.out.println("Hours Worked   : " + this.hoursWorked);
            System.out.println("Hourly Rate    : ₱ " + String.format("%.2f", this.hourlyRate));
            System.out.println("----------------------------------------------------------------");
            System.out.println("Gross Salary   : ₱ " + String.format("%.2f", grossSalary));
            System.out.println("----------------------------------------------------------------");
            System.out.println("Deductions:");
            System.out.println("SSS Deduction      : ₱ " + String.format("%.2f", SSS_DEDUCTION));
            System.out.println("PhilHealth Deduction: ₱ " + String.format("%.2f", PHILHEALTH_DEDUCTION));
            System.out.println("Pag-IBIG Deduction  : ₱ " + String.format("%.2f", PAG_IBIG_DEDUCTION));
            System.out.println("Total Deductions    : ₱ " + String.format("%.2f", totalDeductions));
            System.out.println("----------------------------------------------------------------");
            System.out.println("Taxable Income      : ₱ " + String.format("%.2f", taxableIncome));
            System.out.println("Withholding Tax (20% in excess of ₱20,833): ₱ " + String.format("%.2f", withholdingTax));
            System.out.println("----------------------------------------------------------------");
            System.out.println("Net Salary         : ₱ " + String.format("%.2f", netSalary));
            System.out.println("================================================================");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Getting employee details from the user
        System.out.println("Enter Employee Number: ");
        String employeeNumber = scanner.nextLine();

        System.out.println("Enter Employee Name: ");
        String name = scanner.nextLine();

        System.out.println("Enter Position: ");
        String position = scanner.nextLine();

        System.out.println("Enter Employee Birthday (MM/DD/YYYY): ");
        String birthday = scanner.nextLine();

        System.out.println("Enter Hours Worked in a Week: ");
        int hoursWorked = scanner.nextInt();

        System.out.println("Enter Hourly Rate (₱): ");
        double hourlyRate = scanner.nextDouble();

        // Create an Employee object
        Employee employee = new Employee(employeeNumber, name, birthday, position, hoursWorked, hourlyRate);

        // Display employee details and calculate salary
        employee.displayEmployeeDetails();

        scanner.close();
    }
}
