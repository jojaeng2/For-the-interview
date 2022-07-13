# DataStructure
- [DataStructure](#datastructure)
  - [Array](#array)
  - [List](#list)
  - [Stack](#stack)
  - [Queue](#queue)
  


</br>

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
    int count;
    Stack() { //생성자
        head = new Node(); //더미노드
        count = 0;
    }
 
    void pop() { //데이터 제거
        Node *tmp = head;
        head = head->next; 
        delete tmp; 
        count--;
    }
 
    void push(int i) { //데이터 삽입
        new Node(i, head);
        count++;
    }

};
```


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
    int len = 0;
    LinkedQueue() {
        front = rear = NULL;
    }
    bool isEmpty() {
        return len ==0;
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
        len++;
    }
 
    int pop() {
 
        Node *delNode = front;
        int ret = delNode->data;
        front = delNode->next;
        free(delNode);
        len--;
        return ret;
    }
};
 

```