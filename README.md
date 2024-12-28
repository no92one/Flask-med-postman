# Flask-app med postman-collection  
  
## Vad man behöver  
  
- Python installerat på sin dator.  
- En SQL-databas som man kan koppla upp sig till.  
  
## Setup Guide  
  
### 1. Skapa en virtuel miljö 
Börja med att skapa en virtuel miljö (t.ex. venv). Öppna terminalen i rooten av projektet och skriv in:

```bash
python -m venv venv
```

Vänta på att **venv**-mappen skapats. Skriv sedan in 1 av dessa kommando baserat på vilken terminalen du sitter i:

```bash
source venv/Scripts/activate # Gitbash eller Linux-terminal

venv\Scripts\activate # Command Prompt (cmd)

.\venv\Scripts\Activate.ps1 # Powershell
```

Verifiera att miljön är aktiv genom att kontrollera att `(venv)` visas i terminalen. 


### 2. Installera externa bibliotek
Nu ska vi installera alla externa bibliotek som vi kommer använda i projektet, öppna terminalen och skriv:

```bash
pip install -r requirements.txt
```

Då installeras alla externa bibliotek som Flask, Sqlalchemy, requests mm.


### 3. Skapa databasen
Skapa en SQL-databas med en **users**-tabell med denna strukturen:

| Keys | Column name | Datatype | Other                           |
| ---- | ----------- | -------- | ------------------------------- |
| PK   | id          | Integer  | Auto increment och **Not Null** |
|      | name        | varchar  |                                 |
| UK   | email       | varchar  | **Not Null**                    |

### 4. Konfigurera databas uppkopplingen
I **main.py** finns:

```python
url = URL.create(  
    drivername="postgresql+psycopg2",  
    port="5544",  
    username="postgres",  
    password="abc123",  
    host="localhost",  
    database="dm23"  
)
```

Ändra konfigurationen så den passar till din SQL-databas. [Tryck här för att se hur man konfigurerar för olika SQL-dialekter.](https://docs.sqlalchemy.org/en/20/core/engines.html#backend-specific-urls)

(OBS! Kan va att man behöver installera en ny driver via pip, detta projektet har redan installerat **psycopg2** som används för PostgreSQL-databaser.)

Starta sedan applikationen genom att skriva detta kommando i terminalen:

```bash
flask --app main run --debug
```

### 5. Sätt upp postman
I projektet finns en **postman**-mapp, i den hittar vi 2 st JSON-filer:

- **flask_db_test.postman_collection.json** - Collection med alla request
- **flask_db_test.postman_environment.json** - Envierments för vår collection.

Öppna postman och importera respektive fil för collections och environment. [Läs hur man gör här.](https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-data/)

Gå sedan till **flask_db_test**-collection och välja **flask_db_test**-environment som vårt environment. [Läs hur man gör här.](https://learning.postman.com/docs/sending-requests/variables/managing-environments/#create-an-environment)


### 6. Kör postman collection

1. Höger klicka på **flask_db_test**-collection och välj **Run collection**. 
2. Kontrollera att alla request är valda och tryck sedan på knappen "**Run flask_db_test**".
3. Vänta på att postman kör alla request, kontrollera sedan att det blev **PASS** på alla utom 
