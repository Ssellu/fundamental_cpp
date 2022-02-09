# 필드 기본값

- 객체의 필드에 기본값을 부여하는 방법

  - 방법1. 선언할 때 같이 

    ```c++
    class Person
    {
    	string m_name{"없음"}; 		  // 이 부분!
    	int m_age = 0;					// 이 부분!
    	int m_scores[3] = { 0, 0, 0 };	// 이 부분!
        ...
    ```

  - 방법2. 생성자

  - 방법3. 생성자 초기화 리스트



# 생성자(Constructors)

- 객체 생성 시 초기화를 담당하는 함수
- 함수의 이름이 클래스의 이름과 동일함.
- 리턴자료형 없음. (void 없음!!!!)
- 일반 함수처럼 아무때나 호출할 수는 없다.
- 우리가 생성자를 정의하지 않으면 기본생성자가 내부에서 자동으로 정의된다. 

> ## 클래스명() {...}
>
> ## 클래스명(매개변수 선언) {...}

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
	string name_;
	int age_;

public:

    // 이 부분!
	Person() {
        cout << "Person 생성자 호출!! " << endl;
		name_ = "없음"; 
		age_ = 0;
	}

	void printInfo()
	{
		cout << "name : " << name_ << endl;
		cout << "age : " << age_ << endl;
	}

};
int main() 
{
	Person p1;

	p1.printInfo();

	return 0;
}
```

> Person 생성자 호출!!
> name : 없음
> age : 0
> Press any key to continue . . .


단, 이때 밑의 코드는 에러 발생.

```c++
Person p1{ "Jane Doe", 20 };
```

매개변수가 없는 생성자를 **기본생성자(명시적 생성자)**라고 함.

기본생성자를 정의하면, 딱 기본생성자만 만들어짐.

해결 방법 : 다른 형태의 생성자도 정의한다. 

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
	string name_ = "";
	int age_ = 0;

public:

	Person(string name = "", int age = 0) {
		cout << "Person 생성자 호출!! " << endl;
		name_ = name; 
		age_ = age;
	}

	void printInfo()
	{
		cout << "name : " << name_ << endl;
		cout << "age : " << age_ << endl;
	}

};
int main() 
{
	Person p1{ "Jane Doe", 20 };
	Person p2{ "John Doe" };
	Person p3;

	p1.printInfo();
	p2.printInfo();
	p3.printInfo();


	return 0;
}
```

> Person 생성자 호출!!
>
> Person 생성자 호출!!
>
> Person 생성자 호출!!
>
> name : Jane Doe
>
> age : 20
>
> name : John Doe
>
> age : 0
>
> name :
>
> age : 0
>
> Press any key to continue . . .



## 좀 더 나은 방법 (const 참조변수 사용)

```c++
Person(const string& name = "", const int& age = 0) {
    cout << "Person 생성자 호출!! " << endl;
    name_ = name; 
    age_ = age;
}
```









# 생성자가 없으면..?

1. 객체를 만들 때 들어있는 쓰레기값을 클래스 사용자(다른 개발자)가 직접 처리해야 함. 

   불편한 것도 있지만, 이 객체에 어떤 필드가 있는 지 모른다면? 무엇을 넣어야 할 지 모를 것임.

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
   		cout << "name : " << name << endl;
   		cout << "age : " << age << endl;
   	}
   
   };
   int main() 
   {
   
   	Person p1{ "John Doe", 20 };
   	Person p2;
   
   
   	p1.printInfo();
   	p2.printInfo();
   
   
   	return 0;
   }
   ```

   > name : John Doe
   >
   > age : 20
   >
   > name :
   >
   > age : -858993460
   >
   > Press any key to continue . . .

   ```c++
   // 이럴땐 이렇게 해도 됨.
   class Person
   {
   
   public:
   
   	string name = "";   // 기본값을 '빈 문자열'로 지정
   	int age = 0;		// 기본값을 0으로 지정
   	
   
   	void printInfo()
   	{
   		cout << "name : " << name << endl;
   		cout << "age : " << age << endl;
   	}
   
   };
   ```

   

2. 값을 일일히 넣기가 불편하고 번거롭다.

   ```c++
   Person p2;
   p2.name = "Jane Doe";
   p2.age = 10;
   // ... name, age 말고도 지정해야 할 값이 많다면? --> 한 줄 한 줄 쓰기 번거로움.
   // 여기에 캡슐화까지 구현되어있다면 더 불편해진다.
   ```




# 생성자 초기화 리스트

- 객체의 기본값을 부여하는 또 다른 방법

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
	string m_name;
	int m_age;
	int m_scores[3];

public:

	Person()
        : m_name{"X"}, m_age{-1}, m_scores{100, 100, 100}  // 이 부분!
	{
		cout << "Person 생성자 호출!! " << endl;
	}

	void printInfo()
	{
		cout << "name : "	<< m_name << endl;
		cout << "age : "	<< m_age << endl;
		cout << "Korean : " << m_scores[0] << endl;
		cout << "English : " << m_scores[1] << endl;
		cout << "Math : "	<< m_scores[2] << endl;
	}

};
int main() 
{
	Person p1;
	Person p2;

	p1.printInfo();
	p2.printInfo();


	return 0;
}
```

> Person 생성자 호출!!
>
> Person 생성자 호출!!
>
> name : X
>
> age : -1
>
> Korean : 100
>
> English : 100
>
> Math : 100
>
> name : X
>
> age : -1
>
> Korean : 100
>
> English : 100
>
> Math : 100
>
> Press any key to continue . . .





# 무엇이 더 우선순위가 높을까

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
    // 3등
	string m_name{"없음"};  
	int m_age = 0;
	int m_scores[3] = { 0, 0, 0 };

public:

	Person(string name = "", int age = 0)  // 1등
		: m_name{"X"}, m_age{-1}, m_scores{100, 100, 100} // 2등
	{
		cout << "Person 생성자 호출!! " << endl;
		m_name = name;
		m_age = age;
	}

	void printInfo()
	{
		cout << "name : "	<< m_name << endl;
		cout << "age : "	<< m_age << endl;
		cout << "Korean : " << m_scores[0] << endl;
		cout << "English : " << m_scores[1] << endl;
		cout << "Math : "	<< m_scores[2] << endl;
	}

};
int main() 
{
	Person p1;
	Person p2;

	p1.printInfo();
	p2.printInfo();


	return 0;
}
```



# 위임생성자

- 생성자 내부에서 다른 생성자를 호출

  ```c++
  #include <iostream>
  #include <string>
  using namespace std;
  
  class Person
  {
  private:
  	string m_name;
  	int m_age;
  
  public:
  	Person(string name, int age)
  		: m_name(name), m_age(age)
  	{}
  
  	Person(string name)
  		:Person(name, 0)  // 위임생성자 호출
  	{}
  
  	Person(int age)
  		:Person("", age)  // 위임생성자 호출
  	{}
  
  	void printInfo()
  	{
  		cout << "이름 : " << m_name << endl;
  		cout << "나이 : " << m_age << endl;
  	}
  };
  
  int main()
  {
  	Person people[] = {
  		Person{ "홍길동" }  // 이름만
  		,Person{ 20 }  // 나이만
  		,Person{ "고길동", 10 }  // 이름과 나이만
  	};
  
  	for (auto& person : people)
  	{
  		person.printInfo();
  	}
  
  	return 0;
  }
  ```

  > 이름 : 홍길동
  >
  > 나이 : 0
  >
  > 이름 :
  >
  > 나이 : 20
  >
  > 이름 : 고길동
  >
  > 나이 : 10
  >
  > Press any key to continue . . .



# 깊은 복사(deep copy)와 얕은 복사(shallow copy)

- 얕은 복사 : 주소만 복사
- 깊은 복사 : 객체의 멤버변수까지 모두 복사

## 얕은 복사의 예

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
public:
	string name;
	int age;
	//Person() {}
	Person(string n, int a) :name(n), age(a)
	{
	}
	Person(const Person& origin)
	{
		cout << "복사 생성자 실행!" << endl;
		name = origin.name;
		age = origin.age;
	}

	void printInfo()
	{
		cout << "name : " << name << endl;
		cout << "age : " << age << endl;
	}

};
int main() {
	
	Person p1{"김길동", 10};

	Person* p2 = &p1;  // 얕은 복사

	p2->name = "홍길동";
	p2->age = 20;

	cout << "p2에 p1 얕은 복사 후" << endl;

	p1.printInfo();  // 홍길동 20
	p2->printInfo(); // 홍길동 20

	Person& p3 = p1;  // 얕은 복사

	p3.name = "최길동";
	p3.age = 30;

	cout << "p3에 p1 얕은 복사 후" << endl;

	p1.printInfo();  // 최길동 30
	p2->printInfo(); // 최길동 30
	p3.printInfo();  // 최길동 30


	return 0;
}
```

> p2에 p1 얕은 복사 후
>
> name : 홍길동
>
> age : 20
>
> name : 홍길동
>
> age : 20
>
> p3에 p1 얕은 복사 후
>
> name : 최길동
>
> age : 30
>
> name : 최길동
>
> age : 30
>
> name : 최길동
>
> age : 30
>
> Press any key to continue . . .



특히, new 로 생성되는 객체는 포인터로 접근되기 때문에 얕은 복사에 유의해야 한다.

```c++
int main() {
	
	Person* p1 = new Person{ "홍길동", 10 };
	Person* p2 = p1;

	p2->name = "김길동"; 

	p1->printInfo();
	p2->printInfo();

	return 0;
}
```

> name : 김길동
>
> age : 10
>
> name : 김길동
>
> age : 10
>
> Press any key to continue . . .



## 깊은 복사의 예

- 새 객체를 만들어 원본 객체의 '내용'을 복사한다.

```c++
int main() {
	
	Person* p1 = new Person{ "홍길동", 10 };
	Person* p2 = new Person; // 새 객체를 만든 후..

	p2->name = p1->name; // 내용 복사
	p2->age = p1->age;   // 내용 복사

	p2->name = "김길동"; // p2의 name을 변경해도

	p1->printInfo();  // 홍길동 10  ~> 원본 객체에는 영향을 주지 않는다. 
	p2->printInfo();  // 김길동 10

	return 0;
}
```



# 복사생성자

그렇다면 다음은 어떻게 동작할까?

```c++
int main(){
    Person p1{ "홍길동", 10 };
    Person p2{ p1 }; // 이렇게 하거나
    Person p3 = p1; // 이렇게 하는 경우?
}
```

이런 경우 c++ 에서는 '깊은 복사'가 실행된다. 

깊은 복사를 실행하기 위해 모든 클래스는 다음과 같은 **복사 생성자**가 자동으로 정의된다.

```c++
// 복사 생성자 형식
클래스명(const 클래스명& origin)
{
    멤버변수1 = origin.멤버변수1;
    멤버변수2 = origin.멤버변수2;
    멤버변수3 = origin.멤버변수3;
    ...
}
```

이러한 경우에도 복사 생성자가 자동으로 호출된다.

```c++
void showOlder(Person per1, Person per2)
{
    ....
}
```

```c++
showOlder(p1, p2); // p1은 매개변수 per1에, p2는 매개변수 per2에. 각 인자값에 대한 깊은 복사가 진행되도록 복사생성자가 호출된다.
```

그래서 매개변수 자료형을 일반타입이 아닌 const 참조타입으로 선언 하는 것이다!

```c++
// 올바른 객체 참조 
void showOlder(const Person& per1, const Person& per2) // 이러면 깊은 복사가 아닌 얕은 복사가 진행된다.
{
    ....
}
```



## 복사생성자 예제

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
public:
	string name;
	int age;

	// 복사 생성자
	Person(const Person& origin)
	{
		cout << "복사 생성자 실행!" << endl;
		name = origin.name;
		age = origin.age;
	}
	
    // 주의! 복사생성자도 생성자이므로, 복사생성자를 정의하면 기본 생성자는 정의되지 않는다. 
    // (생성자를 1개라도 정의해버리면 기본 생성자는 만들어지지 않는다는 것을 잊지말자.)
	//  Person p{"XXX", 00} <- 이거 하고 싶다면 생성자를 추가로 정의해야한다.
	Person(string n="", int a=0) 
		:name(n), age(a)
	{}
    
	void printInfo()
	{
		cout << "name : " << name << endl;
		cout << "age : " << age << endl;
	}

};
int main() {
	
	Person p1{ "홍길동", 10 };
	Person p2{ p1 };  // p2의 복사 생성자 실행 

	cout << "!!!!!!!!!!!!!!!" << endl;

	p1.printInfo();
	p2.printInfo();

	return 0;
}
```

> [결과]
>
> 복사 생성자 실행!
>
> !!!!!!!!!!!!!!!
>
> name : 홍길동
>
> age : 10
>
> name : 홍길동
>
> age : 10
>
> Press any key to continue . . .



