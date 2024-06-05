# Python Data Scraper

### Data Scraper Components
The datascarper consists of four seperate python packages.

* Data Classes
    - A collection of related classes
    - Each class provides a `getJsonRepr` method
* Data Scraper
    - Scrapes data direct from formula1.com
    - Creates objects in the Data Classes
* Database Connection
    - Establishes a connection to the MongoDB
    - Preforms the DB update operations
* Tools
    - Supports the other packages
    - Provides a standard logger

### Component Sequence Diagram

```plantuml
@startuml
title Data Scraper Sequence Diagram

actor Main.py

participant "Main.py" as Main
participant "Data Scraper" as Scraper
participant "Data Classes" as Classes
participant "DB Connection" as DB
participant "MongoDB" as MongoDB

Main -> Scraper: Start scraping
Scraper -> Classes: Scrape data\nand create objects
Scraper --> Main: Return parent object
Main -> DB: Insert object into database
DB -> Classes: Call getJsonRepr()
Classes --> DB: Return JSON representation
DB -> MongoDB: Insert JSON into database
DB --> Main: Confirmation
Main --> Main.py: End
@enduml
```

### Main.py Entry point
The datascraper is invoked by calling main.py<br><br>
This script accepts arguments to parse specfic races, specfic seasons (via a Json config) or season profiles.

