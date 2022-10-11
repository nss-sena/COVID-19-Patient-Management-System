#### COVID-19-Patient-Management-System
/*
Mini project
*/

#include <stdio.h>
#include <time.h>

//Structure to store a patient record
typedef struct {
    int NIC;
    char firstName[20];
    char lastName[20];
    int age;
    char gender [10];
    char admissionDate [20];
} patient_t;

//Seperate functions for each operation
patient_t addPatient(); //to insert patients
int* readNICnum();
void printPatient(patient_t patient);
int deletePatient(int patientListIndex, patient_t patientList[]);

//function to display dashes
void printDash(){
	printf("------------------\n");
}


int main(){
    //Initial Main UI
    printf("--------------------------------------------------------------------\n");
    printf("              COVID-19 PATIENT MANAGEMENT SYSTEM\n");
    printf("--------------------------------------------------------------------\n");
    printf("0. Quit\n1. Add a Patient Record\n2. Print a Patient Records\n3. Print all Patient Records\n4. Delete a Patient Record\n.");

    printf("\nTIP - \n        *If you are using an old NIC,DO not include v*\n        Ex :- NIC No - 99568421v\n        Please input - 99568421 only\n");




    //Array to store student information
    patient_t patientList[1000];
    int patientListIndex = 0;

    while(1){       //to run the loop infinitely

        printDash();
        printf("Enter Option [0-4]\n");
        printDash();

        int option;
        printf("Enter option - ");
        scanf("%d",&option);            // get the option to continue

        if(option == 0){

            printf("\n");
            printf("------------------------------------------------------\n");
            printf("\nThank you for using COVID-19 Patient Management System\n................Have a nice day................\n\n");
            printf("------------------------------------------------------\n");
            sleep (5); //Sleep program for 5 seconds to display thank you message
            return 0;   //Quit the programme
        }

        else if(option ==1){

            printf("\n");
            printf("-------------\n");
            printf("Add a patient\n");
            printf("-------------\n");
            printf("\n");

            patient_t patient = addPatient();       //Add a patient data to the array
            patientList[patientListIndex++] = patient;
            printf("\n");
        }

        else if(option==2){

            printf("\n");
            printf("--------------------\n");
            printf("Details of a patient\n");
            printf("--------------------\n");
            printf("\n");

            int*    NICNumArr = readNICnum();   //To get the NIC number

            //find the patient
            _Bool patientFound = 0;
            for (int i=0; i< patientListIndex; i++){
                if(patientList[i].NIC == NICNumArr[0]){
                    //To print the information
                    printPatient(patientList[i]);
                    patientFound= 1;
                }
            }

            //if there is no such patient
            if(patientFound==0){
                printf("No such patient with the NIC number entered.\nPlease check the Admission number!\n");

            }
        }

        else if(option==3){

            printf("\n");
            printf("----------------\n");
            printf("All patient Data\n");
            printf("----------------\n");
            printf("\n");

            //Print all the patients records
            for(int j=0;j<patientListIndex;j++){
                printPatient(patientList[j]);
            }
            printf("\n");
        }

        else if(option==4){

            printf("\n");
            printf("----------------\n");
            printf("Delete a patient\n");
            printf("----------------\n");
            printf("\n");

            //Delete a patient record
            //If the delete is success, print "Delete successfull!"

            int*    NICNumArr = readNICnum();   //To get the NIC number

            //find the patient
            _Bool patientFound = 0;
            for (int i=0; i< patientListIndex; i++){
                if(patientList[i].NIC == NICNumArr[0]){
                    //To print the information
                    printPatient(patientList[i]);
                    patientFound= 1;
                }
            }

            //if there is no such patient
            if(patientFound==0){
                printf("No such patient with the NIC number entered.\nPlease check the Admission number!\n");
                printf("\n");
                continue;

            }

            //Confirmation of deletion
            int confirm;
            printf("Do you want to delete this patient's details! [ 1(YES)/ 0(NO) ]? - ");
            scanf("%d",&confirm);
            printf("\n");


            if(confirm ==1){

                printf("Please Re-enter the NIC to confirm the deletion\n");
                if(deletePatient(patientListIndex,patientList)==1){
                    --patientListIndex;
                    printf("Delete Successful!");
                    printf("\n");
                }


            }else{

                printf("Deletion Terminated!\n\n");
                continue;
            }


        }

        else{

            printf("Invalid input!\nPlease enter a correct input.\n");
            printf("\n");
            continue;
        }
    }

    return 0;

}

//function to get patient data from the user

patient_t addPatient(){
    patient_t patnt;

    printf("Enter the first name of the patient:");
    scanf("%s",&patnt.firstName);

    printf("Enter the  last name of the patient:");
    scanf("%s",&patnt.lastName);

    printf("Enter the NIC number               :");
    scanf("%d",&patnt.NIC);

    printf("Enter the age                      :");
    scanf("%d",&patnt.age);

    printf("Enter patient's gender             :");
    scanf("%s",&patnt.gender);

    printf("Enter the admission date(DD/MM/YY) :");
    scanf("%s",&patnt.admissionDate);
    printf("\n");


    return patnt;
}

//Function to print patient record

void printPatient(patient_t patnt){
    printf("Patient Name        : %s %s \nAge                 : %d\nNIC number          : %d\nGender              : %s\nAdmission Date      : %s \n\n",patnt.firstName,patnt.lastName, patnt.age,patnt.NIC,patnt.gender,patnt.admissionDate);

}

//Function to delete patient records

int deletePatient(int patientListIndex, patient_t patientList[]){
    int*  NICNumArr = readNICnum();

    _Bool patientFound = 0;
    int index;

    for(int k=0; k<patientListIndex; k++){
        if(patientList[k].NIC == NICNumArr[0]){
            index =k;
            patientFound=1;
        }
    }

    if(patientFound ==1){
        for(int d = index; d< patientListIndex-1;d++){
            patientList[d] = patientList[d+1];
        }
        return 1;
    }else{
        printf("No such patient with the NIC number entered.\nPlease check the NIC number!\n");
        return 0;
    }
}

//Function to get NIC number from the user

int* readNICnum(){

    static int NICNumArr[1];
    printf("Enter the NIC number: ");
    scanf("%d", &NICNumArr);
    printf("\n");
    return NICNumArr;
}





