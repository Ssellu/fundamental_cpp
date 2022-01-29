# 포인터와 const

```c++
#include <iostream>
using namespace std;

int main()
{
	int x = 10;

	const int* ptr = &x;
	
	*ptr = 100;  // 에러!

	cout << *ptr; // 10
}
```

```c++
#include <iostream>
using namespace std;

int main()
{
	int x = 10;
	int y = 20;
    
	const int* ptr = &x;  // 이 부분!
	
	ptr = &y;  // 가능

	cout << *ptr;  // 20
}
```

```c++
#include <iostream>
using namespace std;

int main()
{
	int x = 10;
	int y = 20;
    
	int* const ptr = &x;  // 이 부분!
	
	ptr = &y;  		// 에러
	*ptr = 100; 	// 가능
	cout << *ptr;  	// 10
}
```

```c++
#include <iostream>
using namespace std;

int main()
{
	int x = 10;
	int y = 20;
    
	const int* const ptr = &x;  // 이 부분!
	
	ptr = &y;		// 에러
	*ptr = 100;		// 에러
	cout << *ptr;	// 10
}
```



# nullptr



# 참조변수 (reference variable)

> #### 자료형 &변수명 = 참조할 메모리;

- 매번 `*`쓰기 귀찮아서 나옴
- 포인터변수를 쓰면 이런 코드가..

```c++
#include <iostream>
using namespace std;

int main()
{
	int foo = 5;
	int* x = &foo;
	*x = 100;
	cout << foo << endl;  // 100 
    
    return 0;
}
```

- 참조변수를 쓰면 이렇게!

```c++
#include <iostream>
using namespace std;

int main()
{
	int foo = 5;
	int& x = foo;   // 이 부분!
	x = 100;		// *을 사용하지 않아도 자동으로 찾아감
	cout << foo << endl;  // 100 
    
    return 0;
}
```

- 한꺼번에 비교해보자

```c++
#include <iostream>
using namespace std;

int main()
{
	int foo = 5;


	int* x = &foo;
	*x = 100;
	cout << foo << endl;

	int& y = foo;
	y = 200;
	cout << foo << endl;


	cout << "foo : " << foo << endl;
	cout << "&foo : " << &foo << endl;

	cout << "x : " << x << endl;
	cout << "&x : " << &x << endl;
	cout << "*x : " << x << endl;

	cout << "y : " << x << endl;   
	cout << "&y : " << x << endl;	// foo 와 같은 주소를 공유 (foo의 별명이 된다.)
    
    return 0;
}
```

> 100
> 200
> foo : 200
> **&foo : 000000D9971FF730**
> **x : 000000D9971FF730**
> &x : 000000D9971FF738
> *x : 200
> y : 200
> **&y : 000000D9971FF730**
> Press any key to continue . . .



## 참조변수 주의사항

- 선언만 하면 에러

  ```c++
  int& ref; (X)
  ```

  ```c++
  int& ref = a; (O)
  ```

- const 변수를 참조하려면 참조변수 또한 const 여야 함

  ```c++
  const int a = 10;
  int& ref = a; (X)
  ```

  ```c++
  const int a = 10;
  const int& ref = a; (O)
  ```

- 참조변수 사용 팁

  ```c++
  #include <iostream>
  using namespace std;
  
  struct Inner
  {
  	int x;
  	int y;
  };
  
  struct Outer
  {
  	Inner inner;
  };
  int main()
  {
  	Outer outer;
  
  	// 객체나 구조체 이름이 너무 길 때 
  	// 이름을 줄여서 사용 가능..
  	int &x = outer.inner.x;
  	int &y = outer.inner.y;
  
  	x = 10;
  	y = 100;
      
      return 0;
  }
  ```
  
  