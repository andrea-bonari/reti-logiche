>[!note]
>In un circuito sequenziale le uscite dipendono dalla condizione iniziale del circuito e dalla sequenza di ingressi, applicata in un arco temporale, e quindi simulando una memoria degli eventi passati.
>
>Per rappresentarli possiamo usare degli FSM deterministici, e quindi dato uno stato ed una configurazione di ingresso il nuovo stato è identificato univocamente. Talvolta può essere utile avere anche un'unità di elaborazione separata, usando quindi un FSMD.

>[!tip] Clock
>I cambiamenti di stato del sistema sono ammessi solo in particolari istanti di tempo controllati da un segnale esterno periodico detto clock. Il periodo di clock $T_{\text{CK}}$ è il tempo tra i cambiamenti di stato.
>
>Possiamo definire la sua frequenza come: $$f_{\text{CK}}= \frac{1}{T_{\text{CK}}}$$

Quando si usa un'unica macchina a stati ogni ingresso porta il sistema ad uno stato che corrisponde ad uno stato riconosciuto, oppure uno stato di errore.

Mentre quando si usa unità di controllo ed elaborazione:
![[Pasted image 20251216141132.png|center]]

I passi generali per l'implementazione dell'unità di controllo sono:
- Separare rete combinatoria e memoria.
- Identificare i dispositivi di memoria da utilizzare.
- Trasformare la tabella delle transizioni in tabelle delle eccitazioni.
- Sintetizzare la rete combinatoria a più uscite.
- Collegare nuovamente la memoria alla rete combinatoria sintetizzata.

### Bistabili
>[!note]
>Gli elementi in grado di conservare informazioni sono detti bistabili, un elemento stabile in due stati ($0$ e $1$) le cui transizioni di stato sono forzate da un segnale di ingresso.
>
>Le differenze tra i vari tipi di elementi di memoria sono il numero di ingressi e il modo in cui tali ingressi ne determinano lo stato.
>
>Una prima classificazione è la distinzione tra bistabili:
>- Asincroni: modificano il valore in base agli ingressi.
>- Sincroni: la transizione avviene solo in base ad un evento di clock.

>[!tip] Bistabili asincroni SR
>Il bistabile asincrono più semplice è il bistabile Set Reset, è generalmente usato come blocco base per realizzare bistabili più complessi.
>![[Pasted image 20251216143111.png|center]]
>
>Con $Q$ stato presente e $Q^{*}$ stato futuro, possiamo dire che: $$Q^{*}= S+R'Q\qquad S=R\neq1$$

>[!tip] Bistabili sincroni
>I fattori che caratterizzano i bistabili sincroni sono la relazione ingresso-stato (tipo di temporizzazione, può essere sul livello o sul fronte del segnale di controllo) e relazione stato-uscita (quando cambiano le uscite, basate sul livello o sul fronte del segnale di controllo).

>[!tip] Latch SR
>Il Latch SR aggiunge ad un bistabile asincrono SR un circuito di controllo.
>![[Pasted image 20251216144147.png|center]]
>Possiamo dire che: $$Q^{*}=C'Q+C(S+R'Q)$$

>[!tip] Latch D
>Il latch D è ottenuto partendo da un latch SR imponendo che $S=R'$.
>![[Pasted image 20251216144328.png|center]]
>Possiamo dire che: $$Q^{*}=C'Q+CD$$

>[!tip] Flip-Flop Master-Slave
>Per evitare l'effetto di propagazione indesiderata, i bistabili sincroni vengono modificati in modo che lo stato possa modificare le uscite solo in corrispondenza di un evento del segnale di controllo.
>
>Per farlo usiamo due latch che lavorano in contrapposizione di fase:
>![[Pasted image 20251216144630.png|center]]

Spesso, nei flip flop e nei latch sono presenti degli ingressi diretti che sono utilizzati per scavalcare gli ingressi dati, di tipo asincrono. Questi sono utili per stabilire lo stato iniziale, oppure mantenere il flip-flop o il latch in uno stato particolare.

>[!tip] Tabelle di transizioni e eccitazioni
>Tabelle delle transizioni
>![[Pasted image 20251216145157.png|center]]
>Tabelle delle eccitazioni
>![[Pasted image 20251216145120.png|center]]

