# DataStructure

* [Array](#array)


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

<img width="685" alt="image" src="https://user-images.githubusercontent.com/76645095/178654041-6cd10cbd-ed3a-4f14-ac73-f826d6b0e971.png">  

<br>
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

