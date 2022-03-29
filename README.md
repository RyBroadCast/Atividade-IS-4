# Atividade-IS-4

Esta atividade tem como objetivo escrever um programa que simule o algoritimo Round Robin para escalonamento de processos, e que calcule 3 metricas:
- Tempo ativo medio
- Tempo de resposta medio
- Tempo de espera medio


### Como executar:
Através dos comandos:
 - ```make```
 - ```make run```
 - ```make clean```

### Código:
Incluindo bibliotecas e declarando funções:
```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

 struct queue{
    int arrival_time;
    int burst_time;
    struct queue *next;
 };

void enqueue(struct queue **head, struct queue **tail, int a, int b);
int isEmpty(struct queue *head);
```

Função int main(), recebe as entradas, adiciona em uma fila e printa as medias dos valores pedidos.
```c
int main()
{

      struct queue *head = NULL;
	  struct queue *tail = NULL;
  
      int i, nProcess, total = 0, x, validate = 0, time_quantum;
      int wait_time = 0, turnaround_time = 0, arrival_time = 0, burst_time = 0,    
      active_time = 0;
      float average_wait_time, average_turnaround_time, average_active_time;
      scanf("%d %d", &nProcess, &time_quantum);
      x = nProcess;
      for(i = 0; i < nProcess; i++)
      {
 
            scanf("%d %d", &arrival_time, &burst_time);
 
            enqueue(&head, &tail, arrival_time, burst_time);
      }

      struct queue *aux = head;
 
      for(total = 0, i = 0; x != 0;)  {
            if (aux->burst_time <= time_quantum && aux -> burst_time > 0) {
                total += aux -> burst_time;
                aux -> burst_time = 0;
                validate = 1;
            }
            else if (aux -> burst_time > 0) {
                aux -> burst_time = aux -> burst_time - time_quantum;
                total += time_quantum;
            }
        
            if (aux -> burst_time == 0 && validate == 1) {
                x--;
                wait_time += total - aux -> arrival_time - aux -> arrival_time;
                turnaround_time += total - aux -> arrival_time;
                active_time += total;
                validate = 0;
            }
        
            if (aux->next == NULL) { 
                aux = head;          
            }
              
            else if (head -> next -> arrival_time <= total) {
                aux = aux -> next;
            }
              
            else {
                aux = head;
            }
      }
 
      average_wait_time = wait_time * 1.0 / nProcess;
      average_turnaround_time = turnaround_time * 1.0 / nProcess;
      average_active_time = active_time * 1.0 / nProcess;
      
      printf("\nRR %f %f %f", average_active_time, average_turnaround_time, average_wait_time);


      return 0;
}
```

Função enqueue (fila):
```c
void enqueue(struct queue **head, struct queue **tail, int a, int b){

    struct queue *novo = (struct queue *)malloc(sizeof(struct queue));
    	if(novo != NULL){
    		novo-> arrival_time = a;
    		novo -> burst_time = b;
    		novo->next = NULL;
    
    		if(isEmpty(*head)){
    			*head = novo;
    			*tail = novo;
    		}
        else{
    			(*tail)->next = novo;
    			*tail = novo;
    		}
    	}
}
```

Função isEmpty:
```c
int isEmpty(struct queue *head){
    return head == NULL;
  }
```
