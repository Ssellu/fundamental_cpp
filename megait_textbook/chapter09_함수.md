# call by value

```c++
#include <iostream>

using namespace std;

void swap(int a, int b) {
	int c = a;
	a = b;
	b = c;
}

int main() {
	int x = 10;
	int y = 20;

	cout << "변환 전 x : " << x << endl;
	cout << "변환 전 y : " << y << endl;
	
	swap(x, y);

	cout << "변환 후 x : " << x << endl;
	cout << "변환 후 y : " << y << endl;

    return 0;
}
```

> 변환 전 x : 10
> 변환 전 y : 20
> 변환 후 x : 10
> 변환 후 y : 20
> Press any key to continue . . .





# call by address 

```c++
#include <iostream>

using namespace std;

void swap(int *a, int *b) {
	int c = *a;
	*a = *b;
	*b = c;
}

int main() {
	int x = 10;
	int y = 20;

	cout << "변환 전 x : " << x << endl;
	cout << "변환 전 y : " << y << endl;
	
	swap(&x, &y);

	cout << "변환 후 x : " << x << endl;
	cout << "변환 후 y : " << y << endl;
    
    return 0;
}
```

> 변환 전 x : 10
> 변환 전 y : 20
> 변환 후 x : 20
> 변환 후 y : 10
> Press any key to continue . . .



# call by reference

```c++
#include <iostream>

using namespace std;

void swap(int &a, int &b) {
	int c = a;
	a = b;
	b = c;
}

int main() {
	int x = 10;
	int y = 20;

	cout << "변환 전 x : " << x << endl;
	cout << "변환 전 y : " << y << endl;
	
	swap(x, y);

	cout << "변환 후 x : " << x << endl;
	cout << "변환 후 y : " << y << endl;
    
    return 0;
}
```

> 변환 전 x : 10
> 변환 전 y : 20
> 변환 후 x : 20
> 변환 후 y : 10
> Press any key to continue . . .





# return by value

- 리턴값이 값

```c++
#include <iostream>
#include <cmath>

using namespace std;

double GetCircleArea(int radius)
{
	double result = std::pow(radius, 2) * 3.14;
	return result;
}

int main() 
{
	double res;

	res = GetCircleArea(5);

	cout << res << endl;
	return 0;
}
```

> 78.5
> Press any key to continue . . .



# return by address

- 리턴값이 주소

```c++
#include <iostream>
#include <cmath>

using namespace std;

double* GetCircleArea(int radius)
{
	double result = std::pow(radius, 2) * 3.14;
	return &result;
}

int main() 
{
	double res;

	res = *GetCircleArea(5);

	cout << res << endl;
	return 0;
}
```

> 78.5
> Press any key to continue . . .



# return by reference

- 리턴값이 참조

```c++
#include <iostream>
#include <cmath>

using namespace std;

double& GetCircleArea(int radius)
{
	double result = std::pow(radius, 2) * 3.14;
	return result;
}

int main() 
{
	double res;

	res = GetCircleArea(5);

	cout << res << endl;


	double* res2;

	res2 = &GetCircleArea(5);

	cout << *res2 << endl;

	return 0;
}
```

> 78.5
> 78.5
> Press any key to continue . . .



# 여러 개의 값을 한꺼번에 반환하기

## 방법1. 구조체를 반환하기 (C 스타일)

- 단점 : 매번 새로운 함수를 정의할 때마다 그에 맞는 구조체도 정의해야 함. 

```c++
#include <iostream>

using namespace std;

struct MyStruct {
	int res1, res2, res3;
};

MyStruct GetResults() {
	MyStruct my{ 10, 20, 30 };
	return my;
}

int main() 
{
	MyStruct m = GetResults();
	cout << m.res1 << endl;
	cout << m.res2 << endl;
	cout << m.res3 << endl;
	return 0;
}
```

> 10
> 20
> 30
> Press any key to continue . . .



## 방법2. 튜플을 반환하기 (C++ 스타일)

- `<tuple>`의 **std::tuple** 사용

```c++
#include <iostream>
#include <tuple>  // std::tuple, std::make_tuple(), std::get()

using namespace std;

tuple<int, int, int> GetResults() {
	tuple<int, int, int> tu{ 10, 20, 30 };
	return tu;
}

int main() 
{
	tuple<int, int, int> t = GetResults();
	cout << std::get<0>(t) << endl;  // 10 (튜플 t의 0번 원소)
	cout << std::get<1>(t) << endl;  // 20 (튜플 t의 1번 원소)
	cout << std::get<2>(t) << endl;  // 30 (튜플 t의 2번 원소)
    
    // c++ 17을 사용한다면... 
	// (변환 방법 : 프로젝트 우클릭 > 속성 > 구성속성 > C/C++ > 언어 > C++ 언어 표준)
	auto[a, b, c] = GetResults();
	cout << a << endl;
	cout << b << endl;
	cout << c << endl;
	return 0;
}
```

> 10
> 20
> 30
> 10
> 20
> 30
> Press any key to continue . . .



- 참고) **std::make_tuple()**  : 튜플 생성

```c++
#include <iostream>
#include <tuple>  // std::tuple, std::make_tuple(), std::get()

using namespace std;

tuple<int, int, int> GetResults() {
	int x = 10, y = 20, z = 30;
	return make_tuple(x, y, z);
}

int main() 
{
	tuple<int, int, int> t = GetResults();
	cout << std::get<0>(t) << endl;
	cout << std::get<1>(t) << endl;
	cout << std::get<2>(t) << endl;

	return 0;
}
```

> 10
> 20
> 30
> Press any key to continue . . .



