## repodepo

Exam project: Modelli Probabilistici per le Decisioni (2015/16) - University of Milan Bicocca

Based on article:

Sensors 2013, 13, 5460-5477; doi:10.3390/s130505460





#### Project purposes

- Definitions of data structure
- HMM model
- infer the user's activity from sensor data
- data analysis

#### Project Report (ita)

##### Introduzione
L'invecchiamento della popolazione ha un impatto sempre più significativo sul sistema sanitario. Per questo si cercano vie più efficienti per portare assistenza in casa delle persone bisognose, in particolare gli anziani, il cui numero secondo le stime é in costante aumento grazie alle migliori condizioni di vita e di cure.

Monitorare le attività umane (ADL) è diventato un aspetto fondamentale per costruire un ambiente intelligente atto a garantire il benessere in grado di aumentare sia la sicurezza, sia l'autonomia dei soggetti.

Uno degli approcci più promettenti ed economici è il monitoraggio delle attività tramite una rete wireless di sensori (WSN) disposti nell'ambiente abitativo, in quanto molto flessibile e di facile sviluppo.
Sono stati sviluppati parecchi modelli che utilizzano sensori per monitorare le attività ADL, come ad esempio *Reti Bayesiane* o 8Conditional Random Fields8. In particolare, si è notato che *Hidden Markov Model (HMM)*} è un modello performante in questo dominio applicativo; alcuni articoli approfondiscono il modello proponendo soluzioni di HMM ibridi, noi invece abbiamo implementato una versione classica.

##### I sensori
Per costruire e testare il modello, sono stati utilizzati dataset presi da due appartamenti. Ogni appartamento fornisce due dataset: il primo con le rilevazioni generate dai sensori, il secondo con le attività rilevate dai sensori.
I sensori utilizzati sono stati di vario tipo (magnetici, a pressione, elettrici etc), disposti in più zone della casa in maniera il meno invasiva possibile e hanno registrato e salvato i dati per diversi intervalli di tempo (due settimane circa).

`Start time - End time - Location - Type - Place`

![](Report/Sensor.png)

dove la tripla `Location-Type-Place` indica il sensore che ha effettuato la rilevazione. Nel dataset delle attivita ogni riga contiene l’intervallo di tempo e il nome dell’attivita rilevata. Ogni attivita è strettamente legata alla rilevazione effettuata dai sensori, ed è rappresentata su una riga come:


In un HMM standard le variabili nascoste yt (y al tempo t) dipendono solo dallo stato delle variabili yt 1 (y al tempo t − 1), mentre le variabili osservabili xt (x al tempo t) dipendono solo dallo stato delle variabili yt (y allo stesso istante t).
- p(yt∣yt − 1) le probabilità di transizione da uno stato y al successivo; 


Dopodichè, è necessario definire le probabilità iniziali come segue: `model.add transition( model.start, ADL1, 0.6 )` e le probabilità di transizione tra gli stati nel seguente modo:


Queste funzioni prendono in input rispettivamente liste e matrici e normalizzano i dati contenuti, utilizzando la divisione fornita della libreria numpy. In questo modo ogni lista e ogni riga della matrice ha come somma 1.0.
- `csv list e csv matrix` 
Come facilmente intuibile, generano file in formato .csv a partire dai dati in input: lista dei nomi delle variabili (su righe e colonne per la matrice) e lista (o matrice) dei valori da inserire.
Esso genera la sequenza di attività ottima generata in base alla sequence inserita; in questo modo possiamo verificare se la sequenza di ADLs risultante è coerente con quella della fornita dal dataset originale.

- `diff B`


![](Report/ordonezA.png)

