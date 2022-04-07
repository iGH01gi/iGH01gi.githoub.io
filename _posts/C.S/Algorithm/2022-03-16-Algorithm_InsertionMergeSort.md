---
layout: post
title: time complexity의 함정
date: 2022-04-08 00:00:00+0900
category: Algorithm
published: true
---
알고리즘을 실제 코드로 구현하며 execution time을 측정해보면서 느낀 점이 있어 글을 적는다.  
결론은 어떤 알고리즘의 time complexity가 같은 output을 내는 다른 알고리즘의 그것보다 작다고 하여도 무조건적으로 우월한 알고리즘이라고 할 수 없다는 것이다.   
그 예로 matrix multiplication을 예로 들겠다.  
![](/images\Algorithm\matrix.png)  
matrix multiplication은 위와같은 방법으로 행해지게 된다.  
결과를 얻기 위해서(c로 이루어진 matrix)
matrix의 multiplication을 일반적인 방법으로 계산하게 되면 **O(n<sup>3</sup>)**의 시간복잡도를 지니게된다.(for문을 3중첩으로 사용해야 하기때문이다.)  
다음은 30x10행렬과 10x50행렬을 일반적인 방법으로 곱하는 코드이다. 이를 보면 왜 O(n<sup>3</sup>)인지 알수있다.
```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
void setting_matrix(int* arr,int row,int column)
{
    for(int i=0; i<row; i++)
    {
        for(int j=0; j<column; j++)
        {
            int input;
            scanf("%d",&input);
            *(arr+i*column+j)=input;
        }
    }
}
int main()
{
    clock_t start,end;
    int arr1[30][10];
    printf("input 30x10 matrix:\n");
    setting_matrix((int*)arr1,30,10);
    int arr2[10][50];
    printf("input 10x50 matrix:\n");
    setting_matrix((int*)arr2,10,50);
    
    int count=1;
    int result[30][50];

    start=clock();
    for(int i=0; i<30; i++)
    {
        for(int k=0; k<50; k++)
        {
            int temp=0;
            for (int j = 0; j < 10; j++)
            {
                temp+= arr1[i][j] * arr2[j][k];         //for문이 3중첩이므로 O(n^3)
                count++;
            }
            result[i][k]=temp;
        }
    }
    end=clock();
    double running_time;
    running_time=(double)(end-start);

    printf("\n\noutputs:\n");
    for(int i=0; i<30; i++)
    {
        for(int j=0; j<50; j++)
        {
            printf("%3d|",result[i][j]);
        }
        printf("\n");
    }
    printf("execution time:%lfms  iter_count:%d",running_time,count);
}
```  
# Strassen Algorithm은 그럼 더 효율적인가?
그리고 행렬의 곱을 계산하는 유명한 알고리즘이 하나가 있다.  
그것은 **Strassen Algorithm**인데 이것의 time complexity는 **O(n<sup>lg7</sup>)**=(lg7은 대략 2.81이다)  
즉, 시간복잡도만 본다면 일반적인 행렬 곱(O(n<sup>3</sup>))보다 효율적이라고 생각할수있다.  

<br>
아래는 Strassen Algorithm의 간략한 설명이다.   
![](\images\Algorithm\strassen.png)  
**위와 같이 matrix를 4등분하여서 나눠서 계산한다.** 

<br>
![](\images\Algorithm\strassen2.png)  
**divide and conquer**을 사용하는 알고리즘이기 때문에 **Master Method**에 의해서 **O(n<sup>lg7</sup>)**이 나온다.  

<br>
아래는 Strassen Algorithm을 C언어로 구현한 코드다. 이것또한 30x10행렬과 10x50행렬의 곱을 계산하는 코드이다.  
(Strassen Algorithm을 계산하기 위해서는 행렬이 정방행렬이여야 하고 한 줄의 길이가 2<sup>n</sup>를 만족해야하기 때문에 64x64행렬로 만든 뒤 빈 자리에는 0을 넣어준다.)  
(막 코딩한것이라 좀 지저분하다)  
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>

void setting_matrix(int* arr,int row,int column)
{
    for(int i=0; i<row; i++)
    {
        for(int j=0; j<column; j++)
        {
            int input;
            scanf("%d",&input);
            *(arr+i*64+j)=input;
        }
    }
}
void setting_submatrix(int *from_arr,int* to_arr, int len,int spot) 
{
    switch (spot)
    {
    case 1:
        for (int i = 0; i < len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                *(to_arr + i * len + j) = *(from_arr + i * len*2 + j);
            }
        }
        break;
    case 2:
        for (int i = 0; i < len; i++)
        {
            for (int j = len; j < 2*len; j++)
            {
                *(to_arr + i * len + (j%len)) = *(from_arr + i * len*2 + j);
            }
        }
        break;
    case 3:
        for (int i = len; i < 2*len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                *(to_arr + (i%len) *len + j) = *(from_arr + i * len*2 + j);
            }
        }
        break;
    case 4:
        for (int i = len; i < 2*len; i++)
        {
            for (int j = len; j < 2*len; j++)
            {
                *(to_arr + (i%len) * len + (j%len)) = *(from_arr + i * len*2 + j);
            }
        }
        break;
    }
}

void merge_matrix(int *from_arr,int* to_arr, int len,int spot) //len은 from_arr의 한 변의 길이, 즉 더 작은 매트릭스의 길이
{
    switch (spot)
    {
    case 1:
        for (int i = 0; i < len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                *(to_arr + i * len*2 + j) = *(from_arr + i * len + j);
            }
        }
        break;
    case 2:
        for (int i = 0; i < len; i++)
        {
            for (int j = len; j < 2*len; j++)
            {
                *(to_arr + i * len*2 + j) = *(from_arr + i *len + (j%len));
            }
        }
        break;
    case 3:
        for (int i = len; i < 2*len; i++)
        {
            for (int j = 0; j < len; j++)
            {
                *(to_arr + i*(len*2) + j) = *(from_arr + (i%len)*len + j);
            }
        }
        break;
    case 4:
        for (int i = len; i < 2*len; i++)
        {
            for (int j = len; j < 2*len; j++)
            {
                *(to_arr + i*(len*2) + j) = *(from_arr + (i%len)*len + (j%len));
            }
        }
        break;
    }
}

int* minus(int* arr1,int* arr2,int len)
{
    int* temp=(int*)malloc(sizeof(int)*len*len);
    memset(temp,0,sizeof(int)*len*len);
    for(int i=0; i<len; i++)
    {
        for(int j=0; j<len; j++)
        {
            *(temp+i*len+j)=*(arr1+i*len+j)-*(arr2+i*len+j);
        }
    }
    return temp;
}

int* plus(int* arr1,int* arr2,int len)
{
    int* temp=(int*)malloc(sizeof(int)*len*len);
    memset(temp,0,sizeof(int)*len*len);
    for(int i=0; i<len; i++)
    {
        for(int j=0; j<len; j++)
        {
            *(temp+i*len+j)=*(arr1+i*len+j)+*(arr2+i*len+j);
        }
    }
    return temp;
}
int count=1;
int* strassen(int* arr1,int* arr2,int len) 
{
    count++;
    if(len==1)
    {
        int* temp_1=(int*)malloc(sizeof(int));
        memset(temp_1,0,sizeof(int));
        *temp_1=(*(arr1))*(*(arr2));
        return temp_1;
    }
    else
    {
        int *a = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(a,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr1, a, len/2, 1);
        int *b = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(b,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr1, b, len/2, 2);
        int *c = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(c,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr1, c, len/2, 3);
        int *d = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(d,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr1, d, len/2, 4);
        int *e = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(e,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr2, e, len/2, 1);
        int *f = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(f,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr2, f, len/2, 2);
        int *g = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(g,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr2, g, len/2, 3);
        int *h = (int *)malloc(sizeof(int) * ((len / 2) * (len / 2))); memset(h,0,sizeof(int) * ((len / 2) * (len / 2)));
        setting_submatrix(arr2, h, len/2, 4);

        // p1
        int *a_prime = minus(f, h, len/2);
        int *p1 = strassen(a, a_prime,len/2);
        free(a_prime);
        //p2
        int* h_prime=plus(a,b,len/2);
        int *p2=strassen(h_prime,h,len/2);
        free(h_prime);
        //p3
        int* e_prime=plus(c,d,len/2);
        int* p3=strassen(e_prime,e,len/2);
        free(e_prime);
        //p4
        int* d_prime=minus(g,e,len/2);
        int* p4=strassen(d,d_prime,len/2);
        free(d_prime);
        //p5
        int* first5=plus(a,d,len/2); int* second5=plus(e,h,len/2);
        int* p5=strassen(first5,second5,len/2);
        free(first5); free(second5);
        //p6
        int* first6=minus(b,d,len/2); int* second6=plus(g,h,len/2);
        int* p6=strassen(first6,second6,len/2);
        free(first6); free(second6);
        //p7
        int* first7=minus(a,c,len/2); int* second7=plus(e,f,len/2);
        int* p7=strassen(first7,second7,len/2);
        free(first7); free(second7);

        free(a); free(b); free(c); free(d); free(e); free(f); free(g); free(h);

        //r,s,t,u구해서 완성된 matrix를 반환
        //r
        int* r_first=plus(p5,p4,len/2); int* r_second=minus(r_first,p2,len/2);
        int* r=plus(r_second,p6,len/2);
        free(r_first);free(r_second);  free(p6); //p6 더이상 사용x
        //s
        int* s=plus(p1,p2,len/2);
        free(p2); //p2 더이상 사용x
        //t
        int* t=plus(p3,p4,len/2);
        free(p4);
        //u
        int* u_first=plus(p5,p1,len/2); int* u_second=minus(u_first,p3,len/2);
        int* u=minus(u_second,p7,len/2);
        free(u_first); free(u_second); free(p1); free(p3); free(p5); free(p7);

        int* result=(int*)malloc(sizeof(int)*len*len); memset(result,0,sizeof(int)*len*len);
        merge_matrix(r,result,len/2,1); merge_matrix(s,result,len/2,2); merge_matrix(t,result,len/2,3); merge_matrix(u,result,len/2,4);
        free(r); free(s); free(t); free(u);
        return result;
    }
    
}
int main()
{
    clock_t start,end;
    int* arr1=(int*)malloc(sizeof(int)*64*64);
    memset(arr1,0,sizeof(int)*64*64);
    printf("30x10 매트릭스를 입력하세요(띄어쓰기로 구분)\n");
    setting_matrix((int*)arr1,30,10);
    int* arr2=(int*)malloc(sizeof(int)*64*64);
    memset(arr2,0,sizeof(int)*64*64);
    printf("10x50 매트릭스를 입력하세요(띄어쓰기로 구분)\n");
    setting_matrix((int*)arr2,10,50);

    int len=64; //2^n의 값 중에서 arr1,arr2의 행,열중 가장 큰값을 처음으로 초과하는 값이 len
    start=clock();
    int* result=strassen(arr1,arr2,len);
    end=clock();
    for(int i=0; i<30; i++)
    {
        for(int j=0; j<50; j++)
        {
            printf("%3d|",*(result+i*64+j));
        }
        printf("\n");
    }
    double running_time;
    running_time=(double)(end-start);
    printf("execution time:%lfms  number of function call:%d",running_time,count);
    free(result);
    free(arr1);
    free(arr2);
}
```

처음에 쓴 일반적인 행렬의곱 방식과 이 Strassen Algorithm을 적용한 코드의 running time은 어떻게 차이가날까?  
놀랍게도 30x10,10x50행렬을 곱한다는 기준으로 전자는 0.000000ms 이었고 알고리즘을 적용했을때는 174.000000ms이 측정되었다.  
그리고 일반적인 곱 방식에서는 곱 연산이 iteration count:15001번 일어났지만 Strassen Algorithm은 단순 function call만해도 137258번이나 발생하였다.
내 예상과는 반대였다.  왜 그럴까?  
고민한 결과 내 결론은 다음과 같다.  
1. 내 코드 기준 Strassen Algorithm은 동적메모리할당과 해제가 자주 일어나고 heap메모리를 더 자주쓰게 된다.  
2. Strassen Algorithm을 적용하였을때 총 instruction이 더 많이 실행되었다. 이는 divide and conquer특성상 내 코드에서는 n이 충분히 크지 못하기때문에 일반적인 방식보다 총 연산의 횟수가 많아진것으로 생각한다.(+일반 곱방식은 행렬을 그대로 이용했지만 Strassen은 64x64로 변환하여 더욱 큰 행렬이 되었다)  

<br>
그럼 어떻게해야 Strassen Algorithm을 효율적으로 사용할수 있을까?   
물론 이것도 나의 생각이지만 먼저 Strassen Algorithm이 일반적인 행렬 계산보다 더 효율적이게 되는 'n'지점을을 찾는다. (여기서 n은 정방행렬의 길이)  
그리고 그 n미만일 경우에는 일반적인 행렬의 곱을 적용시키고 n보다 클때는 Strassen Algorithm을 적용하게 코드를 짠다면 효율적으로 돌아가는 코드를 짤 수 있을 것 같다.  
(n값은 컴퓨터에 따라 유동적으로 변할것으로 생각이된다. 왜냐하면 컴퓨터마다 계산을 처리하는 방식이 다를테고 속도도 다르기때문에 n지점이 제각각일것이기 때문이다.)  