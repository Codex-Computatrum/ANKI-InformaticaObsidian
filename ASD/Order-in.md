---
author: Lorenzo Tecchia
tags:
  - definition
  - dataStructure
  - operation
  - to-do/implementation
---
### Funzionamento
```python
def DFVIn(X, F, a):
	if x != NULL:
		a = DFVIn(x.sx, F, a)
		a = F(x.dato, a)
		a = DFVIn(x.dx, F, a)
	return a
```
^DFV-InOrder

- $x$ è il nodo della radice di un albero (quindi anche i sotto-alberi)
- $F$ è una funzione che restituisce un valore $F: D \times A \rightarrow A$
- $a$ valore iniziale dell'accumulatore
---
![[Pasted image 20230829154811.png]]
![[Pasted image 20230829154826.png]]

---
