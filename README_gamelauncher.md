# GameVault — Launcher di giochi (UI moderna)

Launcher grafico per organizzare e avviare i tuoi giochi, compatibile con **Windows e Linux**.
Interfaccia scura moderna con sidebar, card con hover, riquadri animati e **sfondo sfocato reale**.
I collegamenti restano salvati tra le sessioni. **L'app NON disinstalla mai i giochi** — rimuove solo i collegamenti dalla libreria.

Contenuto:

- `gamelauncher.py` — sorgente Python unico (Windows + Linux, richiede Python 3.8+)
- `GameVault.exe` — eseguibile Windows standalone (nessuna installazione)
- `GameVault` — eseguibile Linux standalone (equivalente dell'.exe)

## Interfaccia

- **Sidebar** with icon-nav (Libreria / Impostazioni) + titolo brand
- **Header** con barra di ricerca Integrata
- **Card moderne** con icona grande, hover evidenziato, asterisco preferiti, contatore avvii
- **Piattaforma sfondo**: scegli un'immagine → verrà mostrata **sfocata** (cover + blur + velo scuro) dietro tutta l'interfaccia, ridisegnata in tempo reale al resize
- 11 lingue: italiano, inglese, tedesco, francese, spagnolo, russo, hindi, coreano, cinese, giapponese, portoghese

## Funzionalità

### Libreria
- Tutti i giochi collegati in una griglia con icone
- **Barra di ricerca** in alto per trovare subito un gioco
- **Pulsante "+ Game"** nella libreria per aggiungerne uno nuovo
- **Preferiti**: filtro dedicato + stella su ogni scheda
- **Cartelle**: ordina i giochi; crea, rinomina, elimina (a destra in alto)
- **Modifica**: cambio di nome, collegamento, icona, cartella, preferito
- **Rimozione**: solo il collegamento, il gioco resta sul disco
- Contatore avvii per ogni gioco

### Aggiunta guidata di un gioco (3 passi)
1. **Eseguibile o collegamento**: `.exe`, `.lnk`, `.url`, `.bat`, `.cmd` (Windows) — qualsiasi binario o script Linux
2. **Icona**: estratta automaticamente dall'eseguibile, se presente; altrimenti scegli un'immagine
3. **Nome**: il nome con cui apparirà in libreria (+ cartella opzionale e preferito)

### Impostazioni
- **Lingua**: 11 opzioni immediatamente applicate
- **Sfondo**: scegli immagine → sfocata e scurtita dietro l'interfaccia; puoi rimuoverla

## Avvio

### Windows
```
GameVault.exe    → doppio clic e via (niente installazione)
```

### Linux
```
chmod +x GameVault             (solo la prima volta)
./GameVault
```

### Da sorgente (entrambi i sistemi)
```
python gamelauncher.py          # Windows; Linux: python3
python gamelauncher.py --selftest
```

Dipendenze sorgente: `pip install pillow icoextract` + `python3-tk` su Linux.
Gli eseguibili non richiedono nulla.

## Dove sono i dati
Tutto (giochi, cartelle, lingua, sfondo) è salvato in `~/.gamevault/library.json`.
Le icone estratte vengono salvate in `~/.gamevault/icons/`.

## Avvio dei giochi
- **La directory di lavoro viene impostata sempre alla cartella del gioco**: indispensabile per i giochi HaxeFlixel/Friday Night Funkin' (Psych Engine, Kade Engine, Vs mod) che caricano asset con percorsi relativi — senza CWD corretta crashano o bugano all'avvio
- I file `.bat`/`.cmd` vengono avviati con CWD corretta (tipici dei giochi itch.io)
- I collegamenti `.lnk`/`.url` vengono lanciati direttamente, così Windows usa anche argomenti e cartella di lavoro salvati nel collegamento
- Windows: fallback `os.startfile`; Linux: esegue direttamente il file; gli script `.sh` senza +x vengono avviati con `sh`

## Cosa NON fa (per scelta)
- ❌ Non disinstalla i giochi: rimuove solo il collegamento dalla libreria
- ❌ Non cancella mai file di gioco
- ✅ Tutto è persistente tra sessioni

## Licenza
MIT
