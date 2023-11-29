# algorithms

> 질문과 답변은 [이 레포지토리](https://github.com/leegwae/algorithms)에 정리된 텍스트에 기반합니다. 자세한 내용은 해당 레포지토리를 참고하세요.

### 진법을 변환하는 함수를 작성해주세요?

```python
def to_alphabet(decimal: int) -> str:
  if decimal < 10:
      return str(decimal)

  return chr(decimal - 10 + ord('A'))

def to_decimal(alphabet: str) -> int:
  if alphabet.isdigit():
      return int(alphabet)

  return ord(alphabet) - ord('A') + 10

def convert(n: int, base: int):
  converted = ''

  while n > 0:
      converted += to_alphabet(n % base)
      n //= base

  return converted[::-1]

def convert(n: str, base: int):
  decimal = 0

  for i in range(len(n)):
      decimal += to_decimal(n[i]) * (base  (len(n) - i - 1))

  return decimal
```

### 분할 정복에 대해 설명해주세요?

문제를 부분 문제로 분할하고, 가장 작은 하위 문제부터 푼 후, 하위 문제의 답을 병합하여 기존 문제의 답을 푸는 방식이다.

### 정렬 알고리즘에 대해 알고 있나요?

정렬 알고리즘의 종류에 대해 말해주세요? 정렬 알고리즘은 요소들을 일정한 순서대로 나열하는 것이다. 선택 정렬, 삽입 정렬, 버블 정렬, 퀵 정렬, 힙 정렬, 합병 정렬 등이 있다.

### 선택 정렬에 대해 설명해주세요?

선택 정렬은 각 위치에서 어떤 요소를 넣을지 선택하는 정렬 알고리즘이다. 시간 복잡도는 `O(n^2)`이다.

```python
def sort(arr):
  for i in range(0, len(arr)-1):
    min_idx = i
    for j in range(i+1, len(arr)):
      if arr[min_idx] > arr[j]:
        min_idx = j
    arr[i], arr[min_idx] = arr[min_idx], arr[i]
```

### 삽입 정렬에 대해 설명해주세요?

삽입 정렬은 배열의 각 요소를 차례대로 그 앞의 원소들과 비교하여 삽입하는 정렬 알고리즘이다. 이미 정렬되어있는 경우라면 `n-1`번 비교하므로 `O(n)`이고 이 외의 경우는 `O(n^2)`이다.

```python
def sort(arr):
  for i in range(1, len(arr)):
    cur = arr[i]
    j = i - 1
    while j >= 0 and arr[j] > cur:
      arr[j + 1] = arr[j]
      j -= 1
    arr[j+1] = cur
```

### 버블 정렬에 대해 설명해주세요?

버블 정렬은 인접한 두 요소를 비교하여 정렬 기준대로 나열하는 정렬 알고리즘이다. 시간 복잡도는 `O(n^2)`이다.

```python
def sort(arr):
  for i in range(len(arr)-1, 0, -1):
    for j in range(0, i):
      if arr[j] > arr[j+1]:
        arr[j], arr[j+1] = arr[j+1], arr[j]
```

### 버블 정렬 개선해볼 수 있을까요?

루프를 돌았을 때 swap이 되지 않았다면 정렬이 완료된 것으로 볼 수 있다. 그러니 swap이 이루어졌는지 표시하는 플래그를 두면 이미 정렬되어 있는 경우 `O(n)`으로 개선할 수 있다.

### 퀵 정렬에 대해 설명해주세요?

퀵 정렬은 분할 정복 기법을 사용하는 정렬 알고리즘으로, 선택한 피벗을 기준으로 배열을 비균등하게 나누어 각 부분 배열을 다시 퀵 정렬한다. pivot이 최댓값이나 최솟값으로 선정되는 경우 재귀 호출이 `n`번, 각 재귀 호출에서 비교 연산이 `n`번 이루어지므로 시간 복잡도는 `O(n^2)`이고 그 이외에는 `O(nlogn)`이다.

```python
def partition(left, right):
  pivot = left
  for i in range(left, right):
    if arr[i] <= arr[right]:
      arr[pivot], arr[i] = arr[i], arr[pivot]
      pivot = pivot + 1
  arr[pivot], arr[right] = arr[right], arr[pivot]
  return pivot

def sort(left, right):
  if left < right:
    pivot_post = partition(left, right)
    sort(left, pivot_pos - 1)
    sort(pivot_pos + 1, right)
```

### 병합 정렬에 대해 설명해주세요?

병합 정렬은 분할 정복 기법을 사용하는 정렬 알고리즘으로, 정렬하려는 배열을 두 개의 배열로 나눈 후 합치는 과정을 반복한다. 시간 복잡도는 `O(nlogn)`이다.

```python
def merge_sort(left, right):
  if left < right:
    middle = (left + right) // 2
    merge_sort(left, middle)
    merge_sort(middle+1, right)
    merge(left, middle, right)
    
def merge(left, middle, right):
  i = left
  j = middle + 1
  k = left
  
  while i <= middle and j <= right:
    if arr[i] <= arr[j]:
      sorted[k] = arr[i]
      i += 1
      k += 1
    else:
      sorted[k] = arr[j]
      j += 1
      k += 1
      
	while i <= middle:
    sorted[k] = arr[i]
    i += 1
    k += 1

	while j <= right:
    sorted[k] = arr[i]
    j += 1
    k += 1

  for i in range(left, right + 1):
    arr[i] = sorted[i]
```

### 힙 정렬에 대해 설명해주세요?

힙 정렬은 힙 자료구조를 사용한 정렬 알고리즘으로, 힙의 첫번째 요소가 무조건 최대값이거나 최소값인 점을 이용한다. 시간 복잡도는 `O(nlogn)`이다.

```python
def heapify(arr: List[int], size, idx):
	largest = idx
	left = 2 * idx + 1
	right = 2 * idx + 2

	if left < size and arr[largest] < arr[left]:
		largest = left

	if right < size and arr[largest] < arr[right]:
		largest = right

	if largest != idx:
		arr[idx], arr[largest] = arr[largest], arr[idx]
		heapify(arr, size, largest)


def heap_sort(arr: List[int]):
	N = len(arr)
	for i in range(N // 2 - 1, -1, -1):
		heapify(arr, N, i)
	for i in range(N - 1, 0, -1):
		arr[i], arr[0] = arr[0], arr[i]
		heapify(arr, i, 0)
```

### 이진 탐색에 대해 알려주세요?

이진 탐색은 분할과 정복을 사용하여 정렬된 배열에서 탐색 범위를 절반으로 좁히며 주어진 요소를 탐색하는 방법이다. 시간 복잡도는 `O(logn)`이다.

```python
def search(arr, target):
  left, right = 0, len(arr)-1
  
  while left <= right:
    middle = (left + right) // 2
    
    if arr[middle] == target:
      return middle
    
    if arr[middle] < target:
      left = middle + 1
    else:
      right = middle - 1
	return -1

def search(left, right):
  if left > right:
    return -1
  
  middle = (left + right) // 2
  if arr[middle] == target:
    return middle
  elif arr[middle] < target:
    return search(middle+1, right)
  else:
    return search(left, middle-1)
```

