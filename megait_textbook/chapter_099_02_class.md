```c++
#include <iostream>
#include <string>

using namespace std;

struct Person 
{
	string name;
	int age;
	double height;
	string tel;
};

void printPerson(Person p) 
{
	cout << "name : " << p.name << endl;
	cout << "age : " << p.age << endl;
	cout << "height : " << p.height << endl;
}

int main() 
{
	Person dad;
    
	dad.name = "John Doe";
	dad.age = 40;
	dad.height = 179.3;

	Person mom{ "Jane Doe", 38, 170.2 };

	printPerson(dad);
	printPerson(mom);
	return 0;
}


```



```c++
#include <iostream>
#include <string>

using namespace std;

struct Person 
{
	string name;
	int age;
	double height;
	string tel;
    
    void print() 
    {
        cout << "name : " << name << endl;
        cout << "age : " << age << endl;
        cout << "height : " << height << endl;
    }
};



int main() 
{
	Person dad;
    
	dad.name = "John Doe";
	dad.age = 40;
	dad.height = 179.3;

	Person mom{ "Jane Doe", 38, 170.2 };

	dad.print();
    mom.print();
    
	return 0;
}
```

