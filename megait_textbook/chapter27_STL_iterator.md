# 반복자(iterator)

- STL 컨테이너에 저장된 요소를 반복적으로 순회하여, 각각의 요소에 대한 접근을 제공하는 객체.
- 컨테이너의 구조나 원소의 자료형과는 상관없이 컨테이너에 저장된 데이터를 순회.



 

# 반복자의 특징

1. 원소를 주소를 통해 접근. 따라서 참조 연산자(*)가 정의되어있다.

2. 반복자 끼리의 대입 연산, 비교 연산이 가능.

3. 증가 연산자(++)를 통해 다음 원소로 이동.



# 반복자의 종류

1. 입력 반복자(input iterator)
   - 읽기만 가능, 순방향 이동, 현 위치의 원소를 한 번만 읽을 수 있는 반복자

2. 출력 반복자(output iterator)
   - 쓰기만 가능, 순방향 이동, 현 위치의 원소를 한 번만 쓸 수 있는 반복자

3. 순방향 반복자(forward iterator)
   - 읽기/쓰기 모두 가능, 순방향 이동(++)이 가능한 재할당될 수 있는 반복자

4. 양방향 반복자(bidirectional iterator)
   - 읽기/쓰기 모두 가능, 순/역 방향 이동(++, --)이 가능한 반복자 

5. 임의 접근 반복자(random access iterator)
   - 읽기/쓰기 모두 가능, 임의 접근, 양방향 반복자 기능과 +, -, += , -=, [] 연산이 가능

|       반복자의 기능       | 입력 | 출력 | 순방향 | 양방향 | 임의 접근 |
| :-----------------------: | :--: | :--: | :----: | :----: | :-------: |
|         접근(->)          |  ○   |  X   |   ○    |   ○    |     ○     |
|          읽기(*)          |  ○   |  X   |   ○    |   ○    |     ○     |
|          쓰기(*)          |  X   |  ○   |   ○    |   ○    |     ○     |
|      증가 연산자(++)      |  ○   |  ○   |   ○    |   ○    |     ○     |
|      감소 연산자(--)      |  X   |  X   |   X    |   ○    |     ○     |
|      첨자 연산자([])      |  X   |  X   |   X    |   X    |     ○     |
|     산술 연산자(+, -)     |  X   |  X   |   X    |   X    |     ○     |
| 산술 대입 연산자(+=, -=)  |  X   |  X   |   X    |   X    |     ○     |
| 관계 연산자(<, <=, >, >=) |  X   |  X   |   X    |   X    |     ○     |



# 예제1

```c++
#include <iostream>
#include <set>
#include <iterator>
using namespace std;
int main() {
	set<int> s;

	s.insert(10);
	s.insert(5);
	s.insert(1);
	s.insert(20);

	set<int>::iterator it1 = s.begin();
	set<int>::iterator it2 = s.end();
	while (it1 != it2) {
		cout << "*it1 : " << *it1 << endl;
		++it1;
	}
	cout << endl;


	return 0;
}
```



# 예제2

```c++
#include <iostream>
#include <vector>
#include <iterator>

using namespace std;

int main() {
	vector<int> v = { 10, 20, 30 };
	v.push_back(40);
	v.push_back(50);

	copy(v.begin(), v.end(), ostream_iterator<int>(cout, " "));

	return 0;
}
```

