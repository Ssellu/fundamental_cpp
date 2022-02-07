# new와 delete 연산자
## new

> #### 문법1) 포인터변수 = new 자료형;  			  // 초기화 X
>
> #### 문법2) 포인터변수 = new 자료형();			 // 0으로 초기화. {}로 대체 가능
>
> #### 문법3) 포인터변수 = new 자료형(초기값);  // 초기값으로 초기화. {}로 대체 가능

- 동적할당
- heap 메모리에 할당
- 주소(참조)로 접근
- new의 결과값은 할당된 메모리의 **주소**

```c++
#include <iostream>
using namespace std;

int main() 
{
	int* ptr = new int(10);

	cout << ptr << endl;
	cout << *ptr << endl;

	delete ptr;

	return 0;
}
```

- `std::nothrow`
  - 동적메모리가 모두 차있는 상황에서 `new`를 수행하면 예외를 던짐. 이때, 예외를 던지는 대신 메모리 여유가 생길때까지 대기하도록 하는 설정. 

```c++
#include <iostream>
using namespace std;

int main()
{
	int* ptr = new (std::nothrow) int(10);  // 이 부분!

	cout << ptr << endl;
	cout << *ptr << endl;

	delete ptr;

	return 0;
}
```





## delete

- 프로세스 종료 전 동적메모리 해제에 사용
- delete 주소;
- new 로 할당된 메모리만 해제 가능
- 포인터변수가 해제되는 것이 아님. 포인터변수가 참조하고 있는 **도착지가 해제**됨

```c++
// 주의 사항
#include <iostream>
using namespace std;

int main() 
{
	int* ptr = new int(10);

	cout << ptr << endl;
	cout << *ptr << endl;

	delete ptr;
	
    cout << ptr << endl; // 이 부분! 주소는 여전히 있다. 다만 *ptr 이 안되는 것임
	return 0;
}
```



- 따라서 포인터 변수에 남아있던 쓰레기 주소도 지워주는 것이 좋다.

```c++
#include <iostream>
using namespace std;

int main() 
{
	int* ptr = new int(10);

	cout << ptr << endl;
	cout << *ptr << endl;

	delete ptr;
	
    ptr= nullptr;  // 이 부분! ptr 변수에 적혀있는 주소도 함께 지워주면 깔끔
    
    cout << ptr << endl;
	
    return 0;
}
```



## 동적 배열

> #### 방법1) 포인터변수 = new 자료형[길이];
>
> #### 방법2) 포인터변수 = new 자료형[길이]{};
>
> #### 방법3) 포인터변수 = new 자료형[길이]{원소, 원소, 원소, ...};

- 학생 수를 입력 받고 학생 수 만큼의 국어점수를 저장할 배열을 만들어보자. 

- 잘못된 예 - 정적 배열은 그 크기가 컴파일 시점에 결정되어야 한다. 

  ```c++
  #include <iostream>
  using namespace std;
  
  int main()
  {
  	int size;
  	
  	cout << "학생 수 : ";
  	cin >> size;
  	
  	int kr[size]; // 에러!
  
  	return 0;
  }
  ```

- 이렇게 해야 함

  ```c++
  #include <iostream>
  using namespace std;
  
  int main()
  {
  	int size;
  	
  	cout << "학생 수 : ";
  	cin >> size;
  	
  	int* kr = new int[size]();  // 이 부분! () 있으면 0으로 모두 초기화 없으면 초기화 X
  	
  
  	return 0;
  }
  ```

- 완성!

  ```c++
  #include <iostream>
  using namespace std;
  
  int main()
  {
  	int size;
  	
  	cout << "학생 수 : ";
  	cin >> size;
  	
  	int* kr = new int[size]();
  
  	for (int i = 0; i < size; ++i) {
  		cout << i + 1 << "번 째 학생 국어 : ";
  		cin >> kr[i];
  	}
  
  	for (int i = 0; i < size; ++i) {
  		cout << kr[i] << endl;
  	}
      delete[] kr;
  	return 0;
  }
  ```

  > 학생 수 : **4**
  > 1번 째 학생 국어 : **10**
  > 2번 째 학생 국어 : **88**
  > 3번 째 학생 국어 : **90**
  > 4번 째 학생 국어 : **75**
  > 10
  > 88
  > 90
  > 75
  > Press any key to continue . . .

- 동적 배열을 해제할 때는 ..

  ```c++
  delete[] 배열주소;
  ```

  
