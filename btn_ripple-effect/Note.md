## 버튼 물결 효과의 원리
1. button 레이어 위로 :after 속성 활용, 원 그리기
2. 원의 중심 : 버튼 내 마우스 클릭한 위치로 잡음
3. 원의 반지름 : 버튼의 한쪽 끝부터 반대쪽 대각선 끝

### button레이어 위로 : after 속성 활용, 원 그리기
- 반지름 영어로 ? radius / 지름 ? diameter 
- position / transform
- 마우스 포인터 / clientX
- 원의 반지름 : 중심~끝점 / 원의 지름 : 끝점 ~ 끝점
- 원의 반지름 길이 : 직사각형 대각선 길이 관련 JS 공식 -> Radius : Math.sqrt( W*W + H*H)
- Math.sqrt() : 대각선 길이 구하는 공식을 사용한 이유 -> **대각선이 버튼의 가장 긴 거리**임
- 원의 반지름을 기준으로 사각형(버튼)의 대각선 길이 구했기 때문에 이후 radius*2 가 필요한 거임

#### 원의 크기가 버튼 전체를 덮을만큼 커야함
- 이유 : **원이 버튼보다 작으면 애니메이션 되는 중 버튼 모서리까지 덮지 못함**

### 애니메이션의 경우
```
animation: ripple-effect 1000ms linear;
@keyframes ripple-effect {
  100% {
    transform: scale(1);
    opacity: 0;
  }
}
```
- 이런 식으로만 적용할 경우 1회성 애니메이션임


 /* (1) x: 버튼 왼쪽시작위치, width: 버튼 가로 길이
    clientX - x -> 버튼 x값 기준에서 얼마만큼의 지점을 클릭한 것인지 받아옴
    
    ex) clientX : 300, x : 200 -> 버튼의 어느 지점에서 클릭했어? 버튼 가로의 100지점에서 클릭(버튼 x시작 0)

    (2) radius 하는 이유; 원의 중심을 클릭 위치에 맞추기 위함 ->  left를 원의 중심위치가 아닌, 원의 왼쪽 끝 위치를 의미하기 때문
    원의 중심이 클릭 위치보다 오른쪽으로 밀리게 될 때 원의 왼쪽 끝을 클릭 위치보다 반지름 만큼만 왼쪽으로 옮겨줘야 함


    정리 : 버튼 내 클릭한 위치를 구한 뒤, 원의 중심이 클릭 지점에 오도록 반지름만큼 왼쪽으로 뺌


    (3) width * 100 + '%' 하는 이유 : 
    - px 값을 %로 바꾸는 계산
    ex) 버튼 width 200px, 원의 왼쪽 위치가 50px이라면, left는 25%로 나옴

*/

/*
    const clickPositionButton = clientX - x;
    const circleStartPosition = clickPositionInButton = radius;
    const left = (circleStartPosition / buttonWidth) * 100 + '%';
*/

>  const { clientX, clientY } = e; // === const clientX = e.clientX
