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



