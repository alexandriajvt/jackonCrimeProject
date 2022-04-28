# jackonCrimeProject
This is my Software Application project to keep track of crime reports in the Jackson Area.
Violence in Jackson, Mississippi is a major problem. Jackson is Mississippi’s most violent city.

5 helpful sources:

https://www.cnn.com/2021/12/28/us/jackson-mississippi-pandemic-homicides-gun-violence/index.html

https://nypost.com/2021/12/29/jackson-mississippi-hits-all-time-homicide-record/

https://www.clarionledger.com/story/news/2021/12/31/jackson-ms-homicides-violent-crime-2021-broke-records/9059177002/

https://www.usnews.com/news/best-states/mississippi/articles/2021-10-16/jackson-community-and-police-march-against-violent-crime

https://www.jacksonfreepress.com/news/2021/jun/02/violence-city-victims-families-seek-closure-police/


My solution is a software application that will allow Jackson citizens to report crimes in their neighborhoods. 
User’s will be able to enter their name and the location,time, and type of crime committed. The user's report will be added to a list of existing reports, in which
the authorities can use.

![image](https://user-images.githubusercontent.com/97464529/161778929-1892b2fc-ba56-470c-8198-8436444caeee.png)


![just menu1](https://user-images.githubusercontent.com/97464529/165676260-eccf9347-27b2-49e5-9ce6-472dad4b22f4.PNG)

![menu 1 then continue](https://user-images.githubusercontent.com/97464529/165676279-e310c710-7902-4753-8d2e-e78ec371d1d0.PNG)

![menu 2](https://user-images.githubusercontent.com/97464529/165676291-707a469d-9614-49ae-bc80-3f2a85a5b752.PNG)

![menu 2 and 1](https://user-images.githubusercontent.com/97464529/165676313-46322d5c-2d35-410c-afd7-5492b3dd64c5.PNG)


Source Code:
#include <iostream>
#include <string>
#include <fstream>

using namespace std;


class personType {
public:
	void getFirst();
	void getLast();
	void printName();
	string setName();//returns(holds the string) of the user's whole name
	int getChoice();
	int option;//user will choose an option from the menu
	string firstName;

private:
	//string firstName;
	string lastName;
	
};

class crimeType {
public:
	void getCrime();
	string setCrime();//may delete
	void printCrime();
private:
	string crime;
};

class timeType {
public:
	void printDate();
	void printTime();
	string setDate();//contains the string of the date(includes month, day, year)
	string setTime();//contains a string of the time(incldues hour and minute)
	void getDate();
	void getTime();

private:
	string hour; //all data types are string, allowing the getDate and getTime member functions to return strings that are a combination of multiple member variables
	string minute;
	string date;
	string month;
	string year;
};

class locationType{
public:
	void getAddress();
	string setAddress();//returns a string of the location(including the street name and the address)
	timeType time2;//composition
private:
	string streetName;
	string addressNumber;
};

class goodbye : public personType {
public:
	void printRating();
private:
	int rating;
};



personType firstPerson;//declares an instance of each class. These instances will be used in the main function and have global scope
crimeType firstCrime;
timeType firstTime;
locationType firstLocation;
goodbye soLong;//rename this


void menu1() {
	firstCrime.getCrime();
	firstTime.getTime();
	firstTime.getDate();
	firstLocation.getAddress();
	cout << firstPerson.setName() << " is reporting that a(n) " << firstCrime.setCrime() << " took place on " << firstTime.setDate() << " at " << firstTime.setTime()
		<< " at " << firstLocation.setAddress() << endl;
}


void menu2() {
	ifstream inData;
	ofstream outData;
	inData.open("pastCrime.txt");//opens the file which is the past crime an array of structs.
	struct crimeCaseType {
		int caseNo;
		string typeOfCrime;
		string monthReported;
		string dayReported;
		string yearReported;
	};
	crimeCaseType crimeCases[5];
	for (int i = 0; i < 5;i++) {//loop that will display to the user the list of previously reported crimes.
		string crime;
		inData >> crimeCases[i].caseNo >> crimeCases[i].monthReported >> crimeCases[i].dayReported >> crimeCases[i].yearReported; //crimeCases[i].typeOfCrime;
		getline(inData, crime);//used to read the type of Crime because sometimes the name of the crime may be multiple words.

		crimeCases[i].typeOfCrime = crime; //stores the crime into the appropriate struct variable
		cout << "Case #: " << crimeCases[i].caseNo << "		"
			<< "Date Reported: " << crimeCases[i].monthReported << " " << crimeCases[i].dayReported << ", " << crimeCases[i].yearReported << "		"
			<< "Crime Witnessed: " << crimeCases[i].typeOfCrime << endl;
	}
	inData.close();
	outData.close();
}



int main() {
	string greeting = "Hello everyone my name is Alex. Welcome to my program called Jackson Crimes.";
	string *greetingPointer;
	greetingPointer = &greeting;
	cout << greeting << endl<<endl;

	firstPerson.getFirst();
	firstPerson.getLast();
	firstPerson.getChoice();


	if (firstPerson.option == 1) {
		menu1();
		int repeat;
		cout << "Would you like to view existing crimes? Enter 1 for Yes and 2 for No. " << endl;
		cin >> repeat;
		if (repeat == 1) {
			menu2();
			cout << "Case #: 6"<<"		"
				<< "Date Reported: " << firstTime.setDate()<<"		"
				<< "Crime Witnessed: " << firstCrime.setCrime() << endl;
			soLong.firstName = firstPerson.firstName;//adds the newly reporte crime to the old list, since the lsit was printed in menu2 function
			soLong.printRating();
		}
		else if (repeat == 2) {
			soLong.firstName = firstPerson.firstName;
			soLong.printRating();
		}

	}else {
			if (firstPerson.option == 2) {
				menu2();
				int repeat;
				cout << "Would you like to report a crime? Enter 1 for Yes and 2 for No. " << endl;
				cin >> repeat;
				if (repeat == 1) {
					menu1();
					soLong.firstName = firstPerson.firstName;
					soLong.printRating();
			     }
				else {
					if (repeat == 2) {
						soLong.firstName = firstPerson.firstName;
						soLong.printRating();
					}
				}
			}

		}

	}



///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


void personType::getFirst(){
	cout << "Please enter your first name" << endl;
	cin >> firstName;
}
void personType::getLast() {
	cout << "Please enter your last name" << endl;
	cin >> lastName;
}
void personType::printName() {
	cout << firstName << " " << lastName << endl;
}
int personType::getChoice() {
	cout << "Enter a numerical option from the menu below:" << endl <<
		"1. Submit a new crime report" << endl <<
		"2. View existing crime reports" << endl;
	cin >> option;
	return option;
}
string personType::setName() {
	return firstName + " " + lastName;
}




void crimeType::getCrime() {
	cout << "Please enter the crime you witnessed." << endl;
	cin >> crime;
}
string crimeType::setCrime() {
	return crime;
}
void crimeType::printCrime() {
	cout << crime << endl;
}




void timeType::getDate() {
	cout << "What month did the crime take place in? " << endl;
	cin >> month;
	cout << "What date did the crime take place on? " << endl;
	cin >> date;
	cout << "What year did the crime take place in? " << endl;
	cin >> year;
}
void timeType::getTime() {
	cout << "Enter the hour that the crime happened." << endl;
	cin >> hour;
	cout << "Enter the minute that the crime happened." << endl;
	cin >> minute;
}
string timeType::setTime() {
		return hour + ":" + minute;
}
string timeType::setDate() {
	return month + " " + date  + ", " + year;
}
void timeType::printDate() {
	cout << month << " " << date << ", " << year;
}
void timeType::printTime() {
	cout << hour << ":" << minute;
}



void locationType::getAddress() {
	cout << "Please enter the address number where the crime was committed" << endl;
	cin >> addressNumber;
	cout << "Please type the street name where the crime was committed" << endl;
	cin >> streetName;
}
string locationType::setAddress() {
	return addressNumber + " " + streetName + " Street";
}

void goodbye::printRating() {
	cout << "Please rate my program on a scale of 1-5? ";
	cin >> rating;
	cout <<endl<<endl<< "Thank you, " << firstName << " for rating my program a " <<rating <<" out of 5, Goodbye."<< endl;
}
