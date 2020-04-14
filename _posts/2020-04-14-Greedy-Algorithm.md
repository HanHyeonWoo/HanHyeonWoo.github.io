layout: single
title:  "Greedy Algorithm"
date:   2020-04-09 17:12:00 +0900
categories: jekyll update
use_math: true

---

### 문제

09시부터 18시까지 a시간 ~ b시간(1시간 단위, 최소 1시간 이상) 수업을 하는 n개의 강의를 입력받고 하루에 들을 수 있는 최대 강의 수를 구하여라.

### 접근법

강의를 입력받고, 이 강의를 듣냐 안듣냐 중 최고의 선택은 강의를 듣는 것이기 때문에 들을 수 있다면 듣는다.



### 소스코드

```
#include <stdio.h>

typedef struct Lecture {
	int a;
	int b;
}Lecture;

Lecture L[100000];
int a, b, n, N = 0, check = 0;
int time[18] = { 0 }; //시간표 배열. 수업이 없으면 0 있으면 1로표시

int main() {
	printf("강의 수를 입력하세요 : ");
	scanf_s("%d", &n);
	for (int i = 0; i < n; i++) {
		printf("%d번째 강의 시작 시간과 종료 시간을 입력 하세요(9시 ~ 18시 사이) : ",i+1);
		scanf_s("%d %d", &L[i].a, &L[i].b);
		for (int j = L[i].a; j < L[i].b; j++) {
			check += time[j];	//강의의 시작시간과 끝시간 사이에 수업이 있나 체크
			if (j == (L[i].b - 1) && check == 0) {	//수업이 없다면
				for (int k = L[i].a; k < L[i].b; k++) {
					time[k] = 1;	//해당 시간대의 값을 1로 바꾸고
					if (k == L[i].b - 1) N++; //들을 수 있는 강의 수 +1
				}
			}
			else if(j == (L[i].b - 1) && check >0) check = 0;
		}
	}

	printf("%d", N);
	

	return 0;
}
```





