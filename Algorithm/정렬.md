# 정렬
> 데이터를 특정한 기준에 따라서 순서대로 나열하는 것
015432 → 012345

4가지 정렬 방법으로 오름차순을 예시로 작성했습니다.
- 선택 정렬
- 삽입 정렬
- 퀵 정렬
- 계수 정렬

### 선택 정렬
> 매번 가장 작은 것을 선택한다
시간복잡도 : O(n^2)

```python
num_list = [7,5,9,0,3,1,6,2,4,8]
for i in range(len(num_list)):
    min_index = i
    for j in range(i+1,len(num_list)):
    if num_list[j] < num_list[min_index]:
        min_index = j # for문을 돌면서 가장 작은 숫자 정의
    num_list[i],num_list[min_index] = num_list[min_index], num_list[i]
    # 가장 작은 숫자로 정의된 값을 리스트의 작은 인덱스 부터 쌓아간다.

print(num_list)
```

### 삽입 정렬
> 특정한 데이터를 적절한 위치에 삽입한다는 의미
선택 정렬에 비해 실행 시간 측면에서 더 효율적인 알고리즘
시간 복잡도 : O(N^2)

리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작한다.

```python
num_list = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(num_list)):
    for j in reversed(range(i)):
    if num_list[j] < num_list[j-1]:
        num_list[j],num_list[j-1] = num_list[j-1],num_list[j]
    else:
        break

print(num_list)
```

### 퀵 정렬
> 기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법
일반적인 상황에서 가장 많이 사용되는 정렬 알고리즘 중 하나\
병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘\
가장 기본적인 퀵 정렬은 첫 번째 데이터를 기준 데이터(Pivot)로 설정\
재귀적으로 수행된다.\
시간 복잡도 : O(NlogN)\
하지만 최악의 경우 O(N^2)의 시간 복잡도를 가진다.(이미 정렬된 배열에 대해서 퀵 정렬을 수행할 때)

<details>
<summary>동작 과정</summary>
<div markdown=“1”>

![](https://images.velog.io/images/tonic523/post/aac4c3e1-f19a-4822-9c5f-9baa115aa6ac/image.png)![](https://images.velog.io/images/tonic523/post/64a46dd7-1b1c-46b4-98a6-76a613087229/image.png)
  
</div>
</details>

<details>
<summary>구현 코드</summary>
<div markdown=“1”>

```python
'''
1. 피벗을 정한다.
2. 피벗보다 작은 값을 왼쪽으로, 큰 값을 오른쪽으로 정렬한다.
3. 왼쪽과 오른쪽으로 정렬된 리스트를 위와 같은 방법으로 실행한다.
4. 만약 리스트가 1보다 같거나 작다면 더이상 1,2번을 실행하지 않는다.
'''
  def quick_sort(array):
      if len(array) <= 1:
          return array
      pivot = array[0]
      tail = array[1:]
      left_side = [x for x in tail if x <= pivot]
      right_side = [x for x in tail if x > pivot]
      return quick_sort(left_side) + [pivot] + quick_sort(right_side)

  num_list = [7,5,9,0,3,1,6,2,4,8]

  print(quick_sort(num_list))
```
  
</div>
</details>

### 계수 정렬
> 특정한 조건이 부합할 때만 사용할 수 있지만 매우 빠르게 동작하는 정렬 알고리즘
데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능
데이터의 갯수가 N, 데이터(양수) 중 최대값이 K일 때 최악의 경우에도 수행 시간 O(N+K)를 보장한다.
때에 따라서 심각한 비효율성을 초래할 수 있다.

**비효율적일 때**
데이터과 0과 999999로 단 2개만 존재할 경우
**효율적일 때**
계수 정렬은 동일한 값을 가지는 데이터가 여러 개 등장할 때 효과적으로 사용할 수 있다.
성적의 경우 100점을 맞은 학생이 여러 명일 수 있다.

<details>
<summary>동작 과정</summary>
<div markdown=“1”>

![](https://images.velog.io/images/tonic523/post/835a5429-1a71-42fb-9f90-761f979dc054/image.png)
  
</div>
</details>

<details>
<summary>구현 코드</summary>
<div markdown=“1”>

```python
array = [7,5,9,0,3,1,6,2,9,1,4,8,0,5,2]

count = [0] * (max(array)+1)

for i in range(len(array)):
    count[array[i]] += 1

    for i in range(len(count)):
        for j in range(count[i]):
            print(i, end=' ')
```

</div>
</details>

> 4가지 정렬 알고리즘 비교

![](https://images.velog.io/images/tonic523/post/7f903449-d35a-4552-aa02-cbcabfad36c1/image.png)

- 추가적으로 대부분의 프로그래밍 언어에서 지원하는 표준 정렬 라이브러리는 최악의 경우에도 O(NlogN)을 보장하도록 설계되어 있다.

`참고 자료`\
[[한빛미디어] 이것이 취업을 위한 코딩 테스트다 with 파이썬 (나동빈 저)](https://www.youtube.com/watch?v=KGyK-pNvWos)