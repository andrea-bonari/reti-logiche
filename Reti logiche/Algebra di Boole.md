>[!note]
>L'algebra di Boole è un sistema algebrico identificato dalla quintupla: $$(B,+,*,O,I)$$
>Dove $B$ è l'insieme di specificazione, $+$ e $*$ sono operatori binari, e $O,I\in B$ sono elementi speciali.

>[!tip] Sistemi algebrici
>Definiamo un sistema algebrico come una combinazione di un'insieme, e di una o più operazioni.

>[!tip] Operazioni
>Definiamo un operazione $\alpha$ sull'insieme $S=\set{s_{1},s_{2},\cdots}$ come una funzione: $$\alpha: (S\times S)\to S$$

Le proprietà dei due operatori $+$ e $*$ sono dedotte dai seguenti assiomi:
- La somma e il prodotto sono commutativi $\forall x,y\in B$.
- La somma è distributiva rispetto al prodotto, e il prodotto è distributivo rispetto alla somma.
- $O$ è l'elemento neutro della somma, mentre $I$ è l'elemento neutro del prodotto.
- Ogni elemento $x\in B$ ammette un elemento $x'\in B$ tale che $(x+x')=I$ e $(x*x')=O$.

### Algebra di commutazione
>[!note]
>L'algebra Booleana a due valori, anche detta algebra di commutazione è definita da: $$(\set{0,1},+,*,\sim,0,1)$$
>Cioè un estensione dell'algebra di Boole con $B=\set{0,1}$.
>
>Un'espressione Booleana $E$ è definita in modo induttivo come parola composta da operatori booleani, parentesi, costanti e letterali nel modo seguente:
>- Sia gli elementi di $B$, chiamati costanti, che i letterali $x,y,z,\cdots$, sono espressioni booleane.
>- Se $E_{1}$ e $E_{2}$ sono espressioni booleane, anche $E_{1}+E_{2}$, $E_{1}*E_{2}$ e $\sim E_{1}$ lo sono.
>- Non esistono altre espressioni booleane oltre a quelle che possono essere generate da un numero finito di applicazioni delle due regole precedenti.

>[!tip] Proprietà e principio di dualità
>
>| Proprietà          | Somma                   | Prodotto                          |
>| ------------------ | ----------------------- | --------------------------------- |
>| Associativa        | $a+(b+c)=(a+b)+c$       | $a*(b*c)=(a*b)*c$                 |
>| Distributiva       | $a*(b+c)=a*b+a*c$       | $a+(b*c)=(a+b)*(a+c)$             |
>| Idempotenza        | $a+a=a$                 | $a*a=a$                           |
>| Elemento neutro    | $a+1=1$ e $a+0=a$       | $a*0=0$ e $a*1=a$                 |
>| Assorbimento       | $a+(a*b)=a$             | $a*(a+b)=a$                       |
>| Leggi di De Morgan | $(a+b)'=a'*b'$          | $(a*b)'=a'+b'$                    |
>| Consenso           | $a*b+a'*c+b*c=a*b+a'*c$ | $(a+b)*(a'+c)*(b+c)=(a+b)*(a'+c)$ |
>
>Per il principio di dualità ogni identità deducibile dai postulati dell'algebra di Boole è trasformata in un altra identità se:
>- Ogni somma è sostituita da un prodotto, e viceversa.
>- Ogni elemento identità $0$ è sostituito da un elemento identità $1$, e viceversa.

>[!tip] Funzione di commutazione
>Definiamo una funzione di commutazione a $n$ variabili $f(x_{0},\cdots,x_{n-1})$ come una funzione: $$f:\set{0,1}^{n}\to \set{0,1}$$
>
>Queste funzioni possono essere rappresentate comodamente utilizzando una tabella della funzione o una tabella della verità.
>
>Si ha che una funzione booleana di $n$ variabili può essere espressa da un'espressione booleana di $n$ variabili $E$, e quindi dalle proprietà dell'algebra di commutazione si ha che:
>- Possono essere utilizzate per manipolare un'espressione booleana ed ottenerne una equivalente.
>- Due espressioni booleane $E_{1}$ e $E_{2}$ sono equivalenti se e solo se sono riconducibili alla stessa funzione booleana.
>
>Ad un'espressione $E$ di $n$ variabili corrisponde un'unica funzione $f$ di $n$ variabili, e viceversa.
>
>Si ha che qualunque funzione logica può realizzarsi usando un insieme completo di operatori elementari.

Data un'espressione di una funzione booleana l'algebra di commutazione permette di manipolarla per ottenere un'espressione equivalente, ma di forma diversa, eventualmente con caratteristiche, meglio rispondenti a particolari requisiti.

Si ha che l'applicazione delle trasformazioni algebriche non permette di identificare una procedura sistematica. Di conseguenza non è possibile identificare un algoritmo e non è possibile sapere se un'espressione è quella minima.

### Forme canoniche

>[!note] Prima forma canonica
>La prima forma canonica, anche detta SoP, ha come espressione generale: $$(x_{1}'\cdots x_{n}')*f(0,\cdots,0)+(x_{1}'\cdots x_{n})*f(0,\cdots,1)+\cdots+ (x_{1}\cdots x_{n})* f(1,\cdots,1)$$
>Definiamo i mintermini della funzione $f$ come: $$(x_{1}'\cdots x_{n}'),\quad(x_{1}'\cdots x_{n}),\quad\cdots,\quad(x_{1}\cdots x_{n})$$

>[!note] Prima forma canonica
>La seconda forma canonica, anche detta PoS, ha come espressione generale: $$((x_{1}'+\cdots +x_{n}')+f(0,\cdots,0))*((x_{1}'+\cdots +x_{n})+f(0,\cdots,1))*\cdots* ((x_{1}+\cdots +x_{n})+ f(1,\cdots,1))$$
>Definiamo i maxtermini della funzione $f$ come: $$(x_{1}'+\cdots+ x_{n}'),\quad(x_{1}'+\cdots+ x_{n}),\quad\cdots,\quad(x_{1}+\cdots+ x_{n})$$

>[!tip] Teorema di espansione di Shannon
>Sia $f: B^{n}\to B$ una funzione booleana. Per ogni $(x_{1},x_{2},\cdots,x_{n})$ in $B^{n}$ si ha: $$\begin{align*}
>f(x_{1},x_{2},\cdots,x_{n})&= x_{1}'*f_{x_{1}'}+x_{1}*f_{x_{1}}\\
>&= x'_{2}*f_{x_{2}'}+x_{2}* f_{x_{2}}\\
>&= \cdots\\
>&= (x_{1}'+f_{x_{1}})*(x_{1}+f_{x_{1}'})\\
>&= (x_{2}'+f_{x_{2}})*(x_{2}+f_{x_{2}'})\\
>&= \cdots
>\end{align*}$$
>Questo teorema può essere utilizzato anche su espressioni Booleane.

