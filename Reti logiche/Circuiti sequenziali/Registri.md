>[!note]
>Un registro è un elemento di memoria in grado di conservare un insieme parola, detta parola. Per realizzarli si possono utilizzare Flip Flop di tipo D.
>
>I dati si possono leggere e caricare in modo parallelo o seriale, mentre è possibile effettuare operazioni di scorrimento dati anche circolari.

Di seguito un registro parallelo-parallelo a $4\text{ bit}$:
![[Pasted image 20260114142511.png]]
Mentre di seguito un registro serie-serie a $4\text{ bit}$:
![[Pasted image 20260114142550.png]]

Queste architetture si possono combinare, per esempio nell'architettura parallelo-serie:
![[Pasted image 20260114143341.png]]

### Contatori
>[!note]
>Un contatore è una rete sequenziale che riceve in ingresso un evento di conteggio che sposta la posizione corrente in avanti o indietro di una unità.
>
>Il valore raggiunto è associato allo stato presente.

Un contatore si distingue per:
- Modulo $M$: il contatore ha intervallo $(0,M-1)$
- Codice: rappresentazione dello stato esternamente
- Codifica: Definisce la successione degli $M$ valori associato allo stato attraverso cui il contatore evolve.

Inoltre i contatori possono essere sincroni (tutti i bistabili ricevono simultaneamente l'evento di conteggio) o asincroni (ha un ritardo di propagazione).

I contatori in alcuni casi non hanno tabelle di eccitazione regolari, in questo caso si usa una metodologia di sintetizzazione diversa da quella vista.

È possibile realizzare contatori per moduli elevati partendo da contatori più semplici, dove ogni sotto-contatore genera un segnale di traboccamento (carry) che, quando raggiunge $1$, consente al clock di attivare il sotto-contatore collegato ad esso in cascata, dove il modulo del super-super contatore sarà il prodotto dei moduli dei sotto contatori.