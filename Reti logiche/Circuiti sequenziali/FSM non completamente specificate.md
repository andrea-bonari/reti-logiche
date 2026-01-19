>[!note]
>Le FSM non completamente specificate sono macchine in cui per alcune configurazioni degli ingressi e stati correnti non sono specificati gli stati futuri e/o le configurazioni d'uscita.

È possibile estendere la regola di Paull-Unger a queste macchine. Due stati di ingresso sono compatibili se e solo se, per ogni simbolo di ingresso $i_{\alpha}$ valgono le due seguenti relazioni:
Se ambedue sono specificati allora: $$\begin{align*}
\lambda(s_{i},i_{\alpha})&= \lambda(s_{j},i_{\alpha})\\
\delta(s_{i},i_{\alpha})&= \delta(s_{j},i_\alpha)\end{align*}$$

Se uno o entrambi non sono specificati la compatibilità (indicata con $\lor$) si ritiene soddisfatta.

Si può quindi creare la tabella delle implicazioni normalmente, tuttavia si ha che la relazione di compatibilità non è transitiva, e quindi è necessaria un ulteriore analisi.

Si suddivide quindi il grafo di compatibilità in classi di massima compatibilità chiuse:
![[Pasted image 20251218181725.png]]

La soluzione è un insieme chiuso di classi di massima compatibilità e copre tutti gli stati, tuttavia non è necessariamente minima.

### Algoritmo dell'albero di copertura
>[!note]
>L'algoritmo dell'albero di copertura permette di trovare, a partire dal grafo di compatibilità, un insieme di chiuso di classi di massima compatibilità, tuttavia non trova necessariamente la soluzione minima.
>
>La radice dell'albero è un nodo con etichetta tutti gli stati dell'insieme. Da questo nodo, si scende di uno strato scegliendo uno stato, nel nodo di sinistra si inseriscono tutti gli stati tranne quello scelto, mentre quello di destra si inseriscono tutti gli stati che soddisfano almeno una di queste condizioni:
>- Già analizzati in livelli precedenti
>- Corrispondono al nodo di riferimento del livello
>- Sono potenzialmente compatibili con il nodo di riferimento
>
>Il processo si ripete iterativamente su ogni nodo sottostante fino al raggiungimento di una foglia.
>
>Un nodo è eliminato se tutti i suoi strati sono già inclusi in un altro nodo che è identificato come foglia, mentre un nodo è identificato come foglia se sono stati già esaminati tutti gli stati che lo compongono (tranne al più uno).
>
>Le etichette dei nodi foglia identificano le classi di massima compatibilità.

Se si creano due nodi foglia allo stesso livello si preferisce sempre il nodo foglia che contiene più stati.

![[Pasted image 20260114141903.png]]