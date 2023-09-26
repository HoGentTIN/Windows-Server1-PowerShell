# 3 Help gebruiken

## 3.1 Downloaden en installeren van de help files
Sinds versie 3 van PowerShell voegt Microsoft de help files niet meer toe aan PowerShell zelf. Wil je de uitgebreide help-files van de PowerShell cmdlets raadplegen, moet je die eerst downloaden en installeren op jouw computer.

<INS>*Oefening 1*</INS>:  
Download en installeer de `Powershell help files` door volgend commando uit te voeren in de console:
```powershell
Update-Help
```

**Let op!:**  
Het `Update-Help` commando werkt enkel als het uitvoert als administrator!

## 3.2 De help-commando's

De officiële PowerShell cmdlet om een helpfile op te vragen is:  
`"Get-Help"`  
Je kan echter ook gewoon `"help"` of, zoals bij Linux systemen, `"man"` gebruiken. 

<INS>*Oefening 2*</INS>:  
Test de verschillende bovenstaande help-commando's uit door de help files van de `Get-Help`-cmdlet op te zoeken.  
1. Wat is het verschil in output tussen de verschillende commando's?  
2. Wat is de functie van de `spatie` en de `Enter`-toets bij de output van het `help`- of `man`-commando?

## 3.3 Gebruiken van help-files

### 3.3.1 Opzoeken van een commando

Om op een goede manier help-files op te kunnen zoeken is het handig om te weten dat volgende zogenaamde `wildcards` bestaan:

|Symbool|betekenis|
|---|---|
|*|stelt 0 of meer willekeurige karakters voor|
|?|stelt exact 1 willekeurig karakter voor|
|[w-z]|stelt een karakter voor uit de reeks (hier dus w, x, y of z)|
|[axz]|stelt 1 van de opgegeven karakters voor (hier dus a, x of z)|

<INS>Voorbeelden</INS>:
- **`a*`**  zal matchen met `a`, `aa`, `ab` of `appel` maar niet met `banaan`, want de a moet vooraan het woord staan
- **`?n`** zal matchen met `an`, `in` of `on` maar niet met `ran`, want het vraagteken vervangt slechts 1 karakter
- **`[b-d]ook`** zal matchen met `book`, `cook` en `dook`
- **`[bc]ook`** zal enkel matchen met `book` en `cook`
- **`*.txt`** staat voor alle bestanden met extensie `.txt`
- **`file*.txt`** omvat alle bestanden die beginnen met `file` en als extensie `.txt` hebben.
- **`Get-Serv*`** staat voor alle PowerShell commando’s die beginnen met `Get-Serv` (zoals `Get-Services`, `Get-ServerClusterName`, ...)
- **`file?.txt`**: `file1.txt` zal behoren tot de resultaten, maar niet `file12.txt`

Deze wildcards kan je gebruiken om help-files van een bepaald commando op te zoeken zonder dat je het exacte commando kent, maar enkel een idee hebt van wat het zou moeten doen.

Stel dat je bijvoorbeeld het commando zoekt om een bepaalde Windows-service te stoppen.  
Je zou vermoeden dat het commando dat je zoekt, het woord `service` zal bevatten. Om dit te onderzoeken kan je dan volgend commando uitvoeren:

```powershell
get-help *service*
```
Dit commando zal info oplijsten van alle commando's waarin `service` voorkomt. 

<INS>*Oefening 3*</INS>:  
    
1. Zoek met welk commando je een windows service kan stoppen
2. Zoek met welk commando je de naam van je computer kan veranderen
3. Zoek met welk commando je het ip-adres van je NIC kan instellen

   
Een alternatief om commando's op te zoeken is de cmdlet `Get-Command`. Hiermee zoek je daadwerkelijk op commando's en niet enkel op help files. (Waardoor sommige commando's die nog geen help file hebben, toch worden gevonden.)

<INS>*Oefening 4*</INS>:  
Vergelijk de output van `Get-Command *service*` met die van `Get-Help *service*`

### 3.3.2 Parameters van de Get-Help Cmdlet

Eens je het gewenste commando hebt gevonden kan je de help file van de cmdlet opvragen. 

Vraag nog eens de help file op van de `Get-Help` cmdlet met:

```powershell
help Get-Help #of
Get-Help Get-Help #of
man Get-Help
``` 

Wat je zeker moet kunnen interpreteren is de `SYNTAX` van het commando:  
>Welke parameters **kan** je meegeven met het commando en welke parameters **moet** je meegeven. 

Je merkt meteen dat er voor eenzelfde commando verschillende parametersets bestaan. Je kan een cmdlet met andere woorden op verschillende manieren oproepen.

Je ziet ook heel wat symbolen, die in onderstaande tabel worden uitgelegd:

|Symbool|Betekenis|
|---|---|
|`[]`| Als iets tussen vierkante haken staat is het optioneel|
|`<>`|Het type van de waarde die meegegeven kan worden aan een parameter|
|`{}`|Als er bij een parameter een reeks waardes tussen accolades staan (gescheiden van elkaar door `\|`) wil dit zeggen dat enkel deze waardes aanvaard zullen worden|

<INS>*Oefening 5*</INS>:  
Bekijk de help files van het Get-help commando en beantwoord volgende vragen:
1. Hoeveel verschillende parametersets zijn er?
2. Waar zit het verschil tussen deze parametersets
3. Kan je het `Get-Help` commando gebruiken zonder parameters? Zo ja, welke parameterset komt hier mee overeen?


<INS>*Oefening 6*</INS>:  
Welke parameter moet je toevoegen aan de `Get-Help`-cmdlet om:
1. enkel wat voorbeelden te tonen van hoe je de Get-Help cmdlet moet gebruiken, zonder info over de syntax enzo.
2. de volledige, gedetailleerde helpfile te tonen

<INS>*Oefening 7*</INS>:
Vraag enkel de help op van de parameter `category` die je kan meegeven met de `Get-Help`-cmdlet. Bekijk grondig welke info je terugkrijgt


>**Tip!:**
Voeg eens de parameter `-showwindow` toe aan `Get-Help`. Dit zorgt ervoor dat de help file in een apart window getoond wordt waardoor je prompt vrij blijft en je de help file makkelijk kunt doorzoeken.

### 3.3.3 Positionele parameters

De eerste parameter die je kunt toevoegen aan `Get-Help`, namelijk de parameter `-Name`, ofwel de naam van het commando waarvan je de help files opvraagt, ziet er een beetje speciaal uit, en dat is het ook:

```Powershell
Get-Help [[-Name] <System.String>]...
```

Je merkt dat de gehele parameter optioneel is, want hij staat volledig tussen vierkante haken.
Echter... áls je hem gebruikt zie je dat de naam van de parameter (``-Name``) tussen haken staat, en dus optioneel is, maar niet het type dat mee wordt gegeven aan die parameter (`<System.String>`). 
Als je dit ziet betekent dit dat het een positionele parameter is. Je mag dan de naam van de parameter weglaten op voorwaarde dat je de parameter op dezelfde plaats plaatst als in de syntax.

Vb:

Volgende commando's kunnen gebruikt worden om de volledige help files van de Get-Service cmdlet op te vragen:

```powershell
# Dit is de syntax die het best leesbaar is. Alle parameters worden volledig uitgeschreven:

Get-Help -Name Get-Service -full 

# De plaats van de parameters speelt ook geen rol zolang je elke parameter benoemt. Dit kan dus ook:

Get-Help -full -Name Get-Service 

# De naam van de positionele parameter "-Name" is weggelaten, wat perfect kan, want hij is optioneel:

Get-Help Get-Service -full 
```
Dit mag echter niet!:

```powershell
# Als je de naam van de positionele parameter weglaat, moet je die parameter altijd op dezelfde plaats zetten zoals aangegeven in de syntax (wat dus in dit geval betekent: op de eerste plaats):

# NIET OK!!!!!
Get-Help -full Get-Service
# NIET OK!!!!!

# Bemerk wel dat PS hier in dit geval geen probleem van maakt, maar de leesbaarheid lijdt er onder. 
```

<INS>*Oefening 8*</INS>:

1. Welke cmdlet lijst alle items op die zich op een bepaalde locatie, of in een bepaalde container, bevinden?  
(tip: een alias voor dit commando is `dir`)
2. Hoeveel positionele parameters heeft elke parameterset van deze cmdlet?
3. Maak gebruik van deze positionele parameters om alle **tekstfiles** uit de directory `My Documents` of `Mijn documenten` te tonen op het scherm.

### 3.3.3 Switch-parameters

Parameters die geen waarde moeten meekrijgen heten switch-parameters, omdat ze werken als een schakelaar. Aan of af.

<INS>*Oefening 9*</INS>:

* Hoeveel switch-parameters heeft de 'get-childitem' cmdlet?
* Welke switch-parameter kan ervoor zorgen dat de cmdlet niet enkel de inhoud van 1 enkele container toont, maar ook van alle containers in die container?

### 3.3.4 Algemene parameters

Bij de syntax van elke cmdlet zal je op het einde van elke parameterset `[<CommonParameters>]` zien staan. Parameters die ingebakken zitten in PowerShell en die je dus altijd, bij elke cmdlet kan gebruiken.

<INS>*Oefening 10*</INS>:

Hoeveel algemene parameters bestaan er?
Gebruik hiervoor het commando

```powershell

help about_common*

```
<INS>*Oefening 11*</INS>:
Voeg een algemene parameter toe aan onderstaand commando zodat er geen foutmelding (rode tekst) op het scherm komt als je het uitvoert. 
```powershell

Stop-Service "test" 
```
