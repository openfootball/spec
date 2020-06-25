# Football.TXT Format Spec (& Tests)

## Intro - Why? Philosophy

Why not use JSON, CSV, XML, YAML, SQL, your ‹format of choice here›?
Why invent yet another data format?

Excercise: Try to write by hand the round-by-round match schedule
for the English Premier League, for example?
Did you enjoy writing the match schedule in JSON? in CSV? in XML? in SQL? in YAML?

Now retry the exercise using the new Football.TXT mini language designed to make hand-crafting
as easy as possible. See the difference?  Football.TXT Example - [`england/2019-20/1-premierleague.txt`](https://github.com/openfootball/england/blob/master/2019-20/1-premierleague.txt), Football.JSON Example - [`2019-20/en.1.json`](https://github.com/openfootball/football.json/blob/master/2019-20/en.1.json).


> Note: If you auto-generate your datasets and want to focus on
> easy machine-writing and machine-reading, see the [Football.CSV format »](https://footballcsv.github.io/spec/) :-).


The new Football.TXT mini data language for football match schedules using structured text
offers you the best of both worlds, that is,
1) looks 'n' feels like free-form plain text - easy-to-read and easy-to-write -
2) but offers a 100-% data accuracy guarantee (when loading into SQL tables, for example).

The Football.TXT mini data language also includes
support for groups, matchdays, grounds, and much more. Example:


```
= World Cup 2014

Group A  |  Brazil       Croatia              Mexico         Cameroon
Group B  |  Spain        Netherlands          Chile          Australia
Group C  |  Colombia     Greece               Côte d'Ivoire  Japan
Group D  |  Uruguay      Costa Rica           England        Italy
Group E  |  Switzerland  Ecuador              France         Honduras
Group F  |  Argentina    Bosnia-Herzegovina   Iran           Nigeria
Group G  |  Germany      Portugal             Ghana          United States
Group H  |  Belgium      Algeria              Russia         South Korea


Matchday 1  |  Thu Jun 12
Matchday 2  |  Fri Jun 13
Matchday 3  |  Sat Jun 14
...

Round of 16            |  Sat Jun 28 - Tue Jul 1
Quarter-finals         |  Fri Jul 4  - Sat Jul 5
Semi-finals            |  Tue Jul 8  - Wed Jul 9
Match for third place  |  Sat Jul 12
Final                  |  Sun Jul 13


Group A:

(1) Thu Jun 12 17:00   Brazil - Croatia       @ Arena de São Paulo, São Paulo (UTC-3)
(2) Fri Jun 13 13:00   Mexico - Cameroon      @ Estádio das Dunas, Natal (UTC-3)

(17) Tue Jun 17 16:00   Brazil - Mexico        @ Estádio Castelão, Fortaleza (UTC-3)
(18) Wed Jun 18 18:00   Cameroon - Croatia     @ Arena Amazônia, Manaus (UTC-4)

(33) Mon Jun 23 17:00   Cameroon - Brazil      @ Brasília (UTC-3)
(34) Mon Jun 23 17:00   Croatia  - Mexico      @ Recife (UTC-3)


Group B:

(3) Fri Jun 13 16:00   Spain - Netherlands     @ Arena Fonte Nova, Salvador (UTC-3)
(4) Fri Jun 13 18:00   Chile - Australia       @ Arena Pantanal, Cuiabá (UTC-4)

(19) Wed Jun 18 16:00   Spain - Chile             @ Estádio do Maracanã, Rio de Janeiro (UTC-3)
(20) Wed Jun 18 13:00   Australia - Netherlands   @ Estádio Beira-Rio, Porto Alegre (UTC-3)

(35) Mon Jun 23 13:00   Australia - Spain         @ Curitiba (UTC-3)
(36) Mon Jun 23 13:00   Netherlands - Chile       @ São Paulo (UTC-3)
...
```



## Definitions

### Round & Matchday Definition   (Optional)

### Group Definition  (Optional)



## Headers

### Round & Matchday Header

### Group Header

### Date Header


## Date Formats

## Score Formats


## Goal(s) Line


## Stadiums & Grounds 



## Comments & Blank Lines

### Blank links

Use blank links as you wish to make the text look pretty, that is, easy-to-read and easy-to-write.

### Single-line comments

You can use `\#` for comments or as an alternative `%` or `--` or `;`. Example:

```

```


## Language (English, Deutsch, Espanol, etc.)


...

