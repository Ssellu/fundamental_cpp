# const 객체

- 객체 선언 시 앞에 **const** 키워드를 붙인 것

- const 객체는 멤버변수를 **수정**할 수 없고 **보기**만 가능.

  ```c++
  #include <iostream>
  
  using namespace std;
  
  class Foo
  {
  public:
  	int m_value; // Foo 의 멤버
  };
  
  int main() 
  {
  	
  	// 일반적인 객체
  	Foo foo1;
  	foo1.m_value = 10;
  	cout << "foo1 : " << foo1.m_value << endl;
  	
  	// const 객체
  	const Foo foo2;
  	foo2.m_value = 10;  // 에러!
  	cout << "foo2 : " << foo2.m_value << endl; // 보는 건 가능
  
  	return 0;
  }
  ```

  

- const 객체는 일반 멤버메서드를 실행할 수 없음. (내부에서 멤버변수의 값 변경이 일어날 우려가 있기 때문) 

  ```c++
  #include <iostream>
  
  using namespace std;
  
  class Foo
  {
  public:
  	int m_value;
      
      // 메서드 추가
  	void printValue() 
  	{
  		cout << "value : " << m_value << endl;
  	}
  };
  
  int main() 
  {
  	
  	// 일반적인 객체
  	Foo foo1;
  	foo1.m_value = 10;
  	foo1.printValue();
  	
  	// const 객체
  	const Foo foo2;
  	foo2.m_value = 10;  // 에러!
  	foo2.printValue();  // 에러!
  
  	return 0;
  }
  ```

- const 키워드가 추가된 메서드만 실행 가능.

  ```c++
  #include <iostream>
  
  using namespace std;
  
  class Foo
  {
  public:
  	int m_value;
  	void printValue() const // 이 부분에 const를 추가한다.
  	{
  		cout << "value : " << m_value << endl;
  	}
  };
  
  int main() 
  {
  	
  	// 일반적인 객체
  	Foo foo1;
  	foo1.m_value = 10;
  	foo1.printValue();
  	
  	// const 객체
  	const Foo foo2;
  	foo2.m_value = 10;  // 에러!
  	foo2.printValue();  // 정상
  
  
  
  	return 0;
  }
  ```

  