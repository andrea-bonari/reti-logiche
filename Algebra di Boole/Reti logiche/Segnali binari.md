>[!note]
>I sistemi digitali binari sono ottimi per diversi motivi, tra cui la facilità realizzativa e l'ottima immunità ai disturbi. Fisicamente possono essere rappresentati da valori come la tensione elettrica, l'intensità di corrente, e la potenza ottica. Per rappresentare i valori dei segnali nel tempo utilizzeremo dei diagrammi temporali.
>
>![[Pasted image 20250917145014.png]]

### Porte logiche
>[!note]
>Una porta logica è un elemento elettronico che esegue una funzione logica specifica su uno o più ingressi, producendo un uscita in base a quelle istruzioni.
>
>Le principali porte logiche rappresentano le operazioni logiche fondamentali $\text{OR}, \text{ AND}, \text{ NOT}$. Esistono le operazioni $\text{XOR}, \text{ NAND},\text{ NOR}$.
>
>![[Pasted image 20250917145621.png|center]]
>![[Pasted image 20250917145548.png|center]]

A differenza del modello matematico le porte logiche introducono una latenza.

### Reti combinatorie
>[!note]
>Definiamo una rete combinatoria come un circuito logico di $n$ ingressi e $m$ uscite privo di retroazioni, formato collegando porte logiche $\text{OR},\text{ AND},\text{ NOT}$.
>
>Per simularne il funzionamento si assegnano valori agli ingressi della rete propagandoli in avanti, fino a determinare il valore logico dell'uscita.

Definiamo il livello di una rete combinatoria come il numero di livelli di operatori annidati (trascurando la negazione). Il numero di livelli influenza la velocità del circuito e il costo realizzativo.

Data una funzione booleana, esistono infinite reti combinatorie che la realizzano, tuttavia, l'equivalenza logica di una rete non implica l'equivalenza di struttura e costo della rete.

