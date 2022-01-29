# 2. 열거형 클래스

## 일반 enum의 문제점

```c++
#include <iostream>
using namespace std;

enum Day
{
	SUNDAY, MONDAY, TUESDAY, WENDESDAY, THURSDAY, FRIDAY, SATURDAY
};

enum Fruit
{
	APPLE, BANANA, MANGO
};
void main() 
{
	Day today = MONDAY;
	Fruit my_fav_fruit = BANANA;

	// MONDAY, BANANA 둘 다 1이므로 다음은 '참'이 나옴
	if (today == my_fav_fruit) 
		cout << "today와 my_fav_fruit은 같다." << endl;
    
    cout << "today : " << today << endl;
	cout << "my favorite fruit : " << my_fav_fruit << endl;
}
```

> 결과:
>
> today와 my_fav_fruit은 같다.
>
> today : 1
>
> my favorite fruit : 1



따라서 이러한 혼란을 줄이기 위해, `enum class(열거형 클래스)`을 사용할 수 있다. 

```c++
#include <iostream>
using namespace std;

enum class Day  // 이 부분!
{
	SUNDAY, MONDAY, TUESDAY, WENDESDAY, THURSDAY, FRIDAY, SATURDAY
};

enum class Fruit // 이 부분!
{
	APPLE, BANANA, MANGO
};
void ex01() 
{
	Day today = Day::MONDAY; // 이 부분!
	Fruit my_fav_fruit = Fruit::BANANA;  // 이 부분!

	// ** 이제는 자료형 자체가 다르므로 == 연산을 수행할 수 없다. (강제형변환을 한다면 가능)
    // if (today == my_fav_fruit) 
	//  	cout << "today와 my_fav_fruit은 같다." << endl;
    
    // ** '값' 또한 정하지 않았으므로 출력할 수 없다. (강제형변환을 한다면 가능)
    // cout << "today : " << today << endl;
	// cout << "my favorite fruit : " << my_fav_fruit << endl;
	
}

int main() {
	ex01();
	return 0;
}

```



