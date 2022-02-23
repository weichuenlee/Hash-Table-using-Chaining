#include <iostream>
#include <chrono>
#include <vector>
#include <list>
#include <fstream>

using namespace std;

template <typename T>
class hashtable
{
    vector< list<string> > table;

    int hashfunction (string hashitem)
    {
        long sum = 0, mul = 1;
        for (int i = 0; i < hashitem.length(); i++)
        {
            mul = (i % 4 == 0) ? 1 : mul * 256;
            sum += hashitem[i] * mul;
        }
        return (int)(abs(sum) % table.size());
    }

public:
    hashtable (int size)
    {
        table.resize (size);
    }

    int size()
    {
        return table.size();
    }

    void insert (string newItem)
    {
        int position = hashfunction(newItem);
         [position].push_front(newItem);
    }

    bool retrieve (string target)
    {
        int position = hashfunction(target);

        bool found = false;
        list <string> searchlist = table[position];
        for (auto i = searchlist.begin(); i != searchlist.end(); ++i)
        {
            if (*i == target)
            {
                found = true;
                break;
            }
        }
        return found;
    }

};




void searchHashTable(string filename, hashtable<int> ht)
{
    string email;
    ifstream read(filename);

    while(getline (read, email))
    {
        if (ht.retrieve(email))
        {
            cout << email << ": FOUND\n";
        }
        else
        {
            cout << email << ": NOT FOUND\n";
        }
    }
}

void createHashTable(int width, string filename)
{
    auto beginning = chrono::system_clock::now();

    hashtable<int> ht(width);

    string value;
    ifstream readfile(filename);

    while (getline (readfile, value))
    {
        ht.insert(value);
    }

    auto ending = chrono::system_clock::now();
    chrono::duration<double> length = ending - beginning;

    cout << "Insertion time: " << length.count() << "s\n\n";

    cout << "Search for 10 emails that could be found...\n";
    beginning = chrono::system_clock::now();
    searchHashTable("Found.txt", ht);
    ending = chrono::system_clock::now();
    length = ending - beginning;
    cout << "Search time: " << length.count() << "s\n\n";

    cout << "Search for 10 emails that could not be found...\n";
    beginning = chrono::system_clock::now();
    searchHashTable("NotFound.txt", ht);
    ending = chrono::system_clock::now();
    length = ending - beginning;
    cout << "Search time: " << length.count() << "s\n\n";
}



int main()
{
    cout << "Choose data set:\n";
    cout << "1. Set A (100 emails)\n";
    cout << "2. Set B (1,000,000 emails)\n";
    cout << "3. Set C (5,000,000 emails)\n";
    cout << "4. Exit program.\n";

    int i;

    while (true)
    {
        cout << "Choice: ";
        cin >> i;

        cout << "\n\n\n";
        switch (i)
        {
        case 1:
            cout << "Inserting 100 emails into hash table...\n";
            createHashTable(90, "SetA.txt");
            cout << "\n\n";
            break;
        case 2:
            cout << "Inserting 1,000,000 emails into hash table...\n";
            createHashTable(900000, "SetB.txt");
            cout << "\n\n";
            break;
        case 3:
            cout << "Inserting 5,000,000 emails into hash table...\n";
            createHashTable(4500000, "SetC.txt");
            cout << "\n\n";
            break;

        case 4:
            exit(1);
            break;
        default:
            cout << "Wrong input.\n\n";
            break;
        }
    }
}
