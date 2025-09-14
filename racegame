#include <iostream>
#include <string>
#include <limits>

// class specifications
class Player {
    //fields must remain private, don't expose them
private:
    std::string name;
    int score;

public:

    Player(const std::string& n, int startScore);
    //return by const reference, avoids copying the string
    const std::string& getName() const;
    //return by value, int data type because it is small and easy to copy
    int getScore() const;

    bool hasWon(int target) const;

    void addToScore(int amount);
    /*score changes have to go through the addToScore fuction
    it is a pass by value because int is a value, and it will not change the users data
    but since it is a small int number, the pass by value makes it faster to pass data
    */


};


//player method definitions
Player::Player(const std::string& n, int startScore) : name(n), score(startScore) {}

//return by const value
const std :: string& Player::getName() const{
    return name;
}
//return by value
int Player::getScore () const{
    return score;
}

bool Player::hasWon(int target) const{
    return score >= target;
}
void Player::addToScore(int amount){
    score += amount;
}



//free functions
//pass by reference, the "who" is the player
void addMove(Player& who, int step) {
    if (step != 1 && step != 2 && step != 3) {
        std::cout<<"Invalid step number!\n";
        return;
    }
    who.addToScore(step);
    std :: cout << who.getName() << " add + " << step << " points\n"
    << who.getName() << " has " << who.getScore() << " points\n";
}

//pointer to primitive, dereferences the pointer to modify the original int
void  useBonus(int* bonusPtr, Player& who) {
    if (bonusPtr == nullptr) {
        return;
    }
    if (*bonusPtr <= 0) {
        std :: cout << who.getName() << " does not have a bonus\n";
        return;
    }
    who.addToScore(*bonusPtr);
    std :: cout <<"used the bonus points " << *bonusPtr << "\n"
    << who.getName() << " has " << who.getScore() << " points\n";
    *bonusPtr = 0;
}

// Deterministic computer helper
//uses a function-scope to remember the state between calls (like 1 of 2)
int compStep() {
    //returns 1
    static bool OneNext = true;
    int result = OneNext ? 1 : 2;
    OneNext = !OneNext;
    return result;
}


/*the pass-by-reference updates the original object because the addMove function includes the & symbol
in the Player parameter, which makes a reference parameter that references the original and entered
data value to both the same memory access
*/
void addMove(Player& who, int step);


// the parameter of int* bonusPtr makes a pointer of type int and includes it in the parameter to use in the function
void useBonus(int* bonusPtr, Player& who);



int main() {
    const int TARGET = 20;

    //human player
    Player you("You", 0);
    //computer player
    Player computer("Computer", 0);

    //bonus
    int bonus = 2;


    //menu each turn header, reading user input
    int choice;

    //welcoming to the race game
    std ::cout << "Welcome to the race game\n";

    while (true) {
        std :: cout << "menu for each turn\n";
        //option 1 adds one point
        std :: cout << "option 1: add 1\n";
        //option 2 adds two points
        std :: cout <<  "option 2:add 2\n";
        //option 3 adds three points
        std :: cout <<  "option 3: add 3\n";
        //bonus option 2 adds a bonus of two points
        std :: cout <<  "option 4: bonus, one time bonus +2 points\n";
        //quits game
        std :: cout <<  "option 5: quit game\n";

        std :: cout <<  "enter your choice number: \n";
        std::cin >> choice;
        //in case wrong input like letters, i looked up how to discard the wrong input
        if (!(std :: cin >> choice)) {
            std :: cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std :: cout <<"invalid input\n";
            continue;
        }

        switch (choice) {
            case 1:
                std :: cout <<  "you chose 1\n";
                addMove(you, choice);
                break;
            case 2:
                std :: cout <<  "you chose 2\n";
                addMove(you, choice);
                break;
            case 3:
                std :: cout <<  "you chose 3\n";
                addMove(you, choice);
                break;
            case 4:
                std :: cout <<  "you chose the bonus\n";
                useBonus(&bonus, you);
                break;
            case 5:
                std :: cout <<  "exiting the game\n";
                return 0;
            default:
                std :: cout << "opps try again\n";
                continue;
        }


        // checks immdidiently after switch statement if player has enough points
        if (you.hasWon(TARGET)) {
            std::cout << you.getName() << std::endl;
            std::cout << "Human player wins." << std::endl;
            break;
        }

        //computer turn
        int step = compStep();
        addMove(computer, step);


        // end of the round results print
        const bool youAtorOver = you.hasWon(TARGET);
        const bool compAtorOver = computer.hasWon(TARGET);


        //checking scores and printing
        if (youAtorOver && compAtorOver) {
            std::cout << "your score" << you.getScore() << "\n" << "computer score "
                        << computer.getScore() << "\n";
            std :: cout << " it is a tie ";
            break;
        } else if (compAtorOver) {
            std::cout << "your score" << you.getScore() << "\n" << "computer score "
            << computer.getScore() << "\n";
            std :: cout << " computer wins ";
            break;
        }
        std :: cout << "final scores:\n" << "your score " << you.getScore() << "\n" <<
            "computer score " << computer.getScore() << "\n";

    }
    // next round
}
