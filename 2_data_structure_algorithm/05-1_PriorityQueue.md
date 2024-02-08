# Priority Queue 우선순위 큐

## Priority Queue 우선순위 큐란?

* 각 요소마다 우선 순위를 가지고 있으며 가장 높은 우선순위를 가진 데이터가 먼저 처리되는 큐 형식의 자료구조

<br>

---

## 특징

* **특징**:
    * 큐와 다르게 데이터의 추가는 어떤 순서로 해도 상관이 없다.
    * 하지만, 데이터 삭제 시엔 우선순위가 가장 높은 데이터부터 처리된다.
    * 구현 시, 배열, 연결 리스트, 힙 모두 사용 가능하지만 일반적으로 힙을 사용한다.
        * why? 시간복잡도 때문에. 아래에서 설명.

* **장점**:
    * 시간이 중요한 작업에서 요소의 우선 순위대로 빠르게 처리가 가능하다.

* **사용 사례**:
    * 작업 스케줄링: 각 작업은 그 중요도에 따라 처리가 가능하다.
    * 알고리즘 구현: 다익스트라 알고리즘에서 최단 경로를 찾을때 사용가능하다.
    * 네트워크 통신: 네트워크에서 발생하는 패킷을 처리할 때, 우선 순위가 높은 특정 데이터 패킷의 작업 수행을 요구하는 경우 사용한다.
    * 작업 대기열: 긴급 서비스 요청이 들어올 때 큐보다 효과적으로 사용할 수 있다.

<br>

---

## 시간 복잡도

| 구현 방법 | 탐색 | 삽입 | 삭제 |
|-------------------------|-------|-------|-------|
| unsorted Array | O(n) | O(1) | O(n) |
| sorted Array | O(logN) | O(n) | O(n) |
| unsorted Linked List | O(n) | O(1) | O(n) |
| sorted Linked List | O(n) | O(n) | O(n) |
| Heap | O(n) | O(logN) | O(logN) |

* Unsorted Array (정렬되지 않은 배열):
    * 검색: O(n) - 배열을 순회하여 우선순위가 가장 높은 원소를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삽입: O(1) - 배열의 끝에 새로운 원소를 추가하기 때문에 상수 시간이 소요됩니다.
    * 삭제: O(n) - 삭제할 원소를 검색한 후 배열에서 해당 원소를 삭제해야 하므로 선형 시간이 소요됩니다.

* Sorted Array (정렬된 배열):
    * 검색: O(log n) - 이진 검색(Binary Search)을 사용하여 우선순위가 가장 높은 원소를 찾습니다.
    * 삽입: O(n) - 삽입할 위치를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삭제: O(n) - 삭제할 원소를 검색한 후 배열에서 해당 원소를 삭제하고 배열을 재정렬해야 하므로 선형 시간이 소요됩니다.

* Unsorted Linked List (정렬되지 않은 연결 리스트):
    * 검색: O(n) - 연결 리스트를 순회하여 우선순위가 가장 높은 원소를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삽입: O(1)- 리스트의 맨 앞이나 맨 끝에 새로운 노드를 추가하기 때문에 상수 시간이 소요됩니다.
    * 삭제: O(n) - 삭제할 원소를 검색한 후 리스트에서 해당 노드를 삭제해야 하므로 선형 시간이 소요됩니다.

* Sorted Linked List (정렬된 연결 리스트):
    * 검색: O(n) - 연결 리스트를 순회하여 우선순위가 가장 높은 원소를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삽입: O(n) - 삽입할 위치를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삭제: O(n) - 삭제할 원소를 검색한 후 리스트에서 해당 노드를 삭제하고 리스트를 재정렬해야 하므로 선형 시간이 소요됩니다.

* Heap (힙):
    * 검색: O(n) - 힙을 순회하여 우선순위가 가장 높은 원소를 찾아야 하므로 선형 시간이 소요됩니다.
    * 삽입: O(log n) - 새로운 원소를 힙에 추가하고 힙 속성을 유지하기 위해 로그 시간이 소요됩니다.
    * 삭제: O(log n) - 우선순위가 가장 높은 원소를 제거하고 힙 속성을 유지하기 위해 로그 시간이 소요됩니다.

> 따라서 힙은 삽입/삭제 시 최소 O(logN)을 보장하므로 일반적으로 우선순위 큐의 구현에서 힙이 * 용됩니다.

<br>

---

## 구현 코드

* heapq 모듈 활용:

```python
class PriorityQueue:
  def __init__(self):
    self.heap = []

  def insert(self, data, priority):
    heapq.heappush(self.heap, (priority, data))

  def delete(self):
     # 가장 우선순위가 높은 아이템을 삭제하고 반환합니다.
    return heapq.heappop(self.heap)[1]

  def peek(self):
    # 가장 우선순위가 높은 아이템을 반환합니다. 삭제하지 않습니다.
    return self.heap[0][1]

  def is_empty(self):
    # 우선순위 큐가 비어 있는지 확인합니다.
    return len(self.heap) == 0
```

* 파이썬 기본 함수로만 구현:
```python
class PriorityQueue:
    def __init__(self):
        self.heap = []

    def parent(self, i):
        return (i - 1) // 2

    def left_child(self, i):
        return 2 * i + 1

    def right_child(self, i):
        return 2 * i + 2

    def insert(self, item, priority):
        self.heap.append((priority, item))
        self._sift_up(len(self.heap) - 1)

    def _sift_up(self, i):
        while i > 0:
            parent_idx = self.parent(i)
            if self.heap[i][0] < self.heap[parent_idx][0]:
                self.heap[i], self.heap[parent_idx] = self.heap[parent_idx], self.heap[i]
                i = parent_idx
            else:
                break

    def delete(self):
        if len(self.heap) == 0:
            print("Queue is empty")
            return None
        min_item = self.heap[0][1]
        last_item = self.heap.pop()
        if len(self.heap) > 0:
            self.heap[0] = last_item
            self._sift_down(0)
        return min_item

    def _sift_down(self, i):
        while self.left_child(i) < len(self.heap):
            left_idx = self.left_child(i)
            right_idx = self.right_child(i)
            min_child_idx = left_idx
            if right_idx < len(self.heap) and self.heap[right_idx][0] < self.heap[left_idx][0]:
                min_child_idx = right_idx
            if self.heap[i][0] > self.heap[min_child_idx][0]:
                self.heap[i], self.heap[min_child_idx] = self.heap[min_child_idx], self.heap[i]
                i = min_child_idx
            else:
                break

    def peek(self):
        if len(self.heap) == 0:
            print("Queue is empty")
            return None
        return self.heap[0][1]

    def is_empty(self):
        return len(self.heap) == 0
```

<br>

---

## 예상 질문
* 우선순위 큐에 대해 설명하세요.
> 우선순위 큐란 각 요소가 우선순위를 가지고 있으며, 우선순위가 우위한 데이터가 먼저 처리되는 자료구조입니다. 이러한 특성으로 데이터의 추가는 어떤 순서로 해도 상관이 없지만, 삭제 시엔 우선순위가 가장 높은, 다르게 말하면 가장 작은 값을 삭제합니다. 이러한 특성으로 인해 시간이 중요한 작업에서 요소의 우선 순위를 통해 빠르게 처리가 가능하다는 장점을 가지고 있습니다. 이러한 시간적인 장점을 극대화 시키기 위해 주로 이진트리 구조의 힙 구현이 널리 사용되고 있습니다. 이유로는 힙 구현 방식엔 배열이나 연결리스트를 사용할 수 있지만 특정 상황에 따라 O(n)의 시간 복잡도가 요구 됩니다. 반면, 힙으로 구현한 경우 삽입/삭제 시에 O(log n)이 보장되기 때문입니다. 하지만 다른 구현 방법에 비해 힙 구협이 어렵다는 단점도 있습니다. 사용 사례로는 작업 스케줄링, 시뮬레이션 시스템, 네트워크 라우팅 등이 있습니다.

* 우선순위 큐의 동작원리가 어떻게 되나요?
> 우선순위 큐는 우선순위가 가장 높은 데이터를 먼저 꺼내기 위한 자료구조입니다. 따라서 힙이 가장 일반적으로 사용됩니다. 만약 front가 최대라면 최대힙, 최소라면 최소힙으로 구현하게 됩니다. 힙은 이진트리의 구조로 모든 정점이 자신의 자식 보다 높은 우선순위를 가지고 있다는 특성이 있습니다. 이러한 성질 때문에 삽입과 삭제 시 O(logN)의 시간 복잡도를 가집니다.
