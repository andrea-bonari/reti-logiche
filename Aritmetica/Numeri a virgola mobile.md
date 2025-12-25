>[!note]
>Per spostarci dall'insieme $\mathbb{Z}$ all'insieme $\mathbb{Q}$, esistono diverse rappresentazione.
>
>La più immediata è una rappresentazione a virgola fissa, dove si allocano $n\text{ bit}$ alla parte decimale.
>
>Quella meno immediata è a virgola mobile. Consideriamo $S$ come segno, $E$ come esponente e $M$ come mantissa, si ha che: $$N=(-1)^{S}\cdot 2^{E-127}\cdot (1+ 0.M)$$
>Da un punto di vista binario, nella virgola mobile a singola precisione, il MSB è il segno, i successivi $8$ sono l'esponente, e i restanti $23$ sono dedicati alla mantissa.

Per convertire in modulo 2 virgola mobile a singola precisione, si converte la pare decimale $I$ in binario, e poi la parte decimale $D$ in binario.
A questo punto scriviamo in forma normale $I.D$, quindi nel formato $1.\cdots$. La parte decimale della forma normale sarà la mantissa, mentre l'esponente sarà lo shift a sinistra, codificato in modulo segno (primo bit impostato ad $1$ per indicare shift a destra).

>[!tip] Casi particolari
>Nel caso in cui $E=255$, se $M=0$ allora il significato è $\infty$, altrimenti è $\text{NaN}$ (Not-a-Number).
>
>Nel caso in cui $E=0$, se $M=0$ allora il significato è $0$, altrimenti è indicato un numero denormalizzato, cioè dove: $$N=(-1)^{S}\cdot 2^{E-127}\cdot (0.M)$$

Per eseguire la somma (o sottrazione), si procede con lo stesso metodo della somma nella notazione scientifica:
1. Si uniformano gli esponenti
2. Si esegue la somma delle mantisse
3. Si normalizza il risultato

>[!tip] Errori
>Il valore assoluto $E_{a}=\text{val}_\text{real} -\text{val}_\text{actual}$ aumenta all'aumentare di $\text{val}_\text{actual}$, mentre l'errore relativo $E_{r}= \frac{E_{a}}{\text{val}_\text{actual}}$ è approssimativamente costante.

>[!tip] Eccezioni
>Lo standard IEEE754 definisce una serie di eccezzioni:
>- Valore inesatto (rispetto al corrispondente matematico)
>- Divisione per zero
>- Operazione non valida
>- Overflow
>- Underflow

### Circuito sommatore in virgola mobile
>[!note]
>Dati due numeri $A$ e $B$ codificati in floating point singola precisione, con componenti $S_{A},E_{A},M_{A}$ e $S_{B},E_{B},M_{B}$.
>
>Per prima cosa si sceglie il numero con esponente minore e si fa scorrere la sua mantissa a destra un numero di bit pari alla differenza dei due esponenti.
>
>![[Pasted image 20251218161938.png|center]]
>
>Poi si assegna all'esponente del risultato il maggiore tra gli esponenti degli operandi.
>![[Pasted image 20251218162014.png|center]]
>
>Poi si esegue l'operazione di somma tra le mantisse per determinare il valore ed il segno del risultato.
>![[Pasted image 20251218162108.png]]
>
>Infine, si normalizza il risultato.
>![[Pasted image 20251218162127.png|center]]

>[!tip] Circuito completo
>![[Pasted image 20251218162151.png|center]]

