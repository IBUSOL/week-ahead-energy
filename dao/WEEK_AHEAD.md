# Week Ahead Energy

Fork van [Day Ahead Optimizer](https://github.com/corneel27/day-ahead) (testversie 2026.10.0.rc2),
met als doel een energieplanner die ~7 dagen vooruit kijkt op basis van het eigen gedrag van het huishouden.

## Stand: fase A (fundament)

- Eigen add-on: slug `week_ahead_energy`, naam "Week Ahead Energy (experimenteel)".
- Draait naast DAO zonder conflicten:
  - eigen configmap (`/addon_configs/<repo>_week_ahead_energy`), dus eigen `options.json`, logs en SQLite-database;
  - geen poort op de host (alleen via de zijbalk/ingress), dus geen botsing met poort 5000 van DAO;
  - **meekijkmodus** (optie `meekijken`, standaard aan): de planning wordt berekend maar er wordt niets
    naar Home Assistant geschreven of aangestuurd.
- De add-on wordt op Home Assistant zelf gebouwd vanuit de broncode (geen kant-en-klare image).
- De DAO-testversie (`release-testing`) is uit deze repository gehaald, zodat er geen tweede DAO-add-on verschijnt.

## Versies

### 2026.10.0-wae.2
- Kant-en-klare image via GitHub (`ghcr.io/ibusol/week-ahead-energy`): Home Assistant hoeft niet meer zelf te bouwen.
- Machines: het start- en eindvenster mag nu ook een **datum + tijd** zijn (`input_datetime` met datum, of een
  `datetime`-entity). Daarmee kun je een machine dagen vooruit inplannen. Alleen een tijd werkt zoals in DAO.

### 2026.10.0-wae.1
- Eigen add-on naast DAO, meekijkmodus.

## Let op bij installatie

- Gebruikt je DAO-config een MariaDB/PostgreSQL-database, geef deze add-on dan een **eigen database**
  (andere databasenaam), anders schrijven beide in dezelfde tabellen.
- Gebruik in de config van deze add-on geen HA-entities die DAO aanstuurt zolang meekijken uit staat.

## Volgende fasen

Zie het plan: voorspeller per verbruiker, startdata bij installatie, laadpatroon auto, boiler-onttrekking,
horizon 7 dagen, weekstart-review.
