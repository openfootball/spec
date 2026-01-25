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
You can find samples for the Football.TXT format, level 1 in the `/samples` directory
and for level 2 in the `/samples-l2` directory.




## Intro - Why? Philosophy

Why not use JSON, CSV, XML, YAML, SQL, your ‹format of choice here›?
Why invent yet another data format?

Excercise: Try to write by hand the round-by-round match schedule (with results)
for the English Premier League, for example?
Do you enjoy writing the match schedule in JSON? in CSV? in XML? in SQL? in YAML?

Now retry the exercise using the new Football.TXT format / data language designed to make hand-crafting
as easy as possible. See the difference?  Example - [`england/2019-20/1-premierleague.txt`](https://github.com/openfootball/england/blob/master/2019-20/1-premierleague.txt) in Football.TXT, [`2019-20/en.1.json`](https://github.com/openfootball/football.json/blob/master/2019-20/en.1.json) in Football.JSON.


Note: If you auto-generate your datasets and want to focus on
easy machine-writing and machine-reading, 
see the [Football.CSV format »](https://footballcsv.github.io/spec/) :-).


The new Football.TXT format / data language for football match schedules (results, line-ups & more) using structured text
offers you the best of both worlds, that is,
1) looks 'n' feels like free-form plain text - easy-to-read and easy-to-write -
2) but offers a 100-% data accuracy guarantee (when loading into SQL tables, for example).

The Football.TXT format / data language also includes
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
# ...

Round of 16            |  Sat Jun 28 - Tue Jul 1
Quarter-finals         |  Fri Jul 4  - Sat Jul 5
Semi-finals            |  Tue Jul 8  - Wed Jul 9
Match for third place  |  Sat Jul 12
Final                  |  Sun Jul 13


▪ Group A

Thu Jun 12 
  17:00   Brazil - Croatia       @ Arena de São Paulo, São Paulo (UTC-3)
Fri Jun 13 
  13:00   Mexico - Cameroon      @ Estádio das Dunas, Natal (UTC-3)

Tue Jun 17 
   16:00   Brazil - Mexico        @ Estádio Castelão, Fortaleza (UTC-3)
Wed Jun 18 
   18:00   Cameroon - Croatia     @ Arena Amazônia, Manaus (UTC-4)

Mon Jun 23 
   17:00   Cameroon - Brazil      @ Brasília (UTC-3)
   17:00   Croatia  - Mexico      @ Recife (UTC-3)


▪ Group B

Fri Jun 13 
   16:00   Spain - Netherlands     @ Arena Fonte Nova, Salvador (UTC-3)
   18:00   Chile - Australia       @ Arena Pantanal, Cuiabá (UTC-4)

Wed Jun 18 
   13:00   Australia - Netherlands   @ Estádio Beira-Rio, Porto Alegre (UTC-3)
   16:00   Spain - Chile             @ Estádio do Maracanã, Rio de Janeiro (UTC-3)

Mon Jun 23 
   13:00   Australia - Spain         @ Curitiba (UTC-3)
   13:00   Netherlands - Chile       @ São Paulo (UTC-3)
...
```



## What's News (in 2026)?

Note - starting in 2026 the Football.TXT format 
is now split-up into levels. 

Level 1 supports and includes match schedules with goal scorer lines
 BUT no team line-ups, sent-offs props and more.

Level 2 supports all of Level 1 plus team line-ups, sent-offs props and more.


## Football.TXT Format Level 1

Sample:

```
▪ Quarter-finals - 1st Leg

Tue Apr/1
  20.45   FC Barcelona        v Atlético Madrid    1-1  @ Camp Nou, Barcelona
            (Neymar 71'; Diego 56')
  20.45   Manchester United   v Bayern München     1-1  @ Old Trafford, Manchester
            (Vidić 58'; Schweinsteiger 67')
Wed Apr/2
  20.45   Real Madrid         v Borussia Dortmund  3-0  @ Santiago Bernabéu, Madrid
            (Bale 3' Isco 27' Ronaldo 57')
  20.45   Paris Saint-Germain v Chelsea FC         3-1  @ Parc des Princes, Paris
            (Lavezzi 4' Luiz 61'og Pastore 90+3'; Hazard 27'pen)
```


### Match Results & Fixtures

For match fixtures (without results) you MUST separate two team names by `-` or `v`. 
Examples:

```
Brazil   - Mexico
Cameroon - Croatia

Cameroon v Brazil 
Croatia  v Mexico
```

For match results (i) you can separate two team names by `-` or `v`  (same as fixtures) followed by the score (e.g. `0-0`) or separate team names by the score.
Examples:

```
Atlético Mineiro v River Plate    3-0
Botafogo         v Peñarol        5-0

Atlético Mineiro - River Plate    3-0
Botafogo         - Peñarol        5-0

River Plate   0-0  Atlético Mineiro
Peñarol       3-1  Botafogo 
```

For the after extra-time (aet) score or penalties formats, see the score format section.



### Aside - Text and Two Space Rule

Note - The "atomic" text unit in Football.TXT is NOT the classic word or identifier BUT
a text run.  If you want to break text runs use two (or more) spaces.

```
ARG  BOL  BRA   =>   [:TEXT,"ARG"], [:TEXT,"BOL"], [:TEXT,"BRA"]
ARG BOL BRA     =>   [:TEXT,"ARG BOL BRA"]

Fri  Liverpool  =>   [:TEXT,"Fri"], [:TEXT,"Liverpool"]     
Fri Liverpool   =>   [:TEXT,"Fri Liverpool"]

Matchday 1      =>   [:TEXT,"Matchday 1"] 
1860 München    =>   [:TEXT,"1860 München"]
...
```     



### Round Lines (Outlines)

Round lines (outlines) MUST start with `▪` (BLACK SMALL SQUARE) or `»` or `>>` e.g.

```
▪ Quarter-finals - 1st Leg
▪ Group A
▪ Match for third place
...
```


#### Tip - How To Add Stages

To add stages in your match schedules and round lines (outlines) use:

```
▪ Matchday 1                  # no stage (assumes regular season)
▪ Matchday 2
...  
▪ Championship, Matchday 1    # Championship stage
▪ Championship, Matchday 2
...
▪ Europe, Matchday 1          # Europe stage
▪ Europe, Matchday 2
...

# -or-

▪ League, Matchday 1         # League stage
▪ League, Matchday 2
...
▪ Playoffs, Matchday 1       # Playoffs stage
▪ Playoffs, Matchday 2
...
▪ Finals, Round of 16        # Finals stage
▪ Finals, Quarterfinals
▪ Finals, Semifinals
▪ Finals, Final

```


## Stadiums & Grounds 

Use `@` to start with adding "geo" names - that is, stadiums & grounds 
and / or cities (plus optional timezone), countries and more.
Examples:

```
  @ Stadio Olimpico, Roma
  @ Arena Naţională, Bucureşti, Romania
  @ Bucuresti, 23 August
  @ Wien, Prater
  @ Buenos Aires
  @ Brasília (UTC-3)
  @ Arena Fonte Nova, Salvador (UTC-3)
  @ Arena Pantanal, Cuiabá (UTC-4)
  @ Estádio do Maracanã, Rio de Janeiro (UTC-3)
  ...
```

Note - Geo names have their own (lexer) mode and, thus, you can (even) use dates
(e.g. `23 August`) or more. 


### Comments & Blank Lines

#### Blank links

Use blank links as you wish to make the text look pretty, that is, easy-to-read and easy-to-write.

#### Single-line comments 

You can use `#` for comments. Example:

```
# Note - Hugo Lloris saved a penalty from Ricardo Rodríguez at 55'.
```



### Date (Header) Line


#### Date Formats



### Score Formats

#### Basic (Final Result Only) Score Format

#### Score Formats for Half-Time, After-Extra-Time, Penalty-Shootout, & More 




### Goal (Scorer) Line

Goal (scorer) lines MUST be enclosed with `()` and, thus, start with `(` e.g.

```
(Neymar 71'; Diego 56')
(Lavezzi 4' Luiz 61'og Pastore 90+3'; Hazard 27'pen)
...
```





---

## Football.TXT Format Level 2  

The Football.TXT Format Level 2 supports all of Level 1
plus adds:

- Definitions
  - Groups 
  - Rounds (& Matchdays)
- Match Properties
  - Team Line-ups (incl. Trainer, Substitutions, etc.)
  - Yellow Cards, Red Cards, Sent-off
  - Penalty Shootouts
  - Referees 
  - (Stadium) Attendence


### Group Definition  

```
<GROUP>   |  <TEAM>  <TEAM> ...
```

Note - `<GROUP>`is a text run (`<TEXT>`) that MUST match the group matching formula that 
incl. Group 1, Group 2, Group A, Group B, Group A1, Group A2, Group B1, Group B2, etc.

Examples:

```
Group A  |  Brazil       Croatia              Mexico         Cameroon
Group B  |  Spain        Netherlands          Chile          Australia
...
```


### Round (& Matchday Definition)  

```
<ROUND>   |  <DATE>            OR
<ROUND>   |  <DATE_PERIOD>
```

Note - `<ROUND>` is a text run (`<TEXT>`) that MUST match the round matching formula that
incl. Matchday 1, Matchday 2, Round 1, Round 2, Final, and many more.

Examples:

```
Matchday 1  |  Thu Jun 12
Matchday 2  |  Fri Jun 13
Matchday 3  |  Sat Jun 14
...

Round of 16            |  Sat Jun 28 - Tue Jul 1
Quarter-finals         |  Fri Jul 4  - Sat Jul 5
Semi-finals            |  Tue Jul 8  - Wed Jul 9
Match for third place  |  Sat Jul 12
Final                  |  Sun Jul 13
```

What's the point?  If a match has no round header (in scope) than tools can use
the round & match definitions to find a match by date lookup. 


### Prop(erty) Lines

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

Note - you can use multiple lines for the lineup; to continue the lineup 
the line MUST end with `,;-`, that is, comma (`,`), semicolon (`;`) or dash (`-`).



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

Note - you can use multiple lines for the penalties; to continue the penalties 
the line MUST end with `,;`, that is, comma (`,`) or semicolon (`;`).



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

### Attendance / Att / Attn

Examples:

```
Attendance:  44000

att:  23_000
```

Note - You CANNOT use commas in number e.g. `45,000` use underscore e.g. `45_000`






---


## Language (English, Deutsch, Español, etc.)

Note - The focus for the Football.TXT format v1 is on English.   
More formats with conventions used in German (Deutsch)
or Spanish (Español) are planned for later.


For example -  conventions in German (Deutsch) incl.:

-  Score    - use  `2:1 (0:1)` instead of `2-1 (0-1)`
-  Minutes  - use  `44.` or `(44.)`  instead of `44'`
-  etc.





## Questions? Comments?

Yes, you can. More than welcome.
See [Help & Support »](https://github.com/openfootball/help)
