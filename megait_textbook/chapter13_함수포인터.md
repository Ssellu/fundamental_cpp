# 함수 포인터

- 함수 자체도 포인터다. (함수가 위치한 곳의 주소)

```c++
#include <iostream>

using namespace std;

int doSomething(){
	return 10;
}


int main(){

	cout << doSomething() << endl;
	cout << doSomething << endl;

	return 0;
}
```

> 10
> 00007FF716D517FD
> Press any key to continue . . .



- 함수 포인터를 사용하면 그때 그때 다른 함수를 실행할 수 있다.

  > ## 선언 : 자료형(*포인터변수명)(매개변수 자료형);

```c++
#include <iostream>

using namespace std;

void aa(){
	cout << "aa() 실행!" << endl;
}

void bb() {
	cout << "bb() 실행!" << endl;
}

int main(){

	void(*p)(); 
	
	cout << "---checkpoint 0---" << endl;

	p = aa;  // 함수 aa의 위치 주소를 p에 저장 (aa() 실행되지 않는다.)

	cout << "---checkpoint 1---" << endl;

	p();  // aa() 실행

	cout << "---checkpoint 2---" << endl;

	p = bb; // 함수 bb의 위치 주소를 p에 저장 (bb() 실행되지 않는다.)

	cout << "---checkpoint 3---" << endl;

	p();  // bb() 실행

	return 0;
}
```

> ---checkpoint 0---
> ---checkpoint 1---
> aa() 실행!
> ---checkpoint 2---
> ---checkpoint 3---
> bb() 실행!
> Press any key to continue . . .



- 매개변수와 리턴값에 따른 함수포인터 선언 예

  | 함수 원형                                   | 함수 포인터 자료형                      |
  | ------------------------------------------- | --------------------------------------- |
  | **void** ??(**int** ?)                      | **void**(*x)(**int**)                   |
  | **int** ??()                                | **int**(*x)()                           |
  | **char*** ??(**double** ?, **int** ?)       | **char**&#42;(*x)(**double**, **int**)  |
  | **int** ?? (**struct A** ?, **sturct B** ?) | **int**(*x)(**struct A**, **struct B**) |

  

