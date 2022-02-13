# 가상 함수

- 자식 클래스가 재정의할 것으로 기대하는 멤버 함수
- 다형성 구현에 필수

```c++
#include <iostream>
#include <string> 
using namespace std;

class Pokemon {
public:
	virtual void attack()
	{
		cout << "포켓몬 공격 개시!" << endl;
	}
};

class Pikachu : public Pokemon
{
public:
	void attack() // 가상함수 attack 오버라이드
	{
		cout << "피카츄, 백만볼트 공격!" << endl;
	}
};
class Raichu : public Pokemon
{
public:
	void attack() // 가상함수 attack 오버라이드
	{
		cout << "라이츄, 천만볼트 공격!" << endl;
	}
};
class Purin : public Pokemon
{
public:
	void attack() // 가상함수 attack 오버라이드
	{
		cout << "푸린, 자장가 공격!" << endl;
	}
};
```

```c++
int ex01() {
	Pokemon p1;
	Pikachu p2;
	Raichu	p3;
	Purin	p4;

	p1.attack();  // 포켓몬 공격 개시!
	p2.attack();  // 피카츄, 백만볼트 공격!
	p3.attack();  // 라이츄, 천만볼트 공격!
	p4.attack();  // 푸린, 자장가 공격!
	
	return 0;
}
```

```c++
int ex03() {
	// 정적 할당
	Pokemon p1;
	Pikachu p2;
	Raichu	p3;
	Purin	p4;
    
	Pokemon* p;

	p = &p1;
	p->attack();  // 포켓몬 공격 개시!

	p = &p2;
	p->attack();  // 피카츄, 백만볼트 공격!

	p = &p3;
	p->attack();  // 라이츄, 천만볼트 공격!

	p = &p4;
	p->attack();  // 푸린, 자장가 공격!
    
	return 0;
}
```

```c++
int ex03() {

	Pokemon* p;

	// 동적할당
	p = new Pokemon();
	p->attack();  // 포켓몬 공격 개시!

	p = new Pikachu();
	p->attack();  // 피카츄, 백만볼트 공격!

	p = new Raichu();
	p->attack();  // 라이츄, 천만볼트 공격!

	p = new Purin();
	p->attack();  // 푸린, 자장가 공격!
	return 0;
}
```



# 순수 가상 함수

- 순수 가상 함수(Pure Virtual Function) : 자식에게 '무조건 오버라이드' 하도록 강요하는 함수



## 순수 가상 함수의 선언

> ### virtual 멤버함수의원형=0;

```c++
class Pokemon {
public:
	....
	virtual void attack() = 0; // 순수 가상 함수 선언
};

// Pokemon의 자식은 반드시 attack()을 오버라이드 해야 함.
...
```



# 추상 클래스

- 추상 클래스(Abstract Class) : 하나 이상의 순수 가상 함수를 포함하는 클래스

```c++
class Pokemon {
public:
	string name_;
	virtual void attack() = 0; // 순수 가상 함수
	virtual ~Pokemon() {};  // 가상 소멸자
};

void doSomething(Pokemon& p) // p에는 모든 자식 타입 객체가 들어갈 수 있음
{
	p.attack();
}

int main() {

	// Pokemon p1; // 추상 클래스는 객체화 불가능.
	Pikachu p2;
	Raichu	p3;
	Purin	p4;

	doSomething(p2);  // 피카츄, 백만볼트 공격!
	doSomething(p3);  // 라이츄, 천만볼트 공격!
	doSomething(p4);  // 푸린, 자장가 공격!
	
	return 0;
}
```



# 인터페이스 클래스

- 인터페이스 클래스(Interface Class) : 순수 가상 함수로만 구성된 클래스

```c++
class Pokemon {
public:
	virtual void attack() = 0; // 순수 가상 함수
	virtual ~Pokemon() {};  // 가상 소멸자
};
```



# 추상 클래스와 인터페이스 공통점

- 객체화 될 수 없으나, 참조/포인터 변수의 자료형으로는 사용 가능함.
- 여러 타입을 하나의 집합으로 묶을 수 있음.
- 가상 소멸자를 꼭 만들어주자.





# 문제

## 1. 인터페이스 클래스 정의

- 이름 : Shape

- 멤버 : 

  - 멤버변수 : X

  - 멤버함수 : (모두 public 으로)

    - void inputInfo() : 
      - 리턴자료형 void, 매개변수 X
      - 순수 가상 함수로 선언
    - double getArea() : 
      - 리턴자료형 double, 매개변수 X
      - 순수 가상 함수로 선언

    - ~Shape : 
      - 가상 소멸자로 정의

## 2. 자식 클래스 정의

### 2-1. Circle 클래스

- 멤버변수 : 

  - 반지름 (실수, private으로)

- 멤버함수 : 

  - 생성자 : 다음의 코드가 정상적으로 실행되도록 생성자 정의 (public 으로)

    ```c++
    Circle{};  // 반지름 1
    Circle{10}; // 반지름 10
    ```

  - 소멸자 : 소멸자가 호출될 때 다음과 비슷한 방식으로 출력 되도록 함.

    ```c++
    원 객체 해제! (반지름 10)
    ```

  - getArea() 오버라이드
    - 객체가 가지고 있는 반지름 멤버변수를 사용하여 원의 넓이를 계산한 뒤 결과 값을 return 
  - void inputInfo() 오버라이드 
    - 반지름을 입력 받아 멤버변수에 저장



### 2-2. Triangle 클래스

- 멤버변수 : 

  - 밑변, 높이 (실수, private으로)

- 멤버함수 : 

  - 생성자 : 다음의 코드가 정상적으로 실행되도록 생성자 정의 (public 으로)

    ```c++
    Triangle{}; // 밑변 1, 높이 1
    Triangle{10}; // 밑변 10, 높이 1
    Triangle{10, 20}; // 밑변 10, 높이 20
    ```

  - 소멸자 : 소멸자가 호출될 때 다음과 비슷한 방식으로 출력 되도록 함.

    ```c++
    삼각형 객체 해제! (밑변 10, 높이 20)
    ```

  - getArea() 오버라이드
    - 객체가 가지고 있는 밑변, 높이 멤버변수를 사용하여 삼각형의 넓이를 계산한 뒤 결과 값을 return 
  - void inputInfo() 오버라이드 
    - 밑변, 높이를 입력 받아 멤버변수에 저장



### 2-3. Rectangle 클래스

- 멤버변수 : 

  - 밑변, 높이 (실수, private으로)

- 멤버함수 : 

  - 생성자 : 다음의 코드가 정상적으로 실행되도록 생성자 정의 (public 으로)

    ```c++
    Rectangle{}; // 밑변 1, 높이 1
    Rectangle{10}; // 밑변 10, 높이 1
    Rectangle{10, 20}; // 밑변 10, 높이 20
    ```

  - 소멸자 : 소멸자가 호출될 때 다음과 비슷한 방식으로 출력 되도록 함.

    ```c++
    직사각형 객체 해제! (밑변 10, 높이 20)
    ```

  - getArea() 오버라이드
    - 객체가 가지고 있는 밑변, 높이 멤버변수를 사용하여 직사각형의 넓이를 계산한 뒤 결과 값을 return 
  - void inputInfo() 오버라이드 
    - 밑변, 높이를 입력 받아 멤버변수에 저장



## 3. quiz02() 전역함수 정의

1. 사용자에게 원하는 도형을 입력 받는다. (0. 원 1. 삼각형 2. 직사각형)
2. 객체는 new 를 사용하여 동적할당한다.
3. 객체는 Circle, Rectiangle, Triangle 클래스를 사용하되, 참조변수는 Shape형으로 통일한다.
4. 원이면 반지름, 삼각형이나 직사각형이면 밑변과 높이를 입력 받는다.
5. getArea()를 사용하여 넓이를 구하고 이를 출력한다.