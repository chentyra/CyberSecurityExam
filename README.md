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

## SlowLoris: Come installarlo 

Bisogna copia la repository utilizzando il comando:
>sudo pip3 install CyberSecurityExam

Scaricare pip se necessario.
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

# Tecniche di Mitigazione

Ci sono vari modi per mitigare l’attacco tra cui:
* Incrementare il numero massimo di clienti che il web server può accettare;
* Limitare il numero di connessioni che un utente IP può instaurare;
* Limitare l’intervallo di tempo della connessione dedicata al client;
* Implementare alcuni moduli apache tra cui:
  * Mod_limitipconn
  * Mod_qos
  * Mod_evasive
  * Mod security
  * Mod_noloris
  * Mod_antiloris
  * Mod_reqtimeout (disponibile su Apache 2.2.15 ed è una soluzione supportata dagli sviluppatori)
  
## Netstat

Prima di bloccare un indirizzo Ip , probabile causa dell'attacco , devo prima individuare tale indirizzo. Per farlo uso **Netstat**.

Netstat, composto dalle parole network (“rete”) e statistics (“statistiche”), è un programma che funziona tramite istruzioni date dalla riga di comando. Fornisce statistiche essenziali su tutte le attività di rete e dà informazioni su quali porte e indirizzi funzionino le rispettive connessioni (TCP, UDP), oltre a indicare quali siano le porte aperte per accogliere le richieste. Attraverso il comando:
> netstat -ntu -4 -6 |  awk '/^tcp/{ print $5 }' | sed -r 's/:[0-9]+$//' | sort | uniq -c | sort –

Nel caso questo comando non funzioni, usare :
> netstat -ntu |  awk '/^tcp/{ print $5 }' | sed -r 's/:[0-9]+$//' | sort | uniq -c | sort –n

È possibile individuare gli indirizzi IP che utilizzano maggiormente il server , ordinandole e contando le loro occorrenze. Un indirizzo Ip che istaura molte connessioni potrebbe essere la causa dell’attacco.

### Come bloccare un indirizzo IP
* **Prima soluzione**

Uso il comando:
> ip route add blackhole 92.243.xx.xx

Riavviare Apache.

* **Seconda soluzione**

Uso il comando: 
> iptables -I INPUT -p tcp --dport 80 -m connlimit --connlimit-above 50 --connlimit-mask 20 -j DROP

In questo modo è possibile limitare le connessioni che si possono istaurare con il server.

* **Terza Soluzione**
Uso il comando:
> iptables -A INPUT --src <the specific IP> -j DROP
  
 Un indirizzo Ip viene bloccato utilizzando le Ip Tables.













