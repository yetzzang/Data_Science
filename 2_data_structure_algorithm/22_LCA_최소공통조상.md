# 최소 공통 조상 (LCA, )

## 최소 공통 조상 (LCA)란?
> 트리 자료구조에서 특정한 두 노드의 공통된 조상 중 가장 가까운 조상

예시 1)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2136754858C832C90F)

 - LCA(14, 7) = 1

예시2)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F24054D4D58C8330D05)

 - LCA(13, 9) = 2

예시 3)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2336E05058C8336C03)
 - LCA(13, 6) = 13

<br>

---

## 특징

- **장점**
    - 효율적인 검색: 트리에서 두 노드의 가장 가까운 공통 부모를 효율적으로 찾을 수 있다. 특히 트리의 높이가 큰 경우에 유용하다.
    - 트리 구조에서의 관계 파악: 두 노드 간의 관계를 빠르게 파악할 수 있다. 예를 들어, 어떤 트리에서 두 노드 간의 가장 가까운 공통 부모가 무엇인지 확인하는 데 사용한다.

- **단점**
    - 트리 형태에 의존: 최트리가 아닌 다른 자료구조에서는 이 알고리즘이 적용되지 않는다.
    - 계산 복잡성: 일부 구현에서 계산 복잡성이 발생할 수 있다. 이는 트리의 크기와 높이에 따라 달라질 수 있다.

- **사용 사례**
    - 자료구조에서의 관계 파악: 트리 형태의 자료구조에서 두 노드 간의 관계를 파악하는 데 사용된다. 예를 들어, 어떤 개체 간의 상속 관계를 이해하거나 표현할 때 사용될 수 있다.
    - 최단 경로 찾기: 그래프에서 두 노드 간의 최단 경로를 찾을 때, 최소 공통 조상을 활용하여 해당 경로를 찾는데 사용될 수 있다.


<br>

---

## 시간 복잡도

- O(N) 또는 O(depth): 선형 탐색 (주로 DFS/BFS)
- O(NM): 선형 탐색으로 모든 쿼리(M)을 처리할 경우
- O($logN$): DP 구현
- O($MlogN$): DP 구현으로 모든 쿼리(M)을 처리할 경우

<br>

---

## 구현

### 선형 탐색:

- 알고리즘 이해:
    - 트리 노드 정의:
        - TreeNode 클래스를 정의하여 간단한 트리 노드를 나타냅니다. 각 노드는 값(val)과 자식 노드 리스트(children)를 가집니다.
    - DFS를 사용한 트리 순회 및 조상 정보 저장:
        - dfs 함수를 정의하여 DFS를 사용하여 트리를 순회하고, 각 노드의 조상 정보를 저장합니다.
        - ancestor 딕셔너리에 각 노드의 부모 노드를 저장합니다.
    - LCA 찾기:
      - find_lca 함수를 정의하여 주어진 두 노드의 LCA를 찾습니다.
      - 먼저, 두 노드의 깊이를 맞춰주기 위해 각 노드를 조상으로 올라갑니다.
      - 그 후, 두 노드를 동시에 부모 방향으로 이동시켜가며 처음으로 만나는 공통 조상이 LCA가 됩니다.

```python
# 간단한 트리 노드 정의
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.children = []

# DFS를 사용한 트리 순회 및 조상 정보 저장
def dfs(root, parent, depth, ancestor):
    ancestor[root.val] = parent
    for child in root.children:
        dfs(child, root.val, depth + 1, ancestor)

# LCA 찾기
def find_lca(u, v, depth, ancestor):
    # 깊이를 맞춰줌
    while depth[u] > depth[v]:
        u = ancestor[u]
    while depth[v] > depth[u]:
        v = ancestor[v]
    # 두 노드를 동시에 부모 방향으로 이동시켜가며 LCA 찾기
    while u != v:
        u = ancestor[u]
        v = ancestor[v]
    return u
```

### DP:

- 알고리즘 이해:
    - 트리 노드 정의:
        - TreeNode 클래스를 정의하여 간단한 트리 노드를 나타냅니다. 각 노드는 값(val)과 자식 노드 리스트(children)를 가집니다.
    - Sparse Table 구성:
        - build_sparse_table 함수를 사용하여 스파스 테이블을 구성합니다. 이 테이블은 각 노드의 2^j번째 조상을 효율적으로 저장하는데 사용됩니다.
        - log_n은 노드의 수를 기반으로 한 최소 2의 거듭제곱 수를 나타냅니다.
        - 이중 리스트 sparse_table은 초기에 -1로 초기화되고, 각 노드의 1번째 조상 정보를 채우고, 나머지 부분을 채워 나갑니다.
    - DFS를 사용한 깊이 및 부모 정보 계산:
      - DFS를 사용하여 각 노드의 깊이(depth)와 부모 노드(parent)를 계산합니다.
      - 루트 노드에서 시작하여 각 노드에 대한 깊이와 부모 노드를 저장합니다.
  - LCA 찾기:
      - lca 함수를 사용하여 주어진 두 노드의 LCA를 찾습니다.
      - u와 v의 깊이를 맞춰주고, u의 깊이를 v의 깊이로 맞춰줍니다.
      - 이후에는 두 노드를 동시에 부모 방향으로 이동시켜가며 처음으로 만나는 공통 조상이 LCA가 됩니다.
      - 스파스 테이블을 활용하여 각 노드의 2^j번째 조상을 빠르게 찾을 수 있습니다.

```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.children = []

def build_sparse_table(n, parent):
    # 초기화: sparse_table[i][j]는 노드 i의 2^j번째 조상을 저장
    log_n = (n - 1).bit_length()  # n보다 크거나 같은 최소의 2의 거듭제곱 수
    sparse_table = [[-1] * log_n for _ in range(n)]

    # 각 노드의 1번째 조상 정보 채우기
    for i in range(n):
        sparse_table[i][0] = parent[i]

    # sparse_table 채우기
    for j in range(1, log_n):
        for i in range(n):
            if sparse_table[i][j - 1] != -1:
                sparse_table[i][j] = sparse_table[sparse_table[i][j - 1]][j - 1]

    return sparse_table

def lca(u, v, depth, parent, sparse_table):
    # u와 v의 깊이를 맞춰주기
    if depth[u] < depth[v]:
        u, v = v, u

    # 깊이를 맞춘 이후, u의 깊이를 v의 깊이로 맞추기
    log_n = len(sparse_table[0])
    for i in range(log_n - 1, -1, -1):
        if depth[u] - (1 << i) >= depth[v]:
            u = sparse_table[u][i]

    # u와 v가 같지 않다면 공통 조상 찾기
    if u != v:
        for i in range(log_n - 1, -1, -1):
            if sparse_table[u][i] != -1 and sparse_table[u][i] != sparse_table[v][i]:
                u = sparse_table[u][i]
                v = sparse_table[v][i]

        u = parent[u]

    return u
```

<br>

---

## 예상 질문
1. 최소 공통 조상(LCA)이 왜 중요하며 어떤 상황에서 사용될까요?
> 최소 공통 조상은 트리 구조에서 두 노드의 가장 가까운 공통 부모를 찾는 알고리즘입니다. 이는 상속 관계, 계층 구조, 그래프에서의 최단 경로 등 다양한 상황에서 유용하게 활용됩니다. 예를 들어, 소프트웨어 개발에서는 객체 지향적인 관점에서 상속 관계를 나타내는 트리에서 두 클래스의 공통 조상을 찾는 데 사용될 수 있습니다. 그리고 네트워크에서는 최단 경로를 찾는 문제에서도 LCA가 유용하게 활용될 수 있습니다.

2. 최소 공통 조상을 찾기 위한 다양한 알고리즘들이 있는데, 그 중 하나를 선택하고 해당 알고리즘의 장단점을 설명해주세요.
> 스파스 테이블 알고리즘: 장점으로는 전처리 단계에서 O(N log N)의 시간 복잡도를 가지며, 각 쿼리에 대해 O(1)의 시간 복잡도를 제공합니다. 따라서 쿼리가 여러 번 수행되는 상황에서 효율적입니다.하지만 단점으로는, 전처리 단계에서 추가적인 메모리가 필요하며, 트리가 변경되면 다시 전처리해야 합니다.
> 바이너리 리프트 알고리즘: 장점으로는 O(N log N)의 전처리 시간 복잡도를 가지며, 각 쿼리에 대해 O(log N)의 시간 복잡도를 제공합니다. 스파스 테이블에 비해 메모리 사용이 적습니다. 단점으로는 트리의 크기가 클 경우, 상수 계수가 큰 경우에는 스파스 테이블에 비해 상대적으로 느릴 수 있습니다. 또한, 트리가 동적으로 변할 때 전체를 다시 계산해야 하는 번거로움이 있습니다.

3. LCA를 사용한 실제 문제의 예시를 들어보세요.
> 예를 들어, 소셜 네트워크에서 친구 관계를 나타내는 트리가 있다고 가정해봅시다. 두 사용자 간의 최소 공통 조상을 찾으면 두 사용자 간의 가장 가까운 친구 관계를 파악할 수 있습니다. 이를 통해 두 사용자가 몇 단계의 친구를 거쳐 연결되어 있는지 등을 파악할 수 있습니다. 이런 방식으로 LCA는 소셜 네트워크 분석 등 다양한 문제에 적용될 수 있습니다.
