# 4. Objecten
Powershell is een **object-georiënteerde** shell integenstelling tot **tekstgebaseerde** shells zoals `cmd.exe` en `bash`. 
## 4.1 Wat is een object
Een object 
* Een object is van een bepaald type en heeft een **TypeName**
* Een object kan verschillende eigenschappen of **properties** hebben.
* Een object kan verschillende acties hebben die het kan uitvoeren, of die je er kan op uitvoeren. Dit zijn methodes of **methods**.
* Een object kan **events** hebben waarmee ze kunnen signaleren dat er iets gebeurd is. Deze events kunnen dan andere commando´s triggeren.  
(B.v.: Als een auto betrokken is bij een ongeval (= **event**), kan je het commando geven om de hulpdiensten te bellen.



B.v. bij een <ins>auto</ins>:

| Properties | Methods| Events|
| --- | ---- | ----- |
|kleur| draaien | gecrashed|
| merk |wassen| gewassen|
| lengte  | remmen| verkocht|

of toegepast op een <ins>Windows-service</ins> (een Windows-service is een programma dat op de achtergrond draait bij Windows-systemen, zoals een deamon bij Unix-systemen):

| Properties | Methods| Events|
| --- | ---- | ----- |
|Status| Start | Disposed|
| ServiceName|Stop| |
| CanShutDown |Refresh||

## 4.2 Wat is een member van een object

De properties, methods en events van een object worden overkoepelend **members** van dat object genoemd.  
Om de members van een object op te vragen gebruiken we het commando `Get-Member`  

(*Bemerk: In powershell gebruiken we in commando's altijd enkelvoud: **Get-member** en niet **Get-Members***) 
vb: 

```Powershell
Get-Service | Get-Member
```
    Ter info: Het '|'-symbool is het pipeline-symbool en zorgt ervoor dat de output van een commando wordt doorgegeven aan de input van het volgende commando.


Als je dit commando uitvoert is de eerste info die je krijgt de TypeName:

`TypeName: System.ServiceProcess.ServiceController`

Deze TypeName is handig om gedetailleerde info te vinden over het object op het wereldwijde web. Gewoon de typename ingeven in je browser. Onder de TypeName staan alle properties, methods en events van het object opgelijst.

## 4.3 Werken met objecten

### 4.3.1 Sorteren

Het kan handig zijn om de objecten die je als output terugkrijgt van een bepaald commando, te sorteren.
Het sorteren van objecten gebeurt met het commando `Sort-Object`. De object property waarop je wil sorteren geef je mee als extra parameter.

<INS>*Oefening 3.1.0*</INS>:  
Bestudeer de help-info van `Sort-Object`

<INS>*Oefening 3.1.1*</INS>:  
Sorteer alle Windows-services volgens hun status en zorg ervoor dat de services die momenteel actief zijn, eerst worden uitgeschreven.

<INS>*Oefening 3.1.3*</INS>:  
Zoek het commando op dat alle actieve processen op je computer weergeeft.

<INS>*Oefening 3.1.4*</INS>:  
Sorteer de processen volgens de waardes in de kolom `NPM(K)` (Probeer ook eens te vinden wat die NPM betekent.)

### 4.3.2 Selecteren

#### 4.3.2.1 Properties selecteren
Powershell schrijft standaard bepaalde properties van een object uit naar het scherm. Met het commando `Select-Object` kan je zelf een selectie maken uit de object properties die je uitgeschreven wil zien op het scherm.

<INS>*Oefening 3.2.0*</INS>:  
Bestudeer de help-info van `Select-Object`

<INS>*Oefening 3.2.1*</INS>:  
Schrijf alle lokale gebruikers van je computer uit naar het scherm en sorteer ze volgens de property 'Description'

<INS>*Oefening 3.2.2*</INS>:  
Schrijf enkel de namen van alle lokale gebruikers van je computer uit naar het scherm

<INS>*Oefening 3.2.3*</INS>:  
Bekijk eens de 'members' van het object dat je terugkrijgt na een select-object. Wat is er veranderd?

<INS>*Oefening 3.2.4*</INS>: Schrijf enkel de namen van alle lokale gebruikers van je computer uit naar het scherm en sorteer vervolgens zoals in oef 3.2.1 alle gebruikers volgens 'Description'. 

#### 4.3.2.2 Objecten selecteren

Het is ook mogelijk om met de cmdlet `Select-object` een bepaald aantal objecten te selecteren uit een grotere output.

<INS>*Oefening 3.2.5*</INS>:  
Toon de eerste 10 (alfabetisch volgens naam) windows-services op het scherm

### 4.3.3 Filteren

#### 4.3.3.1 Eenvoudige syntax

Soms wil je enkel objecten hebben die voldoen aan bepaalde voorwaarden. Dit kan je doen met de cmdlet `Where-object`. De syntax is als volgt:

```powershell
'Te filteren objecten' | where-object property 'vergelijkingsoperator' waarde
```

Volgende vergelijkingsoperatoren zijn beschikbaar in Powershell:

| Operator | Betekenis |
|-----|-----|
|-eq | gelijk aan|
|-ne | niet gelijk aan|
|-gt| groter dan|
|-lt| kleiner dan|
|-ge|groter of gelijk aan|
|-le| kleiner of gelijk aan|

<INS>*Oefening 3.3.0*</INS>:  
Toon alle Windows-services op het scherm die momenteel actief zijn (en dus niet die met status 'gestopt').

<INS>*Oefening 3.3.1*</INS>:  
Zoek een cmdlet die alle IP-adressen van je computer op het scherm uitschrijft.

<INS>*Oefening 3.3.2*</INS>:  
Schrijf enkel de objecten met IPv6 adressen naar het scherm

<INS>*Oefening 3.3.3*</INS>:  
Schrijf enkel de IPv6 adressen naar het scherm, dus niet de volledige objecten.  

#### 4.3.3.2 Volledige syntax

Voorgaande syntax is enkel te gebruiken bij eenvoudige filtering (filteren op 1 property en 1 waarde). Is er een complexere filtering vereist, dan zullen we moeten gebruik maken van de volledige syntax:

```powershell
'Te filteren objecten' | Where-Object { expressie }
```
Bij het opstellen van de expressie kunnen we gebruik maken van volgende elementen:

* `$_`: Deze placeholder `$_` zal intern telkens vervangen worden door het volgende object dat getoetst wordt aan de expressie.  
* `$_.`: Met het punt achter de placeholder kunnen we een property van een object aanspreken.  
* Vergelijkingsoperatoren zoals in de tabel in [3.3.1](#331-eenvoudige-syntax)
* Logische operatoren:

    | Operator | Betekenis |
    |-----|-----|
    |-and | Geeft True als beide uitdrukkingen True zijn|
    |-or | Geeft True als minstens één van beide uitdrukkingen True is|
    |-not **or** !| Geeft True als uitdrukking False is|
    |-xor| Geeft True als slechts één van beide uitdrukkingen True is (ExclusiveOR) |

Laten we dit even verduidelijken met een voorbeeld:

Stel, we willen alle lopende processen oplijsten waarbij zowel de `PagedMemorySize64` als de `WorkingSet64` groter zijn dan 100 MB. We willen ook enkel deze properties op het scherm tonen. 

<INS>*Oefening 3.3.4*</INS>:  
Zoek uit wat die 2 properties nu precies zijn. Leg uit hoe je tewerk gaat.

Met volgende code kunnen we de processen filteren op de gewenste voorwaarden:
```powershell
Get-Process | Where-Object {($_.PagedMemorySize64 -gt 100mb) -AND ($_.WorkingSet64 -gt 100mb)} | Select-Object PagedMemorySize64, WorkingSet64
```
Met `Get-Process` halen we alle proces-objecten op, die we vervolgens via een pipeline doorgeven aan de filter `Where-Object`.  
In de expressie die tussen `{ }` staat wordt de `$_` nu telkens vervangen door een volgend proces-object. Het punt na de `$_` zorgt ervoor dat we een specifieke property van dat object kunnen aanspreken, die we dan toetsen aan de voorwaarden van de filter.  
Vervolgens wordt met `select-object` gekozen welke properties er uitgeschreven worden naar het scherm.

<INS>*Oefening 3.3.5*</INS>:  
Schrijf alle processen die beginnen met de letter a, die een Handlecount hebben die groter is dan 200 of een WorkingSet64-property kleiner dan 10mb

### 4.3.4 Groeperen

We hebben in een voorgaande oefening de windows-services gefilterd zodat enkel de services die actief waren werden getoond.  
Stel nu dat we willen weten hoeveel services er actief zijn en hoeveel er gestopt zijn. Dit kunnen we eenvoudig door de services op te delen in 2 groepen met behulp van de `Group-Object` cmdlet.  

<INS>*Oefening 3.4.1*</INS>:  
Vraag de manpages op van de `Group-Object` cmdlet

<INS>*Oefening 3.4.2*</INS>:  
Deel de Windows-services op in 2 groepen volgens hun status met de `Group-object` cmdlet.

<INS>*Oefening 3.4.3*</INS>:  
Bekijk TypeName van de objecten die het resultaat zijn van deze `group-object`. Is dit wat je verwachtte?

<INS>*Oefening 3.4.4*</INS>:  
Met het volgend commando lijst je alle files op in je huidige directory:

```powershell
get-childitem -recurse -file
```
Gebruik pipelines om deze files te groeperen volgens hun extentie en sorteer ze zodat de meest voorkomende extentie bovenaan staat.


















