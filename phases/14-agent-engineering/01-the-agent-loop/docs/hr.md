# Petlja AI agenta

Hrvatska prilagodba lekcije [The Agent Loop](en.md) iz projekta [AI Engineering from Scratch](https://github.com/rohitg00/ai-engineering-from-scratch). Izvorni materijal © 2026 Rohit Ghumare, [MIT licenca](../../../../LICENSE).

**Predznanje:** osnovni Python i poznavanje rada s funkcijama. **Trajanje:** oko 60 minuta. Za uvodnu vježbu dovoljan je Python, bez API ključa.

## Što ćeš naučiti

- Pratiti kako agent odlučuje koji alat pozvati, prima rezultat i nastavlja rad.
- Prepoznati kada agent treba završiti ili stati zbog pogreške.
- Testirati kako petlja reagira na neispravne argumente alata.

## Kako radi petlja

Aplikacija može modelu dati popis alata, primjerice funkcije za pretraživanje kataloga ili čitanje internih pravila dostave. Kada model zatraži poziv alata, aplikacija provjerava argumente i dopuštenja, izvršava funkciju i vraća rezultat modelu. Model na temelju tog rezultata može zatražiti još jedan alat ili dati odgovor korisniku. ReAct je jedan od utjecajnih obrazaca za izmjenu planiranja, akcija i opažanja.

Primjer s izmišljenim podacima:

1. Kupac pita šalje li trgovina proizvod u Mostar.
2. Agent poziva `provjeri_dostavu` za uneseni grad i oznaku proizvoda.
3. Alat vraća da je dostava dostupna i daje referencu na pravilo dostave.
4. Agent odgovara kupcu i navodi izvor. Ako provjera završi pogreškom, agent navodi da dostupnost nije mogao potvrditi.

Petlja u aplikaciji vodi povijest poruka, popis dopuštenih alata i uvjete završetka. Uvjete postavljaš unaprijed, primjerice završni odgovor, najviše tri koraka ili prekid kad nema dopuštenja za traženu radnju. Podatke koje alat vrati tretiraj kao podatke. Tekst u dohvaćenom dokumentu nema ovlasti mijenjati pravila agenta.

## Pokreni primjer

Iz korijena repozitorija pokreni:

```bash
python3 phases/14-agent-engineering/01-the-agent-loop/code/main.py
```

[Izvorni primjer](../code/main.py) demonstrira petlju uz skriptirani model i lokalne alate. U ispisu pronađi poziv alata, rezultat koji se vraća modelu i razlog završetka. Pri radu s pravim modelom za otklanjanje pogrešaka bilježi provjerljive događaje poput naziva pozvanog alata, njegova statusa i razloga završetka.

## Vježba

Promijeni skriptirani model tako da jedanput zatraži alat s neispravnim argumentom. Vrati poruku o pogrešci kao rezultat alata i provjeri može li model u idućem koraku poslati ispravan poziv. Zatim simuliraj trajnu pogrešku i provjeri da petlja staje nakon zadane granice te prijavljuje da zadatak nije izvršen.

**Kriterij prolaza:** ispravan poziv završava rezultatom, neispravan poziv vraća jasnu pogrešku, a ponavljana pogreška završava u zadanom broju koraka.

## Kviz

1. Tko stvarno izvršava alat? **A)** Model **B)** Aplikacija **C)** Korisnik
2. Što sprječava beskonačno ponavljanje poziva? **A)** Dulji prompt **B)** Naziv alata **C)** Ograničenje koraka
3. Što agent smije reći kad alat ne može provjeriti dostavu? **A)** Dostava je potvrđena **B)** Dostava se nije mogla potvrditi **C)** Dostava je zabranjena

<details>
<summary>Rješenja s objašnjenjem</summary>

1. **B.** Model predlaže poziv, a aplikacija provjerava i izvršava dopuštenu funkciju.
2. **C.** Granica koraka daje aplikaciji jasan uvjet za prekid.
3. **B.** Neuspjela provjera ne daje ni potvrdu ni odbijenicu.

</details>
