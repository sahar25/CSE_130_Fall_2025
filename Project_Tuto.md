# Symptoms Checker Program (C++)

### Objective
Develop a <u>C++ program</u> that:
- Uses <u>OOP principles</u> (namespaces, classes, inheritance, etc.).
- Generates <u> random patient data with seven symptoms (true/false)</u>.
- Diagnoses each patient based on symptoms into categories: COVID-19, Cold, Flu, or Other.
- Outputs a summary report with patient <u>counts</u> and  <u>percentages</u> per category.

### Functionality
- **Table of Symptoms**: Display symptom occurrence for COVID-19, Cold, and Flu.

Welcome to Symptoms Checker
Guide: * Common    + Sometimes/Rarely    - NO

| Symptoms             | COVID-19 | Cold | Flu |
|----------------------|----------|------|-----|
| Fever                | *        | +    | *   |
| Cough                | *        | +    | *   |
| Shortness of Breath  | *        | -    | -   |
| Runny Nose           | +        | *    | +   |
| Headaches            | +        | +    | *   |
| Sneezing             | -        | *    | -   |
| Fatigue              | +        | +    | *   |


- **Program Input**: Number of patients.
- **Random Symptom Generation**: Randomly assign present/absent: true/false for all seven symptoms per  patient.
- **Diagnosis**: Classify each patient as COVID-19, Cold, Flu, or Other.
- **Report Generation**: Display <u>counts </u> and <u> percentages</u> for each illness category.

**Sample Report Format**
Enter the number of patients? ---
Thank you...

========================================

**Symptoms Checker....**

- -- patients have symptoms of COVID-19
- -- patients have symptoms of Cold
- -- patients have symptoms of Flu
- -- patients may have some other illness

========================================

**Percentage of each illness:**

- COVID-19: [--%]++
- Cold: [--%]++++++++
- Flu: [--%]++++++++
- Other illness: [--%]+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  +++++++++++++++++++


### Proposed C++ Solution

#### 1. **Namespace**:
   ```cpp
   namespace SymptomsChecker {
       // ...
   }
```
#### 2. **Inheritance**:
<u>Base Class</u>:

```cpp
class Patient {
public:
    Patient() {
        // Randomly initialize symptoms (present/absent: true/false)
    }
    
	virtual bool isSick() {};
    
protected:
    bool symptoms[7]; // Fever, Cough, Shortness of Breath, Runny Nose, Headache, Sneezing, Fatigue
};
```
<u>Derived Classes (for each illness type)</u>:
```cpp
class Covid19Patient : public Patient {
public:
    bool isSick() override {
        // Check symptoms specific to COVID-19
    }
};
```
#### 3. **PatientList Class**

```cpp
class PatientList {
public:
    void addPatient(std::unique_ptr<Patient> patient) {
        patients.push_back(std::move(patient));
    }

    void diagnosePatients() {
        // Diagnosis logic
    }

    void printReport() {
        // Report generation logic
    }

private:
    std::vector<std::unique_ptr<Patient>> patients;
    int covidCount = 0, coldCount = 0, fluCount = 0, otherCount = 0;
};
```

