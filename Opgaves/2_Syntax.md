# 2 PowerShell syntax
## 2.1 Cmdlets
Het voornaamste type commando's binnen PowerShell zijn de zogenaamde **cmdlets** (uitgesproken als command-lets).  
Ze bestaan uit een **werkwoord** gevolgd door een **koppelteken** en een **enkelvoudig zelfstandig naamwoord**.  
<ins>Vb</ins>:

|werkwoord|-|zelfstandig naamwoord (enk.)|
|---|---|---|
|Write|-|Host|
|Get|-|Command|
|New|-|ADUser|
|Set|-|Location|

Powershell heeft een beperkt aantal goedgekeurde werkwoorden die kunnen gebruikt worden in cmdlets.

<INS>*Oefening 1*</INS>:  
Bekijk de lijst van goedgekeurde werkwoorden door het volgende commando uit te voeren in de console:
```powershell
Get-Verb
```

Er bestaat geen lijst van goedgekeurde zelfstandige naamwoorden, enkel een paar vuistregels die best worden gerespecteerd:
1. Het zelfstandig naamwoord is altijd enkelvoud. Het is dus `Get-Verb` en niet `Get-Verbs`
2. Bij alle cmdlets van een bepaald softwarepakket zal het zelfstandig naamwoord beginnen met hetzelfde kort voorvoegsel.  
Zo zal je bij alle cmdlets die betrekking hebben tot Active Directory zien dat het zelfstandig naamwoord begint met de letters `AD`.  
<Ins>Vb</Ins>:  
```powershell
Set-ADDomain
Get-ADUser
Rename-ADObject
```

## 2.2 Parameters
Na het eigenlijke commando kan je ook nog extra info meegeven in de vorm van 1 of meerdere parameters (die al dan niet een bepaalde waarde meekrijgen). Een parameter wordt altijd voorafgegaan door een koppelteken `-`

<Ins>Vb</Ins>: 
```powershell
Get-ChildItem -Path C:\Windows\System32 -Filter *.exe -Recurse
```
In bovenstaand voorbeeld geven we 3 parameters mee met de cmdlet Get-ChildItem:
* de parameter `Path` met waarde `C:\Windows\System32`
* de parameter `Filter` met waarde `*.exe`
* de parameter `Recurse` zonder waarde 







