>[!note]
>Le logiche programmabili sono dispositivi hardware che mettono a disposizione componenti logici e linee di connessioni. Sono detti tali perché i componenti disponibili sono connessi a seconda del progetto e sono programmabili.
>
>In base al tipo di programmabilità si categorizzano in:
>- One-Time Programmable
>- Reprogrammable
>- Reconfigurable

>[!tip] Tecnologie fuse e antifuse
>Nella tecnologia fuse (One-Time Programmable) le linee del dispositivo sono prodotte in modo da essere sempre connesse. La programmazione consiste nel bruciare alcune connessioni in modo da mantenere solo quelle necessarie.
>
>![[Pasted image 20251216115144.png|center]]
>
>Viceversa nella tecnologia antifuse, le linee del dispositivo sono prodotte in modo da essere sempre disconnesse, e la programmazione consiste nel creare le connessioni.
>
>![[Pasted image 20251216115252.png|center]]

>[!tip] Tecnologia EEPROM
>Una EEPROM è una memoria programmabile e cancellabile (Reprogrammable), la cui programmazione consiste nel depositare carica sul floating gate del transistor in modo da mantenerlo in conduzione.
>
>![[Pasted image 20251216115423.png|center]]

>[!tip] Tecnologia SRAM
>Una SRAM è prodotta in modo da essere sempre disconnessa. La sua programmazione consiste nel memorizzare un valore logico in una cella RAM statica.
>
>![[Pasted image 20251216120802.png|center]]

Alcuni dispositivo dispongono di linee di connessioni globali, condivise da molti elementi logici.

### Logiche programmabili a due livelli
>[!note]
>Dei dispositivi con bus globali se ne distinguono tre categorie principali:
>- Programmable Logic Array: con piani `and` e `or` programmabili, dove si costruiscono solo i mintermini necessari.
>- Programmable Array Logic: con solo il piano `and` programmabile, dove si costruiscono solo i mintermini necessari.
>- Read-Only Memory: con piano `and` pre-programmato tramite un decoder, dove son disponibili tutti i mintermini.

>[!tip] Schema di un PLA
>![[Pasted image 20251216121759.png|center]]

>[!tip] ROM
>In una ROM viene associato un indirizzo ad una certa parola, usando un address decoder, bruciando poi i collegamenti nella parte programmabile
>![[Pasted image 20251216122119.png|center]]

