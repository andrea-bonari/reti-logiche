>[!note]
>Le FSM non completamente specificate sono macchine in cui per alcune configurazioni degli ingressi e stati correnti non sono specificati gli stati futuri e/o le configurazioni d'uscita.

È possibile estendere la regola di Paull-Unger a queste macchine. Due stati di ingresso sono compatibili se e solo se, per ogni simbolo di ingresso $i_{\alpha}$ valgono le due seguenti relazioni:
Se ambedue sono specificati allora: $$\begin{align*}
\lambda(s_{i},i_{\alpha})&= \lambda(s_{j},i_{\alpha})\\
\delta(s_{i},i_{\alpha})&= \delta(s_{j},i_\alpha)\end{align*}$$

Se uno o entrambi non sono specificati la compatibilità (indicata con $\lor$) si ritiene soddisfatta.

Si può quindi creare la tabella delle implicazioni normalmente, tuttavia si ha che la relazione di compatibilità non è transitiva, e quindi è necessaria un ulteriore analisi.

Si suddivide quindi il grafo di compatibilità in classi di massima compatibilità chiuse:
![[Pasted image 20251218181725.png]]
