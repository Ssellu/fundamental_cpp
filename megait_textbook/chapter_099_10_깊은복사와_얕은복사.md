# 깊은 복사(deep copy)와 얕은 복사(shallow copy)

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person 
{
public:
	string name; 
	int age;		

	void printInfo()
	{
		cout << "name : " << name_ << endl;
		cout << "age : " << age_ << endl;
	}

};
int main(){

	Person p1 {"홍길동", 10};
	Person p2;

	// 얕은 복사
	p2 = p1;

	p1.printInfo();
	p2.printInfo();

	return 0;
}
```

> name : 홍길동
>
> age : 10
>
> name : 홍길동
>
> age : 10
>
> Press any key to continue . . .

