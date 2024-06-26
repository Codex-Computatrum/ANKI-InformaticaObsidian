---
author: Lorenzo Tecchia
tags:
  - to-do/implementation
  - algorithm/graph/search
aliases:
  - BFS
---

### Definizione di BFS
**Breadth-first search** (**BFS**) è un [[algoritmo]] per cercare in una [[struttura dati]] [[Graph|grafo]] in [[Visita in ampiezza|ampiezza]] un nodo che soddisfi una certa proprietà.





## Funzionamento
```python
def BFS(G, v):
	Init(G, c)
	(Q, c(v)) = (Enqueue(Q, v), gr)
	while isNotEmpty(Q):
		(Q,v) = HeadAndDequeue(Q)
		for u in Adj[v]:
			if c(u) == B:
				(Q, c(u)) = (Enqueue(Q, u), gr)
		c(v) = nr	
```
^BFS

```python
def Init(G, c):
	for v in V:
		c(v) = bn
```

^Init

```python
# BFS con calcolo delle distanza da sorgente
def BFS_Modified(G, v):
	for u in V-{v}:
		color[u] = B
		pred[u] = NULL
		dist[u] = \infty
	color[v] = G
	dist[v] = 0
	pred[v] = NULL
	Q = Enqueue(Q, v)
	while isNotEmpty(Q):
		(Q,v) = Head&Dequeue(Q)
		for w in Adj[v]:
			if color[w] = B:
				color[w] = G
				pred[w] = v
				dist[w] = dist[v] + 1
				Q = Enqueue(Q, w)
		Dequeue(Q, v)
		color[v] = N
```
^BFS-Modified



### Idea generale dietro la BFS
- $bn$ Bianco: non scoperto
- $nr$ Nero: visitato
***Init:*** prende in ingresso un [[grafo]] $G$ e un [[Ricerca binaria|array]] $c$ il quale tiene traccia del colore del nodo $v$ Imposta a bianco di tutti i nodi del grafo $G$
Dato che un grafo non ha un nodo radice dal quale partire, basta quindi un nodo arbitrario v dal quale partire.
La funzione ***BFS*** quindi prende in ingresso il grafo e il nodo dal quale partire:
1. Si inizializza il [[Ricerca binaria|vettore]] dei colori dei vertici $c$ con il colore che identifica che il nodo non è stato scoperto, ovvero
    ***il bianco*** (avendo prima specificato il significato dei tre colori).
2. Ogni volta che si incontra un nodo ***bianco*** vuol dire che lo si vuole visitare, quindi lo inserisco in coda e imposto il colore a ***grigio***; ovvero lo scopro ma non lo visito, lo visiterò quando arriverà il suo turno.  
    Quindi come seconda cosa, scopro $v$. Lo metto in [[coda]] e lo coloro di ***grigio***.
3. C’è lavoro da fare finché ci sono nodi nella coda, quindi con un while scorro finché la coda non è vuota.
4. Devo visitare la stella uscente del nodo $v$ in testa alla coda, quindi lo estraggo. per visitarlo.
5. Dovrò visitare ogni nodo $u$ adiacente al nodo $v$ appena estratto, a patto che questo sia bianco. Quindi, se $u$ è bianco, lo inserisco in coda e imposto il suo colore a grigio.
6. Una volta tutta la stella uscente di $v$, ho finito di visitarlo, quindi imposto il colore a nero.


### Quali sono le proprietà sui nodi che ci permette di calcolare una BFS?
Quindi una semplice **BFS** ci permette di calcolare solo ciò che il nodo di partenza $v$ raggiunge nel grafo $G$.
Lo si può capire guardando i colori dei nodi alla fine della funzione.  
I nodi colorati di ***nero*** saranno quelli che il nodo di partenza v raggiunge nel grafo.$$\forall u \in V \;\;\; c(u)=nr \iff (u,v)\in Reach(G)$$
>[!note] 
> Dove la funzione $Reach(G)$ indica la [[Reachability|raggiungibilità]] tra i nodi
Se il nodo $u$ è **nero**, allora c’è un percorso che va da $v$ ad $u$, quindi $v$ raggiunge $u$
Se $v$ raggiunge $u$ , allora vuol dire che $u$ è **nero**
Si può estendere l’algoritmo per:  
- calcolare la [[Calcolo delle distanze|distanza dal nodo di partenza]] a tutti gli altri nodi
- calcolare il percorso con [[Lunghezza minima|lunghezza minima]].
