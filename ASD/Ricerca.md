---
author: Lorenzo Tecchia
tags:
  - operation
  - dataStructure/abr
  - to-do/implementation
---

### Idea generale sulla ricerca in ABR
Dato un puntatore alla radice e un dato, $Search$ ***restituisce il puntatore al nodo con quella chiave (`NULL` se la chiave non è presente)***
- Se il nodo attuale è `NULL`
	- allora non ho trovato l’elemento e restituisco `NULL`.  
- Se invece il nodo attuale non è `NULL`
	- cerco a destra se il dato da cercare è più grande del dato contenuto nel nodo
	- altrimenti cerco a sinistra.  
- Continuo così finché o trovo il dato o sono arrivato alle foglie.



```python
def Search(x, d):
	if x = NULL:
		return NULL
	else:
		if d > x.dato:
			return Search(x.dx, d)
		else if d < x.dato:
			return Search(x.sx, d)
		else
			return x
```
^Ricerca-ABR

### Complessità della ricerca in ABR
Nel caso peggiore, il percorso più lungo sarà quanto l'altezza dell'albero.
L'operazione di ricerca quindi impiega $O(h)$


---

