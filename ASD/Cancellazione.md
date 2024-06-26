---
author: Lorenzo Tecchia
tags:
  - operation
  - dataStructure/abr
  - to-do/implementation
---

### Idea generale sulla cancellazione in un ABR
 Se il nodo da cancellare non **ha figli**, si elimina il nodo stesso
- Se il nodo $x$ da eliminare **ha un solo figlio**, basta collegare il figlio di $x$ al padre di $x$
	- ![[Pasted image 20230830085528.png]]
- Se il nodo $x$ da eliminare **ha entrambi i figli**, ci sono due possibili modi per eliminare il nodo:
	- Sposto il **MAX del ramo sinistro**
		- Il MAX del ramo sinistro può avere al massimo il figlio destro che è più piccolo. Se avesse anche il figlio destro, non sarebbe il massimo
	- Sposto il **MIN del ramo destro**
		- Il Min del ramo destro può avere al massimo il figlio sinistro che è più grande. Se avesse anche il figlio sinistro, non sarebbe il massimo


#### Esempio
![[Pasted image 20230830090150.png]]
In questo caso è stato spostato il **MIN del ramo destro** dovendo eliminare il nodo con dato $10$.

---
>[!important] 
>Prima di definire il metodo $Delete(x,d)\rightarrow$ il metodo per cancellare il nodo con dato $d$.
>Bisogna trovare il [[Minimo-Massimo|minimo]] (o il massimo) quindi definire tale funzione per gli [[Albero binario di ricerca|BST]]

---
## Idea generale sull'algoritmo $\textbf{Delete}$
Questa è la funzione che verrà chiamata per eliminare il nodo contente il dato $d$.
- Cerca il nodo
- Se trovato, chiama la funzione $DeleteNode$
	- Se il nodo ha un solo figlio, verrà fatto [[Minimo-Massimo#$ textbf{SkipRight}$|SkipRight]] se non ha il sinistro, [[Minimo-Massimo#$ textbf{SkipLeft}$|SkipLeft]] se non ha il destro
	- Altrimenti posso eliminarlo in due modi possibili:
		1. ceco il MAX del ramo sinistro
		2. cerco il MIN del ramo destro
	- In questo caso si procede con il MIN 
- Sia $Skip$ che [[Minimo-Massimo#^get-delete-min|Get&Delete]] restituiscono un nodo a $DeleteNode$  
- La funzione $DeleteNode$ restituirà un nodo che sarà restituito alla chiamata ricorsiva di $Delete$. Questo verrà inserito al posto del nodo da eliminare


```python 
def Delete(T, k)
	if T != NULL:  # dato non trovato
		# cerco il nodo che contiene il dato
		if T -> key > k:
			T -> sx = Delete(T -> sx, k)
		else if T -> key < k:
			T -> dx = Delete(T -> dx, k)
		else   # nodo trovato  
			return DeleteNode(T)
	return T
```
^DeleteABR

```python
def DeleteNode(T):
	if T -> sx == NULL:
		return SkipRight(T)
	else if T -> dx == NULL:
		return SkipLeft(T)
	else
		T -> dato = GetAndDeleteMin(T -> dx, T)
		return T
```
^DeleteNodeABR

[[Minimo-Massimo#^get-delete-min|Get&DeleteMin]]

---
