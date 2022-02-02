# 클래스와 객체 

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person 
{
public:
	string name;  	// 멤버변수(=필드)
	int age;		// 멤버변수(=필드)

	void printInfo() // 멤버함수(=메서드)
	{
		cout << "name : " << name << endl;
		cout << "age : " << age << endl;
	}
};
int main(){

	Person p1{ "John Doe", 20 };

	// Person p1;
	// p1.name = "John Doe";
	// p1.age = 20;

	Person p2{ "Jane Doe", 32 };
	
	p1.printInfo();
	p2.printInfo();

	return 0;
}
```

> name : John Doe
> age : 20
> name : Jane Doe
> age : 32
> Press any key to continue . . .



# 접근지정자(Access Modifiers)

- private : 클래스 내부에서만 사용 가능 (디폴트)
- public : 모두가 사용 가능 
- protected : 클래스 내부에 자식 클래스에서만 사용 가능

- 변수는 private, 함수는 public  --> 캡슐화(encapsulation)



# 캡슐화와 은닉화 

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person 
{
    // public:  , protected
	string name_; 
	int age_;		

public:
	void printInfo()
	{
		cout << "name : " << name_ << endl;
		cout << "age : " << age_ << endl;
	}

	void setName(string name) 
	{
		name_ = name;
	}

	void setAge(int age)
	{
		if (age > 0)
			age_ = age;
	}
};
int main(){

	// Person p1{ "John Doe", 20 };
	// Person p2{ "Jane Doe", 32 };
	
	Person p1;
	Person p2;

	p1.setName("John Doe"); 
	p1.setAge(20);

	p2.setName("Jane Doe");
	p2.setAge(32);

	p1.printInfo();
	p2.printInfo();

	cout << "p1 나이에 음수 넣어보기" << endl;

	p1.setAge(-100);
	p1.printInfo();

	return 0;
}
```



## 반대로 getter는..

```c++
int getAge()
{
    return age_;
}

string getName()
{
    return name_;
}
```



## 좀 더 발전한 getter

```c++
const int& getAge()
{
    return age_;
}

const string& getName()
{
    return name_;
}
```



이러한 setter, getter 들을 **접근 함수**라고 한다.

