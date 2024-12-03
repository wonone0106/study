# Stack
스텍은 원소의 삽입, 삭제가 **한쪽** 끝에서만 발생하는 선형 리스트이다.    
이런 입출력 형태를 **LIFO(후입선출)** 이라고 한다.

## Stack의 연산
1. 삽입 연산
    ```c
    #define STACK_SIZE 5
    typedef int element;
    element stack[STACK_SIZE];
    int top = -1;

    void push(element item){
        if(top>=STACK_SIZE-1){
            printf("Stack is Full!\n");
            return;
        }
        else return stack[++top] = item;
    }
    ```
2. 삭제 연산
    ```c
    #define STACK_SIZE 5
    typedef int element;
    element stack[STACK_SIZE];
    int top = -1;

    element pop(){
        if(top == -1){
            printf("Stack is Empty!!\n");
            return ();
        }
        else return stack[top--];
    }
    ```


### stack 예시
---
#### EmptyStack -> push(A) -> push(B) -> pop -> push(C) -> push(D) -> pop    


|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->  
| A |ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->   
| A | B |ㅤ|ㅤ|ㅤ|ㅤ->    
| A |ㅤ|ㅤ|ㅤ|ㅤ|ㅤ->    
| A | C |ㅤ|ㅤ|ㅤ|ㅤ->    
| A | C | D |ㅤ|ㅤ|ㅤ->    
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

