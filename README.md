# Prima di cominciare
Creare un Hackintosh **non è affatto semplice**, infatti potreste riscontrare numerosi errori durante la sua realizzazione che talvolta giungere ad una loro risoluzione può richiedere anche diverse ore di lavoro; ma non demoralizzatevi, questa guida è stata creata appositamente per questo: semplificare la realizzazione di un Hackintosh compatibile su qualsiasi piattaforma (Desktop, Laptop), adoperabile anche da utenti poco esperti e che non se ne intendono, in quanto tenterò di esprimermi sempre con un linguaggio semplice e senza intrecci. Detto questo, siamo pronti per cominciare.

## Pre-requisiti
Un sistema operativo Hackintosh non è compatibile con ogni tipo di hardware, le incompatibilità più frequenti riguardano generalmente la scheda grafica (GPU), il processore (CPU) ed eventuali schede madre (MOBO).

Se non sai di preciso da cosa sia composto il tuo hardware, ti linko alcuni software che possono aiutarti:
* Info CPU: https://www.cpuid.com/softwares/cpu-z.html
* Info GPU: https://www.techpowerup.com/gpuz/

## Incompatibilità note
**dGPU (Dedicate) e iGPU (Integrate)**
* Tutte le dGPU NVIDIA "RTX" di ogni generazione (es: RTX 2060, RTX 3070 Ti, RTX 4080)
* Tutte le dGPU NVIDIA "GTX 16xx" (es: GTX 1650, GTX 1660 Ti)
* Tutte le dGPU AMD "Lexa Series" (es: WX 3100, WX 2100, RX 550X)
* Tutte le iGPU su CPU AMD APU
* Le seguenti iGPU Intel: https://telegra.ph/Hackintosh---iGPU-Intel-NON-SUPPORTATE-12-04

**Info CPU non compatibili**
* Linee guida supporto CPU, se non ve ne intendete potete confrontare le opzioni descritte con le vostre tramite CPU-Z: https://macos86.github.io/macos-limits.html#supporto-cpu

> Nota per quanto riguarda l'incopatibilità con GPU: diversi laptop e desktop potrebbero possedere sia una CPU con grafica integrata che una scheda video dedicata. Esempio: Un `Intel Core i7 9700k` possiede la iGPU `Intel UHD Graphics 630`, la quale non è generalmente usata poiché al suo posto viene sfruttata una scheda video dedicata, mettiamo caso una `GEFORCE RTX 3060 Ti`. In quanto questa dGPU non è supportata da Hackintosh, tramite il `BIOS` si può impostare come output primario la iGPU, e di conseguenza poter far girare l'Hackintosh. Dunque non preoccupatevi. **Quest'ultimo scenario verrà affrontato prossimamente nella guida**.


## Trovare l'hardware ideale
Se vuoi realizzare il tuo Hackintosh su un hardware dedicato, magari assemblando il proprio PC esclusivamente per farci girare un sistema operativo Hackintosh, lascio di seguito alcuni link utili per la scelta dei componenti.
* https://www.tecnogalaxy.it/blog/componenti-per-assemblare-un-hackintosh/
* https://pcblog.altervista.org/componenti-compatibili-con-hackintosh/

Se invece sei in carca di un laptop ideale per Hackintosh, ecco alcuni link:
* Rog Strix G17: https://www.trovaprezzi.it/prezzo_notebook_rog_strix_g17_g713.aspx
* Razer Blade 15: https://www.trovaprezzi.it/prezzo_notebook_razer_blade_15.aspx
* Acer Spin 5: https://www.trovaprezzi.it/prezzo_notebook_acer_spin_5.aspx
* Acer Swift 3: https://www.trovaprezzi.it/prezzo_notebook_acer_swift_3.aspx
* Asus VivoBook 15: https://www.trovaprezzi.it/prezzo_notebook_asus_vivobook_15.aspx


### Per maggiori informazioni relative ai requisiti minimi o consigliati relativi al vostro hardware, allego la guida ufficiale di OpenCore (la piattaforma che sfrutteremo per realizzare questo Hackintosh).
* Requisiti: https://dortania.github.io/OpenCore-Install-Guide/macos-limits.html

***

# [Fase preliminare: crea il supporto di installazione USB](https://github.com/Ludqvico/Guida-Hackintosh-Completa-in-ITALIANO/wiki/Fase-preliminare:-crea-il-supporto-di-installazione-USB)
