# COP2334-1-Module-15-Final-Programming-Project
This is a repository for the Module 15 Final Group Programming Project

#include <iostream> // This is a header file that allows the program to display output on the screen and to get input from the user.
#include <string> // This is a header file that allows the program to use string variables.
#include <vector> // This is a header file that allows the program to use vectors.
using namespace std; // This is a namespace that allows the program to use names for objects and variables from the standard library.

class PatientAccount { // This is a class that represents a patient account.
private: // This is a private access specifier.
    double totalCharges; // This is a private member variable that represents the total charges for the patient account.
    int daysInHospital; // This is a private member variable that represents the number of days spent in the hospital.

public: // This is a public access specifier.
    PatientAccount(int days = 0, double rate = 0.0) : totalCharges(0), daysInHospital(days) { // This is a constructor that initializes the totalCharges and daysInHospital member variables with default values.
        totalCharges += daysInHospital * rate; // This is an assignment statement that calculates the total charges for the patient account.
    }

    void addCharges(double charge) { // This is a member function that adds a charge to the total charges for the patient account.
        totalCharges += charge; // This is an assignment statement that adds the charge to the total charges for the patient account.
    }

    double calculateTotal() const { // This is a member function that calculates and returns the total charges for the patient account.
        return totalCharges; // This is a return statement that returns the total charges for the patient account.
    }
};

class Surgery { // This is a class that represents a surgery.
private: // This is a private access specifier.
    double charges[5] = {36000, 23000, 200000, 33000, 23000}; // This is a private member variable that represents the charges for each surgery.

public: // This is a public access specifier.
    void performSurgery(PatientAccount &account) { // This is a member function that performs a surgery on a patient account.
        int surgeryType; // This is a private member variable that represents the type of surgery.
        while (true) { // This is a loop that continues until a valid surgery type is entered.
            cout << "\nEnter surgery type (1-5):\n"
                 << "1. Aortic Disease Surgery\n"
                 << "2. Bariatric Surgery\n"
                 << "3. Cardiac Surgery\n"
                 << "4. Discectomy\n"
                 << "5. Extremity Reconstruction and Limb Salvage Surgery\n"
                 << "Surgery: "; // This is an output statement that prompts the user to enter the type of surgery.
            cin >> surgeryType; // This is an input statement that reads in the type of surgery from the user.

            if (surgeryType >= 1 && surgeryType <= 5) { // This is an if statement that checks if the surgery type is valid.
                account.addCharges(charges[surgeryType - 1]); // This is an assignment statement that adds the charge for the surgery to the total charges for the patient account.
                break; // This is a break statement that breaks out of the loop.
            } else {
                cout << "Invalid surgery type. Please try again.\n";
            }
        }
    }
};

class Pharmacy { // This is a class that represents a pharmacy.
private: // This is a private access specifier.
    double charges[5] = {20.0, 5.88, 10.40, 22.82, 18.17}; // This is a private member variable that represents the charges for each medication.

public: // This is a public access specifier.
    void prescribeMedication(PatientAccount &account) { // This is a member function that prescribes medication on a patient account.
        while (true) { // This is a loop that continues until a valid medication type is entered.
            int medicationType; // This is a private member variable that represents the type of medication.
            cout << "\nEnter medication type (1-5):\n"
                 << "1. Propranolol\n"
                 << "2. Omeprazole\n"
                 << "3. Midazolam\n"
                 << "4. Percocet\n"
                 << "5. Cefazolin\n"
                 << "Medication: ";
            cin >> medicationType; // This is an input statement that reads in the type of medication from the user.

            if (medicationType >= 1 && medicationType <= 5) { // This is an if statement that checks if the medication type is valid.
                account.addCharges(charges[medicationType - 1]); // This is an assignment statement that adds the charge for the medication to the total charges for the patient account.
            } else { 
                cout << "Invalid medication type. Please try again.\n";
                continue; // This is a continue statement that continues to the next iteration of the loop.
            }

            char choice; // This is a private member variable that represents the user's choice to continue prescribing medication.
            cout << "Do you want to add more medication? (y/n): "; // This is an output statement that prompts the user to continue prescribing medication.
            cin >> choice; // This is an input statement that reads in the user's choice to continue prescribing medication from the user.
            if (tolower(choice) == 'n') break; // This is an if statement that checks if the user's choice to continue prescribing medication is no.
        }
    }
};

class Doctor { // This is a class that represents a doctor.
private: // This is a private access specifier.
    vector<string> doctorNames = {"Dr. Sean S. Ameli", "Dr. Sadeea Abbasi", "Dr. Achilles Aiken", "Dr. Alisa Alayan", "Dr. Alexander Allins"}; // This is a private member variable that represents the names of the doctors.
    vector<string> availabilityTime = {"9:00 - 10:00 AM", "10:00 - 11:00 AM", "11:00 AM - 12:00 PM", "12:00 - 1:00 PM", "1:00 - 2:00 PM"}; // This is a private member variable that represents the availability time of the doctors.
    string selectedDoctor; // This is a private member variable that represents the selected doctor.
    string selectedTimeSlot; // This is a private member variable that represents the selected time slot.

public: // This is a public access specifier.
    void bookAppointment() { // This is a member function that books an appointment with a doctor.
        int doctorChoice, timeSlot; // This is a private member variable that represents the user's choice of doctor and time slot.

        while (true) { // This is a loop that continues until a valid doctor choice is entered.
            cout << "Available Doctors:\n";
            for (int i = 0; i < doctorNames.size(); i++) { // This is a loop that iterates through the doctor names vector.
                cout << i + 1 << ". " << doctorNames[i] << endl;
            }
            cout << "Enter the number for your choice of doctor: ";
            cin >> doctorChoice; // This is an input statement that reads in the user's choice of doctor from the user.

            if (doctorChoice < 1 || doctorChoice > doctorNames.size()) { // This is an if statement that checks if the doctor choice is valid.
                cout << "Invalid doctor selection. Please try again.\n";
                continue; // This is a continue statement that continues to the next iteration of the loop.
            }

            while (true) { // This is a loop that continues until a valid time slot is entered.
                cout << "Available Time Slots:\n";
                for (int i = 0; i < availabilityTime.size(); i++) { // This is a loop that iterates through the availability time vector.
                    cout << i + 1 << ". " << availabilityTime[i] << endl;
                }
                cout << "Enter the number for your available time slot: ";
                cin >> timeSlot; // This is an input statement that reads in the user's available time slot from the user.

                if (timeSlot >= 1 && timeSlot <= availabilityTime.size()) { // This is an if statement that checks if the time slot is valid.
                    selectedDoctor = doctorNames[doctorChoice - 1]; // This is an assignment statement that sets the selected doctor to the doctor name.
                    selectedTimeSlot = availabilityTime[timeSlot - 1]; // This is an assignment statement that sets the selected time slot to the time slot.
                    cout << "Appointment booked with " << selectedDoctor
                         << " at " << selectedTimeSlot << endl << endl; // This is an output statement that displays the booked appointment details.
                    return; // This is a return statement that returns from the function.
                } else {
                    cout << "Invalid time slot. Please try again.\n";
                }
            }
        }
    }

    string getSelectedDoctor() const { // This is a member function that returns the selected doctor.
        return selectedDoctor.empty() ? "No doctor selected" : selectedDoctor; // This is a ternary operator that returns the selected doctor or "No doctor selected" if no doctor is selected.
    }

    string getSelectedTimeSlot() const { // This is a member function that returns the selected time slot.
        return selectedTimeSlot.empty() ? "No time slot selected" : selectedTimeSlot; // This is a ternary operator that returns the selected time slot or "No time slot selected" if no time slot is selected.
    }
};

int main() { // This is the main function of the program.
    PatientAccount patient; // This is an instance of the PatientAccount class that represents the patient account.
    Surgery surgery; // This is an instance of the Surgery class that represents the surgery.
    Pharmacy pharmacy; // This is an instance of the Pharmacy class that represents the pharmacy.
    Doctor doctor; // This is an instance of the Doctor class that represents the doctor.

    cout << "Welcome to the Cedars-Sinai Medical Center Check-Out System." << endl << endl; // This is an output statement that displays a welcome message.
    cout << "Here, you will enter the number of days you've been staying at this hospital, "
         << "what the daily rate in California is, what type of surgery you acquired, "
         << "and what medication you need for your recovery." << endl << endl; // This is an output statement that displays instructions for the user.
    cout << "Once that's done, the system will calculate your total cost in your medical bill." << endl << endl;

    cout << "Enter the number of days in the hospital: "; // This is an output statement that prompts the user to enter the number of days in the hospital.
    int daysInHospital; // This is a private member variable that represents the number of days in the hospital.
    cin >> daysInHospital; // This is an input statement that reads in the number of days in the hospital from the user.

    cout << "Enter the daily rate: $";
    double dailyRate; // This is a private member variable that represents the daily rate in California.
    cin >> dailyRate; // This is an input statement that reads in the daily rate from the user.

    patient = PatientAccount(daysInHospital, dailyRate); // This is an assignment statement that sets the patient account to the number of days in the hospital and the daily rate.

    cout << "\nDoctor's Appointment Booking\n";
    doctor.bookAppointment(); // This is a function call that books an appointment with a doctor.

    surgery.performSurgery(patient); // This is a function call that performs a surgery on the patient account.
    pharmacy.prescribeMedication(patient); // This is a function call that prescribes medication on the patient account.

    double totalCharges = patient.calculateTotal(); // This is a function call that calculates and returns the total charges for the patient account.

    cout << "\nSummary of your visit:\n";
    cout << "You have booked " << doctor.getSelectedDoctor()
         << " for the " << doctor.getSelectedTimeSlot() << " time slot.\n"; // This is an output statement that displays the selected doctor and time slot.
    cout << "Total charges: $" << totalCharges << endl;
    cout << "Thank you for using the Cedars-Sinai Medical Center Check-Out System.\n";

    return 0; // This is a return statement that returns 0 to indicate successful program execution.
} // This is the end of the main function.
