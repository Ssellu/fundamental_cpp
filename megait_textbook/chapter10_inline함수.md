# inline 함수

- 함수는 매개변수, 리턴, 메모리 내부를 이동하는 일련의 과정으로 인해 

  일정량의 메모리와 시간을 더 소모하는 일종의 오버헤드가 발생한다.

  즉, 여러 개의 함수로 쪼개어 구현하는 것은 하나의 함수로 구현하는 것보다 메모리를 많이 쓰고, 시간도 더 걸린다는 것이다.

  ```c++
  void add(int a, int b)
  {	
      int c = a + b;
      return c;
  }
  
  int main(){
      cout << add(10, 20) << endl;
      cout << add(100, 200) << endl;
      cout << add(1000, 2000) << endl;
  }
  ```

  이것보다 

  ```c++
  int main(){
      cout << 10 + 20 << endl;
      cout << 100 + 200 << endl;
      cout << 1000 + 2000 << endl;
  }
  ```

  이것이 실제 실행속도가 훨씬 빠르다는 의미. (어쩌면 너무 당연함...)

  

- 하지만 설계적 관점으로 볼 때, 구현해야하는 기능이 여러가지라면 그만큼 여러 함수로 나누어 정의하는 것이 맞다.

  복잡한 기능을 수행하는 함수라면 함수 호출로 인해 발생하는 오버헤드는 상대적으로 중요하지 않지만, 

  기능이 짧고 간결한 함수에게는 무시할 수 없는 비용이다. 

  간혹 함수 호출을 준비하는 시간이 막상 함수를 실행하는 시간보다 훨씬 긴 경우도 있다. 

  이는 비효율적인 성능 저하로 이어진다.

- 그래서 C++은 **인라인 함수(inline function)**를 제공한다.

  컴파일러가 코드를 컴파일하는 중에 함수 호출 부분을 함수 자체의 내용으로 대체한다. (이를 인-플레이스(in-place) 확장이라고 한다).  매개변수나 리턴이 필요 없도록 말이다.

```c++
#include <iostream>

using namespace std;

inline void print(int a, int b) 
{
	cout << a << endl;
	cout << b << endl;
}
int main() 
{
	print(10, 20);
	return 0;
}
```

> 10
> 20
> Press any key to continue . . .



위 코드는 컴파일하면 이러한 코드로 수정된다.

```c++
#include <iostream>

using namespace std;

int main() 
{
    cout << 10 << endl;
	cout << 20 << endl;
	return 0;
}
```

요즘은 inline이 많이 사용되지 않는다. 컴파일러가 적당한 함수들은 알아서 inline으로 만들어준다.