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

| Comando | Descrizione |
| --- | --- |
| -a | Per specificare il valore iniziale per il test range header |
| -b | Specifica il numero di bytes per il test range header |
| -c | Permette di specificare il numero di connessioni (fino a 65539) | 
| -d | Permette di indirizzare tutto il traffico attraverso un proxy e relativa porta. Ad es. -d proxy:port | 
| -e | Permette di indirizzare solo il traffico dei probe attraverso un server proxy. Ad es. -e proxy:port | 
| *Modi di Test* | *Descrizione* |
| -H, B, R o X |	Specifica il tipo di slow down: -H per la sezione header, -B per la sezione Body del messaggio. -R abilita il range test, -X abilita il test slow read | 
| -g |	Permette di generare statistiche in formato CSV e HTML | 
| -i | Permette di specificare ogni quanti secondi inviare dati per ciascuna connessione. | 
| -k | Per il test di slow read permette di specificare quante volte ripetere la richiesta nella stessa connessione (se il server supporta HTTP pipelining). | 
| -l | Per specificare la durata, in secondi, del test | 
| -n | Per specificare l'intervallo, in secondi, tra le operazioni di lettura dal buffer in ricezione | 
| -o | Specifica un file di output (incluso di path). Utilizzato insieme all'opzione -g | 
| -p | Tempo di attesa (espresso in secondi) di una risposta HTTP su connessione probe dopo il quale il server è considerato non raggiungibile | 
| -r | Connection rate. Numero di connessioni per secondo | 
| -s | Valore in byte del Content-Length header, se l'opzione -B è definita | 
| -t | Permette di specificare un verb personalizzato | 
| -u | Per specificare URL target del test (nello stesso formato utilizzato dai browser) | 
| -v | Verbosity. Specifica il livello di dettaglio del log (valori da 0 a 4).  | 
| -w | Inizio del range, espresso in byte, da cui la dimensione della finestra visualizzata viene prelevata. | 
| -x | massima lunghezza, in byte, dei dati | 
| -y | fine del range, espresso in byte, da cui la dimensione della finestra visualizzata viene prelevata. | 
| -z | Byte da leggere dal buffer in ricezione con una singola operazione di lettura | 







