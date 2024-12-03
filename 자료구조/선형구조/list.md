# List
리스트는 자료를 정리하는 방법 중 하나이다.   

**데이터 구조의 모든 형태는 실제적으로 여러 종류의 리스트**를 의미한다.  
리스트는 배열과 연결리스트로 구현할 수 있음.   

**배열**로 구현할 시 **크기가 고정**됨

**연결리스트**로 구현 할 시 필요할 때 마다 **삽입, 삭제 용이**

- 리스트의 예시
    - 요일: (일요일, 월요일, ... , 토요일)
    - 한글 자음의 모임: (ㄱ, ㄴ, ... , ㅎ)

### 배열로 구현
리스트의 원소들이 기억장치의 저장 공간에 **연속적**으로 있음   

**장점** : 기억 장소의 활용도가 높고, **자주 변하지 않는 데이터의 저장**에 유리   

**단점** : 삽입, 삭제 시 데이터 이동 횟수가 많으며 여유분의 기억 장소 필요

예시)ㅤ| ㄱ | ㄴ | ㄷ | ㄹ | ㅁ |ㅤ->ㅤ( "ㄱ" 삭제 ) ->ㅤ| ㄴ | ㄷ | ㄹ | ㅁ |ㅤ|
   
예시로 보여주고 싶은 것은 "ㄱ"이 삭제 되면 **모든 데이터들이 한 칸씩 이동해야 한다는 것**이다. -> 시간 복잡도 큼

# 연결 리스트 
연결리스트는 자료를 기억하는 장소 이외에 다음 자료를 가리키는 포인터를 두어 자료의 삽입과 삭제 시 자료의 이동을 최소화 함

연결 리스트 Node의 구조   
| Data (자료 부분) -> 실제 원소 값 | Link (연결 부분) -> 다른 자료가 저장된 노드의 주소, 즉 포인터|   

이렇게 **두 부분 (Data, Link)** 으로 나뉜다.

**장점** : **노드의 삽입, 삭제가 용이**함ㅤ/ㅤ**연속적인 기억공간 없이도 저장** 가능   

**단점** : 연결부분의 사용으로 인해 배열보다 **많은 기억공간 필요**ㅤ/ㅤ알고리즘 **구현 복잡**ㅤ/ㅤ마지막 노드의 연결 부분에 NULL이 없거나 어떤 노드에서 포인터를 잃어버리면 다음 노드를 가리킬 수 없어서 **특정 노드 검색시 무한루프**에 빠질 수 있음

## 연결 리스트 구현 코드
1. 단순 연결 리스트 노드 정의
    ```c
    typedef int element;

    typedef struct ListNode{
        element data;
        struct ListNode *link;
    } ListNode;
    ```
2. 헤드 포인터 정의
    ```c
    ListNode *head = NULL;
    head = (ListNode *)malloc(sizeof(ListNode));
    ```
3. 노드의 생성
    ```c
    head->data = 10
    head->link=null;
    ```
4. 두 번째 노드 생성
    ```c
    ListNode *p;
    p = (ListNode *)malloc(sizeof(ListNode));
    p->data = 20;
    p->link = NULL;
    ```
5. 2개의 노드 연결
    ```c
    head->link = p;
    ```
### 결과
![result](./ListEx.png)

## 단순 연결 리스트 연산
1. 삽입 연산   

    i. insert_first      
    ```c
    ListNode* insert_first(ListNode *head, element value){
        ListNode *p = (ListNode *)malloc(sizeof(ListNode));
        p->data = value;
        p->link = head;
        head = p;
        return head;
    }
    ```

    ii.   
    ```c
    ListNode* insert(ListNode *head, ListNode *pre, element value){
        ListNode *p = (ListNode *)malloc(sizeof(ListNode));
        p->data = value;
        p->link = pre->link;
        pre->link = p;
        return head;
    }
    ```
2. 삭제 연산  

    i. delete_first
    ```c
    ListNode* delete_first(ListNode *head){
        ListNode *removed;
        if(head == NULL) return NULL;
        removed = head;
        head = removed->link;
        free(removed);
        return head;
    }
    ```

    ii. delete
    ```c
    ListNode* delete(ListNode *head, ListNode *pre){
        ListNode *removed;
        removed = pre->link;
        pre->link = remode->link;
        free(removed);
        return head;
    }

### 리스트를 역순으로 구현하는 코드
```c
ListNode* reverse(ListNode *head){
    // 순회 포인로 p, q, r을 사용
    ListNode *p, *q, *r;
    p = head;
    q = NULL;
    while(p != NULL){
        r = q;
        q = p;
        p = p->link;
        q->link = r;
    }
    return q;
}
```
# 원형 연결 리스트
원형 연결 리스트는 **마지막 노드의 링크가 첫 번째 노드를 가리키는** 리스트

**장점** : 한 노드에서 다른 모든 노드로의 접근이 가능

## 원형 연결 리스트 연산
1. 삽입
    i. insert_first
    ```c
    void insert_first(ListNode *head, element data){
        ListNode *node = (ListNode*)malloc(sizeof(ListNode));
        node -> data = data;
        if(head == NULL){
            head = node;
            node->link = head;
        }
        else{
            node->link = head->link;
            head->link = node;
        }
        return head;
    }
    ```
    ii. insert_last
    ```c
    void insert_last(ListNode *head, element data){
        ListNode *node = (ListNode*)malloc(sizeof(ListNode));
        node->data = data;
        if(head == NULL){
            head = node;
            node->link = head;
        }
        else{
            node->link = head->link;
            head->link = node;
            head = node;
        }
        return head;
    }
    ```
# 이중 연결 리스트
하나의 노드가 선행 노드와 후속 노드에 대한 **두 개의 링크**를 가지는 리스트,  
 링크가 양방향이므로 양방향으로 검색이 가능 그러나 **공간을 많이 차지**하고 **코드가 복잡**.

## 이중 연결 리스트의 노드 구조
```c
typedef int element;
typedef struct DlistNode{
    element data;
    struct DlistNode *llink;
    struct DlistNode *rlink;
} DlistNode;
```
## 이중 연결 리스트 연산
1. 삽입
    ```c
    void dinsert_node(DlistNode *before, DlistNode *new_node){
        new_node->llink = before;
        new_node->rlink = before->link;
        before->rlink->llink = new_node;
        before->rlink = new_node;
    }
    ```
2. 삭제
    ```c
    void dinsert_node(DlistNode *phead_node, DlistNode *removed){
        if(removed == phead_node) return;
        removed->llink->rlink = removed->rlink;
        removed->rlink->llink = removed->llink;
        free(removed);
    }
    ```