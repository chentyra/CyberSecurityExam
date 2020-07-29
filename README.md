# CyberSecurityExam
In questo documento vedremo come utilizzare il tool slowhttptest e lo slowloris.

* SlowHTTPTest è uno strumento che simula alcuni attacchi Denial of Service a livello di applicazione prolungando le connessioni HTTP in diversi modi.
* Lo SlowLoris invia periodicamente delle intestazioni complete mantendendo in vita diverse connessioni che non vengono chiuse a meno che non lo faccia il server.
## Di cosa abbiamo bisogno per effettuare l'attacco
* Una macchina virtuale Linux che funge da server;
* Una macchina virtuale Kali che funge da client;

## SlowHTTPTest: Come installarlo
Digitare nella command window di Kali:
> sudo apt-get update 

> sudo apt-get install slowhttptest

## Come utilizzare il tool
Digitare nella command window di Kali:
> slowhttptest –c [number_connections] –i[Intervall_send] –r [connections_for_seconds] –t [mode_request] –u [URL_server] –x [header_length] –p [timeout]

In generale è possibile scegliere tra diverse opzioni visibili digitando nella command windown il comando:
> slowhttptest -h

L'output sarà:

| **Comando** | **Descrizione** |
| --- | --- |
|**OpzioniProxy** | **Descrizione** |
| -d | Permette di indirizzare tutto il traffico attraverso un proxy e relativa porta. Ad es. -d proxy:port | 
| -e | Permette di indirizzare solo il traffico dei probe attraverso un server proxy. Ad es. -e proxy:port | 
| -p | Tempo di attesa (espresso in secondi) di una risposta HTTP su connessione probe dopo il quale il server è considerato non raggiungibile | 
|**OpzioniGrafiche** | **Descrizione** |
| -g |	Permette di generare statistiche in formato CSV e HTML | 
| -o | Specifica un file di output (incluso di path). Utilizzato insieme all'opzione -g | 
| -v | Verbosity. Specifica il livello di dettaglio del log (valori da 0 a 4).  | 
| **ModiTest** | **Descrizione** |
| -H, B, R o X |	Specifica il tipo di slow down: -H per la sezione header, -B per la sezione Body del messaggio. -R abilita il range test, -X abilita il test slow read | 
|**OpzioniGenerali** | **Descrizione** |
| -c | Numero di connessioni da istaurare |
| -i | Permette di specificare ogni quanti secondi inviare dati per ciascuna connessione. | 
| -l | Per specificare la durata, in secondi, del test | 
| -r | Connection rate. Numero di connessioni per secondo | 
| -s | Valore in byte del Content-Length header, se l'opzione -B è definita | 
| -t | Permette di specificare un verb personalizzato | 
| -u | Per specificare URL target del test (nello stesso formato utilizzato dai browser) | 
| -x | massima lunghezza, in byte, dei dati | 

*Posso utilizzare WireShark per osservare i pacchetti scambiati tra client e server.*

## SlowLoris: Come installarlo [https://github.com/gkbrk/slowloris] 
Uso le istruzioni indicate dal link sovrastante.
## Come utilizzare il tool
Digitare nella command window di Kali:
> slowloris [url] -s [# socket]

In generale è possibile scegliere tra diverse opzioni visibili digitando nella command windown il comando:
> slowloris -h

L'output sarà:
| **Comando** | **Descrizione** |
| --- | --- |
|**OpzioniProxy** | **Descrizione** |
| -h | Viene mostrato l'help | 
| -s | Numero di socker da instaurare con il server | 
| -p | Porto usato dal sito. Di solito è 80 | 
| -v | Verbosity. Specifica il livello di dettaglio del log (valori da 0 a 4). | 
| -ua | User-agent random per ogni richiesta | 
| --proxy-host | SOCKS5 proxy host | 
| --proxy-port | SOCKS5 proxy port |
| --https | usa https per le richieste | 
| --sleeptime | tempo di attesa tra ogni header inviato | 

*Posso utilizzare WireShark per osservare i pacchetti scambiati tra client e server oppure Etherape per osservare graficamente il traffico fra quest'ultimi.*

## Cos'è Etherape e come installarlo
EtherApe è un monitor di rete grafico per Unix modellato su etherman. Dotato di livelli di collegamento, modalità IP e TCP, visualizza graficamente l'attività di rete. Host e collegamenti cambiano di dimensioni in base al traffico. I protocolli utilizzati per lo scambio dei dati vengono visualizzati con colori differenti. Questo strumento permette anche di esportate i grafici ottenuti.

Per installarlo bisogna prima aggiornare il sistema linux . Per farlo digitare nella command window:
> sudo apt-get update 

Installare Etherape 
> sudo apt-get install etherape

Digitare y.

Per avviarlo digitare
>sudo etherape







