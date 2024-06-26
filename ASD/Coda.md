---
author: Lorenzo Tecchia
tags:
  - definition
  - dataStructure
  - to-do/implementation
---

## Definizione di Coda
Una ***coda*** è un tipo di dati astratto che viene usato per riferirsi a [[Struttura dati|strutture dati]], le cui modalità di accesso sono di tipo: **FIFO**, ovvero **Fast In First Out**. Il primo elemento elemento inserito è il primo ad essere eliminato.


## Operazioni sulla struttura dati coda
Così come un numero di altre strutture dati, la coda possiede tutte le [[operazioni elementari]].
Solo che nel caso dello stack, le funzioni di $Insert$ e $Delete$ si chiamano rispettivamente $Enqueue$ e $Dequeue$.




| Nome           | Descrizione                                                                         |
| ------------------- | ----------------------------------------------------------------------------------- |
| $Coda(D)$          | Nome della classe, in questo caso una $Coda$(FIFO), $D$ è un generico tipo di dato |
| $Enqueue():S$         | Inserisce in coda e restituisce la nuova coda                             |
| $Dequeue():S$           | Rimuove dalla coda e restituisce la nuova                                      |
| $Head():D$           | Restituisce la testa della $Coda$                                         |
| $HeadAndDequeue(): (S,D)$ | Restituisce la testa e la nuova $Coda$, ed elimina la testa                        |
