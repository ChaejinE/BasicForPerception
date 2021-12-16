# Overview
- Echelon form은 **가우시안 소거법에 의한 결과의 모양**이다.
- Row echelon form은 **가우시안 소거 연산이 row에 대해서 수행**된 것이다.
- Column echelon form은 **가우시안 소거 연산이 cloumn에 대해서 수행**된 것이다.
  - row echelon form의 transpose 행렬이다.
  - 따라서 row echelon form만 고려되어 진다고 한다.

# Condition
1. 전체가 0으로 구성되지 않은 행이 있다면 처음으로 오는 0이 아닌 숫자는 1이어야한다.
  - 이 것을 leading 1이라고 부른다.
2. 전체가 0을 구성된 행이 있다면, 그것들을 모아 행렬의 가장 아래에 위치시킨다.
3. 전체가 0으로 구성되지 않은 2개 연속된 행에서 아래 행의 leading 1은 윗 행의 leading 1의 오른쪽에 있어야한다.
4. leading 1을 포함하는 각 열은 leading 1의 위아래가 0이어야한다.

![image](https://user-images.githubusercontent.com/69780812/146302163-4a869050-5247-4894-a1fb-e932fdd0f417.png)

![image](https://user-images.githubusercontent.com/69780812/146302194-1168c79a-18c6-45ac-9de0-ee6c8e07edfe.png)

![image](https://user-images.githubusercontent.com/69780812/146302217-ab776fe6-97a8-4a64-9fd5-f8ba119acfd8.png)

![image](https://user-images.githubusercontent.com/69780812/146302233-c300b9ff-1e40-403f-8d47-818e4a1a0aec.png)