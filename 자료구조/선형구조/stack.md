# Stack
스텍은 원소의 삽입, 삭제가 **한쪽 끝에서만 발생**하는 선형 리스트이다.    

스텍의 입출력 형태는 **LIFO(후입선출)** 이며, **가장 나중에 들어온 데이터가 가장 먼저 나가는 형태**이다.

**top** : **마지막에 들어온 데이터**를 가리키는 포인터 변수이다.   
**element** : 스텍을 구성하는 **데이터 타입**이다.
## Stack의 연산
1. is_full
    ```c
    int is_full(){
        if(top>=STACK_SIZE-1){
            return true;
        }
        else return false;
    }
    ```
2. is_empty
    ```c
    int is_empty(){
        if(top==-1){
            return true;
        }
        else return false;
    }
    ```
3. 삽입 연산
    ```c
    #define STACK_SIZE 5
    typedef int element;
    element stack[STACK_SIZE];
    int top = -1;

    void push(element item){
        if(is_full()==true){
            printf("Stack is Full!\n");
        }
        else return stack[++top] = item;
    }
    ```
4. 삭제 연산
    ```c
    #define STACK_SIZE 5
    typedef int element;
    element stack[STACK_SIZE];
    int top = -1;

    element pop(){
        if(is_empty()==true){
            printf("Stack is Empty!!\n");
        }
        else return stack[top--];
    }
    ```


### stack 예시
---
#### EmptyStack(5) -> push(A) -> push(B) -> pop -> push(C) -> push(D) -> pop    


|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A |ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A | B |ㅤ|ㅤ|ㅤ|ㅤ->    

| A |ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A | C |ㅤ|ㅤ|ㅤ|ㅤ->ㅤ| A | C | D |ㅤ|ㅤ|ㅤ->    

| A | C |ㅤ|ㅤ|ㅤ|

---
## 스택의 응용
#### 중위 표기식을 후위식으로 표현 및 후위식을 계산 기능 구현 가능
1. 전위 표기식   
    **a + b - c * d / fㅤ->ㅤ- + a b / * c d f**
2. 중위 표기식    
    **a + b - c * d / fㅤ->ㅤa + b - c * d / f**
3. 후위 표기식   
    **a + b - c * d / fㅤ->ㅤa b + c d * f / -** 

