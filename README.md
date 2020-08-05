# Snake-and-Ladder-Game.cpp
Implemented with 1D array and string variables. and everything explained in games rules 
//Libraries for I/O , Random Numbers , String Stream(Converting Integars to Strings) and Formatting Ouput 
#include<iostream>
#include<string>
#include<sstream>
#include<conio.h>
#include<iomanip>
#include<cstdlib>
#include<ctime>
using namespace std;

//Funtions Decalarations 

void rules_of_game();
void name_input(string &a , string &b);
void board_filling(string arr[]);
void printing_Board(string arr[]);
void rolling_dice(string name , int &index);
void ladder_snake_checking(int &index);
bool winning_check(string arr[]);
void reminder();
void error_resolving(string arr[] , int index);

//Main Started Here
int main(){
	//For Creating Random Numbers every time
		srand(time(0));
    //For Asking user to play again or not
		char user_key;	
    //Strinf Array for Table
		string array[50];
	//Filling of Board(Table)
		board_filling(array);
	//At starting 
		array[0] = "X and O";

    //Players name and their point Tracking
		string player1 , player2;
		int player1_tracking = 0,  player2_tracking = 0;

//Do While loop for playing game
		do{
	    //Prininting of game rules to screen for players
			rules_of_game(); 
		//Asking the name of Players
			name_input(player1 , player2);
		//Just for Documentation of Code
			reminder();
		//For Clearining Screen
			system("CLS");
		//For Priniting Ludo table for 1st time
			printing_Board(array);
        //LOOP untill a player won
			while(true){
				board_filling(array);
				array[player2_tracking] = "OOOO";
			//Rolling Die for 1st Player
				rolling_dice(player1 ,player1_tracking);	
		    //For checking Whether a Player 1 got Ladder or Bitten by Snake 
				ladder_snake_checking(player1_tracking);
			//For Checking Wether the goti of player 2 already here or not
				if(array[player1_tracking] == "OOOO"){
	       			cout<<"Ouch! " << player2 << " Due to Badluck! you have to GO Back";
	       			player2_tracking = 0;
	      	 		array[player2_tracking] = "OOOO";
	       			getch();
				   }
			//Assigining the values   
				array[player1_tracking] = "XXXX"; 
				system("CLS");
		    	printing_Board(array);
		    //Checking if player won or not
		        if (winning_check(array)){
					cout <<"Congrat's!" << player1 <<" has Won";
				    reminder();
				    system("CLS");
					break;
	    				 }
	    	//A function just to remove previous OOOO 
        			error_resolving(array , player2_tracking);
	        //Rolling Dice for 2nd Player
					rolling_dice(player2 ,player2_tracking);
			//For checking Whether a Player 1 got Ladder or Bitten by Snake 
					ladder_snake_checking(player2_tracking);
			
			//For Checking Wether the goti of player 1 already here or not           
				if(	array[player2_tracking] == "XXXX") {
	       			cout<<"Ouch! " << player1 << " Due to Badluck! you have to GO Back";
	       			player1_tracking = 0;
	       			array[player1_tracking] = "XXXX";
	       			getch();
			   		}
			//Assigning Values
				array[player2_tracking] = "OOOO"; 
				system("CLS");
	        	printing_Board(array);
		    //Checking if Player 2 Won or not
				if (winning_check(array)){
					cout <<"Congrat's!" << player2 <<" has Won\n";
	    			reminder();
	    			system("CLS");
					break;
	     			}
			}	
		//Asking to user if they wanna to play further or not	
			cout << "\nWanna to Play again?(press y if Yes)";
			cin >> (user_key);
			}
		while(user_key=='y' || user_key=='Y');

		return 0;

	}

//Rules of Game
void rules_of_game(){
	cout << "Both Players will start their Gameplay from Position Zero(0)\n";
	cout << "RULES: \n1) You Have to Roll the Dice for Further movements\n";
	cout << "2) If You Achieved Ladder then you will Jumped\n   \t*First Laddder: Starts at 5 and Ends at 17\n   \t*Second Laddder: Starts at 30 and Ends at 46\n";
	cout << "3) If You Bitten by Snake then you will Fallen down\n   \t*First Snake: Mouth at 19 and Tail at 3\n   \t*Second Snake: Mouth at 48 and Tail at 27\n";
	cout << "4) If Both Player Got to Same Box then the player that is Already here\nhave to start his/her game from Start(Postion zero:0)\n";
	cout << "Best of Luck For Your Game\nPress Any key For Starting: ";
    getch();
}

//Getting a Key
void reminder(){
	cout <<"Press Any key to Continue?";
	getch();
	}

//Input of Names
void name_input(string &a , string &b){
	cout << "\nEnter the name of First Player? ";
	cin >> a;
	cout << "Enter the name of Second Player? ";
	cin >> b;
	}

//Array filling for Table Printing
void board_filling(string arr[]){	
	stringstream ss;
	for (int i=0; i<50; i++){
		ss << i+1;
	//Converstion of Integar to String
   		arr[i] = ss.str();
	//For Clearing String stream
		ss.str("");
	}
//Assigning of Ladder and Snakes_bitting Point 
	arr[4] = arr[29] =  "Ladder";
	arr[18] = arr[47] = "Snake";	
	}

//Rolling a die
void rolling_dice(string name ,int &index){
	
	cout <<  name  << "'s Turn:\nPress Any key to Roll Your Dice: ";
	getch();
	int dice = rand() % 5 + 1;
	cout << "You Got " << dice;
	index+=dice;
	if (index > 49){
		cout << "\nTry Again";
		index-=dice;
	}
	
    cout << endl << "Press any Key: ";
    getch();
	}
//Priting a Table in from of Snake_ladder game
void printing_Board(string arr[]){
	cout << endl;
	//Outer Loop
	for (int i=49; i>=0; i-=10){
		
		// First Row of 5 Numbers
			for (int j=0; j<5; j++) cout << "      " <<left <<setw(8) << arr[i-j] << "|";
			
      		cout << "\b " << endl;
      	
	   //For Properly Documentation of Lines
		    for (int n=0; n<5; n++) cout <<"_______________";
		       
			cout << endl << endl;
	    	
	  	// Second Row of 5 numbers in Reverse Order
	        for(int m=9; m>4; m--)cout << "      " <<left <<setw(8) << arr[i-m] << "|";
	
			cout << "\b " << endl;
	 //For Properly Documentation of Lines
		    for (int n=0; n<5; n++) cout <<"_______________";
		       
			 cout << endl << endl;
				}
		}

//For Checking Ladder_Jumping or Snake_Bitten
void ladder_snake_checking(int &index){
	if (index == 18 || index == 47 ){
		cout << "\nOuch! You beaten By a Snake\n";
		if(index == 47 ){
		  cout << "You fallen down to Point 27\n ";
		  index-=21;
			}
		else {
	     cout << "You fallen down to Point 3\n ";
		index-=16;
			}
	getch(); 
		}
				
	if (index == 4 ||  index== 29){
		cout << "\nCongrat's. You Found a Ladder\n";
		if (index == 4){ 
		cout << "You will Moved to Point 17\n";
		index+=12;
			}
		else{
			cout << "You Will be Moved to Point 46\n";
		index+=16;	
			}
		getch(); 
		}	
	}
	//For Checking if player Won or Not 
bool winning_check(string arr[]){
	if (arr[49]=="XXXX" || arr[49] == "OOOO")return true;
	return false;
}

//Just to Resolve a Random Problem
void error_resolving(string arr[] , int index){
	stringstream tt;
	tt << index+1;
	arr[index] = tt.str();
}
