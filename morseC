#include<iostream>
#include<cstring>
#include <sstream>
#include <unordered_map>
#include <fstream>
using namespace std;
struct Node
{
    char letter;//for hashing
    Node* dash;//for BST tree
    Node* dot;
    Node(char c = ' ')
    {
        letter = c;
        dot = NULL;
        dash = NULL;
    }
};
    Node* root = new Node();
unordered_map<char, string> encodeMap;
//INSERTING MORSE INTO TREE
void  insertintree(char letter, string morse)
{
    Node* ptr = root;
    for (char c : morse)
    {
        if (c == '.')
        {
            if (ptr->dot == NULL)
                ptr->dot = new Node();

            ptr = ptr->dot;
        }
        else if (c == '-')
        {
            if (ptr->dash == NULL)
                ptr->dash = new Node(); 
            ptr = ptr->dash;
        }
    }
    ptr->letter = letter;
}
void loadfile()
{
    ifstream file("morsecode.txt");
    if (!file)
    {
        cout << "Dictionary file not found\n";
        return;
    }

    char letter;
    string morse;
    while (file >> letter >> morse)
    {
        encodeMap[letter] = morse;
        insertintree(letter, morse);
    }

    file.close();
}
// TEXT → MORSE
string textToMorse(string text)
{
    string result = "";

    for (char c : text)
    {
        c = toupper(c);

        if (encodeMap.count(c))
            result += encodeMap[c] + " ";

        else if (c == ' ')
            result += "/ ";
    }

    return result;
}

char decodeLetter(string morse)
{
    Node* temp = root;

    for (char c : morse)
    {
        if (c == '.')
            temp = temp->dot;
        else
            temp = temp->dash;
    }

    return temp->letter;
}
string morseToText(string morse)
{
    stringstream ss(morse);
    string code;
    string result = "";

    while (ss >> code)
    {
        if (code == "/")
        {
            result += " ";
        }
        else
        {
            result += decodeLetter(code);
        }
    }

    return result;
}


void saveHistory(string text, string morse)
{
    ofstream file("history.txt", ios::app);

    file << "Text: " << text << endl;
    file << "Morse: " << morse << endl;
    file << "-------------------" << endl;

    file.close();
}
int main()
{
    cout << "This Code is developed by Momina_T\n";
        cout << "It conerts english language words\n";
        cout << "into morse code and morse code into english language words\n";
        cout<<"programm is cccase sensitivve(UPPER CASE) only\n";
        cout << "---------------------------------------------------------";

    loadfile();
    int loop;
    cout << "\nenter how many inputs u want to insert:\n";
    cin >> loop;
    for (int k = 0 ; k <= loop; k++)
    {
        int choice;
        cout << "1 Text to Morse\n";
        cout << "2 Morse to Text\n";
        cout << "3 Exit\n";
        cin >> choice;
        cin.ignore();
        if (choice == 1)
        {
            string text;
            cout << "Enter Text: ";
            getline(cin, text);

            string morse = textToMorse(text);

            cout << "Morse: " << morse << endl;

            saveHistory(text, morse);
        }
        else if (choice == 2)
        {
            string morse;
            cout << "Enter Morse: ";
            getline(cin, morse);

            string text = morseToText(morse);

            cout << "Text: " << text << endl;

            saveHistory(text, morse);
        }
    }
}
