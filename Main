#include <iostream>
#include <fstream>
#include "queueADT.h"
#include "string"

using namespace std;

struct empData
{
  string lastName;
  string firstName;
  int empID;
};


//function prototypes
template <class elemType>
void insertionSort(elemType list[], int length); //insertion sort prototype
int binarySearch(const empData list[], int listLength, int searchItem); //binary search prototye
void menu(); //menu prototype

//main
int main() 
{
  linkedQueueType<string> appt;
  int qID;
  string numstr;
  string fn, ln;
  //opens file
  ifstream inFile;
  inFile.open("employees.txt"); 

  //checks if program can open file
  if(!inFile) 
    cout << "ERROR: File cannot be accessed." << endl;
  int i = 0;
  int size = 100;
  empData employees[size];
  int counter = 0;

  //reads ids from employees.txt into array 
  while(!inFile.eof())
  {
    inFile >> employees[i].lastName;
    inFile >> employees[i].firstName;
    inFile >> employees[i].empID;
    i++;
  }
  inFile.close();//closes file

  insertionSort(employees, size); //sorts array for binary search

  //checks if selection is in bounds
  int choice;
  while (choice != 7)
  {
    menu();
    cout << "Select an option 1-7: ";
    cin >> choice;
    cout << endl;
    if (choice < 1 || choice > 7)
      cout << "ERROR: Selection not within bounds." << endl << endl;

//switch function to activate each menu option
    switch (choice)
    {
//Option 1: Searches for the employee's ID using binary search
//returns the index of the employee's ID
      case 1:
        int key;
        cout << "Enter ID to be found: ";
        cin >> key;
        cout << endl;

        if (binarySearch(employees, size, key) == -1)
        {
          while (binarySearch(employees, size, key) == -1)
          {
            cout << "ERROR: ID not found. Try again." << endl;
            cout << "Enter ID to be found: ";
            cin >> key;
            cout << endl;
          }
        }
        cout << endl
             << "Employee #" << key << ", " 
             << employees[binarySearch(employees, size, key)].firstName << " "
             << employees[binarySearch(employees, size, key)].lastName << " is in index: " 
             << binarySearch(employees, size, key) << endl << endl;
        break;


//Option 2: Checks if ID is valid, then adds employee to the queue
      case 2:
        cout << "Enter employee ID to be added to queue: ";
        cin >> qID;
        cout << endl;

        if (binarySearch(employees, size, qID) == -1)
        {
          while (binarySearch(employees, size, qID) == -1)
          {
            cout << "ERROR: ID not found. Try again." << endl;
            cout << "Enter employee ID to be added to queue: ";
            cin >> qID;
            cout << endl << endl;
          }
        }        
        numstr = to_string(qID);
        ln = employees[binarySearch(employees, size, qID)].lastName;
        fn = employees[binarySearch(employees, size, qID)].firstName;
        appt.addQueue(ln);
        appt.addQueue(fn);
        appt.addQueue(numstr);
        counter++;
        cout << "Employee #" << qID << " has been added to the queue." << endl;   
      break;


//Option 3: Prints all of the employees in the appointment queue in order 
      case 3:
        appt.print();
        cout << endl << endl;
      break;


//Option 4: Removes the first employee in the queue
      case 4:
        if (!appt.isEmptyQueue())
        {
          appt.deleteQueue();
          appt.deleteQueue();
          appt.deleteQueue();  
          counter--;      
          cout << "The next employee in line has been removed. " << endl << endl;
        }
        else
        {
          cout << "Cannot remove employee from an empty queue. " << endl << endl;
        }
      break; 


//Option 5: Shows the last employee in the queue
      case 5:
        if (!appt.isEmptyQueue())
        {
          cout << "The last employee in the queue is employee #" << appt.back() 
             << "." << endl << endl;
        }
        else
        {
          cout << "The queue is empty." << endl << endl;
        }
                      
      break;


//Option 6: Shows the total number of employees in the queue
      case 6:
        cout << "There are a total number of " << counter << " employees in the queue." 
             << endl << endl;
      break;


//Option 7: Terminates the program
      case 7:
        cout << "Goodbye." << endl << endl;
        return 0;
      break;
    }
  }
}//end main



//Funtions


//function that displays the menu
void menu() 
{
  cout << endl;
  cout << "1. Find an employee by id" << endl; 
  cout << "2. Add an employee to the appointment queue" << endl;
  cout << "3. Show the appointment queue" << endl;
  cout << "4. Remove an employee from the appointment queue" << endl;
  cout << "5. Show last employee in the queue" << endl;
  cout << "6. Show total number of employees in the queue" << endl;
  cout << "7. Exit";
  cout << endl << endl;
}//end menu


//Insertion sort function
template <class elemType>
void insertionSort(elemType list[], int length)
{
    for (int firstOutOfOrder = 1; firstOutOfOrder < length;
                                  firstOutOfOrder++)
        if (list[firstOutOfOrder].empID < list[firstOutOfOrder - 1].empID)
        {
            elemType temp; 
            temp.empID = list[firstOutOfOrder].empID;
            temp.firstName = list[firstOutOfOrder].firstName;
            temp.lastName = list[firstOutOfOrder].lastName;
            int location = firstOutOfOrder;

            do
            {
                list[location].empID = list[location - 1].empID;
                list[location].firstName = list[location - 1].firstName;
                list[location].lastName = list[location - 1].lastName;
                location--;
            } while(location > 0 && list[location - 1].empID > temp.empID);

            list[location].empID = temp.empID;
            list[location].firstName = temp.firstName;
            list[location].lastName = temp.lastName;
        }
} //end insertionSort

//Binary search function
int binarySearch(const empData list[], int listLength, int searchItem) 
{
    int first = 0;
    int last = listLength - 1;
    int mid;

    bool found = false;

    while (first <= last && !found)
    {
        mid = (first + last) / 2;

        if (list[mid].empID == searchItem)
            found = true;
        else if (list[mid].empID > searchItem)
            last = mid - 1;
        else
            first = mid + 1;
    }

    if (found) 
        return mid;
    else
        return -1;
}//end binarySearch

