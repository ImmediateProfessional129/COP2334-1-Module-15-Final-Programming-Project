# COP2334-1-Module-15-Final-Programming-Project
This is a repository for the Module 15 Final Group Programming Project

// This program is designed to determine the price range of a medical bill from Cedars-Sinai Medical Center based on the number of days spent in the hospital, the daily rate, and the type of surgery and medication that will establish the total cost of the bill.

#include <iostream> // This is a preprocessor directive that allows input and output to be used in the program.
#include <string> // This is a preprocessor directive that allows the use of string variables in the program.
#include <vector> // This is a preprocessor directive that allows the use of vector variables in the program.
using namespace std; // This is a preprocessor directive that allows the use of standard namespace in the program.

class PatientAccount { // This is a class called PatientAccount that is used to store the patient's information.
private: // This is a private access specifier that is used to declare the variables that are used in the class.
    double totalCharges; // This is a private member variable that stores the total charges for the patient.
    int daysInHospital; // This is a private member variable that stores the number of days the patient was in the hospital.
public: // This is a public access specifier that is used to declare the functions that are used in the class.
    PatientAccount(int days, double rate) : totalCharges(0), daysInHospital(days) { // This is a constructor that is used to initialize the variables in the class.
        totalCharges += daysInHospital * rate; // This is an assignment statement that calculates the total charges for the patient based on the number of days in the hospital and the daily rate.
    }
    void addCharges(double charge) { // This is a member function that is used to add a charge to the total charges for the patient.
        totalCharges += charge; // This is an assignment statement that adds the charge to the total charges for the patient.
    }
    double calculateTotal() { // This is a member function that is used to calculate the total charges for the patient.
        return totalCharges; // This is a return statement that returns the total charges for the patient.
    }
};

class Surgery { // This is a class called Surgery that is used to store the surgery information.
private: // This is a private access specifier that is used to declare the variables that are used in the class.
    double charges[5] = {36000, 23000, 200000, 33000, 23000}; // This is a private member variable that stores the surgery charges for each type of surgery.
public: // This is a public access specifier that is used to declare the functions that are used in the class.
    void performSurgery(int surgeryType, PatientAccount &account) { // This is a member function that is used to perform a surgery and add the surgery charge to the patient's account.
        if (surgeryType >= 1 && surgeryType <= 5) { // This is an if statement that checks if the surgery type is valid.
            account.addCharges(charges[surgeryType - 1]); // This is an assignment statement that adds the surgery charge to the patient's account.
        } else {
            cout << "Invalid surgery type." << endl; // This is an output statement that displays an error message if the surgery type is invalid.
        } // This is an end of if statement.
    }
};

class Pharmacy { // This is a class called Pharmacy that is used to store the medication information.
private: // This is a private access specifier that is used to declare the variables that are used in the class.
    double charges[5] = {20.0, 5.88, 10.40, 22.82, 18.17}; // This is a private member variable that stores the medication charges for each type of medication.
public: // This is a public access specifier that is used to declare the functions that are used in the class.
    void prescribeMedication(int medicationType, PatientAccount &account) { // This is a member function that is used to prescribe medication and add the medication charge to the patient's account.
        if (medicationType >= 1 && medicationType <= 5) { // This is an if statement that checks if the medication type is valid.
            account.addCharges(charges[medicationType - 1]); // This is an assignment statement that adds the medication charge to the patient's account.
        } else {
            cout << "Invalid medication type." << endl; // This is an output statement that displays an error message if the medication type is invalid.
        } // This is an end of if statement.
    }
};

class Doctor { // This is a class called Doctor that is used to store the doctor information.
private: // This is a private access specifier that is used to declare the variables that are used in the class.
    vector<string> doctorNames = {"Dr. Sean S. Ameli", "Dr. Sadeea Abbasi", "Dr. Achilles Aiken", "Dr. Alisa Alayan", "Dr. Alexander Allins"}; // This is a private member variable that stores the names of the doctors.
    vector<string> availabilityTime = {"9:00 - 10:00 AM", "10:00 - 11:00 AM", "11:00 AM - 12:00 PM", "12:00 - 1:00 PM", "1:00 - 2:00 PM"}; // This is a private member variable that stores the available time for each doctor.
    string selectedDoctor; // This is a private member variable that stores the selected doctor.
    string selectedTimeSlot; // This is a private member variable that stores the selected time slot.
public: // This is a public access specifier that is used to declare the functions that are used in the class.
    void displayDoctorNames() { // This is a member function that is used to display the names of the doctors.
        cout << "Available Doctors:" << endl; // This is an output statement that displays a message that indicates that the available doctors are being displayed.
        for (int i = 0; i < doctorNames.size(); i++) { // This is a for loop that iterates through the doctor names.
            cout << i + 1 << ". " << doctorNames[i] << endl; // This is an output statement that displays the doctor name and its corresponding number.
        }
    }
    void displayAvailabilityTime() { // This is a member function that is used to display the available time slots for the doctors.
        cout << "Available Time Slots:" << endl; // This is an output statement that displays a message that indicates that the available time slots are being displayed.
        for (int i = 0; i < availabilityTime.size(); i++) { // This is a for loop that iterates through the availability time slots.
            cout << i + 1 << ". " << availabilityTime[i] << endl; // This is an output statement that displays the time slot and its corresponding number.
        }
    }
    void bookAppointment() { // This is a member function that is used to book an appointment with a doctor.
        int doctorChoice, timeSlot; // This is a variable declaration that declares two integer variables.
        displayDoctorNames(); // This is a function call that calls the displayDoctorNames function.
        cout << "Enter the number for your choice of doctor: ";
        cin >> doctorChoice; // This is an input statement that reads in the doctor choice from the user.
        displayAvailabilityTime(); // This is a function call that calls the displayAvailabilityTime function.
        cout << "Enter the number for your available time slot: ";
        cin >> timeSlot; // This is an input statement that reads in the time slot choice from the user.

        if (doctorChoice >= 1 && doctorChoice <= doctorNames.size() &&
            timeSlot >= 1 && timeSlot <= availabilityTime.size()) { // This is an if statement that checks if the doctor choice and time slot choices are valid.
            selectedDoctor = doctorNames[doctorChoice - 1]; // This is an assignment statement that assigns the selected doctor to the doctor name.
            selectedTimeSlot = availabilityTime[timeSlot - 1]; // This is an assignment statement that assigns the selected time slot to the time slot.
            cout << "Appointment booked with " << selectedDoctor
                 << " at " << selectedTimeSlot << endl << endl; // This is an output statement that displays a message that indicates that the appointment has been booked.
        } else {
            cout << "Invalid selection. Please try again." << endl; // This is an output statement that displays an error message if the doctor choice or time slot choices are invalid.
        }
    }
    string getSelectedDoctor() { // This is a member function that is used to get the selected doctor.
        return selectedDoctor.empty() ? "No doctor selected" : selectedDoctor; // This is a return statement that returns the selected doctor or "No doctor selected" if no doctor has been selected.
    }
    string getSelectedTimeSlot() { // This is a member function that is used to get the selected time slot.
        return selectedTimeSlot.empty() ? "No time slot selected" : selectedTimeSlot; // This is a return statement that returns the selected time slot or "No time slot selected" if no time slot has been selected.
    }
};

int main() { // This is the main function that is used to run the program.
    PatientAccount patient(1, 845.00); // This is an object declaration that creates a PatientAccount object with a patient with 1 day in the hospital and a daily rate of $845.00.
    Surgery surgery; // This is an object declaration that creates a Surgery object.
    Pharmacy pharmacy; // This is an object declaration that creates a Pharmacy object.
    Doctor doctor; // This is an object declaration that creates a Doctor object.

    cout << "Welcome to the Cedars-Sinai Medical Center Check-Out System." << endl << endl; // This is an output statement that displays a welcome message.
    cout << "Here, you will enter the number of days you've been staying at this hospital, "
         << "what the daily rate in California is, what type of surgery you acquired, "
         << "and what medication you need for your recovery." << endl << endl; // This is an output statement that displays instructions for the user.
    cout << "Once that's done, the system will calculate your total cost in your medical bill." << endl << endl;

    cout << "Enter the number of days in the hospital: ";
    int daysInHospital; // This is a variable declaration that declares an integer variable.
    cin >> daysInHospital; // This is an input statement that reads in the number of days in the hospital from the user.

    cout << "Enter the daily rate: $";
    double dailyRate; // This is a variable declaration that declares a double variable.
    cin >> dailyRate; // This is an input statement that reads in the daily rate from the user.

    patient = PatientAccount(daysInHospital, dailyRate); // This is an assignment statement that assigns the patient account with the number of days in the hospital and the daily rate.

    cout << "\nDoctor's Appointment Booking\n";
    doctor.bookAppointment(); // This is a function call that calls the bookAppointment function of the Doctor object.

    cout << "\nEnter surgery type (1-5):\n"
         << "1. Aortic Disease Surgery\n"
         << "2. Bariatric Surgery\n"
         << "3. Cardiac Surgery\n"
         << "4. Discectomy\n"
         << "5. Extremity Reconstruction and Limb Salvage Surgery\n"
         << "Surgery: "; // This is an output statement that displays a message that asks the user to enter the surgery type from five different choices.
    int surgeryType; // This is a variable declaration that declares an integer variable.
    cin >> surgeryType; // This is an input statement that reads in the surgery type from the user.
    surgery.performSurgery(surgeryType, patient); // This is a function call that calls the performSurgery function of the Surgery object with the surgery type and patient account as arguments.

    cout << "\nEnter medication type (1-5):\n"
         << "1. Propranolol\n"
         << "2. Omeprazole\n"
         << "3. Midazolam\n"
         << "4. Percocet\n"
         << "5. Cefazolin\n"
         << "Medication: "; // This is an output statement that displays a message that asks the user to enter the medication type from five different options.
    int medicationType; // This is a variable declaration that declares an integer variable.
    cin >> medicationType; // This is an input statement that reads in the medication type from the user.
    pharmacy.prescribeMedication(medicationType, patient); // This is a function call that calls the prescribeMedication function of the Pharmacy object with the medication type and patient account as arguments.

    double totalCharges = patient.calculateTotal(); // This is a variable declaration that declares a double variable and assigns it the value of the patient account's calculateTotal function call.

    cout << "\nSummary of your visit:\n"; 
    cout << "You have booked " << doctor.getSelectedDoctor() 
         << " for the " << doctor.getSelectedTimeSlot() << " time slot." << endl; // This is an output statement that displays a message that indicates the doctor's name and time slot selected.
    cout << "Total charges: $" << totalCharges << endl;
    cout << "Thank you for using the Cedars-Sinai Medical Center Check-Out System.\n";
    return 0; // This is a return statement that returns 0 to indicate successful program execution.
}
