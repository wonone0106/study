# Queue
큐는 원소의 삽입, 삭제가 **양쪽**에서 발생하는 선형 리스트이다.    

큐의 입출력 형태는 **선입선출(FIFO)** 이며, **가장 먼저 들어온 데이터가 가장 먼저 나가는 형태**이다.

**front** : **삭제된 데이터가 있던 장소**를 가리키는 포인터이다.   
**rear** : **데이터가 삽입된 장소**를 가리키는 포인터이다.   
**element** : 큐를 구성하는 **데이터 타입**이다.

## Queue의 구조체
```c
#define QUEUE_SIZE 5
typedef int element;

typedef struct{
    element data[QUEUE_SIZE];
    int rear, front;
} QueueTpye;
```

## Queue의 연산
1. init (초기화)
    ```c
    void init(QueueTpye *Q){
        Q->rear = Q->front = -1;
    }
    ```
2. is_full
    ```c
    int is_full(QueueTpye *Q){
        if(Q->rear==QUEUE_SIZE-1){
            return true;
        }
        else return false;
    }
    ```
3. is_empty
    ```c
    int is_empty(QueueTpye *Q){
        if(Q->rear==Q->front){
            return true;
        }
        else return false;
    }

4. 삽입 연산
    ```c
    void enqueue(QueueTpye *Q, element item){
        if(is_full(Q)){
            print("Queue is Full!\n");
        }
        else return Q->data[++(Q->rear)] = item;
    }
    ```
5. 삭제 연산
    ```c
    element dequeue(QueueTpye *Q){
        if(is_empty(Q)){
            print("Queue is Empty!\n");
        }
        else return Q->data[++(Q->front)];
    }
    ```

## 선형 Queue의 단점
큐를 사용하면 할수록 **front가 뒤로 밀려나게 되므로 앞에 있는 공간을 활용하지 못한다.**   

예시) EmptyQueue(5) -> enqueue(A) -> enqueue(B) -> dequeue() -> enqueue(C)   

|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A |ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A | B |ㅤ|ㅤ|ㅤ|ㅤ->   

|ㅤ| B |ㅤ|ㅤ|ㅤ|ㅤ->ㅤ|ㅤ| B | C |ㅤ|ㅤ|ㅤ

위 예시와 같이 A 의 자리에 더 이상 데이터를 삽입 및 삭제를 할 수 없다.

이 단점을 보완하기 위해 만들어진 것이 **원형 큐**이다.

# Circular Queue
선형 큐의 **이미 사용한 앞공간은 쓸 수 없다는 단점을 보완**하기 위하여 만들어진 큐이다.

**rear, front** : 각 변수들이 하는 기능은 같지만 **초기값이 "0" 이다.**   


## Queue의 연산
1. init (초기화)
    ```c
    void init(QueueTpye *Q){
        Q->rear = Q->front = 0;
    }
    ```
2. is_full
    ```c
    int is_full(QueueTpye *Q){
        if(Q->front==(Q->rear+1)%QUEUE_SIZE){
            return true;
        }
        else return false;
    }
    ```
3. is_empty
    ```c
    int is_empty(QueueTpye *Q){
        if(Q->rear==Q->front){
            return true;
        }
        else return false;
    }

4. 삽입 연산
    ```c
    void enqueue(QueueTpye *Q, element item){
        if(is_full(Q)){
            print("Queue is Full!\n");
        }
        else{
            Q->rear = (Q->rear + 1) % QUEUE_SIZE;
            return Q->data[(Q->rear)] = item;
        }
    }
    ```
5. 삭제 연산
    ```c
    element dequeue(QueueTpye *Q){
        if(is_empty(Q)){
            print("Queue is Empty!\n");
        }
        else{
            Q->front = (Q->front + 1) % QUEUE_SIZE;
            return Q->data[(Q->front)];
        }
    }
    ```