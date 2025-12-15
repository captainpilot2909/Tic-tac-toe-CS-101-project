# Tic-tac-toe-CS-101-project

#include <iostream>
#include <string>
using namespace std;

int check_winner(string board[3][3]);
void P_VS_P();
void P_VS_Computer();

int main() {
	int choice;
    string name;
    fstream playerfile;

    cout<<"====Please enter your name:===="<<endl;
    getline(cin,name);
    playerfile.open("Players_name.txt",ios::out | ios::app);

    bool check=player_checker(name);
    if(check==false){
        cout<<"Welcome "<<name<<"! you are a new player!"<<endl;
        playerfile<<name<<endl;
    }
    playerfile.close();

	cout<<"============Enter the Gamemode you want to play:============"<<endl;
	cout<<"1.Player VS Player:"<<endl;
	cout<<"2.Player VS computer:"<<endl;
	cin>>choice;
	err_handling_int(choice);

    do{
        switch(choice){
            case 1:
                P_VS_P();
                break;

            case 2:
                P_VS_Computer();
                break;
            default:
                cout<<"Invalid choice"<<endl;
                break;
        }
    }while(playagain=="yes");
    cout<<"Thanks for playing "<<name<<"!"<<endl;
    return 0;
}


int check_winner(string board[3][3]){
    for(int i=0;i<3;i++){
    	if(board[i][0]==board[i][1] &&
		   board[i][1]==board[i][2] &&
		   board[i][0]!=" _ ")
			return 1;    
    }

    for(int j=0;j<3;j++){
    	if(board[0][j]==board[1][j] &&
		   board[1][j]==board[2][j] &&
		   board[0][j]!=" _ ")
			return 1;  
    }  
	
	if(board[0][0]==board[1][1]&&
	   board[1][1]==board[2][2]&&
       board[0][0]!=" _ ") 
	   	return 1;
	
	if(board[0][2]==board[1][1]&&
	   board[1][1]==board[2][0]&&
       board[0][2]!=" _ ") 
	   	return 1;
	else{
		return 0;
	}
}
    
void P_VS_P(){
	    int row, col;
    string arr[3][3];

    // initialize board
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            arr[i][j] = " _ ";

    cout << "=================\n";
    cout << "Welcome to the Tic Tac Toe Game:\n";
    cout << "=================\n";

    // show board
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++)
            cout << arr[i][j];
        cout << endl;
    }

    // PLAYER X
    cout << "Player X begins first" << endl;
    while(true){ 
        cout << "Enter row and column (0-2): ";
        cin >> row ;
        row=err_handling_int(row);
        cin >> col;
        col=err_handling_int(col);

        // validate input
        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position. Try again: ";
            cin >> row >> col;
        }

        arr[row][col] = " X ";

        // print updated board
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        int check=check_winner(arr);
        if(check==1){
        	cout<<"Player X wins!"<<endl;
        	break;
        }

        // PLAYER O
        cout << "Player O turn. Enter row and column (0-2): ";
        cin >> row;
        row=err_handling_int(row);
        cin >> col;
        col=err_handling_int(col);

        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position. Try again: ";
            cin >> row >> col;
        }

        arr[row][col] = " O ";
        check=check_winner(arr);

        // print updated board
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        if(check==1){
        	cout<<"Player O wins!"<<endl;
        	break;
        }
    }
    cout<<"Do you want to Play again?.\n yes/no"<<endl;
    cin>>playagain;
}
void P_VS_Computer(){

	int row, col;
    string arr[3][3];

    // initialize board
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            arr[i][j] = " _ ";

    cout << "=================\n";
    cout << "Welcome to the Tic Tac Toe Game:\n";
    cout << "=================\n";

    // show board

    cout << "Hey,human !\n =====Lets see How well can you play!!!=====" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++)
            cout << arr[i][j];
        cout << endl;
    }

    // PLAYER X

    while(true){ 
        cout << "Enter row and column (0-2): ";
        cin >> row >> col;

        // validate input
        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position. Try again: ";
            cin >> row ;
            row=err_handling_int(row);
            cin >> col;
            col=err_handling_int(col);
        }

        arr[row][col] = " X ";

        // print updated board
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        int check=check_winner(arr);
        if(check==1){
        	cout<<"Human!!! you have won ahhhh!"<<endl;
        	break;
        }

        // PLAYER O
        cout << "Computers turn.yay!!!! "<<endl;
		srand(time(0));
		do{	
			row=rand() % 3;
			col=rand() % 3;
		}while (arr[row][col] != " _ ");

        arr[row][col] = " O ";
        check=check_winner(arr);

        // print updated board
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        if(check==1){
        	cout<<"Computers are here to win!"<<endl;
        	break;
        }
    }
    cout<<"Do you want to Play again?.\n yes/no"<<endl;
    cin>>playagain;
}

int err_handling_int(int check){
	while(true){
		if(cin.fail()){
			cin.clear();
			cin.ignore(1000,'\n');
			cout<<"Invalid input.Re-enter :"<<endl;
			cin>>check;
		}
		else{
			return check;
		}
	}
}

