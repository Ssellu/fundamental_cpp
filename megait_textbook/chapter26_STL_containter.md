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

# 연관 컨테이너



## std::set 과 std::multiset

- 집합(set) 컨테이너는 저장하는 데이터 그 자체를 키로 사용하는 가장 단순한 연관 컨테이너.
- 이 컨테이너는 벡터와 달리 오름차순으로 정렬된 위치에 요소를 삽입하므로 검색 속도가 매우 빠름.
- 키의 중복을 허용하지 않는다.
- 하지만 멀티집합(multiset)은 키의 중복을 허용하므로, 같은 값을 여러 번 저장할 수 있음.
- 이 두 컨테이너는 모두 `set.h`에 들어있음.

```c++
#include <iostream>
#include <set>
using namespace std;
void ex01() {
	set<int> s;

	cout << "----- checkout 1 -----" << endl;
	s.insert(10);
	s.insert(5);
	s.insert(1);
	s.insert(20);
	s.insert(5); // 5 중복
	s.insert(5); // 5 중복
	s.insert(5); // 5 중복
	for (auto& e : s)
	{
		cout << e << endl; // 오름차순 정렬을 지원함
	}


	cout << "----- checkout 2 -----" << endl;
	s.erase(5);
	s.erase(1);
	for (auto& e : s)
	{
		cout << e << endl; // 오름차순 정렬을 지원함
	}
}

void ex02() {
	multiset<int> s;

	cout << "----- checkout 1 -----" << endl;
	s.insert(10);
	s.insert(5);
	s.insert(1);
	s.insert(20);
	s.insert(5); // 5 중복
	s.insert(5); // 5 중복
	s.insert(5); // 5 중복
	for (auto& e : s)
	{
		cout << e << endl; // 오름차순 정렬을 지원함
	}


	cout << "----- checkout 2 -----" << endl;
	s.erase(5);
	s.erase(1);
	for (auto& e : s)
	{
		cout << e << endl; // 오름차순 정렬을 지원함
	}
}
int main()
{
	cout << "========= set =========" << endl;
	ex01();
	cout << "========= multiset =========" << endl;
	ex02();
	
	return 0;
}
```



## 문제 - 로또 추첨기

1 이상 ~ 45 이하 사이의 정수 중 '중복 없이' '오름차순'으로 6개의 숫자를 추출하여 출력하기

랜덤 수 생성은 다음 코드를 참고

```c++
#include <iostream>
#include <set>
#include <cstdlib>  // std::rand(), std::srand()
#include <ctime>  // std::time()
using namespace std;

int main()
{
	int n;

	srand(time(NULL)); // seed 값 설정 (seed : 난수 생성에 필요한 초기값. 시간 데이터를 seed 로 활용(매번 바뀌게))
	
	for (int i = 0; i < 10; ++i)
	{
		// 난수 생성 범위 : 2 ~ 4
		n = rand() % 3 + 2; // 2에서 3개의 숫자 중 하나를 뽑아 n에 저장(2, 3, 4)
		cout << n << endl;
	}

	
	return 0;
}
```



## 답

```c++
#include <iostream>
#include <set>
#include <cstdlib> 
#include <ctime> 
#include <set>
using namespace std;

int main()
{
	set<int> lotto;
	srand(time(NULL)); 
	
	while (lotto.size() < 6)
	{
		lotto.insert(rand() % 45 + 1);
	}

	for (auto& e : lotto)
	{
		cout << e << " ";
	}
	cout << endl;

	return 0;
}
```



## std::map 과 std::multimap

- 맵(map) 컨테이너는 `키 - 값`의 쌍으로 데이터를 저장 및 관리.
- 키를 기준으로 오름차순의 정렬된 위치에 저장하므로 검색 속도가 매우 빠름. 
- 맵(map)은 키의 중복을 허용하지 않음.
- 멀티맵(multimap)은 값의 중복을 허용함. 하나의 키가 여러 개의 값과 연결될 수 있음.
- 모두 `map.h` 에 들어있음.

```c++
#include <iostream>
#include <map>
using namespace std;
void ex01() {
	//map<char, int> m;
	map<char, int> m{pair<char, int>('a', 10), pair<char, int>('b', 20), pair<char, int>('c', 30)};

	cout << "----- checkout 1 -----" << endl;
	
	// 원소 추가 방법1. - [] 기호 사용 (배열처럼 쓰기)
	m['x'] = 100;
	m['y'] = 200;
	m['z'] = 300; 
	m['z'] = 350; // z 중복
	m['z'] = 400; // z 중복

	// 원소 추가 방법2. - pair 클래스 사용
	m.insert(pair<char, int>('i', 111));

	for (auto& e : m)
	{
		cout << e.first << " : " << e.second << endl;
		// first : 키
		// second : 값
	}


	cout << "----- checkout 2 -----" << endl;

	// 원소 삭제
	m.erase('i');
	for (auto& e : m)
	{
		cout << e.first << " : " << e.second << endl;
	}

	cout << "----- checkout 3 -----" << endl;

	// value 조회 (키가 없다면 false(=0) 을 출력)
	int elem = m['y'];
	cout << elem << endl;

}

void ex02() {
	multimap<char, int> m;
	
	cout << "----- checkout 1 -----" << endl;
	m.insert(pair<char, int>('x', 100));
	m.insert(pair<char, int>('y', 200));
	m.insert(pair<char, int>('z', 200));
	m.insert(pair<char, int>('z', 250));  // 중복
	m.insert(pair<char, int>('z', 300));  // 중복

	for (auto& e : m)
	{
		cout << e.first << " : " << e.second << endl;
	}


	cout << "----- checkout 2 -----" << endl;

	// 원소 삭제
	m.erase('y');
	for (auto& e : m)
	{
		cout << e.first << " : " << e.second << endl;
	}

	cout << "----- checkout 3 -----" << endl;

	// multimap의 원소 조회 (value가 여러 개 일 수 있기때문에 이터레이터를 사용하여 반복 처리 실행)
	multimap<char, int>::iterator iter;
	for (iter = m.equal_range('z').first; iter != m.equal_range('z').second; iter++) {
		cout << "키 : " << iter->first << endl;
		cout << "값 : " << iter->second << endl;
	}
}
int main()
{
	cout << "========= map =========" << endl;
	ex01();
	cout << "========= multimap =========" << endl;
	ex02();

	return 0;
}
```



# 컨테이너 어댑터





## std::stack

- 선형의 후입선출(LIFO) 자료 구조.
  - LIFO : 가장 나중에 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조.
- `stack.h`에 들어있음

| 멤버 함수 |                             설명                             |
| :-------: | :----------------------------------------------------------: |
|  empty()  | 스택이 비어 있으면 true를, 비어 있지 않으면 false를 반환함.  |
|  size()   |                스택 요소의 총 개수를 반환함.                 |
|   top()   | 스택의 제일 상단에 있는(제일 마지막으로 저장된) 요소에 대한 참조를 반환함. |
|  push()   |              스택의 제일 상단에 요소를 삽입함.               |
|   pop()   |            스택의 제일 상단에 있는 요소를 삭제함.            |

 ```c++
 #include <iostream>
 #include <string>
 #include <stack>  // std::stack
 using namespace std;
 
 int main()
 {
 	stack<int> s;
 	int t;
 	cout << "------ check point 1 ------" << endl;
 	s.push(10);
 	s.push(20);
 	s.push(30);
 	s.push(40);
 	t = s.top();
 	cout << "top : " << t << endl;
 
 	cout << "------ check point 2 ------" << endl;
 	s.pop();
 	s.pop();
 	t = s.top();
 	cout << "top : " << t << endl;
 
 	cout << "------ check point 3 ------" << endl;
 	s.push(100);
 	s.push(200);
 	t = s.top();
 	cout << "top : " << t << endl;
 	return 0;
 }
 ```



## std::queue

- 선형의 후입선출(FIFO) 자료 구조.
  - FIFO : 가장 먼저 저장된(push) 데이터가 가장 먼저 인출(pop)되는 구조.
- `stack.h`에 들어있음

| 멤버 함수 |                             설명                             |
| :-------: | :----------------------------------------------------------: |
|  empty()  |  큐가 비어 있으면 true를, 비어 있지 않으면 false를 반환함.   |
|  size()   |                 큐 요소의 총 개수를 반환함.                  |
|  front()  | 큐의 맨 앞에 있는(제일 먼저 저장된) 요소에 대한 참조를 반환함. |
|  back()   | 큐의 맨 뒤에 있는(제일 나중에 저장된) 요소에 대한 참조를 반환함. |
|  push()   |                 큐의 맨 뒤에 요소를 삽입함.                  |
|   pop()   |                 큐의 맨 앞의 요소를 삭제함.                  |

```c++
#include <iostream>
#include <string>
#include <queue>  // std::queue
using namespace std;

int main()
{
	queue<int> q;
	int t;
	cout << "------ check point 1 ------" << endl;
	q.push(10);
	q.push(20);
	q.push(30);
	q.push(40);
	cout << "front : " << q.front() << ", back : " << q.back() << endl;

	cout << "------ check point 2 ------" << endl;
	q.pop();
	q.pop();
	cout << "front : " << q.front() << ", back : " << q.back() << endl;

	cout << "------ check point 3 ------" << endl;
	q.push(100);
	q.push(200);
	cout << "front : " << q.front() << ", back : " << q.back() << endl;
	return 0;
}
```

