<?php

abstract class Employee {
    protected $name;
    protected $id;
    protected $department;

    public function __construct($name, $id, $department) {
        $this->name = $name;
        $this->id = $id;
        $this->department = $department;
    }

    
    public function getName() {
        return $this->name;
    }

    public function getId() {
        return $this->id;
    }

    public function getDepartment() {
        return $this->department;
    }

    abstract public function calculateSalary();
}


interface Benefits {
    public function getHealthInsurance();
    public function getLeaveCredits();
}


class FullTimeEmployee extends Employee implements Benefits {
    private $monthlySalary;

    public function __construct($name, $id, $department, $monthlySalary) {
        parent::__construct($name, $id, $department);
        $this->monthlySalary = $monthlySalary;
    }

    public function calculateSalary() {
        return $this->monthlySalary;
    }

    public function getHealthInsurance() {
        return "Full coverage health insurance.";
    }

    public function getLeaveCredits() {
        return "10 paid leave credits per year.";
    }
}


class PartTimeEmployee extends Employee implements Benefits {
    private $hourlyRate;
    private $hoursWorked;

    public function __construct($name, $id, $department, $hourlyRate, $hoursWorked) {
        parent::__construct($name, $id, $department);
        $this->hourlyRate = $hourlyRate;
        $this->hoursWorked = $hoursWorked;
    }

    public function calculateSalary() {
        return $this->hourlyRate * $this->hoursWorked;
    }

    public function getHealthInsurance() {
        return "No health insurance benefits.";
    }

    public function getLeaveCredits() {
        return "5 unpaid leave credits per year.";
    }
}


$employees = [
    new FullTimeEmployee("Jaymark Antonio", 65643, "Project Planner", 800000),
];


foreach ($employees as $employee) {
    
    echo "<br> \n";
    echo "Employee Details:<br> \n <br>\n";  
    echo "\tName: " . $employee->getName() . "<br>\n";
    echo "\tID: " . $employee->getId() . "<br>\n";
    echo "\tPosition: " . $employee->getDepartment() . "<br>\n";
    echo "\tSalary: PHP " . $employee->calculateSalary() . "<br>\n";

    
    if ($employee instanceof Benefits) {
        echo "\tHealth Insurance: " . $employee->getHealthInsurance() . "<br> \n";
        echo "\tLeave Credits: " . $employee->getLeaveCredits() . "<br>\n";
    }

    echo "\n";  
}
?>
