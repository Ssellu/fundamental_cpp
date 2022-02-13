# 템플릿

- 작성자가 아닌 호출자가 자료형을 결정할 수 있도록 자료형을 비워두는 것 
- 이것을 일반화 프로그래밍(Generic Programming)이라고 한다. 



# 함수 템플릿

> template <typename 타입이름>
>
> 함수의 원형
>
> {
>
>   // 함수의 본체
>
> }

```c++
#include <iostream>
#include <string> 
using namespace std;

template <typename T>
void Swap(T& t1, T& t2)
{
	T temp = t1;
	t1 = t2;
	t2 = temp;
}

int main() {

	int a = 10, b = 20;
	cout << "변환 전 a : " << a << ", b : " << b << endl;
	Swap(a, b);
	cout << "변환 후 a : " << a << ", b : " << b << endl;



	string c = "John", d = "Jane";
	cout << "변환 전 c : " << c << ", d : " << d << endl;
	Swap(c, d);
	cout << "변환 후 c : " << c << ", d : " << d << endl;
	return 0;
}
```



## 함수의 명시적 특수화(explicit specialization)

특정 매개변수 타입만 따로 특별한 처리를 해주고 싶다면..

```c++
template <typename T> 
void Swap(T& t1, T& t2)
{
	T temp = t1;
	t1 = t2;
	t2 = temp;
}

// 명시적 특수화. 함수가 (int, int) 타입으로 호출되었다면 다음의 특별한 처리를 실행
template <> 
void Swap(int& t1, int& t2)
{
	cout << "정수 데이터의 Swap 실행!" << endl;
	int temp = t1;
	t1 = t2;
	t2 = temp;
}
```



## 문제

다음 코드가 정상적으로 실행 될 수 있도록 템플릿을 활용하여 `getMax()`를 정의하기

```c++
int main() {

	Person p1{ "홍길동", 10 }; // name_, age_ 
	Person p2{ "최길동", 20 }; // name_, age_ 

	cout << getMax(10, 20) << endl;			// 20
	cout << getMax('A' , 'B') << endl;		// B (A의 정수값은 65, B는 66이다.)
	cout << getMax("ABC", "ABB") << endl;	// ABC (string은 가나다, 알파벳 순으로 대소 비교가 가능하다.)
	cout << getMax(p1, p2).name_ << endl;	// 최길동
	
    return 0;
}
```



## 답

```c++
#include <iostream>
#include <string> 
using namespace std;

template <typename T>
T getMax(T t1, T t2)
{
	return t1 > t2 ? t1 : t2;
}

class Person 
{
public:
	string name_;
	int age_;

	bool operator > (Person& p) // Person 측에 '>' 연산자 오버로딩을 하거나, 템플릿 특수화를 하거나.
	{
		return age_ > p.age_;
	}

};

int main() {

	Person p1{ "홍길동", 10 }; // name_, age_ 
	Person p2{ "최길동", 20 }; // name_, age_ 

	cout << getMax(10, 20) << endl;
	cout << getMax('A' , 'B') << endl;
	cout << getMax("ABC", "ABB") << endl;
	cout << getMax(p1, p2).name_ << endl;
	return 0;
}
```





# 클래스 템플릿

템플릿을 적용하는 대상이 함수가 아닌 클래스

> template <typename 타입이름>
>
> class 클래스템플릿이름
>
> {
>
>   // 클래스 멤버의 선언
>
> }

```c++
#include <iostream>
#include <string> 
using namespace std;

template <typename T>
class Data
{
private:
	T data_;

public:
	Data(T dt) : 
		data_(dt)
	{};
	
	void set_data(T dt) 
	{
		data_ = dt;
	};
	
	T get_data() 
	{
		return data_;
	};

	void printInfo()
	{
		cout << "data : " << data_ << endl;
		cout << "data의 자료형 : " << typeid(data_).name() << endl;
	}
};

int main() {

	Data<int> d1{ 10 };
	Data<double> d2{ 3.14 };
	Data<string> d3{ "ABC" };

	d1.printInfo();
	d2.printInfo();
	d3.printInfo();

	return 0;
}
```

