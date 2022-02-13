# 상속과 생성자

자식 타입의 객체 생성시, 부모 타입의 객체를 먼저 생성한 후 자식의 고유 멤버를 생성한다. 

```c++
#include <iostream>
#include <string> 
using namespace std;
class A 
{
public:
	A() { cout << "A의 생성자 실행" << endl; }
	~A()  { cout << "A의 소멸자 실행" << endl; }
};

class B : public A  // B는 A를 상속 받고..
{
public:
	B() { cout << "B의 생성자 실행" << endl; }
	~B() { cout << "B의 소멸자 실행" << endl; }
};
class C : public B  // C는 B를 상속 받았다.
{
public:
	C() { cout << "C의 생성자 실행" << endl; }
	~C() { cout << "C의 소멸자 실행" << endl; }
};

int main()
{
	// A, B, C 타입 객체를 생성해보고 생성자와 소멸자가 어떤 순서로 호출되는 지 확인해보자.
	// A a;
	// B b;
	C c; 
	cout << "---- check point ----" << endl;

	return 0;
}
```

> A의 생성자 실행
>
> B의 생성자 실행
>
> C의 생성자 실행
>
> ---- check point ----
>
> C의 소멸자 실행
>
> B의 소멸자 실행
>
> A의 소멸자 실행
>
> Press any key to continue . . .



# 자식 클래스의 객체 생성 순서

부모 클래스에 기본생성자(매개변수가 없는 생성자)가 없을 경우, 

자식 클래스에서는 반드시 생성자를 수동으로 정의해야 한다.



## 생성자 복습..

```c++
class Person 
{
public:
	string name_;
	int age_;

	Person(string name, int age) 
		:name_(name), age_(age)
	{
		cout << "Person 생성 완료!" << endl;
	}
};
```



```c++
int main()
{
	Person p1;  // 에러
	Person p2{ "홍길동", 10 };  // 이름, 나이 값을 모두 넣어주어야 함.
	return 0;
}
```



## 상속 관계의 경우..

```c++
#include <iostream>
#include <string> 
using namespace std;
class Person
{
public:
	string name_;
	int age_;

	Person(string name, int age)
		:name_(name), age_(age)
	{
		cout << "Person 생성 완료!" << endl;
	}
};

class Student : public Person
{
public:
	int score_;
};
int main()
{
	Student s;  // 에러!

	return 0;
}
```



## 왜?

자식 타입의 생성자는 다음과 같은 순서로 초기화를 진행함. 

```c++
#include <iostream>
#include <string> 
using namespace std;
class Parent
{

public:
	Parent() // (4) 
		: // (5) 부모의 생성자 초기화 리스트가 있다면 이를 실행
	{
		// (6)
	}
};

class Child : public Parent
{
public:
	Child() // (2) 
		:Parent() // (3) 이 부분! 자식의 생성자 초기화 리스트 시점에 부모 생성자가 호출됨
	{
		// (7)
	}
};

int main() {

	Child c; // (1) 자식 객체 생성

	return 0;
}
```



## 결론

따라서 최소한 이렇게 코드를 수정해야 함

1. 부모 클래스를 수정할 수 없는 경우

```c++
#include <iostream>
#include <string> 
using namespace std;
class Person
{
public:
	string name_;
	int age_;

	Person(string name, int age)
		:name_(name), age_(age)
	{
		cout << "Person 생성 완료!" << endl;
	}
};

class Student : public Person
{
public:
	int score_;

	// 부모의 생성자에 맞춰 자식 생성자 초기화 리스트에 다음과 같이 값을 넣어주어야 함.
	Student()
		:Person("없음", 0)
	{}
};
int main()
{
	Student s;  // 됨

	return 0;
}
```



2. 부모 클래스를 수정할 수 있는 경우 

```c++
#include <iostream>
#include <string> 
using namespace std;
class Person
{
public:
	string name_;
	int age_;

	Person(string name = "없음", int age = 0)  // 생성자 매개변수에 기본값 지정
		:name_(name), age_(age)
	{
		cout << "Person 생성 완료!" << endl;
	}
};

class Student : public Person
{
public:
	int score_;
};
int main()
{
	Student s;  // 됨

	return 0;
}
```





