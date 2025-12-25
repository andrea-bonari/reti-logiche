>[!note]
>È possibile rappresentare un numero in codifica binaria. 
>
>Formalmente per convertire da decimale a binario si usa il metodo delle divisioni successive, ed il metodo delle potenze per la conversione da binario a decimale.
>
>Si ha che per $n$ bit si possono rappresentare fino $2^{n}$ simboli.
>
>Esistono altri metodi per rappresentare i numeri binari oltre alla conversione binaria.

>[!tip] Base $2$ complemento a $2$
>La notazione base 2 complemento a due permette la rappresentazione di numeri negativi, dove se il numero è positivo rimane uguale alla sua codifica binaria diretta, per ottenere però il negativo si effettua il complemento ad $1$ (invertire i bit) e il complemento a $2$ (sommare $1$).
>
>Notiamo che il primo bit indicherà il segno, inoltre si usa il complemento a due poiché le operazioni in complemento a $2$ sono più facili da fare.
>
>Con $n\text{ bit}$ l'intervallo di rappresentazione è $[-2^{n-1},2^{n-1}-1]$.

Dati gli operandi $A$ e $B$, il risultato $S$ ed il resto $C$, è possibile costruire una tabella di verità e quindi un circuito. Si ha che: $$S=A\oplus B\qquad C=A\cdot B$$
Possiamo costruire quindi un circuito chiamato half-adder:![[Pasted image 20251216192203.png|center]]
Da questo ne possiamo costruirne un altro detto full-adder, che somma $3$ numeri $A,B,C_{\text{In}}$: ![[Pasted image 20251216192226.png|center]]
Considerando un ritardo fisso di $1$ per porta logica il ritardo per l'half-adder è: $$\begin{align*}
T(S)=1\\
T(C)=1 
\end{align*}$$
Mentre per il full-adder è:
$$\begin{align*}
&T(S)= 2\\
&T(C_\text{out})= 3
\end{align*}$$
Ponendo full-adder (dove il primo è un half-adder) in parallelo è possibile creare un sommatore a $n$ bit.
![[Pasted image 20251216204537.png|center]]
Tuttavia questo approccio è abbastanza lento, si usa quindi un sommatore CLA.

>[!tip] Sommatore CLA
>Nel sommatore Carry Look Ahead (CLA), si aggiunge un componente CLA che precalcola i valori dei riporti.
>
>Si ha che: $$C_{i+1}= \underbrace{A_{i}\cdot B_{i}}_{G_{i} \text{ funzione generatrice}}+\underbrace{(A_{i}\oplus B_{i})}_{P_{i}\text{ funzione propagazione}}C_{i}$$
>$G_{i}$ indica la necessità di un riporto, mentre $P_{i}$ indica quando va propagato. Se espandiamo questa formula notiamo che il riporto non dipende dai riporti precedenti, in quanto $C_{0}=0$. È quindi possibile costruire il CLA con una rete a 2 livelli.
>
>![[Pasted image 20251216205626.png|center]]
>
>Siccome calcolare le nostre $C_{i}$ richiede delle porte logiche di dimensioni enormi, fisicamente non prodotte, si introduce l'architettura del CLA a blocchi da $m$ block size, consideriamo $m=2$:
>![[Pasted image 20251218110102.png|center]]
>
>Questo ha tempo logaritmico.

### Moltiplicatori
>[!note]
>L'operazione di moltiplicazione è molto più complessa della somma. 
>
>Esistono diversi moltiplicatori, diversi dalla moltiplicazione in colonna, questo perché essa non è efficiente. Per esempio, esiste il caso specifico $Y=A\cdot B\qquad B<0$, che dev'essere calcolato come: $$Y= (-A)\cdot(-B)$$
>Inoltre è necessario estendere il segno dei prodotti parziali.
>![[Pasted image 20251218110959.png|center]]

>[!tip] Moltiplicatore parallelo
>Consideriamo la cella moltiplicatrice:
>![[Pasted image 20251218111530.png|center]]
>Disposte in questo modo possiamo creare un moltiplicatore:
>![[Pasted image 20251218111554.png|center]]
>Dove ogni riga può essere vista come un sommatore. Questo approccio a ha ritardo lineare.

>[!tip] Moltiplicatore di Wallace
>Secondo questo approccio, in primis si moltiplicano tutte le coppie di bit degli operandi, e poi le disponiamo nella matrice. L'idea è di sommare usando un half adder (verde nell'immagine) per le somme di $2\text{ bit}$, e full adder (giallo nell'immagine) per le somme di $3\text{ bit}$
>![[Pasted image 20251218111948.png|center]]
>Questo processo ci da una matrice computazionale con un livello in meno. Ripetendo questo processo ridurremo le somme al risultato.

>[!tip] Operandi negativi in complemento a due
>Consideriamo due numeri $A$ e $B$ in complemento a due. Se consideriamo $$\begin{align*}
>A&= (-a_{3})2^{3}+a_{2}2^{2}+a_{1}2^{1}+a_{0}\\
>B&= (-b_{3})2^{3}+b_{2}2^{2}+b_{1}2^{1}+b_{0}
>\end{align*}$$
>Notiamo che:
>![[Pasted image 20251218112644.png|center]]
>Separiamo quindi la matrice computazionale in due matrici $P^{+}$ e $P^{-}$ per segno:
>![[Pasted image 20251218112736.png|center]]
>$P^{+}$ e $P^{-}$ si sommano separatamente con i metodi visti precedentemente, e infine si calcola con un sommatore $P=P^{+}-P^{-}$, che sarà il nostro risultato corretto.

Esistono degli algoritmi per ottimizzare la moltiplicazione.

>[!tip] Algoritmo di Booth Radix2
>Per l'algoritmo di Booth si aggiunge uno $0$ nella posizione meno significativa al moltiplicatore, e poi lo scomponiamo in coppie da due sovrapposte partendo da destra. Per esempio il numero $11011$ diventerà $11,10,01,11,10$
>
>Sostituiamo poi queste coppie con la codifica:
>
>| Coppia moltiplicatore | Codifica |
>| - | - |
>| $00$ | $0$ |
>| $01$ | $1$ |
>| $10$ | $-1$ |
>| $11$ | $0$ |
>
>Eseguiamo poi la moltiplicazione con la nuova codifica, stando attenti che la moltiplicazione per $-1$ si esegue il complemento a $2$ del numero.

>[!tip] Algoritmo di Booth Radix4
>Funziona esattamente con la stessa logica, però si prendono gruppi sovrapposti da $3\text{ bit}$. Per esempio $00100110$ diventa $001,100,011,100$.
>
>Si usa poi la codifica:
>
>|Tripletta modificatore | Codifica |
>| - | - |
>| $000$ | $0$ |
>| $001$ | $1$ |
>| $010$ | $1$ |
>| $011$ | $2$ |
>| $100$ | $-2$ |
>| $101$ | $-1$ |
>| $110$ | $-1$ |
>| $111$ | $0$ |
>
>A questo punto si procede esattamente come prima. Si nota che la moltiplicazione per $2$ comporta uno shift a sinistra. Inoltre, bisogna lasciare due spazi nella matrice computazionale al posto di uno.



