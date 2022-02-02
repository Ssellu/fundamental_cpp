# this

- 객체가 스스로를 지칭할 때 사용
- this : 이 객체의 주솟값 (포인터)
- 객체가 '본인의 멤버를 지칭할 때' 사용



```c++
#include <iostream>
#include <string> 

using namespace std;

class Person
{
	string m_name;
	int m_age;

public:

	Person(const string& name, const int& age)
		:m_name{name}, m_age{age}
	{}

	void printInfo()
	{
		cout << "this : " << this << endl;   // 이 부분!
		cout << "name : " << m_name << endl;
		cout << "age : " << m_age << endl;
	}
};
int main() 
{
	Person p1{ "홍길동", 10 }; 
	Person p2{ "고길동", 20 };

	p1.printInfo();
	p2.printInfo();
	return 0;
}
```

> this : 00D8FDE8
> name : 홍길동
> age : 10
> this : 00D8FDC0
> name : 고길동
> age : 20
> Press any key to continue . . .





```c++
// 메인 함수를 다음으로 변경해보자.
int main() 
{
	Person* p1 = new Person{ "홍길동", 10 }; 
	Person* p2 = new Person{ "고길동", 20 };

	p1->printInfo();
	p2->printInfo();

	cout << "p1 : " << p1 << endl;
	cout << "p2 : " << p2 << endl;

	return 0;
}
```

> this : 0122B3A0
> name : 홍길동
> age : 10
> this : 0122B210
> name : 고길동
> age : 20
> p1 : 0122B3A0
> p2 : 0122B210
> Press any key to continue . . .



- 원래는 클래스의 멤버함수 내부에서 같은 멤버변수/함수를 지칭할 때 자동으로 `this->`가 추가됨.

  ```c++
  class Person
  {
  	...
          
  	void printInfo()
  	{
  		cout << "this : " << this << endl;
  		cout << "name : " << this->m_name << endl;   // m_name에 this-> 가 자동 적용 
  		cout << "age : " << this->m_age << endl;	 // m_age에 this-> 가 자동 적용
          this->xx(); 	// xx(); 에 this-> 가 자동 적용
  	}
      
      void xx() { .. }
  };
  ```

  

- 그렇다면 언제 this를 쓸까?

  - `this->`가 안붙는 유일한 경우가 있음. 매개변수나 함수의 지역변수가 멤버변수와 이름이 같을 때.

    ```c++
    class Person
    {
    	int x;
    
    public:
    
    	void set(int x)  // 이럴 때
    	{
            
    	}
        
        void test()
        {
            int x;  // 이럴 때
        }
    	
    };
    ```

    이런 상황이면 함수 내부에서 필드를 지칭해야 할 때 `this->`를 꼭 붙여야 함.

    ```c++
    // 예
    class Person
    {
    	int x = 1000;
    
    public:
    
    	void set(int x)
    	{
            cout << x << endl;
            cout << this->x << endl;
    	}
        
        void test()
        {
            int x = 10;
            cout << x << endl;
            cout << this->x << endl;
        }
    };
    ```

    