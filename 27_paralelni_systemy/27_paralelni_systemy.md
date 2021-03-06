# 27\. - Paralelní systémy

> Paralelní systémy, kategorie, paralelizace zpracování, víceprocesorové systémy, programování v paralelních a distribuovaných systémech – přístupy, prostředky, metody vzájemné synchronizace.

## Základní pojmy

**Paralelismus** - Vytváření souběžnosti, zdánlivý nebo skutečný paralelní běh více procesů zároveň.

- **Skutečný** (_paralelismus_) - Každý proces má svůj vlastní procesor, v praxi téměř nemožné.
- **Zdánlivý** (_pseudoparalelismus_) - Několik procesů se navzájem dělí o časové kvantum na jednom CPU, takto funguje drtivá většina moderních systémů.

**Multitasking** - Schopnost operačního systému provádět (přinejmenším zdánlivě) několik procesů současně.

**Program** - Realizace algoritmu v programovacím jazyce, pro interpretované jazyky je vyskytuje ve formě spustitelného skryptu a pro kompilované jazyky jako spustitelný binární soubor.

**Proces** - Spuštěný program, který OS zavedl do operační paměti a přidělil mu určitá práva a vyhrazenou pamět.

**Vlákno** - Při vytvoření nového procesu je automaticky vždy vytvořeno primární vlákno. Vlákno je objektem OS, ve kterém běží samotný programový kód. Všechny vlákna v rámci procesu sdílí tentýž virtuální adresní prostor.

> V rámci jednoho **procesu** může běžet několik **vláken**, ty mají sdílenou pamět a při jejich střídání nemusí docházet ke změně kontextu. Díky tomu je mezi vláknová komunikace jednoduší a střídání vláken je rychlejší. Použití oddělených procesu se používá například z bezpečnostních důvodů k omezení přístupu do sdílené paměti.

## Vlákna

### Podpora v OS

Vlákna můžeme dělit z hlediska správy v OS:

- **Vlákna na uživatelské úrovni** (_ULT_)

  - správu vláken provádí vláknová knihovna (vytváří a ruší vlákna, plánuje běh vlákna, předává data a zprávy mezi vlákny, uchovává a obnovuje kontext vláken)
  - není potřeba OS
  - přepínání mezi vlákny je nezávislé na OS
  - vytvoření nepotřebuje náročné systémové volání
  - nemohou běžet paralelně
  - priority vláken se uplatňují jen v rámci času procesu

- **Vlákna na úrovni jádra** (_KLT_)

  - správa vláken provádí OS
  - každé vlákno v uživatelském prostoru je zobrazeno na vlákno v jádře.
  - Samotné jádro vytváří, ruší a plánuje vlákna.
  - vlákna mohou běžet paralelně
  - volání systému neblokuje ostatní vlákna téhož procesu
  - jeden proces může využít více procesorů
  - tvorba, rušení a přepínání mezi vlákny je levnější než mezi procesy
  - vytvoření vlákna je časově náročnější

- **Kombinace** (_ULT_ a _KLT_)

### Modely vícevláknových aplikací

Modely řešící způsob jak vytvářit a rozdělit práci mezi vlákny

- **Boss/Worker**

  - hlavní vlákno řídí rozdělení úlohy jiným vláknům
  - hlavní vlákno je zodpovědné za vyřizování požadavků
  - pracuje v cyklu: přijde požadavek - vytvoří se vlákno pro řešení příslušného úkolu - čeká se, až se požadavek vrátí
  - jednotlivé Workers nemusí vědět o vstupu, ale musí o něm vědět Boss, který pak rozděluje úlohy

![Boss/Worker](27_boss_worker.png)

- **Peer**

  - vlákna běží paralelně bez specifického vedoucího
  - neobsahuje hlavní vlákno
  - všechny vlákna jsou si rovny
  - vlákno je zodpovědné za svůj vstup a výstup
  - všechny 3 Workery si sahají na vstup pro data

![Peer](27_peer.png)

- **Pipeline**

  - zpracování dat sekvencí operací.
  - dlouhý vstupní proud dat
  - sekvence operací, každá vstupní jednotka musí projít všemi částmi zpracování
  - jednotky jsou nezávislé
  - o vstupu ví jen první, udělí se část dat a předá dál

![Pipeline](27_pipeline.png)

- **Producent a konzument**

  - předávání dat mezi vlákny je realizováno vyrovnávací pamětí (buffer)
  - _producent_ - vlákno, které předává data jinému vláknu
  - _konzument_ - vlákno, které přijímá data od jiného vlákna
  - přístup do vyrovnávací paměti musí být synchronizovaný (exkluzivní přístup)

![Producent/Consument](27_pro_con.png)

## Paralelní systémy

Jako paralelní označujeme systém, v němž může probíhat několik procesů současně (paralelně).

- snaha zvyšovat výkonnost nad hranici danou technologií výroby součástek (mikroprocesorů)
- rozměry, cena a energetická náročnost elektronických prvků klesá rychleji než roste jejich rychlost
- výkonnost většinou neroste lineárně s počtem procesorů (má spíše logaritmický průběh) - vlivem komunikace CPU, synchronizace, nedokonalým vytížením, nevhodnými algoritmy apod.
- od jisté hranice je přidávání procesorů nerentabilní viz [okruh 26](https://github.com/tomaskrizek/tul-szz-it-nv/blob/master/26_zakladni_architektury_pocitacu/26_zakladni_architektury_pocitacu.md), Amhdalův zákon.

**Superpočítač** - Jednolitý počítač, kde jsou komponenty úzce propojeny a komunikují po interní sběrnici a sdílejí pamět. Lze si představit jako velkou základní desku s mnoha sloty. Obrovský výpočetní výkon, ale zároveň i velká počáteční investice a složité možnosti rozšiřování.

**Cluster** - Sada nezávislých počítačů propojených rychlou sítí. Obvykle se vyskytují společně v jedné serverovně a mají stejný operační systém s nadstavbu pro společnou komunikaci. Snadné rozšiřování pouhým přidáváním dalších uzlů.

**Grid** - Podobné jako cluster, ale počítače jsou rozmístěny v internetu a nemusí mít stejný operační systém. Propojení je řešeno přes speciálních aplikací (middleware). Po spuštění aplikace se stáhne sada výpočtů, které počítač provádí a výsledek je odesílán zpět. Viz různé vědecké projekty na hromadné zkoumání genomu či vesmíru. Případně může jít o spojení několika clusterů, kvůli snadné správě a sdílení výpočetního výkonu.

### Architektura

Rozlišujeme 2 druhy architektur:

1. **Paralelní počítače (multiprocesory) se sdílenou pamětí** (superpočítač)

  - Procesory mohou sdílet paměť (RAM) jednoho počítače
  - U symetrických multiprocesorů může běžet kterýkoliv proces na kterémkoliv procesoru, procesory jsou univerzální
  - U asymetrických multiprocesorů je každý procesor specializován na určitý úkol
  - procesory se mohou synchronizovat, ale problém exkluzivity přístupu do paměti

2. **Paralelní počítače(multiprocesory) s distribuovanou pamětí** (cluster)

  - je to více strojů spojených dohromady pomocí komunikační sítě
  - Procesory spolu komunikují zasíláním zpráv
  - masivně paralelní počítače a clustery
  - není problém s exkluzivitou přístupu, ale komunikační problém

### Flynova klasifikace

Podle toku instrukcí:

- **SI** (_Single Instruction Stream_) s jedním tokem instrukcí
- **MI** (_Multilple Instruction Stream_) s vícenásobným tokem instrukcí

Podle toku dat:

- **SD** (_Single Data Stream_) s jedním tokem dat
- **MD** (_Multilple Data Stream_) s vícenásobným tokem dat

Kategorie:

- **SISD** - Počítač zpracovává data sériově podle jednoho programu (Von Neuman)
- **SIMD** - Počítač používající větší množství stejných procesorů řízených společným programem (vektorové počítače). Procesory provádějí stejnou instrukci, ale s jinými daty.
- **MISD** - Není běžné, vznikla uměle. Série procesorů, které postupně zpracovávají společná data.
- **MIMD** - Multiprocesorový systém, každý procesor je řízen samostatným programem pracujícím na samostatných datech.

## Paralelizace

### Druhy paralelismu

- **Funkční paralelismus**

  - Složitá činnost (popsaná nějakou funkcí) se rozdělí na více jednodušších, dílčích činností.
  - Každou z těchto dílčích činností vykonává jedno vlákno (proces).
  - Pro složité úlohy nad jednoduchými daty.
  - Analogie se životem: při stavbě rodinného domku se zároveň zavádí elektřina i plyn.
  - Má smysl i na jednoprocesorových počítačích.

- **Datový paralelismus**

  - Používá se v případě relativně jednoduché činnosti nad rozsáhlými daty.
  - Data se rozdělí „na kousky" a nad každým kouskem dat provede jedno vlákno tutéž činnost.
  - Analogie se životem: dlouhý výkop hloubí parta kopáčů, každý je zodpovědný za jeden úsek výkopu.
  - Prakticky nemá smysl provozovat na jednoprocesorovém stroji.

- **Zřetězené zpracování dat**

  - Vlákna (procesy) si „předávají" nějaký datový záznam.
  - Každé s ním udělá nějaký „kus práce" a předá jej dál.
  - V tom okamžiku je již připraveno opět přijmout další záznam.

## Programovací prostředky pro paralelizaci

- **Jazyk s explicitní podporou paralelismu** (paralelismus je přímou součástí jazyka)

  - Podpora paralelismu na úrovních příkazů, procedur a procesů.
  - Typickým představitelem je ADA a High Performance Fortran.

- **Použití speciálních paralelizačních kompilátorů**

  - Možnost použití univerzálního jazyka (např. C nebo Fortran).
  - Kompilátor automaticky detekuje možnou souběžnost kódu v sekvenčním algoritmu.
  - Umožňuje „bezpracný" převod na paralelní zpracování - řešení není vždy přímočaré.

- **Použití speciálních paralelizačních knihoven**

  - Možnost použití univerzálního jazyka a běžného kompilátoru (výhoda).
  - Paralelizace je realizována pomocí speciálních knihoven externích funkcí a objektů.
  - Nejčastěji jsou používány knihovny PVM (Parallel Virtual Machine) či MPI (Message Passing Interface).
  - Typickými jazyky jsou C, C++, Fortran, Java (balíčky JPVM a mpiJava).
  
### PVM (Parallel Virtual Machine)
- distribuovaná pamět
- heterogenní clustery (můžou být obyčejné počítače připojeny na obyčejnou síť)
- funguje na principu předávání zpráv
- na každém počítači musí běžet démon
- pro komunikaci s uzly slouží knihovna PVM poskytující rozhraní pro paralelní operace (jazyk C, C++, Fortran)

### MPI (Message Passing Interface)
- distribuovaná pamět
- homogenní clustery
- MPI aplikace můž být spuštěna ve dvou módech:
    - **Multicore mode** - mod použitý na vícejádrových počítačích
    - **Cluster mode** - mod určený pro clustery homogenních počítačů
- procesy se shlukují do do skupin (tzv. komunikátorů)
- pro komunikaci jsou k dispozici 2 mechanismy:
    - Message passing
    - Remote memory access
- Typpy komunikace:
    - point to point
        - blokující (sychronní)
        - neblokující (asynchronní)
    - kolektivní komunikace (cílem je více procesů)
        - Synchronizace (každý komunikátor realizuje tzv. bariéru, na které je možné všechny procesy synchronizovat)
        - Přesuny dat (rozselání dat všem procesům)
        - Redukční operace (Redukce dat všech procesů na jednu hodnotu - MAX, MIN, SUM, AVG atd.)
