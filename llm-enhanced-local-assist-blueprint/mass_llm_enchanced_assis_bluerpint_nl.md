![Image](https://github.com/music-assistant/voice-support/blob/main/assets/music-assistant.png?raw=true)

# Media afspelen via Music Assistant met hulp van een LLM

[![Open je Home Assistant en laat het blueprint importeer venster zien met deze specifieke blueprint al ingevuld.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmusic-assistant%2Fvoice-support%2Fblob%2Fmain%2Fllm-enhanced-local-assist-blueprint%2Fmass_llm_enhanced_assist_blueprint_en.yaml)

### Configuratie

1. Er moet een LLM integratie geïnstalleerd zijn. Dit kan een reeds geïnstalleerde LLM integratie zijn. Deze automatisering is bedoeld om gebruikt te worden met een LLM Conversation agent die geen toegang heeft om het huis te bedienen. Gebruik met een LLM welke wel het huis kan bedienen kan voor fouten zorgen, bijvoorbeeld dat er mediaspelers gekozen worden die geen Music Assistant speler zijn. Indien je LLM toegang heeft tot het huis, is [optie 3](../README.md#option-3-script-which-can-be-used-as-a-tool-by-an-llm-integration-like-open-ai-conversation-chatgpt-or-google-generative-ai-gemini) de aanbevolen optie.
2. Importeer de blueprint met de knop hierboven.
3. Maak een automation met de blueprint. Kies de LLM integratie van stap 1. Optioneel kun je nog verdere instellingen voor het afspelen via Music Assistant instellen.
4. Wijzig de trigger en response instellingen zodat deze vertaald zijn. De vertalingen vind je hieronder.
5. Wijzig optioneel nog de instellingen voor het prompt, en of the automatisering je area- en mediaspelernamen mag delen met de LLM.
6. Sla de automatisering op en geef deze een naam.

#### Vertalingen
|Naam van veld|Suggestie voor vertaling|
|---|---|
|Conversation trigger sentences|`(speel\|luister naar) {query}`|
|Combine word|`en`|
|No target response|`Er kon niet bepaald worden waar de media afgespeeld moet worden en er is geen standaard mediaspeler ingesteld`|
|Area response|`<media_info> wordt gespeeld in <area_info>`|
|Player response|`<media_info> wordt gespeeld op <player_info>`|
|Area and Player response|`<media_info> wordt gespeeld in <area_info> en op <player_info>`|

### Blueprint instellingen

#### Verplicht

* Selecteer een LLM Conversation agent welke door de automatisering gebruikt moet worden. De blueprint is bedoeld om gebruikt te worden met een converation agent die geen toegang tot het huis heeft.

#### Optional

* Stel een `Default Player` die gebruikt wordt als er geen area meegegeven wordt, en de area van de voice satellite ook niet gebruikt kan worden.
* Verander de instelling voor `Radio Mode`. Standaard wordt de `Don't stop the music` instelling van de Music Assistant mediaspeler gebruikt.
* Kopieer de vertaling voor de trigger en responses naar de betreffende velden en voeg eventueel nog extra trigger-zinnen toe.
* Wijzig de instelling om de area- en mediaspeler namen mee te sturen naar de LLM. Standaard staat deze instelling aan. Indien je dit uit zet, werkt het vermomen van een area of mediaspeler in een commando alleen als deze exact overeenkomt met de naam in Home Assistant (niet hoofdlettergevoelig). Voorbeel: als in Home Assistant de areanaam _Slaapkamer Sophia_ is, werkt het niet als je _Sophia's slaapkamer_ gebruikt, of als the Speech to Text integratie _Sofia_ gebruikt in plaats van _Sophia_. Helaas kunnen aliases niet gebruikt worden in een automation, dus er kan alleen met de namen vergeleken worden.
* Verander het prompt wat gebruikt wordt voor de LLM conversation agent. Je hoeft dit niet te vertalen. Dit kan nodig zijn voor kleinere modellen, om op sommige punten meer duiding te geven.

### Gebruik

Elke zin moet:

* beginnen met de woorden `Speel` of `Luister naar` gevolgd door een beschrijving van de media die je wil afspelen

* optioneel gevolgd door een area of Music Assistant mediaspeler waarop je de media wil afspelen

### Hoe het doel voor de media bepaald wordt

1. Indien er één of meerdere areas en/of één of meerdere mediaspelers vermeld wordenin het commando, en deze aan een area en/of speler voor Music Assistant gekoppeld kunenn worden, worden deze gebruikt. Als je de namen niet naar de LLM stuurt, en een area of speler vermeld die niet exact overeen komt, wordt de `No target response` reactie gegeven.
2. Als er geen area of speler in het commando vermeld wordt, maar er wel een area bepaald kan worden op basis van het apparaat waarvan het commando gestuurd wordt, wordt deze area gebruikt indien er ook een Musuc Assistant mediaspeler in die area is.
3. Indien er geen area of mediaspeler vernoemd wordt, en deze ook niet bepaald kan worden op basis van het apparaat waarvan het commando komt, wordt de media gespeeld op de `Default Player`. Indien die niet ingesteld is, wordt de `No target response` reactie gegeven.

#### Voorbeelden

```
Speel de beste Pink Floyd nummers in de keuken
Luister naar Jagged Little Pill in de woonkamer
Luister naar het album Greatest Hits door James Taylor in de keuken
Speel het nummer New Years Day in de slaapkamer
Speel A Hard Days Night door Billy Joel in de slaapkamer
Luister naar de playlist Classic Rock in het kantoor
Luister naar BBC Radio 1 in de slaapkamer
Speel het album Classical Nights op de Slaapkamer Sonos Speaker
Luister naar de plaat Classical op de Slaapkamer Sonos Speaker
Speel liedjes van U2
Speel muziek van de componist van Oppenheimer
Speel dat album met op de voorkant de naakte baby die naar een bankbiljet zwemt
```
'
