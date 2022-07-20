# DataStructure
- [DataStructure](#datastructure)
  - [Array](#array)
  - [List](#list)
  - [Stack](#stack)
  - [Queue](#queue)
  - [Heap](#heap)
  - [B Tree](#b-tree)
  - [Hash](#hash)
  


</br>

* * *
## Array
데이터가 많아지면 관련된 데이터끼리 그룹으로 관리해야 하는 필요성이 생긴다. 이때 여러 데이터를 하나의 이름으로 묶어서 편하게 사용할 수있는 자료구조이다.
<br>
<br>
Array를 이용하면 하나의 변수에 여러 정보를 담을 수있고, 인덱스라는 식별자를 이용해 value에 접근할 수있다. 인덱스는 값이 몇번째 인지를 나타내는데 사용된다.

배열의 특징은 아래와 같다.
<br>
1. 크기가 정해져 있다.
2. 인덱스를 가지며, value의 인덱스는 변하지 않는다. 
3. 메모리에 데이터를 순차적으로 나열할 수있다.
4. 인덱스를 사용하여 조회 시 O(1)의 시간 복잡도가 소요된다.
5. 인덱스를 사용하여 데이터를 가져오기 때문에 데이터에 대한 인덱스 값이 고정된다. 따라서 value가 삭제되어도 인덱스 공간을 그대로 유지하고, 이는 메모리를 낭비하는 것이다.

<br>
배열의 한계는 아래와 같은 것들이 존재한다.

<br>

1. 배열의 크기를 바꿀 수없다.
2. 배열의 크기를 유동성있게 바꿔야 할때는 Linked List를 사용한다.
3. 배열은 인덱스에 따라서 값을 유지하기 때문에 value가 삭제되면 null이 채워지고, 메모리는 낭비된다.

Array를 그림으로 나타내면 아래와 같다.

<img width="685" alt="image" src="https://user-images.githubusercontent.com/76645095/178654041-6cd10cbd-ed3a-4f14-ac73-f826d6b0e971.png">  

<br>
C++ 코드를 예시로, 배열을 사용해보면 아래와 같다.
<br>
<br>

```C++
#define NUM 2000100
using namespace std;
int array[NUM];

void init() {
    array[0] = 1;
    array[1] = 2;
    array[2] = 2;
}


int main() {    
    ios_base :: sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    init();
}

```
* * *
## List
배열의 가장 큰 특징은 인덱스가 있다는 것이다. 원하는 데이터의 인덱스를 알고 있다면 O(1)만에 해당 데이터를 얻을 수있다. 
하지만, 이것은 단점이기도 하다. 인덱스를 이용해서 데이터를 가져오려면, 데이터에 대한 인덱스의 값이 고정되어야 하기 때문에 해당 value가 삭제되면 삭제된 상태의 빈 공간이 생기게 되고 이는 메모리 낭비를 야기한다. 

<br>
리스트는 배열이 가지고 있는 인덱스라는 장단점을 아예 버리고, 대신 빈틈없는 데이터의 적재라는 장점을 취한 자료구조이다.
따라서 null이 생기지 않고 value 간 공백이 생기지 않는다는 특징을 가진다. 
<br>
리스트의 가장 큰 특징은 순서가 있다는 것이다. 따라서 배열의 인덱스를 이용하는 것 같이 임의로 특정 value에 접근할 수가 없다. 만약 어떤 value를 사용하고 싶다면 순차적으로 value를 찾아야 한다.
<br>
<br>
리스트의 특징은 아래와 같은 것들이 있다.  

1. 크기가 고정되지 않는다.
2. 삽입, 삭제에 O(1)이 소요된다.
3. 배열의 인덱스와 달리 value에 바로 접근할 수 없다.
4. 메모리가 낭비되지 않는다.
5. 배열과 달리 메모리에 연속적으로 저장되지 않아도 된다.


리스트의 단점은 아래와 같다.
1. value에 접근하기 위해서 최대 O(N)의 시간복잡도가 소요된다.
2. 순차 리스트라면 다음 노드를 가리키는 포인터를 삽입/삭제시 마다 변경해야 하는 귀찮은 작업이 필요하다.

리스트를 그림으로 나타내면 아래와 같다.
<br>

<img width="1189" alt="image" src="https://user-images.githubusercontent.com/76645095/178659129-3cf95bae-7ee5-4898-9a80-a9f2ca0a1359.png">

<br>

리스트는 메모리에 연속적으로 저장되지 않아도 된다는 특징이 있다. 대신, '노드'라는 개념으로 각각 독립된 공간을 사용하며 이 공간에 데이터를 저장한다.  
각 노드는 실제 데이터가 저장되는 공간인 '데이터 필드'와 다음 노드의 주소값을 가리키는 '링크 필드'로 이루어져 있다. 

C++ 코드로 List의 삽입과 삭제를 구현해보면 아래와 같다.

```C++
#include <iostream>

using namespace std;

//노드 struct 구현 (data값과 nextNode가 존재)
struct node {
	int data;
	node* nextNode;
};

//링크드 리스트 클래스
class LinkedList {
private:
	node* head;
	node* tail;
public:
	LinkedList() {
		//head 와 tail의 포인터를 초기화;
		head = NULL;
		tail = NULL;
	}

	//node 삽입
	void insertNode(node* prevNode, int n);
	//node 삭제
	void deleteNode(node* prevNode);

};


//node 삽입
void LinkedList::insertNode(node* prevNode,int n) {
	node* temp = new node;
	temp->data = n;

	//temp의 nextNode 저장
	temp->nextNode = prevNode->nextNode;
	
	//temp앞의 node의 nextNode를 temp로 저장
	prevNode->nextNode = temp;
}

//node 삭제
void LinkedList::deleteNode(node* prevNode) {

	//삭제할 node를 temp에 저장
	node* temp = prevNode->nextNode;

	//삭제할 node의 nextNode를 1단계 전 node의 nextNode에 저장
	prevNode->nextNode = temp->nextNode;

	//temp 삭제
	delete temp;
}

```

* * *
## Stack
스택은 기본적으로 LIFO(Last In First Out), 즉 후입선출의 개념을 가지고 있는 자료구조이다.  
나중에 들어간 것이 가장 먼저 나오는 특성상 깊이 우선 탐색에 DFS의 구현에 자주 사용하곤 한다. 
<br>
DFS는 재귀로도 구현할 수있고, 나도 재귀로 짜는것을 굉장히 선호한다. 그러면 왜? DFS에 재귀와 스택이 둘다 사용될 수있는지 자연스레 의문이 생긴다.  
이는 재귀 함수가 하드웨어 상으로 어떻게 구현되는지 이해하면 아주 쉽게 납득할 수있다.
<br>

![image](https://user-images.githubusercontent.com/76645095/178663156-47b4fd86-d4b0-40c1-9328-a65a4f1da3ae.png)  

<br>
프로세스의 메모리는 위와같이 구성된다. 이때 재귀 함수를 들어가면 스택 영역 메모리에 각 함수별 데이터가 들어간다.  
<br>
<br>
현재 함수에서 재귀 함수를 실행한다면, 현재 함수의 상태가 스택 영역에 저장되고 pop 되기를 기다린다. 새롭게 실행된 함수가 또 재귀 함수를 호출하고 .. 스택 영역에 또 저장된다. 
<br>
<br>
만약 함수가 계속 들어가서 스택 영역에 할당된 메모리 영역을 벗어나게 된다면, 이때 마주치는 것이 스택오버 플로우이다. 
<br>
<br>
이 흐름을 잘보면, 재귀 함수도 후입 선출의 구조를 가진다는 것을 알 수있다. 그리고 이는 스택 자료구조의 패러다임과 일치한다. 그리고 가장 깊은 노드를 우선으로 탐색하는 DFS 알고리즘의 패러다임이 일치하기 때문에 재귀와 스택 모두를 활용할 수있는 것이다.

<br>

스택 자료구조가 가지는 특징은 아래와 같다.  
1. 배열과 달리 index를 사용할 수없기 때문에 특정 인덱스 value에 O(1)에 접근할 수없다.
2. 스택에 데이터를 추가하거나 삭제하는 연산은 O(1)이 소요된다. 
3. 배열과 리스트로 구현이 가능하고, 리스트의 장점 중 하나인 메모리 낭비가 없다는 특징을 그대로 살릴 수있다.

스택 자료구조를 그림으로 나타내면 아래와 같이 나타낼 수있다.
<br>

<img width="326" alt="image" src="https://user-images.githubusercontent.com/76645095/178665681-e3c1f601-5626-4b64-bf5b-50ef08b48e24.png">

<br>
<br>

스택은 배열과 연결 리스트 둘다 활용해서 구현할 수있다. 연결 리스트를 이용해 C++로 구현해보면 아래와 같다.

```C++
struct Node {
    int data;
    Node* next;
    Node() {
        next = NULL;
        data = 0;
    }
 
    Node(int i, Node* ptr) //ptr 뒤에 추가
    {
        data = i;
        next = ptr->next;
        ptr->next = this; 
    }    
};
 
struct Stack {
    Node *head;
    Stack() { //생성자
        head = new Node(); //더미노드
    }
 
    void pop() { //데이터 제거
        Node *tmp = head;
        head = head->next; 
        delete tmp; 
    }
 
    void push(int i) { //데이터 삽입
        new Node(i, head);
    }

};
```

* * *
## Queue
큐도 스택만큼 간단한 자료구조이다.  
스택은 LIFO 자료구조인 반면, 큐는 FIFO 자료구조이다. 다른 CS 과목들을 공부한적 있다면 FIFO는 하드웨어 상에서 굉장히 자주 사용하는 기법인 것을 알것이고, 큐를 이해하기도 쉬울 것이다.  
<br>
큐는 스택과 굉장히 유사하지만, pop을 하는 위치가 다르다. 따라서 큐의 특징은 스택과 굉장히 유사하다고 볼 수있다.

1. 배열과 달리 index를 사용할 수없기 때문에 특정 인덱스 value에 O(1)에 접근할 수없다.
2. 큐에 데이터를 추가하거나 삭제하는 연산은 O(1)이 소요된다. 
3. 배열과 리스트로 구현이 가능하고, 리스트의 장점 중 하나인 메모리 낭비가 없다는 특징을 그대로 살릴 수있다.

큐 자료구조는 터널을 생각하면 바로 이해할 수있다. 자동차가 터널에 들어간다면, 분명히(?) 들어간 순서대로 자동차가 나올 것이다. 그림으로 나타내면 아래와 같다.
<br>

<img width="257" alt="image" src="https://user-images.githubusercontent.com/76645095/178669567-0197da6e-0085-466f-b0f1-fdc1195debbb.png">

<br>

스택은 배열로 구현하기 간단하다. 하지만, 큐는 어떻게 배열로 구현할 수있을까? 큐를 배열로 구현하기 위해서는 modulo 연산을 활용하여 순환 배열을 만들어주면 된다.  
그럼에도 리스트로 구현하는 것이 훨씬 간단하기 때문에 리스트로 큐를 구현해보면 아래의 코드와 같이 구현할 수있다. 한번 구현해봤다면 그냥 맘편하게 STL을 쓰자.

```C++
using namespace std;
struct Node {
    int data;
    Node *next;
};
 
struct LinkedQueue {
    Node *front, *rear;
    LinkedQueue() {
        front = rear = NULL;
    }
 
    void push(int data) {
        Node *node = (Node*)malloc(sizeof(Node));
        node->data = data;
        node->next = NULL;
        if (isEmpty()) {
            front = rear = node;
        }
        else {
            rear->next = node;
            rear = rear->next;
        }
    }
 
    int pop() {
 
        Node *delNode = front;
        int ret = delNode->data;
        front = delNode->next;
        free(delNode);
        return ret;
    }
};
 

```
* * *
## Heap
힙은 내가 좋아하는 자료구조 중 하나이다. 처음 힙을 공부했을때 어떻게 이런 천재적인 발상을 떠올릴 수있는건지 충격을 받았던 기억이 난다.

​

우리에게 어떤 배열이 있다고 가정해보자. 여기는 값이 중복될 수도 있고, 중복되지 않아도 된다. 하지만 아쉽게도 값들은 정렬이 되지 않은 상태이다.

​

이 배열에서 가장 큰 값을 찾고 싶다면 어떻게 해야할까? 

정렬이 되지 않았기 때문에 당연하게도 모든 값을 확인해야 한다. 따라서 배열의 크기가 N일때 가장 큰 값을 찾는데 걸리는 시간은 최대 O(N)이 소요된다. 

​

그런데 놀랍게도 힙 자료구조를 사용하면 O(1)에 가장 큰 값을 찾을 수있다. 물론 값을 제거하거나 추가하면, 힙을 갱신하는 동안 O(logN)이 소요되긴 하지만 말이다. 

​

이것이 어떻게 가능할까. 최대힙을 기준으로 먼저 살펴보고, 최소 힙을 살펴보자. 최소힙은 사실 최대힙만 이용해도 쉽게 구현할 수있다.

​

최대 힙은 딱 2가지만 기억하면 된다.

1. 힙은 완전 이진 트리이다. 

2. 부모 노드의 value가 항상 자식 노드의 value 보다 큰 상태를 유지한다. 

​

그림으로 나타내면 아래와 같은 트리를 최대힙이라고 볼 수있다.
<br>
<br>
![image](https://user-images.githubusercontent.com/76645095/178906652-a48f85a3-570f-4eb9-9849-cc6b029c47a5.png)
<br>
이진트리이고, 부모가 자식보다 크기 때문에 최대힙 조건을 만족한다.

​

힙은 배열로 구현하는 것이 가장 간단하다. 

​

힙을 구현할때 최상위 루트 노드의 인덱스는 1로 설정한다. 

최상위 부모 노드인 루트노드를 인덱스 1로 나타내는 이유는 간단하다. 힙에서는 왼쪽 자식 노드를 현재 노드 인덱스의 *2, 오른쪽 자식 노드를 인덱스 * 2 + 1로 나타내기 때문이다. 당연하게도 현재 노드의 인덱스 / 2는 부모 노드의 인덱스가 된다.

​

만약 인덱스를 0부터 시작하면 루트 노드의 인덱스도 0이고, 루트 노드의 왼쪽 자식 노드의 인덱스도 0이 되기 때문에 별도의 처리를 해줘야 한다. 

​

반면 인덱스 1부터 시작하면 [*2, *2+1]로 자식 노드의 위치를 전부 처리할 수있다. 구현의 편리함 때문에 인덱스를 1부터 시작해서 관리하곤 한다.

​

위의 조건을 만족하도록 이진트리를 만들면, 가장 큰 값은 무조건 루트 노드에 존재하게 된다. 따라서 O(1)에 배열 내 최댓값을 찾을 수있는 것이다.

​

하지만, 배열에는 삽입과 삭제 연산이 발생하곤 한다. 

이때 힙도 값의 갱신이 필요한데, 항상 루트 노드를 기준으로 갱신한다. 따라서 삽입과 삭제가 아무리 많이 발생해도 결국 갱신이 된 후 최댓값을 찾는데는 O(1)이 소요된다.

​

먼저 힙은 삽입을 어떻게 처리하는지 살펴보자.

힙의 삽입은 아주 간단하게 설명이 가능한데, 마지막 노드에 value를 넣고 -> 부모 노드가 자신보다 클때까지 부모로 올라간다. 이다.
<br>

![image](https://user-images.githubusercontent.com/76645095/178906733-c8c273d0-b913-4475-9eec-d8e5e24a2521.png)
<br>

그림이 조금 삐뚤어졌지만, 13이라는 값을 힙에 새로 삽입하고 싶다고 가정하자.

먼저 새로운 값을 마지막 노드에 추가를 해준다. 그다음 자신의 부모 노드를 확인하는데, 자신보다 작기 때문에 서로 위치를 swap 해준다.

![image](https://user-images.githubusercontent.com/76645095/178906785-39ba4f6a-9145-438c-8b32-9be4a1827480.png)


아직 현재 위치가 루트가 아니기 때문에 계속해서 부모 노드와 비교한다. 부모가 8이므로 현재 노드보다 작다. 따라서 서로 swap 해준다.

![image](https://user-images.githubusercontent.com/76645095/178906848-5dacb212-0dde-4037-8ad3-01d38c47ffca.png)

또 부모 노드와 비교한다. 부모가 나보다 작기 때문에 swap해준다.

![image](https://user-images.githubusercontent.com/76645095/178906913-0b79eed3-904c-4616-8988-b21609ed3f91.png)

이제 더이상 비교할 부모 노드가 존재하지 않기 때문에 연산을 마무리한다.

​

이제 힙의 삽입 연산의 끝이다. 

삽입 연산에 소요되는 시간복잡도는 O(logN)이다. 힙은 이진 트리로 구성되어 있기 때문에 노드의 개수가 N이라고 할때 트리의 높이는 logN이 된다. 그리고 새로운 값을 삽입하면 현재 높이부터 루트 노드의 높이까지 올라갈 수있기 때문에 최대 logN의 비교가 필요하다.

​

이렇게 힙에 새로운 노드를 삽입하면 힙은 자연스레 갱신이 된다. 여전히 루트 노드는 이 배열의 값 중 가장 큰 값이 된다.

​

삭제 연산도 간단하다.

루트 노드를 삭제하고 -> 가장 마지막 노드를 루트로 가져와 -> 루트부터 현재 노드를 내리면 된다.

![image](https://user-images.githubusercontent.com/76645095/178906964-51f64f03-9b62-48ef-aa6e-54f4262fa2f2.png)

이 힙에서 pop을 하면, 13을 제거하고 인덱스상 마지막 노드인 2를 루트 노드로 올린다.

![image](https://user-images.githubusercontent.com/76645095/178907020-baecbcd3-ca88-462e-8321-921837c07cbe.png)

마지막 노드였던 2는 자신의 왼쪽과 오른쪽 자식의 값을 비교한다. 9와 11 중 11이 더 크기 때문에 11과 위치를 바꾼다.

![image](https://user-images.githubusercontent.com/76645095/178907065-081ba09b-0243-4948-bbe6-c8299fd20a1e.png)

2는 다음 자식 노드를 살펴본다. 8과 4 모두 자신보다 크고, 8이 4보다 크기 때문에 8과 위치를 swap 한다.

![image](https://user-images.githubusercontent.com/76645095/178907124-a0134999-c2e0-4008-90d5-2544a09ec6a6.png)

더이상 자식 노드가 없으므로, pop 연산은 끝이난다.

​

삭제 연산의 시간복잡도도 O(logN)이 소요된다. 삽입과 같은 이유인데, 최악의 경우 루트 노드부터 리프 노드에 도달할때까지 계속해서 비교 연산이 발생할 수있다. 

​

이때 트리의 높이가 logN 이므로 아무리 많아도 logN 안에 힙 트리를 구성할 수있음을 보장받는다. 

​

최대 힙의 삽입과 삭제를 코드로 구현하면 아래와 같다.

```C++
int heap[HEAP_SIZE]; 
int heap_count = 0; 
void swap(int * a, int * b) {
	int tmp = *a; *a = *b; *b = tmp;
}

void push(int data) {

	heap[++heap_count] = data;

	int child = heap_count;
	int parent = child / 2;
	while (child > 1 && heap[parent] < heap[child]) {
		swap(&heap[parent], &heap[child]);
		child = parent;
		parent = child / 2;
	}

}

int pop() {

	int result = heap[1];

	swap(&heap[1], &heap[heap_count]);
	heap_count--;

	int parent = 1;
	int child = parent * 2;
	if (child + 1 <= heap_count) {
		child = (heap[child] > heap[child + 1]) ? child : child + 1;
	}

	while (child <= heap_count && heap[parent] < heap[child]) {
		swap(&heap[parent], &heap[child]);

		parent = child;
		child = child * 2;
		if (child + 1 <= heap_count) {
			child = (heap[child] > heap[child + 1]) ? child : child + 1;
		}
	}

	return result;
}
```

최소힙은 더쉽다. 사실 최대 힙에서 더 작은 값이 부모가 되도록 유지하기만 하면 되는데, 더 간단하게 최대힙으로도 최소힙을 만들 수있다.

​
단순한 배열로 이 원리를 살펴보자.

```C++
[1, 2, 3, 4, 5, 6, 7, 8, 9] 
[-1, -2, -3, -4, -5, -6, -7, -8, -9]
```

위의 두 배열을 비교해보면, 위의 배열은 오름차순 정렬이 되어있고, 아래의 배열은 내림차순 정렬이 되어있다. 부호만 바꿨을 뿐인데 말이다. 이 원리를 이용해 최대힙에 값을 넣을때 -를 붙혀 부호를 바꿔주면 최댓값이 배열내 최솟값이 되어버리고, 최솟값이 최댓값이 되어버린다.

​

가장 작은 값이 임시로 가장 큰값이 되었으므로 당연히 최대힙에서 루트 노드에 존재할 것이다. 그리고 이 값을 pop 할때 다시 부호를 바꿔주면 가장 작은 값을 루트에서 얻을 수있게 된다. 


## B Tree
B-Tree는 데이터의 검색 시간을 단축하기 위한 자료구조이고, 일반적인 RDBMS의 인덱스는 대부분 B-tree 구조로 되어 있다. 
B-Tree(Balanced-Tree)는 'root node', 'internal node', 'leaf node'로 구성되며, 리프 노드가 모두 같은 레벨에 존재하는 balanced tree 이다.


node 자식의 수 중 최댓값을 K라고 하면 K차 B-Tree라고 부른다. 아래의 그림은 3차 B-Tree를 보여준다.

![image](https://user-images.githubusercontent.com/76645095/179175564-f9ece6c1-8077-417e-ab4c-cd3f145c40d7.png)  

B-tree의 각 노드는 키 값과 포인터를 가진다. 

키 값은 오름차순으로 저장되어 있으며, 각 노드는 좌우에 포인터를 가지는데, '좌' 포인터는 키 값보다 작은 값을 가진 다음 노드를 가리키고, '우' 포인터는 키 값보다 큰 값을 가진 다음 노드를 가리킨다. 따라서 키 값을 비교하여 다음 단계의 노드를 쉽게 찾을 수있다. 

​
모든 검색은 루트 노드에서부터 시작하여 내부 노드를 지나 리프노드까지 내려가면서 이루어진다. 

B-Tree는 키 값이 새로 추가되거나 삭제될 경우 동적으로 노드를 분할하고, 통합하여 항상 균형 상태를 유지한다는 특징을 가진다.

이 '균형'을 맞춘다는 것이 굉장히 중요한데, 흔한 이진 트리는 노드가 한쪽으로 편향될 가능성이 있기 때문에 탐색 시간은 최악의 경우 O(N)이 소요된다. 

반면 균형 트리는 항상 높이를 logN으로 유지하기 때문에 최악의 경우에도 O(logN)만에 원하는 value를 찾아낼 수있는 것을 보장하기 때문에 매우 효율적이다.

​![image](https://user-images.githubusercontent.com/76645095/179175880-402218ef-0093-44ab-b96c-e43d6e8b4375.png)  

위와같이 값이 채워져있다고 가정해보자. 여기서 22라는 값을 찾고 싶은 상황이다. 
그러면 가장먼저 루트노드부터 key 값과 22라는 값을 비교한다.  

![image](https://user-images.githubusercontent.com/76645095/179176031-ab057aeb-8512-4df5-b4f7-df7a19cae6ca.png)  

22는 루트 노드의 key 값인 12 보다는 크고, 24보다는 작기 때문에 사이에 있는 포인터가 가리키는 자식 노드로 이동하게 된다.  

![image](https://user-images.githubusercontent.com/76645095/179176091-ef773f2b-d534-4dde-9bb2-19fc8aff4ff5.png)  

그다음 자식 노드에서 key 값들과 22를 비교해본다. 

key 값중 가장 큰 값인 20보다 22가 크기 때문에 오른쪽에 있는 포인터를 이용해 자식 노드로 이동한다.

![image](https://user-images.githubusercontent.com/76645095/179176219-e820fa22-3622-4eb1-9a29-926b4af27a98.png)  

리프 노드까지 내려오니, 22의 값을 찾을 수있었다. 이제 같은 값을 발견했으므로, 검색을 중지한다.

여기서 주의해야 할 것은 하나의 노드에 여러개의 key가 존재할 수있다는 것이다. 

부모 노드 포인터가 가리키는 자식 노드로 내려왔다면, 자식 노드에서 다음 자식 노드를 찾기 위해 현재 노드에 있는 모든 key 들과 현재 찾고자 하는 값을 비교애햐 한다. 따라서 이 순간에는 어쩔수 없이 선형 탐색을 진행해야 한다. 


하지만, 여기서 각 노드의 key 들도 모두 '정렬'되어 있다는 특징을 이용하면 이분탐색을 적용해 좀더 효율적인 탐색을 진행할 수있다.

​
B-Tree에서 삽입 작업의 경우 루트 노드에서부터 시작하여 값을 비교하면서 -> 삽입될 위치를 먼저 찾고, 노드에 저장할 공간이 없으면 새로운 노드로 분할하여 값을 이동시킨 후 삽입한다. 이러한 과정을 통해 값이 새로 입력되더라도 트리는 향상 균형 상태를 유지한다.

## Hash
해시(Hash)는 데이터를 Key-Value 쌍으로 저장할 수 있는 자료구조이다.  
Hash는 Key를 해싱하여 Value가 저장된 위치를 빠르게 찾을 수있게 해주는데, 해시 충돌이 발생하지 않는다고 가정하면 값을 삽입하고, 삭제하고, 검색하는데 상수 시간이 소요된다.  
해시 충돌은 뒤에 나오는 내용이다.
<br>
<br>
<img width="880" alt="image" src="https://user-images.githubusercontent.com/76645095/179971994-701da9be-d876-4325-86b3-ba8c76564304.png">
<br>

그림을 보면, 4가지 영역이 존재하는 것을 볼 수있다. 각각의 영역의 역할은 아래와 같다.  
- Key : 우리가 key로 설정한 값, 해시 함수의 input값이 된다.
- Hash Function : 해시 함수는 input으로 들어온 사용자의 키를 변환한다. 이때 나오는 value는 위의 그림에서 Hash 영역의 값이다. 또한 Hash Function의 특징은 무조건 Value의 길이를 고정된 값으로 반환한다는 것이다. Key에 따라 Value의 길이가 변한다면 그만큼 공간 효율성이 떨어지기 때문에 무조건 길이가 같은 value를 반환하도록 한다.
- Hash : Hash Function로 처리된 Value로 데이터가 저장된 주소를 가리킨다. 
- Bucket : 데이터가 저장되는 공간이다.

이 요소들을 이해하면, Hash에서 왜 연산을 수행하는데 O(1)이 소요되는지 이해할 수있다.  
위의 그림에서는 탐색에 필요한 연산이 보이질 않는다. 그냥 Key에 대하여 Hash Function을 수행하고, 결과로 얻은 Value를 통해 데이터가 저장된 영역에 접근하면 된다.  
<br>
Hash Function 연산은 매우 빠른 시간내에 수행되므로, O(1)만에 데이터가 저장된 주소를 얻을 수있고, 바로 데이터에 접근할 수있다.  

이런 사기적인 자료구조를 왜? 안쓰고 다른 자료구조들을 쓸까? 그 이유는 간단하다.  

컴퓨터 자원이 유한하기 때문이다.  
모든 Key에 대하여 O(1) 접근을 보장하기 위해서는 HashFunction으로 얻은 Value에 대응하는 Bucket이 무수히 많아야 한다. 하지만, 우리가 Key로 선택할 수있는 값은 무한하다. 아주 쉬운 예시로 문자열을 무한대로 붙혀 Key로 사용하고, 대응하는 Bucket을 만든다해도 우리의 컴퓨터 자원은 언젠가는 고갈된다.  

따라서 Hash Function을 사용하는 많은 구현체들은 메모리를 절약하기 위하여 실제 해시 함수 표현 범위 N 보다 작은 'M'개의 Bucket만을 사용한다.  
이렇게 Bucket M개를 사용한다고 고정하면, Hash Function으로 얻은 Value 들은 1/M의 확률로 같은 Bucket을 사용하게 된다.  
서로 다른 Key가 같은 Bucket을 사용하게 되는 이 현상을 '해시 충돌'이라고 부르고, 해시 충돌은 해시 함수를 얼마나 잘 구현했는지 상관없이 무조건 발생한다.   

하지만, 해시 충돌이 발생하더라도 [Key - Value] 쌍 데이터를 잘 저장하고 조회할 수있게 하는 대표적인 방식이 2가지 존재하며 Hash를 사용하는 대부분의 자료구조는 이 두가지 방법을 응용한 것이다.  

1. Chaining  
Chaining은 Bucket에 연결리스트를 추가하는 방법이다. 
<br>
<br>
<img width="841" alt="image" src="https://user-images.githubusercontent.com/76645095/179980517-06255acc-4702-4700-b60b-d336ea314aba.png">
<br>
<br>
그림을 보면, 새로운 Key4가 Value4를 저장하려고 한다. 하지만, Hash Function으로 얻은 결과가 Key1의 Hash값과 충돌이 발생했다.  
여기서 Chaining 방식은 동일한 버킷에 저장하되, 연결 리스트 형식으로 데이터를 추가한다.  
<br>
이제 연결 리스트를 이용해 해시 충돌이 발생해도 값을 유지하지만, 연산에 필요한 시간복잡도는 더이상 O(1)이 아니다. 버킷에 존재하는 모든 연결리스트를 탐색해야 하기 때문에 탐색에 필요한 최악의 시간은 O(N)에 수렴하게 된다. 

2. Open Addressing  
Open Addressing은 Chaining과는 조금 다르게 비어있는 bucket 공간을 활용하는 특징을 가진다.
Open Addressing을 구현하는 방법에도 2가지로 쪼개지는데, 하나씩 살펴보자.  
    <br>
   (1) Linear Probing  
    <br>
    <img width="866" alt="image" src="https://user-images.githubusercontent.com/76645095/179980863-cbafcfed-99ab-42c8-b6f5-2c94136fdc22.png">
    <br>
    해시 충돌이 발생하면 단순히 한칸씩 옮기며 빈 공간을 찾고, 빈 공간을 찾으면 데이터를 Bucket에 저장한다.  
    매우 간단하지만, Chaining과 마찬가지로 더이상 삽입 연산에 필요한 시간복잡도는 O(1)이 아니며 최악의 경우 O(N)이 소요된다.  
    <br>
    Linear Probing 방식을 사용하면 한가지 문제가 또 존재한다. 바로 데이터들이 특정 위치에 집중된다는 것인데, 이 문제를 해결하기 위해서 아래의 방법이 사용된다.  
    <br>
    (2) Quadratic Probing
    <br>
    <br>
    <img width="836" alt="image" src="https://user-images.githubusercontent.com/76645095/179981851-3e22b45d-6421-4ff3-a903-eb5ccd6f8955.png">
    <br>
    <br>
    Quadratic Probing은 해시 충돌이 발생했을때 순차적으로 보지 않고, n^2씩 건너뛰며 빈 공간을 찾는다. 이러면 Linear Probing의 문제점을 해결할 수있지만, 마찬가지로 삽입 연산은 최악의 경우 O(N)에 수렴한다.