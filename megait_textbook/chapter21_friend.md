# friend 키워드

- 해당 클래스의 private 및 protected 멤버에 접근권한이 있는 클래스, 전역 함수, 멤버 함수



# friend 클래스

- 어떠한 클래스의 private 멤버에 접근할 수 있는 클래스

- 다음 코드는 에러 발생.

```c++
class Person 
{
private:
	string name_;
	int age_;
};


class Pet
{
public:
	Person master_;
	string petName_;

	void printPet() const
	{
		cout << master_.name_ << endl;  // 에러
		cout << petName_ << endl;
	}
};
```



- 하지만 Pet을 Person의 friend 클래스로 선언하면 해결됨.

```c++
// 클래스 선언 (안하면 Person 클래스가 Pet 함수를 인식 못함. Why? Pet 정의가 Person 정의 밑에 있어서..)
// 이를 '전방 선언'이라고 한다.
class Pet;

class Person 
{
private:
	string name_;
	int age_;

	friend class Pet;
};


class Pet
{
public:
	Person& master_;
	string petName_;

	void printPet() const
	{
		cout << master_.name_ << endl;  // 됨!
		cout << petName_ << endl;
	}
};
```



# friend 전역 함수 

- 알다시피 private 멤버는 클래스 외부에서 접근할 수 없음.

```c++
class Person 
{
private:
	string name_;
	int age_;
};


void printPerson(const Person& person)
{
	cout << person.name_ << endl; // 에러
	cout << person.age_ << endl;  // 에러
}
```



- 하지만 Person 클래스 내부에 해당 함수를 friend 로 선언하면 private 멤버에 접근할 수 있음.

```c++
// 함수 선언 
void printPerson(const Person& person);  

class Person 
{
private:
	string name_;
	int age_;

	friend void printPerson(const Person& person);
};


void printPerson(const Person& person)
{
	cout << person.name_ << endl;  // 됨!
	cout << person.age_ << endl;  // 됨!
}
```





# friend 멤버함수

- 클래스 전체를 friend로 지정하는 대신 일부 메서드만 friend로 지정하고 싶을 때
- 주의! 서로가 서로를 참고하고 있기 때문에 전방 선언이 필수이며, 멤버함수 정의와 선언을 분리해야 한다.

```c++
#include <iostream>
#include <string> 
using namespace std;

class Person;

class Pet
{
public:
	Person& master_;
	string petName_;

	void printPet() const;
};

class Person
{
private:
	string name_;
	int age_;

	friend void Pet::printPet() const;

public:
	Person(string name, int age)
		:name_(name), age_(age)
	{}

};

void Pet::printPet() const
{
	cout << master_.name_ << endl;  // 에러
	cout << petName_ << endl;
}

int main()
{
	Person person{ "홍길동", 20 };
	Pet pet{ person, "뽀삐" };

	pet.printPet();

	return 0;
}
```

