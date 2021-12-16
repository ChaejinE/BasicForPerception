# Perspective Projection
![image](https://user-images.githubusercontent.com/69780812/146289111-89f74ff6-7076-4f15-a781-1b9022617c91.png)
- 왼쪽 이미지를 오른쪽 이미지 처럼 변화시키는 것이라고 생각하면 된다.
- 이미지를 바로 잡는 것이 아니라 이미지가 투영되는 면을 변화시키는 것이다.

![image](https://user-images.githubusercontent.com/69780812/146289184-cf95d44f-ddf8-4543-a9c8-82e4b5884a6a.png)
- 연보라색 면이 상이 맺히는 곳이라고 할 때, Perspective transform은 **보라색 면을 이동시킨 것 같은 효과**를 주기 위해 사용한다.

## Projection matrix
![image](https://user-images.githubusercontent.com/69780812/146289412-ca0b613b-3eb3-4722-843a-790cf83f034d.png)
- Perspective Transform을 위한 식이다.
- homogenious coordinate를 사용하고 있으므로 x', y'에 대한 식은 아래와 같다.

![image](https://user-images.githubusercontent.com/69780812/146289481-fa39a16e-e910-4747-88f1-cc7bd4886f84.png)

![image](https://user-images.githubusercontent.com/69780812/146289506-f2e0dbd3-9eda-46ca-82d9-c89965afe9c2.png)
- 정리하면 위와 같은 꼴로 만들 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146289626-6e619e84-aab0-43fe-aec4-0f60a0dfc572.png)
- 값을 **알고 싶은 변수들은 a, b, c, d, e, f, g, h (8개)** 이므로 **x, y와 그에 대응되는 x', y' 쌍을 4개**만 알고 있으면 projection matrix를 구할 수 있다.
- 8x8 matrix의 inverse matrix를 구하여 matrix에 곱해주면 되겠다.

# Implementation of Perspective projection
- Perspective Matrix 구현을 위해서는 Matrix Multiplication과 inverse를 위한 인터페이스가 필요하다.
- Matrix multiplication : 서로 곱할 수 있는 형식인지 Check 후 단순 계산
- Inverse : guass elimination을 통해 reduced row echelon form으로 만들어주는 것을 통해 구해낸다.
- 이후 warping만 구현하면 된다.

## forward mapping
- src의 x, y 좌표에 대해 dst의 x', y'을 계산한 뒤 채워주는 방식이다.

```
for ( y = 0; y < height ; y++)
    for (x = 0; x < width; x++)
        x' = (ax+by+c) / (gx+hy+1);
        y' = (dx+ey+f) / (gx+hy+1);
        dst[y'][x'] = src[y][x];
```
- pseudo code로 표현하면 위와 같이 표현할 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146308428-bc3b0a0b-60bc-4732-b7ba-d36916c8c649.png)
- 막상 구현하면 위와 같이 hole이 발생하는 것을 확인할 수 있다.

## backward mapping
- 위의 hole을 방지하기 위한 방법중 하나다.
- forward warping에서 src의 좌표를 기준으로 dst 좌표를 계산했다면, dst 좌표를 기준으로 src의 좌표를 계산하는 것이다.

```
for (y' = 0; y' < height; y'++)
    for (x' = 0; x' < width; x'++)
        x = (ax'+by'+c) / (gx'+hy'+1);
        y = (dx'+ey'+f) / (gx'+hy'+1);
        dst[y'][x'] = src[y][x];
```
- pseudo code로 표현하면 위와 같다.

![image](https://user-images.githubusercontent.com/69780812/146308673-4d11ad3c-4f3e-4d59-8aaf-ad995776ccd6.png)
- hole은 없애주지만 아주 깔끔한 결과가 나오지는 않는다.

## forward (or backward) warping with interpolation
- forward warping : hole 발생
- backward warping : 화질 저하
  - interploation 을 통해 개선할 수 있다.

![image](https://user-images.githubusercontent.com/69780812/146308774-a77e8edd-3978-4477-a5f8-acd2588de368.png)
- forward warping + linear interpolation을 사용한 사진이다.
- hole이 줄긴했지만 여전히 존재한다.

![image](https://user-images.githubusercontent.com/69780812/146308830-9983817a-7f46-44c9-a5c1-ecd9e0f146be.png)
- backward warping + linear interpolation을 사용한 사진이다.
- hole도 없고 보기에도 상당히 괜찮아 진 것을 확인할 수 있다.

# Reference
- https://github.com/Tee0125/snippet/tree/master/perspective_projection
- https://b.mytears.org/2007/10/599/