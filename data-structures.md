# data-structure

> 질문과 답변은 [이 레포지토리](https://github.com/leegwae/data-structures)에 정리된 텍스트에 기반합니다. 자세한 내용은 해당 레포지토리를 참고하세요.

### 스택에 대해 알려주세요?

스택은 가장 최근에 들어온 데이터가 먼저 나가는 자료구조이다.

```javascript
class ListNode {
	constructor(value, next = null) {
		this.value = value;
		this.next = next;
	}
}

class Stack {
	top = null;

	isEmpty() {
		return this.top === null;
	}

	push(value) {
		this.top = new ListNode(value, this.top);
	}

	pop() {
		if (this.isEmpty()) return null;

		const deletedItem = this.top;
		this.top = this.top.next;
		return deletedItem.value;
	}

	peek() {
		if (this.isEmpty()) return null;

		return this.top.value;
	}
```

### 큐에 대해 알고 있나요?

큐는 가장 먼저 들어간 요소가 먼저 나가는 자료구조이다.

```javascript
class ListNode {
	constructor(value, next = null) {
		this.value = value;
		this.next = next;
	}
}

class Queue {
	head = null;
	tail = null;

	isEmpty() {
		return this.head === null;
	}

	push(value) {
		const newItem = new ListNode(value, null);

		if (this.isEmpty()) {
			this.head = this.tail = newItem;
			return;
		}

		this.tail.next = newItem;
		this.tail = this.tail.next;
	}

	pop() {
		if (this.isEmpty()) return null;

		const deletedItem = this.head;
		this.head = this.head.next;

		return deletedItem.value;
	}

	peek() {
		if (this.isEmpty()) return null;

		return this.tail.value;
	}
}
```

### 연결 리스트에 대해 설명해주세요?

연결 리스트는 데이터 값과 다음 노드에 대한 참조 값을 가지는 노드들이 연결된 자료구조이다.

### 연결 리스트와 배열의 차이를 설명해주세요?

첫번째, 연결 리스트는 연속적인 메모리에 저장되지 않을 수 있지만 배열은 연속적인 메모리에 저장된다. 두번째, 연결 리스트는 동적으로 크기를 변경할 수 있지만 배열은 정적인 크기를 가진다. 세번째, 연결 리스트는 특정 요소에 접근하기 위해 순회해야하므로 `O(n)`의 시간 복잡도를 요하지만 배열은 인덱스를 사용하여 상수 시간에 접근할 수 있다. 네번째, 연결 리스트는 삽입과 삭제 연산에 상수 시간을 요하지만(탐색에는 `O(n)`을 필요로 함) 배열은 요소의 이동이 필요하므로 `O(n)`의 시간 복잡도를 요한다.

### 캐시를 연결 리스트와 배열로 구현한다고 하면, 지역성 원리 관점에서 어떤 자료구조가 더 성능이 좋을까요?

캐시는 공간 지역성에 따라 인접한 데이터까지 함께 블록 단위로 저장하기 때문에, 연속적으로 저장되지 않을 수 있는 연결 리스트보다 연속적으로 저장되는 배열의 캐시 적중률이 더 높다.

### 리스트와 배열의 차이에 대해 설명해주세요?

배열은 동일한 데이터 타입의 값들을 순차적으로 저장한 유한한 크기의 자료구조이다. 리스트는 동적으로 크기를 변경할 수 있으며 요소들의 데이터 타입은 서로 다를 수 있다.

### 트리에 대해 설명해주세요?

사이클이 없는 그래프의 일종이고 노드들은 부모와 자식이라는 계층 관계를 가진다. 트리의 노드가 `n`개라면 간선은 `n-1`개이다.

### 트리와 그래프의 차이에 대해 설명해주세요?

첫번째, 트리에서 노드들은 부모-자식이라는 계층 관계를 가지지만 그래프는 그러지 않을 수도 있다. 두번째, 트리에는 사이클이 없지만 그래프는 사이클이 생길 수도 있다.

### 힙에 대해 설명해주세요?

힙은 우선순위 큐를 구현하기 위해 사용하는 자료구조로, 완전 이진 트리의 형태를 가지고 있다. 상수 시간에 최댓값 또는 최솟값에 접근할 수 있고, 삽입과 삭제 연산을 `O(logn)`의 시간 복잡도에 수행할 수 있다.

### 힙 삽입 연산에 대해 설명해주세요?

요소를 가장 하위 레벨의 최대한 왼쪽에 삽입한다(배열의 경우 가장 뒤에 요소를 추가한다). 힙의 성질을 만족할 때까지 부모 노드와 노드를 교환한다.

### 힙 삭제 연산에 대해 설명해주세요?

루트 노드를 삭제한다. 가장 하위 레벨의 가장 오른쪽에 있는 노드(배열의 경우 가장 뒤에 있는 요소)를 골라 루트 노드에 삽입한다. 힙의 성질을 만족할 때까지 삽입한 노드와 자식 노드를 교환한다.