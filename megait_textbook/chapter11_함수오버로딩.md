# 함수 오버로딩 

- 같은 이름의 함수를 여러 버전으로 정의하는 것.

알다시피 **매개변수와 인자값은 반드시 그들의 자료형과 개수가 서로 일치해야 한다.**

```c++
void doSomething(int a, int b) { ... }
```

이러한 함수가 있을 때, 이 함수를 실행하려면 반드시 정수 2개를 넣어야 한다.



```c++
doSomething(); 			// 에러!
doSomething(10); 		// 에러!
doSomething(10, 20); 	// 가능
doSomething(10, 20, 30);// 에러!
```



이때 같은 이름의 함수를 여러 개 정의하면 위 에러를 해결할 수 있다.

이를 함수 오버로딩(Overloading)이라고 한다.

```c++
void doSomething() { ... }
void doSomething(int a) { ... }
void doSomething(int a, int b) { ... }
void doSomething(int a, int b, int c) { ... }
```



```c++
#include <iostream>

using namespace std;

int addTwoNums(int a, int b) {
	cout << "addTwoNums(int, int) 실행!" << endl;
	return a + b;
}
double addTwoNums(double a, double b) {
	cout << "addTwoNums(double, double) 실행!" << endl;
	return a + b;
}
float addTwoNums(float a, float b) {
	cout << "addTwoNums(float, float) 실행!" << endl;
	return a + b;
}
int main() 
{
	cout << addTwoNums(10  , 20) << endl;
	cout << addTwoNums(10. , 20.) << endl;
	cout << addTwoNums(10.f, 20.f) << endl;
	return 0;
}
```

> addTwoNums(int, int) 실행!
> 30
> addTwoNums(double, double) 실행!
> 30
> addTwoNums(float, float) 실행!
> 30
> Press any key to continue . . .



# 오버로드의 목적

- 내가 만든 함수를 사용할 다른 개발자의 편의를 위한 것.

- 여러 개의 함수를 정의하는 것은 똑같지만, 비슷한 작업을 한다면 이름을 통일 시키는 것이 함수 호출 입장에서 안 헷갈림.

  ```c++
  int addTwoInt(int a, int b) {
      return a + b;
  }
  double addTwoDouble(double a, double b) {
      return a + b;
  }
  float addTwoFloat(float a, float b) {
      return a + b;
  }
  ```

  ```c++
  int		res1 = addTwoInt(10, 20); 
  double	res2 = addTwoDouble(1.1, 2.2); 
  float	res3 = addTwoFloat(1.1f, 2.2f); 
  ```

  

  보다

  ```c++
  int addTwoNums(int a, int b) {
      return a + b;
  }
  double addTwoNums(double a, double b) {
      return a + b;
  }
  float addTwoNums(float a, float b) {
      return a + b;
  }
  ```

  ```c++
  int		res1 = addTwoNums(10, 20); 
  double	res2 = addTwoNums(1.1, 2.2); 
  float	res3 = addTwoNums(1.1f, 2.2f); 
  ```

  이게 낫다!!

  

# 오버로드 주의사항

1. 오버로드 작성할 때는 매개변수의 자료형이나 개수에 차이점을 두어야 한다. 

   함수 호출 시에 어떤 함수를 실행할 지 고를 수 있는 뚜렷한 기준은 **함께 넣어주는 인자값의 개수와 자료형**이기때문이다.

2. 리턴값은 오버로드와 상관없다. 따라서 리턴자료형은 같아도 되고 달라도 된다.

   ```c++
   void aa() {..}		
   int aa(char a){..}  // 됨
   void aa(int a){..}  // 됨
   ```

   

3. 단, 리턴자료형이 다르다고 해서 오버로드 되는 것은 아님. 무조건 1번 조항을 따름!

   ```c++
   void aa(int x){ .. }
   int  aa(int x){ .. } // 안됨 
   ```

   

4. 매개변수 이름이 다른 것도 오버로드와 상관없다. 자료형과 개수에만 집중됨.

   ```c++
   void aa(int a){..}
   void aa(int x){..} // 에러
   ```

5. 모호한 호출은 에러가 발생한다.

   ```c++
   // void aa(int a) { .. } // 이 함수가 없다면
   double aa(double a) { .. }
   int aa(unsigned int a) { .. }
   ```

   ```c++
   aa(10);					// 에러! (double과 unsigned int 모두 적용 가능하므로 모호함)
   aa((double)10);   		// 됨
   aa((unsigned int)10); 	// 됨
   ```

   







