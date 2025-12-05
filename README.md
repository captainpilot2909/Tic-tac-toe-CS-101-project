# Tic-tac-toe-CS-101-project

#include <iostream>
#include <string>
using namespace std;

int check_winner(string board[3][3]);

int main() {
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
        cin >> row >> col;

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
        cin >> row >> col;

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
    
