# Football.TXT Format Spec (& Tests)


## What's News (in 2025)?

###  fbtok & fbtree

Note - you can try the default/standard parser (& tokenizer) for the
Football.TXT (match schedule, results, line-ups & more) 
format as (standalone) command-line tools.

For the tokenizer (lexer) try:

     $ fbtok england/2019-20/1-premierleague.txt

and for the parser - outputing the (abstract) parse tree - try:

     $ fbtree england/2019-20/1-premierleague.txt


Tip - to install the tools use:

     $ gem install fbtok     # (incl. fbtree and others)


###  Request for Comments

You are welcome to comment on the default/standard Football.TXT format.
You can find samples in the /samples directory.



## Intro - Why? Philosophy

Why not use JSON, CSV, XML, YAML, SQL, your ‹format of choice here›?
Why invent yet another data format?

Excercise: Try to write by hand the round-by-round match schedule
for the English Premier League, for example?
Did you enjoy writing the match schedule in JSON? in CSV? in XML? in SQL? in YAML?

Now retry the exercise using the new Football.TXT mini language designed to make hand-crafting
as easy as possible. See the difference?  Example - [`england/2019-20/1-premierleague.txt`](https://github.com/openfootball/england/blob/master/2019-20/1-premierleague.txt) in Football.TXT, [`2019-20/en.1.json`](https://github.com/openfootball/football.json/blob/master/2019-20/en.1.json) in Football.JSON.


Note: If you auto-generate your datasets and want to focus on
easy machine-writing and machine-reading, 
see the [Football.CSV format »](https://footballcsv.github.io/spec/) :-).


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


Group A

(1) Thu Jun 12 17:00   Brazil - Croatia       @ Arena de São Paulo, São Paulo (UTC-3)
(2) Fri Jun 13 13:00   Mexico - Cameroon      @ Estádio das Dunas, Natal (UTC-3)

(17) Tue Jun 17 16:00   Brazil - Mexico        @ Estádio Castelão, Fortaleza (UTC-3)
(18) Wed Jun 18 18:00   Cameroon - Croatia     @ Arena Amazônia, Manaus (UTC-4)

(33) Mon Jun 23 17:00   Cameroon - Brazil      @ Brasília (UTC-3)
(34) Mon Jun 23 17:00   Croatia  - Mexico      @ Recife (UTC-3)


Group B

(3) Fri Jun 13 16:00   Spain - Netherlands     @ Arena Fonte Nova, Salvador (UTC-3)
(4) Fri Jun 13 18:00   Chile - Australia       @ Arena Pantanal, Cuiabá (UTC-4)

(19) Wed Jun 18 16:00   Spain - Chile             @ Estádio do Maracanã, Rio de Janeiro (UTC-3)
(20) Wed Jun 18 13:00   Australia - Netherlands   @ Estádio Beira-Rio, Porto Alegre (UTC-3)

(35) Mon Jun 23 13:00   Australia - Spain         @ Curitiba (UTC-3)
(36) Mon Jun 23 13:00   Netherlands - Chile       @ São Paulo (UTC-3)
...
```



## Definitions


### Text and Two Space Rule

The "atomic" text unit in Football.TXT is NOT the classic word or identifier BUT
a text run.  If you want to break text runs use two (or more) spaces.

     ARG  BOL  BRA   =>   TEXT(ARG), TEXT(BOL), TEXT(BRA)
     ARG BOL BRA     =>   TEXT(ARG BOL BRA)

     Fri  Liverpool  =>   WDAY(Fri), TEXT(Liverpool)     
     Fri Liverpool   =>   TEXT(Fri Liverpool)

     Matchday 1      =>   TEXT(Matchday 1) 
     1860 München    =>   TEXT(1860 München)
     ...
     


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

You can use `#` for comments. Example:

```

```


### Prop(erty) lines

Property lines start with a team name followed by double colon (`:`)
for lineups or known property keywords / names (e.g. Penalties, Goals, Referee, etc.)
followd by double colon (`:`) for all other props.

#### Lineup

Examples:

```
Yugoslavia: Soskic, Durkovic, Jusufi, Zanetic, Zebec, Perusic, Knez,
            Jerkovic, Galic, Sekularac, Kostic
France: Lamia, Wendling, Rodzik, Marcel, Herbin, Ferrier, Heutte, Müller, 
        Wiesnieski, Stievenard, Vincent

Italy:              Gianluigi Donnarumma - Alessandro Florenzi (Giovanni Di Lorenzo),
                    Leonardo Bonucci, Giorgio Chiellini, Leonardo Spinazzola -
                    Nicolò Barella, Jorge Frello Filho, Manuel Locatelli (Bryan Cristante) - 
                    Domenico Berardi (Federico Bernardeschi), Ciro Immobile (Andrea Belotti), 
                    Lorenzo Insigne (Federico Chiesa); Coach: Roberto Mancini
Turkey:             Uğurcan Çakır - Mehmet Zeki Çelik, Merih Demiral, Çağlar Söyüncü,
                    Umut Meraş - Okay Yokuşlu (İrfan Can Kahveci) - 
                    Kenan Karaman (Halil Dervişoğlu), Yusuf Yazıcı (Cengiz Ünder), 
                    Ozan Tufan (Kaan Ayhan), Hakan Çalhanoğlu - Burak Yılmaz;
                    Coach: Şenol Güneş

Switzerland:        Yann Sommer -  Nico Elvedi, Manuel Akanji, 
                    Ricardo Rodríguez (Admir Mehmedi 87') - Silvan Widmer (Kevin Mbabu 73'), 
                    Remo Freuler, Granit Xhaka, Steven Zuber (Christian Fassnacht 79') -
                    Breel Embolo (Ruben Vargas 79'), Xherdan Shaqiri (Mario Gavranović 73'), 
                    Haris Seferović (Fabian Schär 97'); Coach: Vladimir Petković 
France:             Hugo Lloris - Benjamin Pavard, Raphaël Varane, 
                    Clément Lenglet (Kingsley Coman 46' (Marcus Thuram 111')), 
                    Presnel Kimpembe, Adrien Rabiot -
                    Paul Pogba, N'Golo Kanté, Antoine Griezmann (Moussa Sissoko 88') -
                    Karim Benzema (Olivier Giroud 94'), Kylian Mbappé;
                    Coach: Didier Deschamps

Palmeiras: Marcos - Francisco Javier Arce (Evair 57'), Júnior Baiano,
           Roque Júnior, Rogério, César Sampaio, Alex (75' Euller), Zinho,
           Oséas, Paulo Nunes; trainer: Luiz Felipe Scolari
Deportivo Cali: Rafael Dudamel - John Wilmer Pérez (Herman Gaviria 84'), 
                Andrés Mosquera, Mario Yepez, Gerardo Bedoya, Martín Zapata,
                Alexander Viveros, Arley Betancourt, Mayer Candelo (Freddy Hurtado 62'), 
                Geovanny Córdoba (Manuel Valencia 81'), 
                Victor Bonilla; trainer: José Hernández
```



#### Penalties / Penalty Shootout

Examples:

```
Penalties:       1-0  Mario Gavranović, 1-1 Paul Pogba, 2-1  Fabian Schär, 2-2 Olivier Giroud,
                 3-2  Manuel Akanji, 3-3 Marcus Thuram, 4-3 Ruben Vargas,
                  4-4  Presnel Kimpembe, 5-4 Admir Mehmedi,  Kylian Mbappé (save)

Penalty shootout: 0-0 Zinho (held), 0-1 Dudamel; 
                  1-1 Júnior Baiano, 1-2 Gaviria;
                  2-2 Roque Júnior, 2-3 Yepes; 
                  3-3 Rogério, 3-3 Bedoya (post);
                  4-3 Euller, 4-3 Zapata (wide) 
```

#### Goals

Examples:

```
Goals:  Arruabarrena 22' Arruabarrena 61'; Pena 43' Euller 63' 

Goals:  Galic 11' Zanetic 55' Knez 75' Jerkovic 77', 78'; 
          Vincent 12'  Heutte 43', 62' Wiesnieski 52'
```


#### Yellow Card; Red Cards / Sent Off

Examples:

```
Yellow Cards:      Çağlar Söyüncü 88',  Halil Dervişoğlu 90'

Yellow Cards:     Nico Elvedi 32',  Ricardo Rodríguez 62', Granit Xhaka 76',  Manuel Akanji 108';
                  Raphaël Varane 30',  Kingsley Coman 88', Benjamin Pavard 91'

Yellow cards: Sampaio 54', Argel 77';  Barros Schelotto 65',  Bermúdez 76' 

Red cards: Mosquera, Evair

Sent off: Páez
```

#### Referee / Ref

Examples:

```
Referee:            Danny Makkelie (Netherlands)

Referee:            Fernando Rapallini (Argentina)

Referee: Aquino (Paraguay)

ref: Jionni (Italy)   
```


## Language (English, Deutsch, Español, etc.)

The focus for the Football.TXT format v1 is on English.   
More formats with conventions used in German (Deutsch)
or Spanish (Español) are planned for later.


For example -  conventions in German (Deutsch) incl.:

-  Score    - use  `2:1 (0:1)` instead of `2-1 (0-1)`
-  Minutes  - use  `44.` or `(44.)`  instead of `44'`
-  etc.


