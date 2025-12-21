#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;
string playagain="yes";

void P_VS_P();
void P_VS_Computer();
int check_winner(string board[3][3]);
int countMoves(string board[3][3], int i = 0, int j = 0); // recursive draw checker
int err_handling_int(int check);
bool player_checker(string name);

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

    do{
        cout<<"============Enter the Gamemode you want to play:============"<<endl;
        cout<<"1.Player VS Player:"<<endl;
        cout<<"2.Player VS computer:"<<endl;
        cin>>choice;
        err_handling_int(choice);
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
    
    return 0;
}

// Recursive draw checker
int countMoves(string board[3][3], int i, int j){
    if(i==3) return 0;
    int count = (board[i][j] != " _ ");
    if(j==2) return count + countMoves(board, i+1, 0);
    else return count + countMoves(board, i, j+1);
}

void P_VS_P(){
    int row, col;
    string arr[3][3];

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            arr[i][j] = " _ ";

    cout << "Player X begins first" << endl;
    while(true){ 
        cout << "Enter row and column (0-2): "<<endl;
        cout<<"Row: ";
        cin >> row ;
        row=err_handling_int(row);
        cout<<"Column: ";
        cin >> col;
        col=err_handling_int(col);

        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position "<<endl;
            cout<<"Row: ";
            cin >> row ;
            row=err_handling_int(row);
            cout<<"Column: ";
            cin >> col;
            col=err_handling_int(col);
        }

        arr[row][col] = " X ";
        cout<<endl;

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }

        if(check_winner(arr)){
            cout<<"Player X wins!"<<endl;
            break;
        }
        if(countMoves(arr)==9){
            cout<<"Game Draw!"<<endl;
            break;
        }

        // PLAYER O
        cout << "Player O turn. Enter row and column (0-2): "<<endl;
        cout<<"Row: ";
        cin >> row;
        row=err_handling_int(row);
        cout<<"Column: ";
        cin >> col;
        col=err_handling_int(col);

        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position "<<endl;
            cout<<"Row: ";
            cin >> row ;
            row=err_handling_int(row);
            cout<<"Column: ";
            cin >> col;
            col=err_handling_int(col);
        }

        arr[row][col] = " O ";
		cout<<endl;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        if(check_winner(arr)){
            cout<<"Player O wins!"<<endl;
            break;
        }
        if(countMoves(arr)==9){
            cout<<"Game Draw!"<<endl;
            break;
        }
    }
    cout<<"Do you want to Play again?.\n yes/no"<<endl;
    cin>>playagain;
}

void P_VS_Computer(){
    int row, col;
    string arr[3][3];

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            arr[i][j] = " _ ";

    cout << "Hey,human !\n =====Lets see How well can you play!!!=====" << endl;
    
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++){
            cout << arr[i][j];
        }
        cout << endl;
    }

    srand(time(0));

    while(true){ 
        cout << "Enter row and column (0-2): ";
        cout<<"Row: ";
        cin >> row ;
        row=err_handling_int(row);
        cout<<"Column: ";
        cin >> col;
        col=err_handling_int(col);

        while (row < 0 || row > 2 || col < 0 || col > 2 || arr[row][col] != " _ ") {
            cout << "Invalid or occupied position "<<endl;
            cout<<"Row: ";
            cin >> row ;
            row=err_handling_int(row);
            cout<<"Column: ";
            cin >> col;
            col=err_handling_int(col);
        }

        arr[row][col] = " X ";
        cout<<endl;

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        if(check_winner(arr)){
            cout<<"Human!!! you have won ahhhh!"<<endl;
            break;
        }
        if(countMoves(arr)==9){
            cout<<"Game Draw!"<<endl;
            break;
        }

        // PLAYER O
        cout << "Computers turn.yay!!!! "<<endl;
        do{    
            row=rand() % 3;
            col=rand() % 3;
        }while (arr[row][col] != " _ ");

        arr[row][col] = " O ";
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++)
                cout << arr[i][j];
            cout << endl;
        }
        if(check_winner(arr)){
            cout<<"Computers are here to win!"<<endl;
            break;
        }
        if(countMoves(arr)==9){
            cout<<"Game Draw!"<<endl;
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

bool player_checker(string name){
    fstream file_checker;
    file_checker.open("Players_name.txt",ios::in);
    string line;
    while(getline(file_checker,line)){
        if(name==line){
            cout<<"Welcome Back "<<name<<"!"<<endl;
            file_checker.close();
            return true;
        }
    }
    return false;
}
