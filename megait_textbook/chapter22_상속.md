# 상속(Inheritance)

- 객체지향의 꽃!!!!!!!!!!!!!
- 기존 클래스를 '확장'하여 '새 클래스'를 만드는 작업
  - 원본 클래스 : 기초 클래스(base class) / 부모 클래스(parent class) / 상위 클래스(super class)
  - 새 클래스 : 파생 클래스(derived class) / 자식 클래스(child class) / 하위 클래스(sub class)

```c++
#include <iostream>
#include <string> 
using namespace std;
class Person
{
public:
	string name_;
	int age_;
};

class Student : public Person 
{
public:
	/* < 부모의 모든 것을 갖는다. >
	string name_;
	int age_;
	*/
	int num_;
	int score_;
};

class Teacher : public Person
{
public:
	/* < 부모의 모든 것을 갖는다. >
	string name_;
	int age_;
	*/
	string subject_;
};

int main()
{
	Student s;
	s.name_ = "홍길동";
	s.age_ = 13;
	s.num_ = 1;
	s.score_ = 100;

	Teacher t;
	t.name_ = "고길동";
	t.age_ = 42; 
	t.subject_ = "물리";

	cout << "---- 학생 정보 ----" << endl;
	cout << "이름 : " << s.name_ << endl;
	cout << "나이 : " << s.age_ << endl;
	cout << "학번 : " << s.num_ << endl;
	cout << "점수 : " << s.score_ << endl;

	cout << "---- 교사 정보 ----" << endl;
	cout << "이름 : " << t.name_ << endl;
	cout << "나이 : " << t.age_ << endl;
	cout << "담당과목 : " << t.subject_ << endl;
	return 0;
}
```

> ---- 학생 정보 ----
>
> 이름 : 홍길동
>
> 나이 : 13
>
> 학번 : 1
>
> 점수 : 100
>
> ---- 교사 정보 ----
>
> 이름 : 고길동
>
> 나이 : 42
>
> 담당과목 : 물리
>
> Press any key to continue . . .



# 상속과 접근지정자

<table>
    <thead>
    	<th>상속 접근 지정자</th>
        <th>부모클래스의 멤버</th>
        <th>자식클래스가 받을 때</th>
    </thead>
    <tbody>
        <tr>
            <th rowspan="3">public</th>
            <td>public</td>
            <td>public</td>
        </tr>
        <tr>
			<td>private</td>
            <td>X</td>
        </tr>
        <tr>
        	<td>protected</td>
            <td>protected</td>
        </tr>
        <tr>
            <th rowspan="3">private<br/>(default)</th>
            <td>public</td>
            <td>public</td>
        </tr>
        <tr>
            <td>private</td>
            <td>X</td>
        </tr>
        <tr>
            <td>protected</td>
            <td>private</td>
        </tr>
        <tr>
            <th rowspan="3">protected</th>
            <td>public</td>
            <td>protected</td>
        </tr>
        <tr>
            <td>private</td>
            <td>X</td>
        </tr>
        <tr>
            <td>protected</td>
            <td>protected</td>
        </tr>
    </tbody>
</table>



# 함수 오버라이드(Override)

- 멤버함수 재정의
- 부모가 물려준 멤버함수를 자식이 덮어씀. 
- 부모가 물려준 함수의 `{}`영역만 고쳐야 함. **원형은 똑같이 정의해야 함**
- 목적 : 자식과 부모의 **멤버함수 사용방법을 통일** 및 **다형성** 구현

```c++
class Parent 
{
public:
	void doSomething()
	{
		cout << "이것은 Parent의 doSomething" << endl;
	}
};

class Child : public Parent
{
public:
	void doSomething()  // 이 부분!
	{
		cout << "이것은 Child의 doSomething" << endl;
	}
};

int main()
{
	Parent parent;
	Child child;

	parent.doSomething();  // 이것은 Parent의 doSomething
	cout << "---------checkpoint 1---------" << endl;

	child.doSomething();  // 이것은 Child의 doSomething
	cout << "---------checkpoint 2---------" << endl;

	return 0;
}
```



- 자식 클래스 내부에서, 부모가 물려준 원본 함수를 실행하고 싶다면..

```c++
#include <iostream>
#include <string> 
using namespace std;
class Parent 
{
public:
	void doSomething()
	{
		cout << "이것은 Parent의 doSomething" << endl;
	}
};

class Child : public Parent
{
public:
	void doSomething()
	{
		cout << "이것은 Child의 doSomething" << endl;
	}

	void doSomethingMore()  
	{
		Child::doSomething();  // 오버라이드된 doSomething
		Parent::doSomething();  // 원본 doSomething  <~~ 이 부분! 
	}
};

int main()
{
	Child child;

	child.doSomethingMore();

	return 0;
}
```

> 이것은 Child의 doSomething
>
> 이것은 Parent의 doSomething
>
> Press any key to continue . . .



# 문제1

## 1-1. 위의 Person, Student, Teacher 예제에서 다음 메서드를 추가

- 생성자 만들지 말 것!

- Person (부모)
  - printInfo() - 이름, 나이를 cout

- Student (자식1)
  - printInfo() 오버라이드 - 이름, 나이, 학번, 점수를 cout
- Teacher (자식2)
  - printInfo() 오버라이드 - 이름, 나이, 담당과목을 cout

## 1-2. quiz01() 에서 테스트



# 문제2

## 2-1. 클래스 정의

### 부모클래스 : Book

- public 멤버변수 : 
  - title_  : 책의 제목
  - author_ : 저자의 이름
  - price_ : 가격
- public 멤버함수 : 
  - printInfo() - 모든 멤버변수를 cout 
  - inputInfo() - 모든 멤버변수를 cin

### 자식클래스1 : Novel (소설클래스)

- public 멤버변수 : 
  - genre_ : 책의 장르
- public 멤버함수 : 
  - printInfo() - 모든 멤버변수를 cout 
  - inputInfo() - 모든 멤버변수를 cin

### 자식클래스2 : Comic (코믹클래스)

- public 멤버변수 : 
  - genre_ : 책의 장르
  - minAge_ : 제한 나이
- public 멤버함수 : 
  - printInfo() - 모든 멤버변수를 cout 
  - inputInfo() - 모든 멤버변수를 cin

### 자식클래스3 : Textbook (교과서클래스)

- public 멤버변수 : 
  - subject_ : 과목
- public 멤버함수 : 
  - printInfo() - 모든 멤버변수를 cout 
  - inputInfo() - 모든 멤버변수를 cin



## 2-2. quiz02() 에서 

- 사용자에게 어떤 종류의 책을 등록할 지 번호를 입력 받음

  (예. (1)일반책 (2)소설 (3)만화 (4)교과서)

- 선택한 종류의 책 객체를 생성하여 inputInfo() 로 값을 입력 받기

- printInfo() 로 결과 출력






# 상속의 목적

1. 코드의 재사용 
2. 그룹화(가족화) ~> 자료형 통일 ~> 같은 가족끼리는 사용 방법 (멤버함수) 통일
3. 다형성





# 상속 받은 멤버의 접근지정자 바꾸기

```c++
#include <iostream>
#include <string> 
using namespace std;
class Parent
{
protected:
	int x;

public:
	void doSomething() {}
};

class Child : public Parent
{
public:
	using Parent::x;  // protected인 x를 public 으로 바꾸기

private:
	using Parent::doSomething; // public인 doSomething을 private 으로 바꾸기( 괄호 X )
};

int main() {

	Child c; 
	c.x = 10;
	cout << c.x << endl;
	
	c.doSomething(); // 에러
	return 0;
}
```

단, 부모의 private 멤버는 변경 불가. 



# 다중 상속

- 다중 상속 : 하나의 클래스가 여러 부모 클래스를 상속 받는 것.

- C++은 다중 상속을 지원함.
- 복잡한 상속 관계인 경우는 다중 상속은 문제가 많기 때문에 사용 자제.

```c++
class ParentA
{
};

class ParentB
{
};

class Child : public ParentA, public ParentB // 이 부분
{
};
```



## 다중 상속 문제점

1. 멤버 충돌의 가능성. 부모끼리 같은 이름의 멤버가 있을 수 있음. 

```c++
class ParentA
{
	void doSomething() {}
};

class ParentB
{
	void doSomething() {}
};

class Child : public ParentA, public ParentB // 이 부분
{
};

int main() {

	Child c; 
	c.doSomething();  // 에러! 
	return 0;
}
```



2. 하나의 클래스를 간접적으로 두 번 이상 상속받을 가능성.

```c++
#include <iostream>
#include <string> 
using namespace std;
class GrandParent {
public:
	int x;
};
class ParentA : public GrandParent
{
};

class ParentB : public GrandParent
{
};

class Child : public ParentA, public ParentB // 이 부분
{
};

int main() {

	Child c; 
	c.x = 0;  // 에러
	return 0;
}
```



