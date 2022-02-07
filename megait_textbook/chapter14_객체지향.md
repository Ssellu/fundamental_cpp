# 클래스와 객체 

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person 
{
public:
	string name;  	// 멤버변수(=필드)
	int age;		// 멤버변수(=필드)

	void printInfo() // 멤버함수(=메서드)
	{
		cout << "name : " << name << endl;
		cout << "age : " << age << endl;
	}
};
int main(){

	Person p1{ "John Doe", 20 };

	// Person p1;
	// p1.name = "John Doe";
	// p1.age = 20;

	Person p2{ "Jane Doe", 32 };
	
	p1.printInfo();
	p2.printInfo();

	return 0;
}
```

> name : John Doe
>
> age : 20
>
> name : Jane Doe
>
> age : 32
>
> Press any key to continue . . .



# 연습문제

## 문제1. Unit 클래스 정의하기

- public 멤버변수
  - name : 문자열
  - level : 양의 정수
  - hp : 양의 정수
- quiz01() 정의
  - Unit 객체 3개 선언
  - 사용자에게  이름, 레벨, 체력을 입력 받고 이를 Unit 객체에 저장 -> 3번 반복
  - 3개의 Unit 객체에 정보를 출력

## 문제2. 문제 1번 확장

- quiz02() 정의 (문제(1)의 quiz01() 의 내용을 객체 배열로 변경. )
  - Unit 객체 3칸짜리 배열 1개 선언
  - 사용자에게 이름, 레벨, 체력을 입력 받고 이를 Unit 배열에 차례로 저장 -> 3번 반복
  - 3개의 Unit 객체에 정보를 출력



## 문제3. Student 클래스 정의하기

- public 멤버변수 
  - name : 이름, 문자열
  - num : 학번, 문자열
  - kr : 영어점수, 양의 정수
  - en : 영어점수, 양의 정수
  - ma : 수학점수, 양의 정수
- public 멤버메서드
  - void printInfo() : 이 객체의 모든 멤버변수를 출력 하기
  - double getAvg() : 이 객체의 국, 영, 수의 평균값을 return
  - std::string getGpa() : 이 객체의 평균값에 따른 학점을 return 
    - 90 이상 : "A"
    - 80 이상 90 미만 : return "B"
    - 70 이상 80 미만 : return "C"
    - 60 이상 70 미만 : return "D"
    - 60 미만 : return "F"
- quiz03() 정의 
  - Student 객체 2개 선언
  - 사용자에게 이름, 학번, 국, 영, 수 정보 입력 받기 X 2번 반복
  - 사용자의 이름, **평균**, **학점**을 출력







# 접근지정자(Access Modifiers)

- 종류

  - private : 클래스 내부에서만 사용 가능 (디폴트)

  - public : 모두가 사용 가능 

  - protected : 클래스 내부에 자식 클래스에서만 사용 가능


```c++
class A 
{
// A 클래스 안에서만 사용 가능
private:
	int x; 
    void xx() {}
    
// 모든 곳에서 사용 가능    
public:
    int y; 
    void yy() {}
}

int main()
{
	A a;
    a.x = 10; // 에러
    a.y = 20; // 가능
    
    cout << a.x << endl; // 에러
    cout << a.y << endl; // 가능
    
    a.xx(); // 에러
    a.yy(); // 가능
    
    return 0;
}
```





# 캡슐화와 은닉화 

- 은닉화 

  - 객체의 무결성을 위하여 데이터를 은닉시키는 것. 
  - 보여줄 것만 보여준다.

- 캡슐화(encapsulation)

  - 은닉화의 방법 중 하나
  - 변수(데이터)의 접근은 제한하고, 대신 중간자 역할의 메서드를 정의하는 것

  - 변수는 **private**, 함수는 **public** 

```c++
#include <iostream>
#include <string> 

using namespace std;

class Person 
{
    // public:  , protected
	string name_; 
	int age_;		

public:
	void printInfo()
	{
		cout << "name : " << name_ << endl;
		cout << "age : " << age_ << endl;
	}

	void setName(string name) 
	{
		name_ = name;
	}

	void setAge(int age)
	{
		if (age > 0)
			age_ = age;
	}
};
int main(){

	// Person p1{ "John Doe", 20 };
	// Person p2{ "Jane Doe", 32 };
	
	Person p1;
	Person p2;

	p1.setName("John Doe"); 
	p1.setAge(20);

	p2.setName("Jane Doe");
	p2.setAge(32);

	p1.printInfo();
	p2.printInfo();

	cout << "p1 나이에 음수 넣어보기" << endl;

	p1.setAge(-100);
	p1.printInfo();

	return 0;
}
```



## 반대로 getter는..

```c++
int getAge()
{
    return age_;
}

string getName()
{
    return name_;
}
```



## 좀 더 발전한 getter

```c++
const int& getAge()
{
    return age_;
}

const string& getName()
{
    return name_;
}
```



이러한 setter, getter 들을 **접근 함수(Accessors)**라고 한다.

