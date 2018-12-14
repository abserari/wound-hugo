+++
author = "Abser"
categories = ["C","Unix编程"]
date = "2018-12-14"
description = "多生产者单消费者模型"
featured = "pic01.jpg"
featuredalt = "猎人"
featuredpath = "date"
linktitle = ""
title = "Produce Consume"
type = "post"

+++

## __ Processes Programming__

### Task description:
Create 3 processes to handle data. One process *PGone* generates int numbers and stores them in a loop array including 10 elements. One process *PGtwo* also generates int numbers and stores them in the same loop array. One process *PS* stores the generated numbers into a txt file in hard disk.
 
### Requests:
1. The 3 processes should work concurrently.
2. *PGone and PGtwo *can generate numbers at any time as long as the array is not occupied by the other processes, and there still remains spaces or there exists elements that have been stored by *PS*.
3. *PS *can store numbers at any time as long as there exists numbers that have not been stored.

## Solution
```c
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define NBUFF 10
#define MAXNTHREADS 20

int nitems, npg;

struct
{
    int buff[NBUFF];
    int nput;
    int nputval;
    sem_t mutex, nempty, nstored;
} shared;

void *PG(), *PS();

int main(int argc, char **argv)
{
    int i;
    pthread_t tid_PG[MAXNTHREADS], tid_PS;

    if (argc != 3)
        exit(2);
    nitems = atoi(argv[1]);
    npg = atoi(argv[2]) > MAXNTHREADS ? MAXNTHREADS : atoi(argv[2]);

    /* initialize semaphores */
    sem_init(&shared.mutex, 0, 1);
    sem_init(&shared.nempty, 0, NBUFF);
    sem_init(&shared.nstored, 0, 0);

    /* create PG and PS */
    for (i = 0; i < npg; i++)
    {
        pthread_create(&tid_PG[i], NULL, PG, NULL);
    }
    pthread_create(&tid_PS, NULL, PS, NULL);

    /* wait for end */
    for (i = 0; i < npg; i++)
    {
        pthread_join(tid_PG[i], NULL);
    }
    pthread_join(tid_PS, NULL);

    /* end work */
    sem_destroy(&shared.mutex);
    sem_destroy(&shared.nempty);
    sem_destroy(&shared.nstored);

    exit(0);
}

void *
PG()
{
    for (;;)
    {
        sem_wait(&shared.nempty);
        sem_wait(&shared.mutex);

        if (shared.nput >= nitems)
        {
            sem_post(&shared.nempty);
            sem_post(&shared.mutex);
            return (NULL);
        }

        /* generate int number */
        shared.buff[shared.nput % NBUFF] = shared.nputval;
        shared.nput++;
        shared.nputval++;

        usleep(300);
        sem_post(&shared.mutex);
        sem_post(&shared.nstored);
    }
}

void *
PS()
{
    int i;

    FILE *fpWrite = fopen("data.txt", "w");
    for (i = 0; i < nitems; i++)
    {
        sem_wait(&shared.nstored);
        sem_wait(&shared.mutex);

        /*dosomething()*/
        fprintf(fpWrite, "%d", shared.buff[i % NBUFF]);
        usleep(400);
        sem_post(&shared.mutex);
        sem_post(&shared.nempty);
    }
    fclose(fpWrite);
    return NULL;
}
```

