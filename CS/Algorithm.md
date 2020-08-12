# Sorting Algorithms

아래에서 시각적으로 알고리즘의 차이를 볼 수 있다
https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html

## Big-O 표기법

## Ω 표기법


## Bubble Sort (버블 정렬)
> 자신이 오른쪽보다 작으면 가만히 있고 크면 오른쪽 요소와 자리를 바꾼다

pseudocode 는 다음과 같다
```
Repeat n–1 times

    For i from 0 to n–2

        If i'th and i+1'th elements out of order

            Swap them
```

중첩 루프를 돌아야 하고, n개의 값이 주어졌을 때 각 루프는 각각 n-1번, n-2번 반복되므로
$$(n-1)*(n-2) = n^2-3n+2$$
번의 비교 및 교환이 필요합니다.

여기서 가장 크기가 큰 요소는 n^2 이므로 위와 같은 코드로 작성한 버블 정렬 실행 시간의 상한은 O(n^2)이라고 말할 수 있습니다.

정렬이 되어 있는지 여부에 관계 없이 루프를 돌며 비교를 해야 하므로 위와 같은 코드로 작성한 버블 정렬의 실행 시간의 하한도 여전히 Ω(n^2)이 됩니다.

## Selection Sort (선택정렬)
> 자신을 기억하고 모든 요소를 찾은 뒤 가장 작은 요소를 자신과 자리바꿈 한다.

pseudocode 는 다음과 같다
```
For i from 0 to n–1

    Find smallest item between i'th item and last item

    Swap smallest item with i'th item
```

요소가 n개라면 맨 처음에 n 번 검색하고 그 다음에<br>
n-1 번 검색하고 그 다음에<br>
n-2 번 검색하고 그 다음에<br>
n-3 번 검색하고 이렇게 반복된다. 이것을 수식으로 하면 다음과 같다

$$n+(n-1)+(n-2)+ ... + 1$$
$$n(n+1)/2$$
$$n^2/2 + n/2$$
Big-O 표시법에서는 가장 큰 수가 중요하므로 
$$O(n^2)$$

## Merge Sort (병합 정렬)
> 원소가 한 개가 될 때까지 계속해서 반으로 나누다가 다시 합쳐나가며 정렬
> 원소들을 계속해서 좌우 반으로 나누다가 더 이상 나눌 수 없게 되면(요소가 한 개가 되면 나눌수 없음) 좌우를 병합