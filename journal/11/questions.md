# A bit more CSharp and SQL
1. What does ***inheritance*** accomplish for us in C#?

  > | Inheritance allows us to pass down information from existing classes into new ones. This can preserve the data from the parent class when child classes extend their uses or have other elements that may change, but should not affect the higher level class. |

2. How does ***member inheritance*** work in C#? Does a `Class` inherit all members of the base `Class`?

  > | Select information can be filtered down through member inheritance. However, the way to manage this is to overwrite the data you do not want from the higher order class. |

3. How does ***accessibility*** affect inheritance?

  > | Accessibility determines what values of a class are passed down. If a certain method is labelled private, it cannot be manipulated through lower level classes. |

4. What is the difference between a `PRIMARY KEY` and a `FOREIGN KEY`

  > | Primary keys are related to the table at hand, while foreign keys access data from a different table. Account information is often a foreign key on other tables for this reason. |

5. What is an ***alias***?

  > | Sydney Bristow. Aliases allow data titles to be abbreviated. Another use is to generate alignment or differentiation in naming to better organize code. |

6. Demonstrate how you would query a join statement that would get all of a doctors patients from the following collections:

  ```SQL
  CREATE TABLE doctors (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patients (
    id INT NOT NULL AUTO_INCREMENT,
    -- CODE OMITTED
    PRIMARY KEY (id)
  )

  CREATE TABLE patient_doctors (
    id INT NOT NULL AUTO_INCREMENT,
    doctorId INT NOT NULL,
    patientId INT NOT NULL,

    FOREIGN KEY (doctorId)
      REFERENCES doctors(id),
    FOREIGN KEY (patientId)
      REFERENCES patients(id),
  )

  ```

  > | 
  List<Patient> patients = _db.Query<Patient_Doctors, Patient, Patient>(sql, (patient_doctor, patient)=>
  {
    patient.Patient_DoctorId = patient_doctor.id;
    patient.DoctorId = patient_doctor.DoctorId;
    return patient_doctor;
  }, new {DoctorId}).ToList;
  return patients;
   |
