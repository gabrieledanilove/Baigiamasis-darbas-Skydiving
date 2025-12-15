# AFF Skydiving Assistant

Interaktyvus dirbtinio intelekto asistentas apie parašiutizmą ir AFF (Accelerated Freefall) mokymus, veikiantis lietuvių ir anglų kalbomis. [web:654]

## Funkcijos

- Atsako į klausimus apie parašiutizmą ir AFF mokymus (teorija, taisyklės, įranga). [web:657]
- Dirba lietuvių ir anglų kalbomis, atpažįsta kalbą automatiškai.
- Vartotojo sąsaja naršyklėje (tekstiniai pranešimai ir balso įvestis / išvestis).
- Užklausos keliauja per n8n workflow į LLM API (OpenAI/OpenRouter). [web:666]
- Naudojami webhook’ai ir HTTP užklausos tarp frontendo ir n8n. [web:661]

## Technologijos

- Frontend: paprastas HTML / CSS / JavaScript puslapis.
- Backend orkestracija: n8n workflow (webhook, funkcijų, LLM ir kitų įrankių node’ai). [web:666]
- DI modelis: LLM API pasiekiamas per HTTP užklausas.
- (Jei pridėsi) Vektorinė duomenų bazė / RAG žinioms apie parašiutizmą. [web:664]

## Kaip paleisti

1. **Frontend**
   - Atsisiųsk repozitoriją:
     ```
     git clone https://github.com/TAVO_VARDAS/Baigiamasis-darbas-Skydiving.git
     cd Baigiamasis-darbas-Skydiving
     ```
   - Paleisk statinį serverį (pvz. VS Code Live Server arba `python -m http.server 8000`) ir atidaryk `index.html` naršyklėje. [web:655]

2. **n8n workflow**
   - Importuok `aff-assistant-workflow.json` į savo n8n instancą. [web:666]
   - Nustatyk aplinkos kintamuosius / credencials DI API raktui.
   - Įsitikink, kad webhook URL sutampa su tuo, kuris naudojamas `index.html` faile. [web:661]

## Naudojimas

- Atidaryk puslapį naršyklėje, rašyk ar kalbėk klausimus apie parašiutizmą.
- Visi atsakymai yra tik informaciniai; prieš realius šuolius visada vadovaukitės instruktoriaus nurodymais ir oficialiomis taisyklėmis. [web:665]

## Saugumo atsakomybės apribojimas

Skydivingas yra aukštos rizikos veikla, galinti sukelti rimtus sužalojimus ar mirtį. Šis asistentas nepakeičia oficialių mokymų ir instruktoriaus nurodymų. [web:662]
