# 변수

- c언어 사용방법과 동일
- 초기화 안된 변수 
  - Dedug 모드 : 에러, 쓰레기값
  - Release 모드 : 0으로 변경 (좋은 거 아님)
- 초기화 방법 2가지
  1. int a = 10;
  2. int b(10);



# 자료형

| Group                    | 이름                         | 사이즈                                             |
| ------------------------ | ---------------------------- | -------------------------------------------------- |
| Character types          | **char**                     | Exactly one byte in size. At least 8 bits.         |
|                          | **char16_t**                 | Not smaller than `char`. At least 16 bits.         |
|                          | **char32_t**                 | Not smaller than `char16_t`. At least 32 bits.     |
|                          | **wchar_t**                  | Can represent the largest supported character set. |
| Integer types (signed)   | **signed char**              | Same size as `char`. At least 8 bits.              |
|                          | *signed* **short** *int      | Not smaller than `char`. At least 16 bits.         |
|                          | *signed* **int**             | Not smaller than `short`. At least 16 bits.        |
|                          | *signed* **long** *int*      | Not smaller than `int`. At least 32 bits.          |
|                          | *signed* **long long** *int* | Not smaller than `long`. At least 64 bits.         |
| Integer types (unsigned) | **unsigned char**            | (same size as their signed counterparts)           |
|                          | **unsigned short** *int*     |                                                    |
|                          | **unsigned** *int*           |                                                    |
|                          | **unsigned long** *int*      |                                                    |
|                          | **unsigned long long** *int* |                                                    |
| Floating-point types     | **float**                    |                                                    |
|                          | **double**                   | Precision not less than `float`                    |
|                          | **long double**              | Precision not less than `double`                   |
| Boolean type             | **bool**                     |                                                    |
| Void type                | **void**                     | no storage                                         |
| Null pointer             | **decltype(nullptr)**        |                                                    |

출처 https://www.cplusplus.com/doc/tutorial/variables/

