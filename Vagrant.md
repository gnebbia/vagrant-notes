# Vagrant Notes

## Requisiti

1. Installare un provider (pref Virtualbox) : `Virtualbox`
https://www.virtualbox.org/wiki/Downloads
2. Installare `Vagrant` https://www.vagrantup.com/downloads.html

## Box (VM image)

### Download Box
E' possibile scaricare dal `Vagrant Cloud` :
https://app.vagrantup.com/boxes/search delle immagini pre-create dagli
utenti e dalla hashicorp. Da shell basta digitare:
```sh
vagrant box add hashicorp/precise64
``` 
Questo scarichera' (se non gia' presente nella list delle immagini
scaricate) il box precise64 cioe' un sistema Ubuntu 12.04 a 64 bit.

### Lista Box Scaricati  
Per visualizzare la lista di tutti i box presenti (scaricati) all'interno del sistema host da shell basta digitare:  
```
vagrant box list
```

### Delete Box
Per cancellare un Box da shell basta digitare:  
```sh
vagrant delete hashicorp/precise64
```
E' necessario passare l'id del box per cancellare il box prescelto.  

## Inizializzare il progetto  
Ogni progetto in Vagrant deve essere inserito in una directory personale,
e per lavorare con essi e' necessario spostarsi nella directory del
progetto prescelto.  E' necessario, creare una nuova directory, spostarsi
all'interno e inizializzare il progetto
```
mkdir project1
cd project1
vagrant init hashicorp/precise64
```
In questo modo verra' creato un file `Vagrantfile` contenete tutte le
caratteristiche del progetto, in questo caso sara':
```sh
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
end
```
Ora tutto cioe' che abbiamo e' una VM (non avviata) basata su Ubuntu 12.04 a 64 bit

## Avviare il progetto

### Primo Avvio
Se il progetto e' stato appena inizializzato per avviare la VM bisogna
spostarsi all'interno della cartella del progetto e avviarla in questo
modo:
```
cd project1
vagrant up
```
In questo modo viene forzato il provisioning (effettuato tramite Shell,
Chef, Puppet , ...) e il sistema guest viene avviato

### Generico Avvio
Se il progetto e' stato gia' avviato in precedenza si consiglia per
avviarlo l'utilizzo del comando:
```
cd project1
vagrant reload
```
Questo comando permette l'avvio della macchina senza che vengano
effettuate le operazioni di ricarica sul provisioning, se sono state
effettuate operazioni di provisioning per renderle effettive e'
necessario lanciare:
```
cd project1
vagrant reload --provision
```

## Stato VM
Per visualizzare lo stato delle VM sono presenti due comandi da eseguire
in posizioni differenti:
- vagrant status (locale)
- vagrant global status (globale)

### Vagrant Status

Questo comando restituisce lo stato delle vm:
```sh
cd project1
vagrant status
```
Ci restituira' lo stato delle macchine contenute in project1:
- `not created`
- `running`
- `stopped` 
in base a dove esso e' eseguito.

### Vagrant global status

Questo comando ci permette di visualizzare lo stato di tutte le VM
precedentemente create, spesso lo stato non e' aggiornato quindi si
consiglia di effettuare una forzatura del reload dello stato:
```sh
vagrant global-status --prune
```

## Gestione VM

Vagrant mette a disposizione diversi comandi per interagire con le VM:
- Stoppare la VM:
```sh
vagrant halt
```
se viene utilizzato all'interno di una cartella contenente diverse
VM tutte vengono fermate a meno che non venga specificato l'id della
macchina guest da fermare.

- Sospendere la VM:
```sh
vagrant suspend
```
se viene utilizzato all'interno di una cartella contenente diverse
VM tutte vengono sospese a meno che non venga specificato l'id della
macchina guest da sospendere

- Cancellare la VM:
```sh
vagrant destroy
```
questo comando e' un po' diverso dai precedenti infatti se eseguito
all'interno di una cartella contenente un progetto con piu VM, da la
possibilita' di scegliere in maniera interattiva quali cancellare e
quali no; invece se viene specificato l'id e' possibile cancellare la
VM ovunque essa si trovi.

- Interagire con la VM:

