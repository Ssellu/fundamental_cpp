# 연산자 함수 오버로딩

- `객체 + 객체`, `객체 - 객체` 같이 객체와 연산자를 같이 쓰고 싶다? ==> 연산자 함수 오버로딩
- 

```c++
class 클래스
{
    ...
    // 멤버함수로 정의 가능
    리턴자료형 operator 연산자 (매개변수선언) {
        return 결과;
    }
}

// 전역함수로도 정의 가능
리턴자료형 operator 연산자 (매개변수선언) {
    return 결과;
}
```





## 예제: Person의 나이를 비교하는 <, > 연산자

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

	// 이 부분!
	bool operator > (const Person& p)
	{
		return age > p.age;
	}

	// 이 부분!
	bool operator < (const Person& p)
	{
		return age < p.age;
	}
};
int main() {
	
	Person p1{ "홍길동", 10 };
	Person p2{ "고길동", 20 };  

	cout << (p1 > p2) << endl;
	cout << (p1 < p2) << endl;
	cout << (p1 <= p2) << endl; // 에러!
	cout << (p1 >= p2) << endl; // 에러!
	return 0;
}
```



## 문제

- 클래스명 : Circle
  - private 멤버변수 : 반지름, 원주율 (const 로 선언. 3.14로 지정)
  - public 멤버함수
    - 생성자 (자유롭게)
    - getter (const 선언)
      1. getRadius() : 반지름 return
      2. getPi() : 원주율 return
      3. getArea() : 원의 넓이를 구하여 이를 return 
    - setter
      1. setRadius() : 반지름 저장
    - `+` 연산자 함수 : 두 원의 반지름을 더하여 새 Circle 객체의 반지름으로 지정. 만들어진 새 Circle 객체를 return
    - `-` 연산자 함수 : 두 원의 반지름을 뺀 값을 새 Circle 객체의 반지름으로 지정. 만들어진 새 Circle 객체를 return

-  다음 메인메서드가 잘 실행되도록 Circle 클래스 정의

  ```c++
  int main() {
  	
  	Circle c1{ 1 };
  	Circle c2{ 2 };
  
  	Circle c3 = c1 + c2;
  	Circle c4 = c1 - c2;
  
  	// c3 반지름 : 3, 넓이 : 28.26
  	cout << "c3 반지름 : " << c3.getRadius() << ", 넓이 : " << c3.getArea() << endl;
  
  	// c4 반지름 : -1, 넓이 : 3.14
  	cout << "c4 반지름 : " << c4.getRadius() << ", 넓이 : " << c4.getArea() << endl;
  
  	return 0;
  }
  ```



## 답

```c++
#include <iostream>
#include <string> 
#include <cmath>
using namespace std;

class Circle
{
private:
	double radius_;
	const double pi_ = 3.14;

public:
	Circle(double radius = 0)
		:radius_(radius)
	{}

	double getArea() const 
	{
		return pow(radius_, 2) * pi_;
	}

	double getRadius() const
	{
		return radius_;
	}

	void setRadius(int radius)
	{
		radius_ = radius;
	}

	Circle operator + (const Circle& c)
	{
		return Circle(radius_ + c.radius_);
	}
	Circle operator - (const Circle& c)
	{
		return Circle(radius_ - c.radius_);
	}
};

/* 연산자 오버로딩을 전역함수로 하려면
Circle operator + (const Circle& c0, const Circle& c1)
{
	return Circle(c0.getRadius() + c1.getRadius());
}
Circle operator - (const Circle& c0, const Circle& c1)
{
	return Circle(c0.getRadius() + - c1.getRadius());
}
*/
```



# 연산자 오버로딩 제약사항

1. 전혀 새로운 연산자를 정의 불가.

   > ~!#, ###, &~!~! 

 

2. 원시 타입을 다루는 연산자는 오버로딩 할 수 없음. 따라서 오버로딩된 연산자의 피연산자 중 하나는 반드시 사용자 정의 타입이어야 함.

   > 두 개의 double 형에 대한 덧셈 연산자(+)가 뺄셈을 수행하도록 오버로딩할 수 없음.
   >
   > 3.14 + 2.2 를 위한 연산자 오버로딩은 안됨. 하지만 `3.14 + circle 객체` 를 위한 오버로딩은 가능.

 

3. 오버로딩된 연산자는 기본 타입을 다루는 경우에 적용되는 피연산자의 수, 우선순위 및 그룹화를 준수해야 함.

   > 단항 연산자를 이항연산자로 오버로딩할 수 없음. 

 

4. 오버로딩된 연산자는 디폴트 인수를 사용할 수 없음.

   > bool operator + (int n = 1)  <~ `=1` 이 부분 안됨!



# 오버로딩 할 수 없는 연산자 목록

|      연산자      |        설명        |
| :--------------: | :----------------: |
|        ::        |  범위 지정 연산자  |
|        .         |    멤버 연산자     |
|        .*        | 멤버 포인터 연산자 |
|       ? :        |  삼항 조건 연산자  |
|      sizeof      |    크기 연산자     |
|      typeid      |     타입 인식      |
|    const_cast    |   상수 타입 변환   |
|   dynamic_cast   |   동적 타입 변환   |
| reinterpret_cast |  재해석 타입 변환  |
|   static_cast    |   정적 타입 변환   |



# 멤버 함수로만 오버로딩할 수 있는 연산자

- 전역 함수가 아닌 멤버함수로만 오버로딩 가능

| 연산자 |       설명       |
| :----: | :--------------: |
|   =    |   대입 연산자    |
|   ()   |    함수 호출     |
|   []   |   배열 인덱스    |
|   ->   | 멤버 접근 연산자 |