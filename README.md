# 6-02

```C++

#include <iostream>
#include <vector>
#include <map>

using namespace std;

void BackTrack(int index, vector<string> path, string digits, map<string, vector<string>> letters, vector<string>& combinations)
{
    if (path.size() == digits.size())
    {
        string s = "";
        for (auto& element : path)
        {
            s += element;
        }
        combinations.push_back(s);
        return;
    }

    string ind = digits.substr(index, 1);
    vector<string> possibleLetters;

    for (int i = 0; i < letters[ind].size(); i++)
    {
        possibleLetters.push_back(letters[ind][i]);
    }

    if (possibleLetters.size() > 0)
    {
        for (int letter = 0; letter < possibleLetters.size(); letter++)
        {
            path.push_back(possibleLetters[letter]);
            BackTrack(index + 1, path, digits, letters, combinations);
            path.pop_back();
        }
    }
}

vector<string> LetterCombinations(string digits)
{
    vector<string> combinations = {};

    if (digits.size() == 0)
    {
        return {};
    }

    map<string, vector<string>> digitsMapping;
    digitsMapping.insert({ "0", {"+", " "}});
    digitsMapping.insert({ "1", {"@"}});
    digitsMapping.insert({ "2", {"a", "b", "c"} });
    digitsMapping.insert({ "3", {"d", "e", "f"} });
    digitsMapping.insert({ "4", {"g", "h", "i"} });
    digitsMapping.insert({ "5", {"j", "k", "l"} });
    digitsMapping.insert({ "6", {"m", "n", "o"} });
    digitsMapping.insert({ "7", {"p", "q", "r", "s"} });
    digitsMapping.insert({ "8", {"t", "u", "v"} });
    digitsMapping.insert({ "9", {"w", "x", "y", "z"} });

    BackTrack(0, {}, digits, digitsMapping, combinations);
    return combinations;
}

int main()
{
    vector<string> digitsArray = { "20", "120", "720"};
    int counter = 1;

    for (const auto& digits : digitsArray)
    {
        cout << counter << ". \t All letter combinations for '" << digits << "': [";
        auto combinations = LetterCombinations(digits);

        for (size_t i = 0; i < combinations.size(); ++i)
        {
            cout << "\"" << combinations[i] << "\"";
            if (i < combinations.size() - 1)
                cout << ", ";
        }
        cout << "]" << endl;
        counter++;
        cout << string(100, '-') << endl;
    }
}

```
