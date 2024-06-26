---
author: Lorenzo Tecchia
tags:
  - definition
  - operation/graph
  - theorem
  - graph
---

### Definizione di ordinamento topologico
Un ***ordinamento topologico*** di un $\textbf{DAG}$ ($\textbf{Directed Acyclic Graph}$) è un ordinamento lineare di tutti i suoi vertici tale che se $\textbf{G}$ contiene un arco $(v, w)$, allora $v$ appare prima di $w$ nell’ordinamento.
Possiamo anche vedere un ordinamento topologico di $G$, come una [[Permutazione|permutazione]] dei suoi nodi.  
Quindi, un ordinamento topologico è un percorso $\pi \in Perm(V)$, di conseguenza possono esistere anche più ordinamenti topologici per lo stesso grafo.
$$\exists i,j \in [0, |V|), i < j \;:\;\pi_{i}= v \; \land\; \pi_{j}=w$$
>[!important] 
> Non può esistere un ordinamento topologico se il grafo ha dei cicli, deve **essere [[Aciclicità|aciclico]]**


### Teorema sull'ordinamento topologico
Se $G$ è aciclico allora esiste un **ordinamento topologico**
>[!important] 
>$$G\;\text{aciclico} \iff \exists \;\text{un ordinamento per}\; G$$



### Dimostrazione del teorema sull'ordinamento topologico
-  $\Leftarrow$ per assurdo: Se esiste un ordinamento topologico allora il grafo è aciclico
![[Pasted image 20230910153324.png]]
 Possibile ordinamento topologico: $\pi_0 \rightarrow \pi_1 \rightarrow \pi_{2} \rightarrow \pi_{0}$
 Essendo l’ordinamento topologico una permutazione (di V ), vuol dire che i vertici non possono ripetersi.
 In questo caso si ripete $\pi_0$
- $\Rightarrow$ per assurdo: Se il grafo è aciclico, allora esiste almeno un ordinamento topologico
Supponiamo che non esistono vertici senza archi entranti.
![[Pasted image 20230910153659.png|250]]
 Partiamo da $v_0$ che ha $v_1$ come arco entrante.  
 A sua volta $v_1$ deve avere un arco entrante, $v_2$  
 $v_2$ a sua volta deve avere un arco entrante e così via, fino a non avere più nodi in $V$ . L’ultimo nodo $v_k$ non può avere archi entranti:
	1. sono finiti i nodi e in una permutazione non possono esserci ripetizioni
	2. se pure ci fosse una ripetizione, si formerebbe un ciclo
Ma dato che il grafo è aciclico e finito, $v_k$ non ha archi entranti, il ché va in contraddizione con quanto supposto prima.


---
### Osservazione sull'ordinamento topologico
Dato un grafo $G$ ***aciclico***, anche un suo ***sotto-grafo*** $G′$ è aciclico
$$G \;\text{acicliclo} \land G′ ⊑ G ⇒ G′ \;\text{è aciclico}$$
*Dimostrazione per assurdo*
1. Supponiamo che il sotto-grafo $G′$ sia ciclico e $G$ aciclico.  
2. Per definizione di sotto-grafo, gli archi di $G′$ sono anche archi di $G$.  
3. Ciò vuol dire che se $G′$ ha dei cicli, anche $G$ avrà quegli stessi cicli e questo va in contraddizione con quanto supposto prima
---

### Idea generale dell'algoritmo sull'ordinamento topologico in ampiezza
Dato un grafo $G$, la funzione restituisce una lista $\pi$ di vertici di $G$ che rappresenta un ordinamento topologico.
Restituisce solo un ordinamento dei tanti che potrebbero esserci.




### Definizione di grado entrante di un vertice
Si definisce **grado entrante** del vertice $v$, il numero di archi entranti in $v$
$$gr(v) \triangleq |\{\forall w \in V\;|\;(v,w)\in E\}|$$
Quando un nodo ha $0$ archi entranti, non è vincolato da nessun altro nodo, può essere quindi inserito nella lista $\pi$. Possiamo immaginare che il nodo appena inserito in $\pi$ sia stato anche eliminato dal grafo, di conseguenza i gradi dei nodi adiacenti diminuiscono di $1$.




Nell’esempio sotto, i numeri all’interno dei nodi rappresentano il numero di archi entranti.
![[Pasted image 20230910161600.png]]
L’algoritmo sfrutta la [[visita in ampiezza]].

```python
def TopologicalOrdering(G):
	ge = EnteringDegree(G)
	Q = InitQueue(G, ge)
	while isNotEmpty(Q):
		(Q, v) = HeadAndDequeue(Q)
		for w in Adj[v]:
			ge(w) = ge(w) - 1
			if ge(w) == 0:
				Q = Enqueue(Q, w)
		π = Append(π, v)
	return π	
```
^Topological-Ordering

- In coda entrano solo i nodi senza archi entranti.
- Estraggo il nodo $v$ in coda e diminuisco il grado entrante di tutti i suoi adiacenti.
- Se uno di questi, una volta decrementato, ha grado pari a $0$, allora lo incodo anche.
- Finito con gli adiacenti, aggiunge $v$ alla lista $\pi$

```python
def EnteringDegree(G):
	for v in V:
		ge(v) = 0
	for v in V:
		for w in Adj[w]:
			ge(w) = ge(w) + 1
	return ge
```
^Entering-Degree

- Imposta prima tutti i gradi a $0$.
- Successivamente se un nodo $w$ è adiacente di un altro nodo $v$, allora $w$ ha l’arco entrante $(v, w)$ quindi il grado di $w$ aumenta di $1$

```python
def InitQueue(G, ge):
	for v in V:
		if ge(v) == 0:
			Q = Enqueue(Q, v)
	return Q
```
^Init-Queue-OT

- Inserisce in coda solo i nodi che non hanno archi entranti.
---
### Idea generale dell'algoritmo sull'ordinamento topologico in profondità
È possibile calcolare un ordinamento topologico anche usando una $\textbf{DFS}$.  
In questo caso non viene restituita una lista ma uno stack.  
La funzione inserisce nello stack a partire dal nodo più vincolato, quindi dall’ultimo che avremo nell’ordinamento.
Inserendolo in uno stack, quando lo si andrà leggere, lo si leggerà in maniera ordinata.




```python
def TopologicalOrdering(G):
	c = Init(G)
	for v in V:
		if c(v) = bn:
			S = DFSTopologicalOrdering(G, S, v, c)
	return S
```
^TopologicalOrdering-Depth

```python
def DFSTopologicalOrdering(G, S, v, c):
	c(v) = gr
	for w in Adj[v]:
		if c(w) = bn:
			S = DFSTopologicalOrdering(G, S, w, c)
	(c(v), S) = (nr, Push(S,v))
	return S
```
^DFS-TopologicalOrdering