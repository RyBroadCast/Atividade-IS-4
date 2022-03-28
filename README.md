# Atividade-IS-4

Esta atividade tem como objetivo escrever um programa com múltiplas threads que receba valores na linha de comando e crie 3 threads para fazer 3 funções diferentes:
- Retornar o valor máximo
- Retornar o valor médio
- Retornar o valor mínimo


### Como executar:
Através dos comandos:
 - ```make```
 - ```make run```
 - ```make clean```

### Código:
Incluindo bibliotecas, declarando variáveis e funções:
```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#define MAXARR 1024

int max_num, min_num, average_num;
int num_amount, arr[MAXARR], i;

void *average();
void *max();
void *min();
```
Função int main(), recebe os números, cria as threads e printa os resultados das operações feitas nas funções.
```c
int main() {

        int num = 0, i, t;

        scanf("%d",&num_amount);

        for (i = 1; i < num_amount + 1; i++) {
                scanf("%d",&num);
                arr[i] = num;
        }

        pthread_t t1;
        pthread_t t2;
        pthread_t t3;

        t = pthread_create(&t1,NULL,&average, NULL);
        pthread_join(t1,NULL);

        t = pthread_create(&t2,NULL,&min, NULL);
        pthread_join(t2,NULL);

        t = pthread_create(&t3,NULL,&max, NULL);
        pthread_join(t3,NULL);
        printf("The average value is %d\n",average_num);
        printf("The minimum value is %d\n",min_num);
        printf("The maximum value is %d\n",max_num);


        return 0;
}
```

Função average (média):
```c
void *average() {
        int sum = 0;
        for (int i = 1; i <= num_amount; i++){
                sum = sum + arr[i];
        }

        average_num = sum / num_amount;

}
```

Função max (maior número):
```c
void *max() {
        max_num = arr[1];
        for (int i = 1; i <=  num_amount; i++) {
                if(arr[i] > max_num) {
                         max_num = arr[i];
                }
```

Função min (menor número):
```c
void *min() {
        min_num = arr[1];
        for (int i = 1; i < num_amount; i++) {
                if(arr[i] < min_num) {
                         min_num = arr[i];
                }
        }
}
```
