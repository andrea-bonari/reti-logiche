>[!note]
>I metodi di sintesi di reti sequenziali sono in costante evoluzione.
>
>Un circuito sincrono può essere modellato in modo comportamentale o strutturale.

>[!tip] Macchina a stati
>Il valore delle uscite all'istante $t$ dipende dalla successione degli ingressi che precedono l'istante $t$, questo implica il concetto di stato.
>
>Usiamo quindi una macchina a stati, definita dalla quintupla: $$(I, U, S, \delta, \lambda)$$
>Dove $I$ è l'alfabeto di ingresso, $U$ è l'alfabeto d'uscita, $S$ è l'insieme degli stati, $\delta: S\times I\to S$ è la funzione stato prossimo e $\lambda$ è la funzione d'uscita.
>
>La funzione di uscita $\lambda$ dipende dal tipo di macchina. Se è una macchina di Mealy (l'uscita dipende da stato e ingresso) allora: $$\lambda: S\times I\to U$$
>Se è una macchina di Moore (l'uscita dipende solamente dallo stato) allora: $$\lambda: S\to U$$
>
>Una FSM può essere descritta da una tabella degli stati, dove gli indici di colonna sono i simboli di ingresso $i_{\alpha}\in I$, e gli indici di riga sono $s_{j}\in S$ e indicano lo stato presente.
>
>Per rappresentarli si usa il diagramma degli stati, cioè un grafo orientato $G(V,E,L)$, con $V$ insieme dei nodi (stati), $E$ insieme degli archi (transizioni di stato) e $L$ insieme degli ingressi e uscite (Mealy) o solo uscite (Moore).

Generalmente la struttura di una macchina a stati è:
![[Pasted image 20251216160022.png]]

Il problema della sintesi comportamentale consiste nell'identificazione delle funzioni $\delta$ e $\lambda$, e sintetizzare la rete combinatorie che le realizza, riducendo il più possibile il numero di flip-flop.

Per sintetizzare, si realizza la tabella degli stati, e si ottimizzano riducendo i numeri. Si costruisce poi la tabella delle transizioni e la tabella delle eccitazioni, infine si sintetizza la rete combinatoria da tale tabella.

>[!tip] Codifica degli stati
>Esistono diversi metodi per codificare gli stati, le più conosciute sono:
>- Minima: con elementi in memoria $\lceil \log_{2}|S|\rceil$.
>- One-Hot: con elementi in memoria $S$.
>
>La scelta influisce su area e performance.

### Sintesi delle FSM completamente specificate
>[!note]
>Per ridurre il numero flip-flop, si può usare una codifica diversa degli stati, oppure ottimizzare il numero di stati.
>
>Si ha che il numero di flip-flop minimo è: $$N_\text{FF,min}=\lceil \log_{2}|S|\rceil$$
>Tuttavia nel modello della FSM alcuni stati potrebbero essere ridondanti, pertanto identificare ed eliminare questi stati comporta reti combinatorie meno costose e un numero minore di elementi di memoria.

In primis, si eliminano gli stati non raggiungibili dallo stato iniziale.

Dalla tabella degli stati questa operazione è possibile cercando tutti gli stati raggiungibili iterativamente, partendo dallo stato di partenza.

Inoltre, si possono rimuovere molti stati tramite la proprietà degli stati indistinguibili, minimizzando gli stati.

>[!tip] Stati indistinguibili
>Si consideri una macchina completamente specificata, e $I_{a}$ la generica sequenza di ingresso, $U_{a}$ la sequenza d'uscita associata ad $I_{a}$. Consideriamo inoltre due generici stati $s_{i},s_{j}\in S$. Questi sono detti indistinguibili se: $$s_{i}\sim s_{j}\iff U_{\alpha,i}= \lambda(s_{i}, I_{\alpha})= \lambda(s_{j},I_{\alpha})=U_{\alpha,j}\quad \forall I_{\alpha}$$
>
>L'indistinguibilità è una relazione di equivalenza, e quindi godono di proprietà riflessive, simmetriche e transitive. In generale due stati equivalenti possono essere raggruppati in un unica classe.
>
>L'insieme delle classi identificate determina l'insieme degli stati della macchina minima equivalente unica.
>
>Formalmente per il partizionamento in classi $c_{1},\cdots,c_{m}$: $$\begin{align*}
>&c_{1}\cup c_{2}\cup\cdots\cup c_{m}=S\\
>&c_{i}\cap c_{j}=\emptyset\quad \forall i,j\quad i\neq j
>\end{align*}$$
>
>Per semplificare questo tipo di analisi si usa le regola ricorsiva di Paull-Unger: Due stati sono indistinguibili se per ogni simbolo di ingresso $i_{a}$: $$\lambda(s_{i},i_{a})=\lambda(s_{j},i_{a}),\quad \delta(s_{i},i_{a})= \delta(s_{j}, i_{a})$$
>Dopo un numero finito di passi si ricadrà nelle condizioni $s_{i}\not\sim s_{j}$ oppure $s_{i}\sim s_{j}$.
>
>Inoltre per evidenziare le indistinguibilità si può usare la tabella delle implicazioni, dove ogni elemento può contenere non equivalenza, equivalenza oppure un rimando ad analisi di altri passaggi.
>
>Una volta costruita la tabella, si cerca l'indistinguibilità con 

La macchina a stati finiti ottenuta mediante la minimizzazione degli stati gode delle proprietà:
- Equivalenza alla precedente
- Minima
- Unica

### Analisi delle macchine sequenziali
>[!note]
>È possibile ottenere un modello delle funzionalità di una macchina sequenziale tramite l'analisi del circuito.
>
>Per farlo, prima si identificano le funzioni implementate dalla rete combinatoria, e poi si rappresenta le funzioni sulla tabella degli stati.
>
>Questo processo non è banale per bistabili di tipo D.

