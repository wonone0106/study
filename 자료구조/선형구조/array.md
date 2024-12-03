# Array

배열이란 동일한 **데이터형(data type)** 을 가진 원소가 **순서적**으로 구성된 집합이다.   
자료들을 **연속적인** 기억 장소에 저장한다
   

### C언어 예제
```c
int main(){
    int array[5], i = 0;

    array[0] = 1;
    array[1] = 2;
    array[2] = 3;
    array[3] = 4;
    array[4] = 5;

    for(i; i<5; i++){
        printf("%d", array[i]);
    }
}
```
출력 값: 12345
