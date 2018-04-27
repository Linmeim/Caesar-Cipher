//# Caesar-Cipher
//Caesar Cipher encryption and decryption from users input

 /**********************************************************
*File: midTermProject.cpp                                 *
*Describtion: This program is designed for user to        *
*decode or encode their text with their key entry         *
*student: Linmei Mills				                      *
*Class#: CS105						                      *
*Date: 4/7/2018										      *
**********************************************************/
#include<iostream>
#include<string>
#include<fstream>
#include<cmath>
using namespace std;

/*function prototypes*/
int getMenu();
void getEM(int key, char message[]);
void getDM(int key, char message[]);
void getFile(int key, char message[]);




/*****************************************************************
*FUNCTION:  main()                                               *
*DESCRIPTION:  create case choices with directions of what       *
*user wish to do. Chose to manually encry or decry or chose to   *
*read from a file and decide encrypt or decrypt                  *
*RETURNS: 0														 *
*NOTES: Menu choice is not in main function                      *
****************************************************************/
int main()
{
	ofstream fout;
	char  choice, answ, answer, answer2, m;
	int key;
	char message[80];
	fout.open("out.txt");


	do {
		choice = getMenu();

		switch (choice)
		{
		case 'A':
			cout << "Please enter the key" << endl;//get key from user
			cin >> key;


			cout << "Do you wish to do mannully or read from a file(m/f)" << endl;
			cin >> answer;

			if (answer == 'm' || answer == 'M')//use chose mannual entry
			{
				cout << "Please enter the message" << endl;
				cin.ignore();
				cin.getline(message, 80);

				cout << "please chose encrypt or decrypt(e/d)" << endl;

				cin >> answer2;

				if (answer2 == 'e' || answer2 == 'E')// user chose to mannally encrypt msg
				{

					getEM(key, message);
				}

				else if (answer2 == 'd' || answer2 == 'D')
				{
					getDM(key, message);
				}

			}

			else if (answer == 'f' || answer == 'F')//user chose read msg from a file
			{
				getFile(key, message);
			}
			/*cout << "Would you wish to go back to menu?" << endl;
			cin >> answ;
			if (answ = 'yes')
			getMenu();
			else
			cout << "goodbye" << endl;*/
			fout.close();
			break;
		case 'B': // do nothing
			cout << "Just Kidding" << endl;
			break;
		case'C':// do nothing
			cout << " May The Force be With You" << endl;
			break;
		case 'D':// user chose to quit program
			cout << "You chose to quit. Goodbye拢隆" << endl;
			break;
		default:
			cout << "Invalid Entry. Please enter again.";
		}
	} while (choice == 4);
	cout << endl;
	system("pause");
	return 0;
}


/*****************************************************************
*FUNCTION:  getMenu()                                            *
*DESCRIPTION:  create a menu selection                           *
*RETURNS: choice(menu choice)									 *
*****************************************************************/
int getMenu()
{
	char choice;
	cout << "Please Selection Options" << endl;
	cout << "A  Encoding/Decoding Text" << endl;
	cout << "B  Surprise" << endl;
	cout << "C  Life is Good" << endl;
	cout << "D  Quit Program " << endl;
	cin >> choice;
	choice = toupper(choice);
	return choice;
}

/*****************************************************************
*FUNCTION:  getEM()                                              *
*DESCRIPTION:  encrypt message mannually                         *
*RETURNS: nothing(void function)			    				 *
*****************************************************************/
void getEM(int key, char message[])
{
	char letter;
	for (int i = 0; message[i] != '\0'; i++)//from A to Z
	{
		message[i] = toupper(message[i]);
		letter = message[i];

		if (letter >= 'A' && letter <= 'Z')
		{
			letter = letter + key;
			if (letter > 'Z')
				letter = letter - 'Z' + 'A' - 1;
		}
		message[i] = letter;
	}
	cout << "Encrpyted message: " << message << endl;
}


/*****************************************************************
*FUNCTION:  getDM()                                              *
*DESCRIPTION:  decrypt message mannually                         *
*RETURNS: nothing(void function)			    				 *
*****************************************************************/
void getDM(int key, char message[])   // //something wrong here????? it does not translate the msg at all.???
{
	char letter;

	for (int i = 0; message[i] != '\0'; i++)
	{
		
		message[i] = toupper(message[i]);
		letter = message[i];

		if (letter > 'A' && letter <= 'Z')
		{
			//cout << "[DEBUG] OLD LETTER: " << letter << endl;
			letter = letter - key;
			//cout << "[DEBUG] NEWLETTER: " << letter << endl;
		}
		if (letter > 'Z')
		{
			letter = letter + 'Z' - 'A' + 1;
		}
		if (letter == 'A')
		{
			if (key > 0)
			{
				letter = 'Z' - (key - 1);
			}
		}
		message[i] = letter;

	}
	cout << "decrpyted message: " << message << endl;
	
	system("pause");
}

/*****************************************************************
*FUNCTION:  getEMF()                                             *
*DESCRIPTION:  Encrypt message from a file                       *
*RETURNS: nothing(void function)			    				 *
*****************************************************************/
void getFile(int key, char message[])
{
	bool stop = false;
	string fileName;
	char answer2;
	ifstream inputFile;
	cout << "Please enter the name of your file" << endl;
	//cin.ignore();
	cin >> fileName;

	inputFile.open(fileName);

	if (!inputFile)
	{
		cout << "Invalid" << endl << "Please enter again" << endl;

		stop = true;
	}

	//if file is open, read from it
	if (stop == false)
	{
		while (inputFile.getline(message, 80))
		{
			cout << "please chose encrypt or decrypt(e/d)" << endl;
			cin >> answer2;

			if (answer2 == 'e' || answer2 == 'E') // user chose encrypt msg from an file
			{
				getEM(key, message);
			}
			if (answer2 == 'd' || answer2 == 'D')
				getDM(key, message);
		}

	}
	inputFile.close();
	
}
/*****************************************************************
*FUNCTION:  getDMF()                                             *
*DESCRIPTION:  Decrypt message from a file                       *
*RETURNS: nothing(void function)			    				 *
*****************************************************************/
