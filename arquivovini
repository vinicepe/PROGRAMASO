#include <stdio.h>

#include <stdlib.h>

#include <pthread.h>

 

typedef struct {

  int saldo;

} conta;

 

conta from, to;

int valor;

pthread_mutex_t mutex;

 

// The child thread will execute this function

void *transferencia(void *arg)

{

  pthread_mutex_lock(&mutex);

 

  if (from.saldo >= valor){ // 2

    from.saldo -= valor;

    to.saldo += valor;

  }

 

  printf("Transferência concluída com sucesso!\n");

  printf("Saldo de c1: %d\n", from.saldo);

  printf("Saldo de c2: %d\n", to.saldo);

 

pthread_mutex_unlock(&mutex);

  return NULL;

}

 

#define NTHREADS 10

 

int main()

{

  pthread_t threads[NTHREADS];

 

  if ( pthread_mutex_init(&mutex, NULL) ) {

    perror("pthread_mutex_init");

    exit(1);

  }

 

  // Todas as contas começam com saldo 100

  from.saldo = 100;

  to.saldo   = 100;

  valor      = 10;

  puts("Transferindo 10 para a conta c2");

 

  for (int i = 0; i < NTHREADS; i++) {

    if ( pthread_create(&threads[i], NULL, transferencia, NULL) ) {

      perror("pthread_create");

      exit(2);

    }

  }

 

  for (int i = 0; i < NTHREADS; i++)

    pthread_join(threads[i], NULL);

 

  printf("Transferências concluídas e memória liberada.\n");

  return 0;

}
