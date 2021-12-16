# Overview
- 연립 방정식을 푸는 방법 중 하나이다.

![image](https://user-images.githubusercontent.com/69780812/146304188-5425a145-dc43-409e-a6fb-19067129111c.png)
- 행렬에는 다양한 형태가 존재한다.
- 정방행렬 : 정사각형
- 일반행렬 : 직사각형
- LU분해 등으로 사용했던 삼각형

![image](https://user-images.githubusercontent.com/69780812/146304298-449498e3-0105-4bc4-b193-74bc29733353.png)
- 위 그림과 같은 형태를 사다리꼴이라 한다.
- 기약 행 사다리꼴(RREF Reduced Row Echelon Fomr) 성질
  - 1. 만약 한 행의 원소가 전부 0 이아니면 행의 첫번째 0이 아닌 수는 1이다. (선행이라 부른다.)
  - 2. 만약 어떤 행들이 모두 0 으로 이루어져 있으면 그 행들은 모두 행렬의 아래 쪽 행에 놓여진다.
  - 3. 두 개의 연속된 행이 모두 0 이아니라면 아래 행에 있는 선행1이 윗 행에 있는 선행1의 오른쪽에 위치한다.
  - 4. 선행 1을 가진 열은 1을 제외한 다른 곳이 모두 0이다.
- 행 사다리꼴 (Row Echelon Form) 성질
  - 1, 2, 3의 성질을 만족하는 행렬이다.

# RREF
![image](https://user-images.githubusercontent.com/69780812/146304758-ac56fb03-5e76-4863-87b1-6a58b2773909.png)
- 1. 행의 원소가 전부 0이 아니고 0이아닌 첫번째 수는 1임을 알 수 있다.
  - 1, 2, 3번 째 그림, 4번의 모두 0인 것도 기약 행 사다리꼴에 들어간다.
- 2. 모두 0으로 이루어져 있으면 모두 행렬 아래 놓인다.
  - 3, 4번 째 그림
- 3. 두 개의 연속된 행이 모두 0이 아니면 아래 행에 있는 성행 1이 윗 행에 있는 선행의 오른쪽에 위치한다.
  - 1, 2, 3 참조 시 아래행의 선행이 윗행의 선행보다 오른쪽에 위치한다.
- 4. 선행 1을 가진 열은 다른 곳이 모두 0이다.
  - 1, 2, 3을 참조하면 무조건 선행의 위열과 아래열은 0이라는 것이다.

## 왜 이런 형태를 만든걸까?
- 이런 형태가 나오기는 사실 힘들다.
- 하지만, 기약 행 사다리꼴 형태로 된 행렬을 가지고 연립방정식을 구하기 매우 쉬워진다.

![image](https://user-images.githubusercontent.com/69780812/146305058-38a4b56b-4ae1-4c36-939d-17f57c50225d.png)
- 보통, 일반 행렬을 **기약 행 사다리꼴의 형태로 바꾸어서 빠르게 풀려고 배우는 것**이다.
- 기약 행 사다리꼴로 만든 것이 Gauss-Jordan Elimination, 행 사다리꼴로 만드는 것이 Gauss Elimination인 것이다.

# Gauss Elimination
![image](https://user-images.githubusercontent.com/69780812/146305169-45184e30-6fa8-4bcd-823a-01c9502f2cd0.png)
- 위와 같은 행렬을 가우스 소거 방식을 통해 구해보자.

![image](https://user-images.githubusercontent.com/69780812/146305184-8ea3f83e-9177-41d2-afb9-0aac96abc3b1.png)
- 1. 가장 왼쪽이 모두 0으로 이루어지지 않도록 행렬을 정리

![image](https://user-images.githubusercontent.com/69780812/146305452-87ab69ba-aa28-4d0c-9c3c-48170bb612f5.png)
- 2. 필요하다면 1단계에서 구한 열의 첫째 성분이 0이 되지 않도록 행의 위치를 바꾼다.

![image](https://user-images.githubusercontent.com/69780812/146305499-29edfab2-3075-42c9-83b9-da1ce6ee29fa.png)
- 3. 열의 첫째 성분이 1이 아니라면(A값이라고 가정) 선행 1을 얻기 위해 1/A를 곱해서 1로 만들어준다.

![image](https://user-images.githubusercontent.com/69780812/146305566-af2fbf16-726d-447f-8fda-e74ff1d77f2b.png)
- 4. 선행 아래 성분이 0이디도록 첫째행에 적당한 값을 곱해 아래 행들에 더한다.

![image](https://user-images.githubusercontent.com/69780812/146305622-3abe5c9c-65de-4353-8e36-ebf272a5448b.png)
- 첫째 행은 그대로 놔두고 나머지 행에 대해 1~4 단계를 적용한다.
- 행 사다리 꼴을 만든다.

# Gauss Jordan Elimination
![image](https://user-images.githubusercontent.com/69780812/146305749-ccf9cc3c-2955-467a-85f9-5702b4750974.png)
- Jordan은 한단계를 더 추가하여 기약 행 사다리꼴을 만들었다.
- 0이 아닌 가장 아래 행에서 시작해서 위 방향으로 실행한다.
- 선행 1의 위에 위치한 원소가 0이 되도록 각행에 적당한 수를 곱학 위에 있는 행에 더한다.

# Inverse Matrix Calcuation using the Gauss elimination
![image](https://user-images.githubusercontent.com/69780812/146306366-5ed3a8bb-d2ec-4aa4-850b-638de3f88954.png)

![image](https://user-images.githubusercontent.com/69780812/146306377-ae314e95-ac99-4aca-85cb-ba8bd2675f83.png)

![image](https://user-images.githubusercontent.com/69780812/146306397-2d6a5ff0-9447-40c9-97c5-1aefdfbabe14.png)
- **행렬 A의 값을 좌측**에 두고 같은 차수의 **단위 행렬을 우측**에 둔다.

![image](https://user-images.githubusercontent.com/69780812/146306436-4bd76ad0-fdfc-4639-be84-de71f7a91ad8.png)
- 1. 가장 위 행부터 시작한다.
- 0을 제외한 **첫번째에 위치한 행렬값을 1**로 맞출 수 있도록 모든 행에 같은 값을 곱해준다.
- 첫번째 행은 값이 1이므로 아무것도 수행하지 않는다.

![image](https://user-images.githubusercontent.com/69780812/146306522-39a0fb96-a971-4fc7-a1b5-25a4f8a0acd5.png)

![image](https://user-images.githubusercontent.com/69780812/146306539-5bf08640-3c8e-492a-a0a6-01dcfff9d2fb.png)
- 2. 1번 수행한 행에서 1로 변경된 행렬값과 동일한 열에 있는 행렬 값이 0이 올 수 있는 숫자 a를 각 행별로 구한 뒤 1번을 수행한 행에 모두 곱하여 다른 행들에게 위에서부터 차례대로 합연산을 수행한다.

![image](https://user-images.githubusercontent.com/69780812/146306709-80ba1c73-7112-4ce3-b6a5-9d743f036947.png)
- 2번째 행이 위와 같이 변경된다.

![image](https://user-images.githubusercontent.com/69780812/146306771-dc9d0d07-6b24-47a1-8ec8-e684bf9a9e2d.png)
- 이어서 3번째 행에대해서도 동일하게 연산을 수행한다.

![image](https://user-images.githubusercontent.com/69780812/146306804-7b6c394d-b43e-41d3-b5e9-233b8b46ad39.png)
- 3번째 행이 위와 같이 변경된다.
- 1번과 2번을 **좌측 행렬이 단위행렬이 나올 때까지 반복**하면된다.

![image](https://user-images.githubusercontent.com/69780812/146307058-009e5e74-5989-4720-a9b4-36cda1c21509.png)
- 1번

![image](https://user-images.githubusercontent.com/69780812/146307078-8d9ca19f-16ac-4de9-a373-8c973e9a7e8c.png)
- 2번

![image](https://user-images.githubusercontent.com/69780812/146307227-1fcee274-dbe5-4525-8608-a5a24ca8e821.png)
- 첫째 행 변경

![image](https://user-images.githubusercontent.com/69780812/146307246-c6add18e-c003-4e00-bf96-1f0a065eef39.png)
- 3번째 행의 첫번째 값과 두번째 값이 0이므로 1번은 건너뛰고 -1만 곱해주면된다.

![image](https://user-images.githubusercontent.com/69780812/146307303-f53d6e71-10d2-4d7f-920f-fcf6fd34661b.png)

![image](https://user-images.githubusercontent.com/69780812/146307346-105a3102-99f6-4708-94cc-6baab6f4690e.png)

![image](https://user-images.githubusercontent.com/69780812/146307363-8203f469-cc92-43f8-b4dc-703467adc5f7.png)

![image](https://user-images.githubusercontent.com/69780812/146308088-512133b8-ca38-486c-a056-bfd39cd2229d.png)
- 첫번째 행 변경

![image](https://user-images.githubusercontent.com/69780812/146307436-f5f54afa-d047-4a90-a069-b7b9f1962f48.png)
- 마지막으로 두번째 행을 변경해주면 된다.

![image](https://user-images.githubusercontent.com/69780812/146307537-913cade1-0475-4819-9c23-52d523baf74c.png)
- 연산종료
- 좌측 행렬이 단위행렬로 변경된다.
- **우측행렬이 바로 역행렬**이다.

# Reference
- https://carstart.tistory.com/164
- https://m.blog.naver.com/wndrlf2003/221549970389