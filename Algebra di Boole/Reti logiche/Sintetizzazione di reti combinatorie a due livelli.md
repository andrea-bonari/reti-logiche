>[!note]
>Nelle reti combinatorio a due livelli si hanno due obiettivi: ridurre il numero di termini prodotti e ridurre il numero dei letterali. Si hanno diversi metodi sintetizzare ottimamente, tra cui il metodo delle mappe di Karnaugh, il metodo di Quine-McCluskey, e le euristiche per sintesi a due livelli.

### Mappe di Karnaugh
>[!note]
>Per applicare il metodo delle mappe di Karnaugh si identificano forme minime a due livelli applicando la regola di riduzione: $$aZ+a'Z=(a+a')Z=Z$$
>In cui $Z$ è un termine prodotto di $n-1$ variabili. Questo metodo può essere applicato iterativamente ad un numero di termini pari a $2^{n}$ mantenendo inalterato il numero dei livelli. Le somme di prodotti rimangono tali, al più tali espressioni possono banalizzarsi.
>
>Questa relazione può essere applicata direttamente alle espressioni algebriche che definiscono la rete, tuttavia non è sempre immediato. Si ricorda che la relazione di replicazione dei termini: $$x=x+x$$
>Definiamo la mappa di Karnaugh come uno schema deducibile  dalla rappresentazione geometrica delle configurazione.
>
>Nella regola di riduzione si identificano le configurazioni binarie associate ai termini prodotto che sono a distanza di Hamming unitaria, e a tali configurazioni corrispondono coppie di mintermini in cui una sola variabile è naturale in un mintermine e complementata nell'altra.
>
>Una funzione binaria $f$ a $n$ variabili può anche essere rappresentata mediante rappresentazione geometrica cartesiana in uno spazio $n$-dimensionale in cui gli assi sono le variabili della funzione. "Srotolando" lo spazio l'oggetto $n$-dimensionale su una tabella bidimensionale si ottiene la mappa di Karnaugh, dove due caselle che condividono un lato di un $n$-cubo corrispondono a due configurazioni di variabili adiacenti.
>
>Definiamo un implicante come una funzione $p$ associata ad un termine prodotto di $m$ letterali con $1\leq m\leq n$ tale per cui $f\geq p$, cioè $p\Rightarrow f$. Un mintermine è un implicante in cui $m=n$. Tra gli implicanti definiamo gli implicanti primi, cioè una funzione $p$ associata ad un termine prodotto a cui corrisponde un raggruppamento di dimensione massima. Tra gli implicanti primi definiamo gli implicanti primi essenziali, cioè implicanti primi che coprono uno o più $1$ non coperti da nessun altro implicante primo.
>
>Si ha che esiste una forma minima costituita solo da implicanti primi. Si può quindi identificare una forma SoP che includa il numero minimo di implicanti che garantisca la copertura di tutti gli $1$ della funzione.
>
>Ad ogni raccoglimento è associato un termine prodotto, associato ad un implicante ottenuto identificando le variabili che non cambiano mai di valore, riportando ogni variabile in modo diretto se il valore è $1$, e in modo complementato se il valore è $0$.
>
>Si ottiene una forma PoS utilizzando "implicanti di $0$".
>
>Riguardo le condizioni di indifferenza, gli implicanti primi realizzati solamente mediante condizioni di indifferenza non hanno alcun scopo, inoltre, un implicante primo non diventa essenziale quando è l'unico a coprire una data condizione di indifferenza.

>[!tip] Distanza di Hamming
>Definiamo la distanza di Hamming come il numero di bit "diversi" tra una configurazione e l'altra.

>[!tip] Condizioni di indifferenza
>Le condizioni di indifferenza corrispondono a configurazioni di ingresso per le quali il valore dell'uscita non è noto e non è neppure di interesse sapere quanto può valere.
>
>Le configurazioni di ingresso per le quali il valore dell'uscita non è specificato costituiscono il $\text{DCset}$ della funzione, e sulla tabella delle verità il valore non specificato si indica con i simboli $-$ o $\text{x}$.
>
>Nel processo di sintesi le condizioni di indifferenza sono i gradi di libertà, gli si può assegnare il valore $0$ o $1$ a seconda di quanto conviene

### Metodo di Quine-McCluskey
>[!note]
>Il metodo di Quine-McCluskey è un metodo di minimizzazione tabellare articolato in due fasi, ricerca degli implicanti primi e ricerca della copertura ottima. Di seguito riferimento alla sola forma SoP, tuttavia è facilmente estendibile alla forma PoS.
>
>Per ricercare gli implicanti primi si applica sistematicamente la semplificazione: $$aZ+a'Z=(a+a')Z=Z$$
>Il punto di partenza è l'insieme dei mintermini della funzione. Si confrontano esaustivamente tutti i termini prodotto ricavati dal passo precedente, e si semplificano tutte quelle coppie che hanno una parte comune ed una sola variabile differente. I termini prodotto semplificati sono marcati. Si crea poi un nuovo insieme di termini prodotto da confrontare e si ripete il primo passo. Il processo termina se non sono più possibili delle riduzioni.
>
>Si ha che i termini prodotto non marcati sono implicanti primi.

