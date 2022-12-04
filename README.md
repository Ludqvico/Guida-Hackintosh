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


# Fase preliminare: crea il supporto di installazione USB
Siamo pronti per iniziare: prima di tutto per seguire questa fase sarà necessario possedere un suppporto USB (USB Drive) con i seguenti requisiti:
* Almeno 4GB di memoria
* Qualora sia superiore di 16 GB formattere sempre il drive in FAT32

In questa guida seguiremo il suddetto metodo "Online", effettuabile da macOS/Linux o Windows. Qui approfondiremo la versione per Windows.

## Pre-requisiti
* Connessione ad internet (cablata o wireless)
* Python eseguibile da CMD (Da scaricare da qui: https://apps.microsoft.com/store/detail/python-310/9PJPW5LDXLZ5?hl=it-it&gl=it)

## EFI
Per prima cosa scarica la seguente release di OpenCore https://github.com/acidanthera/OpenCorePkg/releases, ed estrai il contenuto dell'archivio all'interno di una directory che chiameremo convenzionalmente `OpenCore Pkg`.

Dopodiché naviga nella path `...\OpenCore Pkg\X64` e copia la cartella `EFI`.

Ora recati nel `Desktop` (o nella directory che più ti fa comodo) e crea una nuova cartella che chiameremo `Hackintosh`, successivamente accedi all'interno di quest'ultima e incolla la cartella `EFI` precedentemente copiata.

## Ottimizzazione
Una volta fatto ciò sarà necessario rimuovere alcuni file al momento superflui.
* Per prima cosa recati in `...\Hackintosh\EFI\OC\Drivers`, e rimuovi tutti i file `.efi` tranne `OpenRuntime.efi`.
* Successivamente recati in `...\Hackintosh\EFI\OC\Tools`, e ripeti il medesimo procedimento rimuovendo ogni file a discapito di `OpenShell.efi`.


# Drivers
Per il corretto funzionamento del tuo Hackintosh è necessario scaricare ed inserire nella directory `...\Hackintosh\EFI\OC\Drivers` il file `HfsPlus.efi` scaricabile dal seguente link: https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi


# Kexts
> Questo passaggio è di fondamentale importanza. Garantisce l'ottimale comunicazione tra hardware e software nei parametri quali integrazione dGPU/iGPU,  driver audio e scheda di rete, dialogo con le funzionalità della CPU, funzionamento delle porte USB e altro ancora.

Per integrare un `Kernel Extension` nella configurazione del proprio Hackintosh sarà necessario recarsi nella path `...\Hackintosh\EFI\OC\Kexts` e inserire ogni `Kext` scaricato dalla relativa release GitHub sottoforma della sua cartella rinominata `xxx.kext`.

## Kexts obbligatori
### VirtualSMC
* https://github.com/acidanthera/VirtualSMC/releases
> Nota per quanto riguarda VirtualSMC. Questo Kext per il suo corretto funzionamento dovrà essere inserito nella relativa directory in combinazione con i seguenti Kexts:

**CPU Intel**
* VirtualSMC.kext
* SMCSuperIO.kext
* SMCProcessor.kext

**CPU AMD**
* VirtualSMC.kext

**Laptop DELL**
* SMCDellSensors.kext

> Nella guida ufficiale di OpenCore è riportato come in caso di Hackintosh su laptop sono necessari ulteriori kext inclusi nell'archivio di VirtualSMC per il corretto funzionamento di funzioni quali gestione della batteria, ambient light sensor (sensore adattamento automatica luminosità display) ed altri sensori. **Allego la guida specifica di OpenCore:** https://dortania.github.io/OpenCore-Install-Guide/ktext.html#virtualsmc-plugins

### [Lilu](https://github.com/acidanthera/Lilu/releases)
> Copia nella relativa directory `...\Hackintosh\EFI\OC\Kexts` esclusivamente il kext `Lilu.kext`.

### [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)
> Copia nella relativa directory `...\Hackintosh\EFI\OC\Kexts` esclusivamente il kext `WhateverGreen.kext`.

### [AppleALC](https://github.com/acidanthera/AppleALC/releases)
> Copia nella relativa directory `...\Hackintosh\EFI\OC\Kexts` esclusivamente il kext `AppleALC.kext`.

### [XHCI-unsupported](https://github.com/RehabMan/OS-X-USB-Inject-All)
> Necessario solamente su sistemi basati su `Intel`, dunque gli utenti `AMD` possono saltare questo passaggio.
**Necessario sulle seguenti `MOBO` con Socket `Intel`**
* H370
* B360
* H310
* Z390 (Non necessario su Hackintosh Mojave o superiori)
* X79
* X99
* ASRock Intel boards (tranne B460/Z490 e superiori)

## Ethernet
> In questo momento abbiamo bisogno di conoscere che scheda di rete utilizza il nostro sistema, in modo tale da poter scaricare il relativo kext.

> Per scoprirlo sarà necessario cercare tramite il menu Start o tramite la barra di ricerca del nostro computer `Gestione dispositivi`
![Immagine 2022-12-04 124310](https://user-images.githubusercontent.com/119785907/205493500-c4e5bf95-8c33-46be-8b78-2fb9c01a070d.png)

> Una volta aperto, identifica la sezione realtiva alle `Schede di rete`
![Immagine 2022-12-04 124435](https://user-images.githubusercontent.com/119785907/205493556-8574f0d4-08ff-4de9-a670-805ad5c5d488.png)

> Quindi estendi il menu a tendina `Schede di rete` e visualizza il modello della tua scheda di rete; nel mio caso la `Realtek Gaming GbE Family Controller`.
![Immagine 2022-12-04 124900](https://user-images.githubusercontent.com/119785907/205493737-16049548-d5b3-4d10-8763-f6a4222ab724.png)

In base a quest'ultima, ora puoi scegliere il Kext compatibile:
* **[IntelMausi](https://github.com/acidanthera/IntelMausi/releases)**
* **[AppleIGB](https://github.com/donatengit/AppleIGB/releases)**
* **[SmallTreeIntel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases)**
* **[AtherosE2200Ethernet](https://github.com/Mieze/AtherosE2200Ethernet/releases)**
* **[RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases)** (Questa nel mio specifico caso)
* **[LucyRTL8125Ethernet](https://www.insanelymac.com/forum/files/file/1004-lucyrtl8125ethernet/)**

## WiFi e Bluetooth
> Sempre nella relativa sezione su `Gestione dispositivi` qualora il nostro computer supportasse il collegamento WiFi e Bluetooth sarà necessario aggiungere alcuni Kexts.

**Qualora aveste una scheda Bluetooth non-nativa (es: PC Desktop)**
* **[BlueToolFixup](https://github.com/acidanthera/BrcmPatchRAM/releases)** (Da usare solo su macOS 12.x)

**Schede di rete Intel**
* **[AirportItlwm](https://github.com/OpenIntelWireless/itlwm/releases)** (Funziona sulla maggior parte delle schede di rete Intel)
* **[Qualora non funzionasse AirportItlwm](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#wifi-and-bluetooth)**

**Schede di rete Broadcom**
* **[AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup/releases)**

## Altri Kext richiesti su CPU AMD
* **[XLNCUSBFIX](https://cdn.discordapp.com/attachments/566705665616117760/566728101292408877/XLNCUSBFix.kext.zip)** (Solo per AMD FX, non consigliato per Ryzen)
* **[VoodooHDA](https://sourceforge.net/projects/voodoohda/)** (Per AMD FX e sistemi Ryzen Desktop con input Mic/Audio sul pannello frontale)
* **[AMDRyzenCPUPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor)** (Solo per Ryzen, gestione potenza CPU, **ancora in sviluppo/potenzialmente instabile**)
* **[AppleMCEReporterDisabler](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)** (Solo su macOS 12.x su sistemi AMD)

## Kext Extra
* **[AppleMCEReporterDisabler](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)** (Richiesto su macOS 10.5 e precedenti eseguito su sistemi Intel dual-socket)
* **[CpuTscSync](https://github.com/lvs1974/CpuTscSync/releases)** (Richiesto su Intel HEDT e su MOBO per server)
* **[NVMeFix](https://github.com/acidanthera/NVMeFix/releases)** (Corregge eventuali incompatibilità con unità NVMe non di Apple)
* **[CPUTopologyRebuild](https://github.com/b00t0x/CpuTopologyRebuild)** (Solo per CPU Intel Alder Lake di 12esima generazione)

## Kext Laptop
### Mouse e Tastiera
> Nel metodo precedentemente illustrato per la sezione [Ethernet](https://github.com/Ludqvico/Guida-Hackintosh-Completa-in-ITALIANO/wiki/Installazione-guidata/_edit#ethernet), recarsi su `Gestione dispositivi`. 
* **[VoodooPS2](https://github.com/acidanthera/VoodooPS2/releases)** (Richiede macOS 10.11 o superiori, funziona sulla maggior parte dei Mouse/Tastiere)
* **[VoodooSMBus](https://github.com/VoodooSMBus/VoodooSMBus/releases)** (Supporta macOS 10.14 o superiori, da usare qualora il primo non funzionasse)

### Touchpad
* **[VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI/releases)** (Richiede macOS 10.11 o superiori, funziona sulla maggior parte dei laptop)
* **[VoodooSMBus](https://github.com/VoodooSMBus/VoodooSMBus/releases)** (RichiedemacOS 10.14 o superiori, da usare qualora il primo non funzionasse)

### Altro
* **[VoodooI2C](https://github.com/VoodooI2C/VoodooI2C/releases)**

# SSDTs
