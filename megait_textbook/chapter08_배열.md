# 배열

- c 스타일의 배열 사용 가능
- c++에서는 array 자료형(클래스)이 있음 

# &lt;array&gt; 의  std::array

```c++
#include <iostream>
#include <array> // std::array

using namespace std;

int main() {


	// 일반 적인 배열
	int arr1[5] = { 10,20,30,40,50 };

	// std::array
	array<int, 5> arr2 = { 10, 20, 30, 40, 50};

	cout << arr2[0] << endl;		// 10
	cout << arr2.at(0) << endl;		// 10

	return 0;
}
```

> 10
> 10
> Press any key to continue . . .



# 배열의 크기

```c++
#include <iostream>
#include <array>

using namespace std;

int main() {

	array<int, 10> arr2 = { 10, 20, 30, 40, 50, 60 };
	int size = arr2.size();
	cout << "arr2의 원소 개수 : " << size << endl;

	return 0;
}
```

> arr2의 원소 개수 : 10
> Press any key to continue . . .



# 배열의 반복처리

```c++
#include <iostream>
#include <array>

using namespace std;

int main() {

	array<int, 10> my_array = { 10, 20, 30, 40, 50, 60 };

	// 방법1
	cout << "for : ";
	for (int i = 0; i < my_array.size(); ++i) {
		cout << my_array[i] << " ";
	}
	cout << endl;

	// 방법2
	cout << "enhanced for (복사) : ";
	for(auto element: my_array) {
		cout << element << " ";
	}
	cout << endl;

	// 방법3
	cout << "enhanced for (참조) : ";
	for (auto& element : my_array) {
		cout << element << " ";
	}
	cout << endl;

	return 0;
}
```

> for : 10 20 30 40 50 60 0 0 0 0
> enhanced for (복사) : 10 20 30 40 50 60 0 0 0 0
> enhanced for (참조) : 10 20 30 40 50 60 0 0 0 0
> Press any key to continue . . .



# enhanced for - 일반 변수 vs 참조 변수 차이점

```c++
#include <iostream>
#include <array>
using namespace std;

int main() {

	array<int, 3> my_array = { 10, 20, 30 };

	for(auto element: my_array) {
		element = 0;
	}

	cout << my_array[0] << endl;  // 10
	cout << my_array[1] << endl;  // 20
	cout << my_array[2] << endl;  // 30

	for (auto &element : my_array) {
		element = 0;
	}

	cout << my_array[0] << endl;  // 0
	cout << my_array[1] << endl;  // 0
	cout << my_array[2] << endl;  // 0


	return 0;
}
```



# 배열의 정렬 

- `<algorithm>`의 **std::sort()**

```c++
#include <iostream>
#include <array>
#include <algorithm>

using namespace std;

int main() {

	array<int, 10> my_array = { 7,8,1,3,2,5,8,10,2,3 };


	cout << "----변환 전----" << endl;
	for (auto element : my_array) {
		cout << element << " ";
	}
	cout << endl;

	// 오름차순 정렬
	sort(my_array.begin(), my_array.end());

	// 내림차순 정렬
	// sort(my_array.rbegin(), my_array.rend());

	cout << "----변환 후----" << endl;
	for (auto element : my_array) {
		cout << element << " ";
	}
	cout << endl;

	return 0;
}
```

> (오름차순 정렬 실행 시)
>
> ----변환 전----
> 7 8 1 3 2 5 8 10 2 3
> ----변환 후----
> 1 2 2 3 3 5 7 8 8 10
> Press any key to continue . . .



> (내림차순 정렬 실행 시)
>
> ----변환 전----
> 7 8 1 3 2 5 8 10 2 3
> ----변환 후----
> 10 8 8 7 5 3 3 2 2 1
> Press any key to continue . . .



# 동적 배열 - std::vector (아주 중요!)

- 무제한 배열 (동적으로 메모리를 할당하므로, 무한 추가/삭제 가능)
- 메모리 누수가 일어나지 않는다. (자동으로 delete 실행 됨)





## std::vector 생성

> ### std::vector<자료형> 변수명;
>
> ### std::vector<자료형> 변수명 = { 원소, 원소, 원소 };
>
> ### std::vector<자료형> 변수명{ 원소, 원소, 원소 };

```c++
#include <iostream>
#include <vector> // vector

using namespace std;

int main() {

	vector<int> v1;						// 0칸 생성
	vector<int> v2 = { 10, 20, 30 };	// 3칸 생성
	vector<int> v3{ 10, 20, 30, 40, 50 };// 5칸 생성 
	// vector<int> v4( 10, 20, 30, 40, 50 ); // 에러!


	// vector의 크기 
	cout << "v1의 크기 : " << v1.size() << endl;
	cout << "v2의 크기 : " << v2.size() << endl;
	cout << "v3의 크기 : " << v3.size() << endl;

	return 0;
}
```

> v1의 크기 : 0
> v2의 크기 : 3
> v3의 크기 : 5
> Press any key to continue . . .



## std::vector의 원소 변경 (배열과 동일)

```c++
#include <iostream>
#include <vector> // vector

using namespace std;

int main() {

	vector<int> v = { 10, 20, 30 };	// 3칸 생성

	for (auto &element : v) {
		cout << element << " ";
	}
	cout << endl;

	v[0] = 100;
	v[1] = 200;
	v[2] = 300;

	for (auto &element : v) {
		cout << element << " ";
	}
	cout << endl;
}
```

> 10 20 30
> 100 200 300
> Press any key to continue . . .



## std::vector의 길이 변경 (resize)

- vector 또한 배열과 마찬가지로 길이에 초과되는 원소를 추가할 수 없음

  ```c++
  #include <iostream>
  #include <vector> // vector
  
  using namespace std;
  
  int main() {
  
  	vector<int> v = { 10, 20, 30 };	// 3칸 생성
  
  	v[0] = 100;
  	v[1] = 200;
  	v[2] = 300;
  	// v[3] = 400; // 에러!!
      
      return 0;
  }
  ```

  

- resize() 함수를 사용하면 vector의 크기를 조절할 수 있음

  ```c++
  #include <iostream>
  #include <vector> // vector
  
  using namespace std;
  
  int main() {
  
  	vector<int> v = { 10, 20, 30 };	// 3칸 생성
  
  	v[0] = 100;
  	v[1] = 200;
  	v[2] = 300;
  	
  	v.resize(4);  // 이 부분!
  
  	v[3] = 400;
  
  	for (auto &e : v)
  		cout << e << endl;
      
      return 0;
  }
  ```
  
  > 100
  > 200
  > 300
  > 400
  > Press any key to continue . . .





## std::vector의 원소 추가 (push_back)

- 매번 리사이즈 후 값을 넣는 것이 귀찮다면

  ```c++
  #include <iostream>
  #include <vector>
  
  using namespace std;
  
  int main() {
      
  	vector<int> v = { 10, 20, 30 };
  	v.push_back(40); // 이 부분!
  	v.push_back(50); // 이 부분!
  	v.push_back(60); // 이 부분!
  
  	for (auto &e : v)
  		cout << e << " ";
  	cout << endl;
      
      return 0;
  }
  ```
  
  > 10 20 30 40 50 60
  > Press any key to continue . . .



## std::vector의 원소 삭제 (erase)

- 인덱스로 삭제

  ```c++
  #include <iostream>
  #include <vector>
  
  using namespace std;
  
  int main() {
  	vector<int> v = { 10, 20, 30, 40, 50, 60 };
  
  	v.erase(v.begin() + 0); // 0 번 원소를 삭제
  
  	for (auto &e : v)
  		cout << e << " ";
  	cout << endl;
  
      return 0;
  }
  ```
  
  

