# 매개변수의 기본값

- 매개변수에 기본값을 부여하면 인자값을 생략해도 된다.

  ```c++
  #include <iostream>
  
  using namespace std;
  
  
  void doSomething(int x = 10, int y = 20, int z = 30) {
  	cout << "x : " << x << endl;
  	cout << "y : " << y << endl;
  	cout << "z : " << z << endl;
  	cout << endl;
  }
  
  int main(){
  
  	doSomething();
  	doSomething(100);
  	doSomething(100, 200);
  	doSomething(100, 200, 300);
  
  	return 0;
  }
  ```

  > x : 10
  > y : 20
  > z : 30
  >
  > x : 100
  > y : 20
  > z : 30
  >
  > x : 100
  > y : 200
  > z : 30
  >
  > x : 100
  > y : 200
  > z : 300
  >
  > Press any key to continue . . .



- 단, 함수를 선언하는 경우 **함수 정의**, **함수 선언** 중 **둘 중 한 곳에만** 기본값을 부여해야 한다.

  ```c++
  #include <iostream>
  
  using namespace std;
  
  void doSomething(int x = 10, int y = 20, int z = 30);  
  
  void doSomething(int x = 10, int y = 20, int z = 30) { // 에러
  	cout << "x : " << x << endl;
  	cout << "y : " << y << endl;
  	cout << "z : " << z << endl;
  	cout << endl;
  }
  
  int main(){
  
  	doSomething();
  	doSomething(100);
  	doSomething(100, 200);
  	doSomething(100, 200, 300);
  
  	return 0;
  }
  ```

  ```c++
  #include <iostream>
  
  using namespace std;
  
  void doSomething(int x, int y, int z);  // 이렇게
  
  void doSomething(int x = 10, int y = 20, int z = 30) {
  	cout << "x : " << x << endl;
  	cout << "y : " << y << endl;
  	cout << "z : " << z << endl;
  	cout << endl;
  }
  
  ...
  ```

  ```c++
  #include <iostream>
  
  using namespace std;
  
  void doSomething(int x = 10, int y = 20, int z = 30);
  
  void doSomething(int x, int y, int z) { // 혹은 이렇게
  	cout << "x : " << x << endl;
  	cout << "y : " << y << endl;
  	cout << "z : " << z << endl;
  	cout << endl;
  }
  
  ...
  ```

  

- 기본값을 모두 부여해야 할 필요는 없다.

  ```C++
  #include <iostream>
  
  using namespace std;
  
  void doSomething(int x, int y, int z = 30) {
  	cout << "x : " << x << endl;
  	cout << "y : " << y << endl;
  	cout << "z : " << z << endl;
  	cout << endl;
  }
  
  int main(){
  
  	// doSomething();  		// 에러
  	// doSomething(100);	// 에러
  	doSomething(100, 200);
  	doSomething(100, 200, 300);
  
  	return 0;
  }
  ```

  > x : 100
  > y : 200
  > z : 30
  >
  > x : 100
  > y : 200
  > z : 300
  >
  > Press any key to continue . . .



- 단, 부분적으로 기본값으로 부여한다면 마지막 매개변수에 기본값을 꼭 부여해야 하고, 중간 중간 기본값을 부여하는 행위는 안된다.

  ```c++
  void doSomething(int x = 10, int y = 20, int z = 30) {..}  // 됨
  void doSomething(int x, 	 int y = 20, int z = 30) {..}  // 됨
  void doSomething(int x, 	 int y, 	 int z = 30) {..}  // 됨
  void doSomething(int x = 10, int y, 	 int z = 30) {..}  // 안됨
  void doSomething(int x = 10, int y = 20, int z	   ) {..}  // 안됨
  ...
  ```

  



# 생각해보기

```c++
#include <iostream>

using namespace std;

void doSomething(int x){}
void doSomething(int x, int y = 0) {}

int main(){

	// 이건 되는데..
	doSomething(10, 20); 
	

	// 이 둘은 왜 안될까?
	doSomething(10);
	doSomething();

	return 0;
}
```

