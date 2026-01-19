>[!note]
>Nelle reti combinatorio a due livelli si hanno due obiettivi: ridurre il numero di termini prodotti e ridurre il numero dei letterali.
>
>Si hanno diversi metodi sintetizzare ottimamente, tra cui il metodo delle mappe di Karnaugh, il metodo di Quine-McCluskey, e le euristiche per sintesi a due livelli.

>[!tip] Sintesi a più livelli
>Talvolta per ridurre il numero di porte logiche si può tornare a reti combinatorie a più di due livelli. Per farlo si effettuano delle fattorizzazioni.
>
>Questo però introduce una maggiore latenza.
>
>![[Pasted image 20251217175653.png|center]]
>
>L'euristica usata modella strutturalmente e comportamentalmente il circuito combinatorio usando un grafo orientato aciclico. Questo grafo si può modificare localmente, o globalmente, impattando l'area e le prestazioni.
>
>Le trasformazioni possono essere:
>- sweep: sostituisce la variabile assegnata nel nodo a monte in tutti i nodi a valle
>- eliminate: sostituisce l'espressione di un nodo in uno o più nodi a valle e elimina il nodo originale
>- simplify: manipola l'espressione di un nodo per portarla su due livelli
>- factor: fattorizza l'espressione di un nodo, ottenendo un'espressione su più livelli
>- substitute: utilizza un nodo già presente nella rete per semplificare un altro nodo, sostituendo una sotto espressione
>- extract: ricerca ed estrazione di un divisore comune a due nodi
>- decompose: usando il teorema di Shannon estrae da un nodo $2^{k}$ nodi

### Mappe di Karnaugh
>[!note]
>Il metodo delle mappe di Karnaugh è un metodo grafico per la sintesi ottimale di una rete combinatoria a due livelli. La sua applicazione è semplice per funzioni di un numero di variabili fino a $4$, e risulta complesso per fino a $5$ o $6$ variabili. Sopra le $6$ variabili risulta praticamente inattuabile.
>
>Rappresentando i mintermini come sequenze di bit, identifichiamo due configurazioni con distanza di Hamming pari ad $1$, e sono quindi adiacenti.
>
>Per rappresentare graficamente la distanza di Hamming si possono usare gli $n$-cubi, dove ogni segmento tra i vertici rappresenta le adiacenze.
>![[Pasted image 20251211150852.png|center]]
>
>Generalmente per semplicità, si mappano gli $n$-cubi su due dimensioni mantenendo le adiacenze.
>![[Pasted image 20251211151337.png|center]]
>
>Su questa mappa, l'adiacenza fisica sulla mappa di Karnaugh degli $1$, questi sono detti implicanti.
>
>Dopo aver identificato tutti gli implicanti, si identificano primi, cioè implicanti non contenuti in nessun'altro implicante.
>
>Dopo aver poi coperto tutti gli $1$ della funzione con gli implicanti, gli implicanti che coprono un $1$ non coperto da nessun altro implicante sono detti implicanti primi essenziali.
>
>Ad ogni raccoglimento è associato un termine prodotto, identificato dalle variabili che non cambiano di valore.
>![[Pasted image 20251211152555.png|center]]
>
>Per la scelta di copertura, si scelgono prima gli implicanti primi essenziali, seguiti dai rimanenti implicanti primi, seguiti infine dai rimanenti implicanti. La corrispondenza della copertura da noi scelta sarà una forma minima.
>
>In caso di condizione di indifferenza (rappresentata da $-$ o $\text{x}$, indicante una configurazione per cui il valore di uscita non è noto e non di interesse), gli implicanti possono coprire anche questi, tuttavia non sono da considerare essenziali se l'elemento univoco è la condizione di indifferenza stessa. Inoltre, implicanti primi formati solo da condizioni di indifferenza sono inutili.

>[!tip] Distanza di Hamming
>Definiamo la distanza di Hamming come il numero di bit da cambiare per passare da una configurazione binaria all'altra.
>
>Nel contesto degli $n$-cubi due configurazioni sono a distanza unitaria se e solo se i vertici associati sono collegati da un lato.

Matematicamente, il principio dietro le mappe di Karnaugh consiste nell'applicazione iterativa della regola di riduzione: $$aZ+a'Z=(a+a')Z=Z$$

Si ha che applicando questo metodo sugli $0$ e non sugli $1$, si ottengono i maxtermini.

>[!tip] ALEE statiche
>Le ALEE statiche sono un fenomeno che introduce un ritardo tra il segnale logico e quello reale in un punto reale. Per evitarlo, si aggiunge alla forma minima degli implicanti che collegano più aree adiacenti che erano prima separate.
### Metodo di Quine-McCluskey
>[!note]
>È facile estendere il principio delle mappe di Karnaugh ad un numero di variabili arbitrario. 
>
>Si parte cercando tutti gli $1$ e confrontandoli tutti, si cercando le configurazioni con distanza di Hamming unitaria. Le configurazioni non adiacenti saranno implicanti primi, mentre quelle adiacenti saranno riportate nuovamente usando il simbolo di don't care. Questo processo si ripete finché non è possibile ridurre ulteriormente. I termini rimasti saranno implicanti primi.
>
>Per ridurre i confronti si possono costruire gruppi di mintermini contenenti lo stesso numero di $1$, e si comparano tra loro solo le configurazioni appartenenti a gruppi adiacenti.
>
>![[Pasted image 20251215172831.png|center]]
>
>Si costruisce poi una tabella di copertura, usata per trovare gli implicanti primi essenziali. Per ridurre la complessità della ricerca della copertura si usano metodi quali criterio di essenzialità e il criterio di dominanza
>![[Pasted image 20251215174611.png|center]]
>Per il criterio di essenzialità, si cercano gli implicanti primi (unici a coprire un uno), e poi si costruisce un altra tabella senza questo.
>
>Per il criterio di dominanza per righe si cercano gli implicanti che coprono solo una riga, si aggiungono all'insieme di copertura e si itera la procedura rimuovendo le colonne coperte da quell'implicante. Inoltre, in caso una riga sia contenuta in un altra riga si cancella e basta.
>
>Analogo è il criterio di dominanza per le colonne, dove si cercano le colonne sottoinsieme di altre, e si elimina la colonna più grande.

>[!tip] Funzioni a più uscite
>Nel caso di funzioni a più uscite non basta minimizzare le funzioni singolarmente con condivisione.
>
>Per creare una sintesi ottima si vanno a ricercare degli implicanti condivisi.
>
>Nel metodo Quine-McCluskey, si costruisce e trovano gli implicanti normalmente, specificando l'appartenenza alle funzioni. 
>
>Durante la fase di espansione, l'identificatore del nuovo implicante sarà l'and bit a bit. In base al valore di questo si decide cosa fare:
>- $0\cdots0$: l'espansione non è valida.
>- diverso da $0\cdots0$ e diverso anche dagli identificatori originali: l'espansione è valida ma non marchiamo niente.
>- uguale ad uno degli identificatori originali: l'espansione è valida e marchiamo l'identificatore uguale.
>- uguale ad entrambi gli identificatori originali: l'espansione è valida e marchiamo entrambi gli identificatori.
>
>![[Pasted image 20251216112307.png]]
>
>La tabella di copertura poi si costruisce, usando variazioni dei criteri già visti.
>![[Pasted image 20251216112059.png|center]]
>
>Per il criterio di essenzialità, si cerca un implicante primo essenziale per tutte le funzioni, rimuovendo le colonne. Se è essenziale solo per una funzione, la riga non è rimossa e sono eliminate le colonne della funzione per cui è essenziale.
>
>Il criterio di dominanza di riga rimane invariata, mentre il criterio di dominanza di colonna si applica alla singola funzione.







