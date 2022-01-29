# 1. .cpp 파일의 기본 구조

> 폰트 사이즈 : `ctrl` + `마우스휠`
>
> 주석 : `ctrl` + `K` + `C`



## ex01_helloworld1.cpp

```c++
#include <iostream>  // 헤더파일 (stdio.h 대신 iostream)

int main() // 메인함수는 C와 동일
{
	std::cout << "Hello, World!" << std::endl;  // printf() 대신
	return 0;
}
```



## ex02_helloworld2.cpp

```c++
#include <iostream>
int main()
{
	int x = 10;
	double y = 20;
	std::cout << x + y << std::endl;

	return 0;
}
```



# 2. cout과 cin

- cout : 표준 출력  (printf  대신)
- cin : 표준 입력 (scanf 대신)
- **#include &lt;cstdio&gt;** 하면 printf와 scanf 를 사용할 수 있음. (권장 X)



## ex03_cout_cin.cpp

### ex01() 
- &lt;&lt; : output operator

```c++
void ex01() {
    int x = 10;
    std::cout << "cout 테스트~" << std::endl;
	std::cout << "x는 " << x << "입니다." << std::endl;
}
```

<hr/>

### ex02 
- &gt;&gt; : input operator

```c++
void ex02() {
	int x;
	std::cin >> x;
	std::cout << "입력한 정수는 " << x << "입니다" << std::endl;
}
```

<hr/>

### ex03() 

- using namespace std; 

```c++
void ex03() {
	// 'std::'를 일일히 붙이기 싫다면
	using namespace std; 

	int x;
	cin >> x;

	cout << "입력한 정수는 " << x << "입니다" << endl;

}
```

<hr/>

### main()
```c++
int main() {
	ex01();
    ex02();
    ex03();
	return 0;
}
```


