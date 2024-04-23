#include <iostream>
#include <cmath>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;
/* This code is inspired by my cats Cypher, Patches, Geralt, Jericho, and Marble. Within this code they are racers on a circuit, the output displays their speed as well as how they place (1st, 2nd, 3rd, 4th, and 5th). Their speed is randomized, but the speeds they reach are influenced by constraints inspired by them in real life. Run the code and see how they fair! Who will win the Kitten Cup? Place your bets. */

//setting up our struct for later so we can keep their identity paired with their speed
struct Race {
    std::string name;
    int speed;
};

/* we create our racers names and integer values to store their randomized speeds. You can see they get nerfs or boosts based on real life characteristics */

int main() {
    srand(time(0));

    string cyp = "Cypher";
    string pat = "Patches";
    string ger = "Geralt";
    string jeri = "Jericho";
    string marb = "Marble";

    int speedCyp = rand() % 101 - 5; //Cypher is a cautious cat
    int speedPat = rand() % 101 + 10; //Pat is a silly tiny one who is quiet graceful, but ultimately his prowess is in the vertical space
    int speedGer = rand() % 101 - 10; //Geralt is a tank and thus moves slower because of gravity
    int speedJeri = rand() % 101 + 15; //Jericho is a rocket, the girl zooms like no other
    int speedMarb = rand() % 101 - 10; //Marble is a older lady, she prefers lower speeds

/*Within these three chunks of "if's" I set up circumstancial relationships between the cats speeds. The first chunk has special events happen if certain cats random speed is below 5, the second assigns the cats 13 if their random speed/the first "if chunk" makes their speed go negative, the third gives certain cats boosts if other cats meet certain requirements*/
    
    if (speedCyp < 5) {
            speedCyp = speedCyp + ((speedPat % 3) + ((speedJeri * 2) /3));
        } if (speedPat < 5) {
            speedPat = speedPat + (speedGer - speedMarb);
            } if (speedGer < 5) {
                speedGer = speedGer + ((speedCyp * 1) /2) + 1;
            } else if (speedJeri < 5) {
            speedJeri = speedJeri + ((speedPat * 4) % 3) - 1;
        } else (speedMarb < 5); {
            speedMarb = speedMarb + ((speedJeri - 20) - (speedGer % 2));
    }

    if (speedCyp < 1) {
            speedCyp = 13;
        } if (speedPat < 1) {
            speedPat = 13;
            } if (speedGer < 1) {
                speedGer = 13;
            } else if (speedJeri < 1) {
            speedJeri = 13;
        } else (speedMarb < 1); {
            speedMarb = 13;
    }
    
    if (speedCyp > 60 || speedCyp < 30) {
        speedPat = speedPat - (speedPat % 3);
    }
    if (speedPat > 90 || speedPat < 20) {
        speedPat = speedPat + 5;
        speedJeri = speedJeri + ((speedJeri % 6) + ((speedMarb / 2) - 4));
    }
    if (speedGer > 40 || speedGer < 15) {
        speedCyp = speedCyp + 15;
        speedPat = speedPat + 2;
        speedJeri = speedJeri + 3;
    }
    if (speedJeri > 80) {
        speedMarb = speedMarb + (((speedPat * 3) + (speedCyp * 3)) /3);
        speedJeri = speedJeri + 10;
    }
    if (speedMarb < 15) {
        speedMarb = speedMarb + ((speedPat / 2) + (speedJeri % 3));
        speedGer = speedGer + 15;
    }

/* Tying the string names to their speeds after the speeds have been altered a random amount of times */
    
    Race info[] = {
        {"Cypher", speedCyp},
        {"Patches", speedPat},
        {"Geralt", speedGer},
        {"Jericho", speedJeri},
        {"Marble", speedMarb}
    };

/* infoSize is how many identities we have, in this case we have 5 to keep track of and sort through when we are outputting them. Basically within this code we associate strings with the speeds based on how they were orginally entered. So since Cypher was at the top of the strings list and speedCyp was at the top of the integer list, they are associated and when we increment down the struct the next pair is read into memory and eventually outputted as directed by the cout statements at the bottom */

    size_t infoSize = sizeof(info) / sizeof(info[0]);

    int i, j;
    for(i = 0; i < infoSize; i++) {
        for(j = i + 1; j < infoSize; j++) {
            if(info[i].speed > info[j].speed) {
                Race tmp = info[i];
                info[i] = info[j];
                info[j] = tmp;
            }
        }
    }
    cout << "The results are in for the first lap ladies and gentlemen!" << endl;
    for(i = 0; i < infoSize; i++) {
        std::cout << info[i].name << " " << info[i].speed << "\n";
    }

	


    cout << "In first place we have " << info[4].name << "! Blazing past the finish line at a whopping " << info[4].speed << " miles per hour!" << endl;

    cout << "In second place, which is no small feat, put your hands together for " << info[3].name << "! " << info[3].speed << " secured them a comfortable position in second place" << endl;

    cout << "Sitting in third place " << info[2].name << " is celebrating a underdogs victory! Coming in at " << info[2].speed << " they deserve to pop a champagne bottle!" << endl;

    cout << "In fourth place, inching past the competition by the skin of his teeth, ladies and gentlemen " << info[1].name << "! It was a close call, but" << info[1].speed << " was enough horsepower to secure fourth place!" << endl;

    cout << "And last but not least, in fifth place, our resident slow poke this evening let's give a round of applause to " << info[0].name << " coming in at a snails pace of " << info[0].speed << "! Better luck next time!" << endl;
    

    return 0;
}