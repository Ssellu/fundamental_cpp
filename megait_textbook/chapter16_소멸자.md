# 소멸자(Destructors)

```c++
#include <iostream>
#include <string> 

using namespace std;

class Sample
{
	int m_x, m_y;

public:

	Sample(int x = 0, int y = 0)
		: m_x(x), m_y(y)
	{
		cout << "생성자!" << endl;
	}

    // 이 부분!
	~Sample() 
	{
		cout << "소멸자!" << endl;
	}

	void printInfo()
	{
		cout << "x : " << m_x << endl;
		cout << "y : " << m_y << endl;
	}

};
int main() 
{
	Sample s1(10, 20);
	Sample s2;

	s1.printInfo();
	s2.printInfo();


	return 0;
}
```

> 생성자!
>
> 생성자!
>
> x : 10
>
> y : 20
>
> x : 0
>
> y : 0
>
> 소멸자!
>
> 소멸자!
>
> Press any key to continue . . .



- 소멸자가 호출되는 경우 2가지 

  1. 프로그램이 종료 될 때의 객체 해제 시점
  2. delete 키워드 (동적할당된 객체를 해제하는 연산자. new의 반대)로 객체를 해제할 때

- 소멸자의 역할 : 해제 작업!

  특히 객체의 필드가 동적할당한 배열이나 객체일 때 메모리 누수를 방지하는 역할로 사용한다.

  ```c++
  #include <iostream>
  #include <string> 
  
  using namespace std;
  
  class Sample
  {
  	int* m_arrptr;
  
  public:
  
  	Sample(int size)
  	{
  		m_arrptr = new int[size];
  	}
  
  	~Sample() 
  	{
  		delete[] m_arrptr;
  	}
  
  };
  ```

  