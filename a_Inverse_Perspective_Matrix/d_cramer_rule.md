# Cramer's Rule
- 대학과정 이상에서는 복잡한 연립방정식을 풀게된다.
- 보통 연립방정식, 행렬식을 푸는데는 대치법, 가우스소거법, 크래머 공식 등 다양한 방법이있다.

![image](https://user-images.githubusercontent.com/69780812/146302835-b5ce052c-af69-476b-952b-fcdc2937138c.png)
- n까지 있는 연립방정식을 푼다고 가정해보자.

![image](https://user-images.githubusercontent.com/69780812/146302888-099736d9-b26c-488f-9ec8-e12f0d4852b5.png)
- 이를 쉽게 풀기 위해 B = AX 형식으로 행렬 연산을 나타낸다.

![image](https://user-images.githubusercontent.com/69780812/146303142-4a4d9462-1dfa-4429-98bc-e7d3a3382461.png)
- 여기서 A는 n x n  정방행렬이고, X와 B는 nx1 열 벡터다.

![image](https://user-images.githubusercontent.com/69780812/146303182-55c830b7-8bb9-4138-9314-bda5a9ad724d.png)
- 각각의 해는 위와 같이 표현이 가능하다.
- 세모 : A의 행렬식 값
- 세모_n : A에서 제 n열의 값을 B로 바꾼 행렬식 값

## Condition
- B = AX
  - B가 영행렬이면 동차, 그렇지 않으면 비동차라한다.
- A가 정칙행렬 즉, 역행렬이 존재하는 경우에는 비동차연립일차방정식으로 AX=B는 유일한 해를 가지게 된다.
- 위와 같은 조건이 만족하면 크래머 공식이 성립한다.

### Ex
![image](https://user-images.githubusercontent.com/69780812/146303416-ad40fe35-db0b-4c58-8861-e17122c46788.png)
- 간단히 3개의 연립방정식을 푼다고 해보자.

![image](https://user-images.githubusercontent.com/69780812/146303453-7fa87758-127e-4e06-84fa-bfd8498c3a83.png)
- 행렬식으로 표현하면 위와 같다.
- 여기서 B는 0행ㄹㄹ이 아님에 주목한다.
- A 행렬은 역행식 값이 0이 아니므로 정칙행렬이다.

![image](https://user-images.githubusercontent.com/69780812/146303804-302e418c-1881-47e0-a2c8-d3b2c804f8c2.png)
- 위식을 이용해 행렬식을 구한다.

![image](https://user-images.githubusercontent.com/69780812/146303518-28e33123-3228-4178-8276-6ba2456fe469.png)

![image](https://user-images.githubusercontent.com/69780812/146303554-8a8d7a78-e892-439c-8f0c-8951cb83c72b.png)
- 두 조건을 만족하면 크래머 공식을 이용해 해를 구하면 된다.

![image](https://user-images.githubusercontent.com/69780812/146303924-348368c8-0a23-4085-ab47-e1b929cd0897.png)
- 결과는 위와 같다.

# Reference
- https://carstart.tistory.com/160