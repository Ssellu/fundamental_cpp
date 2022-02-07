# const

- 값 변경을 불가능하게 하는 키워드.
- constant(상수)에서 따옴.



## const 변수 

```c++
const double pi = 3.14;
pi = 3.1415; // 에러. 변경 불가
```



- 주의! const 변수는 선언 시 초기화를 해야 함.  

```c++
const double pi; // 에러.
pi = 3.1415;
```



- const 멤버변수 - 클래스 안에서 선언된 const 변수

```c++
class Circle
{
public:
	const double pi = 3.14; // 이 부분!
	double radius;
};

int main()
{
	
	Circle c1; 
	c1.radius = 10;
	c1.pi = 3.1415;  // 에러 (변경 불가)

	return 0;
}
```



- const 멤버변수의 초기화

  1. 선언 및 초기화

     ```c++
     class Circle
     {
     public:
     	const double pi = 3.14;
     	double radius;
     };
     ```

  2.  초기화 리스트 활용 

     ```c++
     #include <iostream>
     using namespace std;
     
     class Circle
     {
     public:
     	const double pi;
     	double radius;
     
     	Circle(double p, double r)
     		:pi(p), radius(r)  // 이 부분!
     	{}
     
     };
     
     int main()
     {
     	
     	Circle c1{ 3.1415, 10 };
     	Circle c2{ 3.14, 20 };
     
     	cout << c1.pi << ", " << c1.radius << endl;
     	cout << c2.pi << ", " << c2.radius << endl;
     
     	return 0;
     }
     ```

     > 3.1415, 10
     >
     > 3.14, 20
     >
     > Press any key to continue . . .

     

     단, 다음은 에러. (객체가 생성된 이후에 `{}`영역이 실행되므로 이미 `pi`는 생성이 끝나있기 때문)

     ```c++
     class Circle
     {
     public:
     	const double pi;
     	double radius;
     
     	Circle(double p, double r)
     	{
     		pi = p;  // 에러!
     		radius = r;
     	}
     };
     ```

     



## const 포인터 변수 

- const가 자료형 앞에 있으면 - 참조 대입 불가능

```c++
int num = 1;
const int* ptr = &num;  // *ptr을 변경 못하게

*ptr = 2;  // 에러
num = 2;  // 가능
```



- const가 자료형 뒤에 있으면 - 포인터 변수의 값 변경 불가능

```c++
int num1 = 1;
int num2 = 2;
int* const ptr = &num1;  // ptr을 변경 못하게

ptr = &num2;  // 에러
*ptr = 2;  // 가능
```



- 따라서 참조 대입도 불가능하게 하고, 포인터 변수의 값도 변경 못하게 하려면

```c++
const int* const ptr = &num1;
```



## const 멤버 함수

- 멤버 함수에 const 를 붙인 것

  ```c++
  class A:
  {
      ...
          
      void aa() const  // <-- 이 부분
      {
          ...
      }
  }
  ```

  

- const 멤버 함수의 용도 

  1. const 변수는 값 변경 불가능. 객체 변수가 const로 선언되면 객체의 필드도 변경 불가능.

  ```c++
  #include <iostream>
  #include <string>
  
  using namespace std;
  
  class Person
  {
  public:
  	string m_name;
  	int m_age;
  
  	Person(string name, int age)
  		:m_name(name), m_age(age)
  	{}
  
  };
  int main()
  {
  	const Person p1{ "홍길동", 10 };
  	p1.m_name = "고길동";  // 에러
  	return 0; 
  }
  ```

  

  2. 이 경우 멤버 변수 대입(`=`) 뿐만 아니라 객체에 관련된 **모든 멤버함수도 호출 불가능**!!!

  ```c++
  #include <iostream>
  #include <string>
  
  using namespace std;
  
  class Person
  {
  public:
  	string m_name;
  	int m_age;
  
  	Person(string name, int age)
  		:m_name(name), m_age(age)
  	{}
  
  	void printInfo()  // 새 일반 멤버 함수 추가
  	{
  		cout << "이름 : " << m_name << endl;
  		cout << "나이 : " << m_age << endl;			
  	}
  };
  int main()
  {
  	const Person p1{ "홍길동", 10 }; 
  	p1.printInfo();  // 에러
  	return 0; 
  }
  ```

  

  3. const 객체는 **const 멤버함수만 호출**할 수 있음

  ```c++
  #include <iostream>
  #include <string>
  
  using namespace std;
  
  class Person
  {
  public:
  	string m_name;
  	int m_age;
  
  	Person(string name, int age)
  		:m_name(name), m_age(age)
  	{}
  
  	void printInfo() const // 이 부분!
  	{
  		cout << "이름 : " << m_name << endl;
  		cout << "나이 : " << m_age << endl;			
  	}
  };
  int main()
  {
  	const Person p1{ "홍길동", 10 }; 
  	p1.printInfo();  // 해결
  	return 0; 
  }
  ```

  

  4. 이때 const 멤버함수는 멤버 변수 변경이 불가능. (const 함수 내부에서 선언된 지역변수는 이와 상관없이 변경 가능.)

  ```c++
  class Person {
      
  	...
          
  	void changeAge() const
  	{
  		++m_age;  // 에러
  	}
      
      ...
  }
  ```

  

  5. 결론 : 객체가 const가 될 경우를 대비해 getter 와 같은 **읽기 전용 함수**는 const를 선언하는 것이 좋다.

