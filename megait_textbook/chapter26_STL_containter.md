# STL (Standard Template Library)

다양한 자료구조와 알고리즘을 제공하는 표준 라이브러리



## STL의 구성요소

1. 컨테이너(container) - 창고
2. 반복자(iterator) - 창고 관리자
3. 알고리즘(algorithm) - 창고의 재고(원소) 처리 방법



# 컨테이너 (container)

- 여러 데이터를 저장하는 창고의 역할.
- 배열의 단점을 보완함.
  - 배열의 단점
    1. 크기를 변경할 수 없음.
    2. 물리적인 연속 배치. -> 중간 원소를 삽입하거나 삭제할 시, 뒤의 원소들을 하나씩 당기거나 미는 재배치를 수행해야 함.



## 컨테이너의 종류

- 시퀀스 컨테이너(sequencial container)
  - 데이터를 **선형**구조로 저장하며, 특별한 제약이나 규칙이 없는 **가장 일반적인 컨테이너**
  - 종류 : `vector`, `deque`, `list`, `forwad_list`
- 연관 컨테이너(associative container)
  - 데이터를 **비선형**구조로 저장하며 일정 규칙에 따라 조직화한 컨테이너
  - 종류 : `set`, `multiset`, `map`, `multimap`
- 컨테이너 어댑터(container adapter)
  - 간결함과 명료성을 위해 인터페이스를 제한한 시퀀스나 연관 컨테이너의 변형
  - 단, 반복자(iterator)를 지원하지 않음.
  - 종류 : `stack`, `queue`, `priority_queue`



# 시퀀스 컨테이너



## 시퀀스 컨테이너의 주요 함수

- int size() : 컨테이너에 현재 담겨있는 원소의 개수 
- void push_back(원소) : 원소 추가
- void pop_back() : 가장 마지막 원소 삭제
- void pop_back() : 가장 마지막 원소 삭제
- bool empty() : 벡터가 비어있는 지 확인
- void clear() : 모든 원소 삭제 



## std::vector

- 동적 배열 템플릿 (무제한 배열)
- 원소가 추가되거나 삭제될 때마다 자동으로 메모리를 재할당하여 크기를 동적으로 변경
- `vector.h`에 들어있음

```c++
#include <iostream>
#include <vector>  // std::vector

using namespace std;

int main()
{
	int length;

	// 백터 생성
	vector<int> v = { 10, 20, 30 };

	cout << "---- checkpoint 0 ----" << endl;
	length = v.size();  // 3
	cout << "원소 개수 : " << length << endl;

	cout << "---- checkpoint 1 ----" << endl;
	v.push_back(40); // 맨 뒤에 원소 추가
	length = v.size();  // 4
	cout << "원소 개수 : " << length << endl;

	//cout << v[0] << endl;  // 10
	//cout << v[1] << endl;  // 20
	//cout << v[2] << endl;  // 30
	//cout << v[3] << endl;  // 40

	//for문 방법 1
	cout << "---- checkpoint 2 ----" << endl;
	for (int i = 0; i < v.size(); ++i)
	{
		cout << v[i] << endl;
	}

	//for문 방법 2
	cout << "---- checkpoint 3 ----" << endl;
	for (auto& e : v)
	{
		cout << e << endl;
	}
	
	cout << "---- checkpoint 4 ----" << endl;
	v.pop_back();  // 마지막 원소 삭제
	for (auto& e : v)
	{
		cout << e << endl;
	}
	
	cout << "---- checkpoint 5 ----" << endl;
	bool e = v.empty();
	cout << "e : " << e << endl;  // 0 (false)

	cout << "---- checkpoint 6 ----" << endl;
	v.clear();
	for (auto& e : v)
	{
		cout << e << endl;
	}
	
	return 0;
}
```



## std::deque

- queue + stack 의 구조
- 양쪽에 커서가 있음
- 양 끝에서 빠르게 요소를 삽입하거나 삭제
- `deque.h`에 들어있음

 ```c++
 #include <iostream>
 #include <deque>  // std::deque
 #include <iterator> // std::ostream_iterator, std::copy
 using namespace std;
 
 int main()
 {
 
 	// 데크 생성
 	deque<int> deq{ 20,30,40 };
 
 	cout << endl;
 	copy(deq.begin(), deq.end(), ostream_iterator<int>(cout, "!"));
 
 	// void push_back(원소) : 맨 뒤에 원소 추가
 	// void push_front(원소) : 맨 앞에 원소 추가 (vector에 없음)
 	deq.push_back(50);
 	deq.push_front(10);
 
 	cout << endl;
 	copy(deq.begin(), deq.end(), ostream_iterator<int>(cout, "!"));
 
 	cout << endl << endl;
 	cout << "deq.front() : " << deq[0] << endl;
 	cout << "deq.front() : " << deq[1] << endl;
 	cout << "deq.front() : " << deq[2] << endl;
 	cout << "deq.front() : " << deq[3] << endl;
 	cout << "deq.front() : " << deq[4] << endl;
 
 	cout << endl;
 
 	deq.pop_back(); // 가장 마지막 원소를 삭제 (50 삭제)
 	copy(deq.begin(), deq.end(), ostream_iterator<int>(cout, " "));
 	cout << endl;
 
 	deq.pop_front(); // 가장 앞 원소를 삭제 (10 삭제) (vector에 없음)
 	copy(deq.begin(), deq.end(), ostream_iterator<int>(cout, " "));
 	cout << endl;
 
 	return 0;
 }
 ```



## 문제1.

deque를 사용하여 다음과 같은 순서의 원소를 저장하여 출력해보자. 

> 10 9 8 7 6 5 4 3 2 1 0 0 1 2 3 4 5 6 7 8 9 10



## 문제2.

다음과 같은 메뉴를 출력하고 사용자가 0을 입력할 때까지 기능을 수행하도록 해보자.

> < 포켓몬 도감 >
>
> 1. 포켓몬 추가
> 2. 모든 포켓몬 보기
>
> 0. 종료

- Pokemon 클래스를 만들 것 : 

  - private 멤버변수 : 이름, 레벨, 체력

  - public 멤버함수 
    - 생성자 : 기본생성자로 작성 (매개변수 없는 생성자)
    - printInfo() : 이름, 레벨, 체력을 cout
    - inputInfo() : 이름과 레벨은 cin으로 입력 받고, 체력은 레벨의 100배

- vector 혹은 deque 를 사용할 것.

  - (1)번을 선택할 때마다 원소가 1개씩 추가되는 구조

  - (2)번을 선택할 경우 컨테이너에 저장되어있는 모든 Pokemon 객체를 출력할 것

<hr/>



