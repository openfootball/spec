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
Why invent yet another (structured text) data format?

Excercise: Try to write by hand the round-by-round match schedule (with results)
for the English Premier League?
How do you enjoy writing the match schedule (for 20 teams with 38 rounds with 10 matches each) in JSON? in CSV? in XML? in SQL? in YAML?

Now retry using the new Football.TXT format / (structured text) data language designed to make hand-crafting
as easy as possible. See the difference?
Example - [`england/2025-26/1-premierleague.txt`](https://github.com/openfootball/england/blob/master/2025-26/1-premierleague.txt) in Football.TXT:

```
▪ Matchday 1
  Fri Aug 15 
    20:00  Liverpool FC            v AFC Bournemouth          4-2 (1-0)
  Sat Aug 16
    12:30  Aston Villa FC          v Newcastle United FC      0-0
    15:00  Brighton & Hove Albion FC v Fulham FC              1-1 (0-0)
           Sunderland AFC          v West Ham United FC       3-0 (0-0)
           Tottenham Hotspur FC    v Burnley FC               3-0 (1-0)
    17:30  Wolverhampton Wanderers FC v Manchester City FC    0-4 (0-2)
  Sun Aug 17
    14:00  Nottingham Forest FC    v Brentford FC             3-1 (3-0)
           Chelsea FC              v Crystal Palace FC        0-0
    16:30  Manchester United FC    v Arsenal FC               0-1 (0-1)
  Mon Aug 18
    20:00  Leeds United FC         v Everton FC               1-0 (0-0)

...
```

vs Example - [`2025-26/en.1.json`](https://github.com/openfootball/football.json/blob/master/2025-26/en.1.json) in Football.JSON:

``` json
"matches": [
    { "round": "Matchday 1", "date": "2025-08-15", "time": "20:00",
      "team1": "Liverpool FC", "team2": "AFC Bournemouth", "score": {"ht": [1,0], "ft": [4,2]}
    },
    { "round": "Matchday 1", "date": "2025-08-16", "time": "12:30",
      "team1": "Aston Villa FC", "team2": "Newcastle United FC", "score": {"ft": [0,0]}
    },
    { "round": "Matchday 1", "date": "2025-08-16", "time": "15:00",
      "team1": "Brighton & Hove Albion FC", "team2": "Fulham FC", "score": {"ht": [0,0], "ft": [1,1]}
    },
    { "round": "Matchday 1", "date": "2025-08-16", "time": "15:00",
      "team1": "Sunderland AFC", "team2": "West Ham United FC", "score": {"ht": [0,0], "ft": [3,0]}
    },
    { "round": "Matchday 1", "date": "2025-08-16", "time": "15:00",
      "team1": "Tottenham Hotspur FC", "team2": "Burnley FC", "score": {"ht": [1,0], "ft": [3,0]}
    },
    { "round": "Matchday 1", "date": "2025-08-16", "time": "17:30",
      "team1": "Wolverhampton Wanderers FC", "team2": "Manchester City FC", "score": {"ht": [0,2], "ft": [0,4]}
    },
    { "round": "Matchday 1", "date": "2025-08-17", "time": "14:00",
      "team1": "Nottingham Forest FC", "team2": "Brentford FC", "score": {"ht": [3,0], "ft": [3,1]}
    },
    { "round": "Matchday 1", "date": "2025-08-17", "time": "14:00",
      "team1": "Chelsea FC", "team2": "Crystal Palace FC", "score": {"ft": [0,0]}
    },
    { "round": "Matchday 1", "date": "2025-08-17", "time": "16:30",
      "team1": "Manchester United FC", "team2": "Arsenal FC", "score": {"ht": [0,1], "ft": [0,1]}
    },
    { "round": "Matchday 1", "date": "2025-08-18", "time": "20:00",
      "team1": "Leeds United FC", "team2": "Everton FC", "score": {"ht": [0,0], "ft": [1,0]}
    },  ...
]
```



Note: If you auto-generate your datasets and want to focus on
easy machine-writing and machine-reading, 
see the [Football.CSV format »](https://footballcsv.github.io/spec/) :-).


The new Football.TXT format / data language for football match schedules (results, line-ups & more) using structured text
offers you the best of both worlds, that is,
1) looks 'n' feels like free-form plain text - easy-to-read and easy-to-write -
2) but offers a 100-% data accuracy guarantee (when loading into SQL tables or exporting/converting into JSON, CSV, and friends, for example).

The Football.TXT format / data language also includes
support for groups, matchdays, grounds, and much more. Example:

```
= World Cup 2022

Group A  | Qatar      Ecuador        Senegal        Netherlands
Group B  | England    Iran           United States  Wales
Group C  | Argentina  Saudi Arabia   Mexico         Poland
Group D  | France     Australia      Denmark        Tunisia
Group E  | Spain     Costa Rica      Germany        Japan
Group F  | Belgium    Canada   Morocco    Croatia
Group G  | Brazil    Serbia  Switzerland   Cameroon
Group H  | Portugal   Ghana   Uruguay    South Korea


▪ Group A, Matchday 1
Sun Nov 20
  19:00      Qatar   v Ecuador  0-2 (0-2)    @ Al Bayt Stadium, Al Khor
               (Enner Valencia 16'(p), 31')
Mon Nov 21
  19:00     Senegal  v Netherlands   0-2 (0-0)   @ Al Thumama Stadium, Doha
               (Cody Gakpo 84', Davy Klaassen 90'+9)
...

▪ Match for third place
Sat Dec 17
  18:00     Croatia  v Morocco    2-1 (2-1)  @ Khalifa International Stadium, Al Rayyan
              (Joško Gvardiol 7', Mislav Oršić 42'; Achraf Dari 9')
▪ Final
Sun Dec 18
  18:00     Argentina  v France   3-3 a.e.t. (2-2, 2-0) 4-2 pen.  @ Lusail Iconic Stadium, Lusail
              (Lionel Messi 23'(p), 108', Ángel Di María 36';
               Kylian Mbappé 80'(p), 81', 118'(p))
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

Tue Apr 1
  20:45   FC Barcelona        v Atlético Madrid    1-1  @ Camp Nou, Barcelona
            (Neymar 71'; Diego 56')
  20:45   Manchester United   v Bayern München     1-1  @ Old Trafford, Manchester
            (Vidić 58'; Schweinsteiger 67')
Wed Apr 2
  20:45   Real Madrid         v Borussia Dortmund  3-0  @ Santiago Bernabéu, Madrid
            (Bale 3' Isco 27' Ronaldo 57')
  20:45   Paris Saint-Germain v Chelsea FC         3-1  @ Parc des Princes, Paris
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
ARG  BOL  BRA   =>   [:TEXT,"ARG"], [:TEXt,"BOL"], [:TEXT,"BRA"]
ARG BOL BRA     =>   [:TEXT,"ARG BOL BRA"]

Fri  Liverpool  =>   [:TEXT,"Fri"], [:TEXT,"Liverpool"]     
Fri Liverpool   =>   [:TEXT,"Fri Liverpool"]

Matchday 1      =>   [:TEXT,"Matchday 1"] 
1860 München    =>   [:TEXT,"1860 München"]
...
```     



### Round Lines (Outlines)

Round lines (outlines) MUST start with `▪` (BLACK SMALL SQUARE) or `::` (for ASCII-style)  e.g.

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

Use the geo marker, that is, `@` to start with adding "geo" names - that is, stadiums & grounds 
and / or cities, countries and more.
Examples:

```
  @ Stadio Olimpico, Roma
  @ Arena Naţională, Bucureşti, Romania
  @ Bucuresti, 23 August
  @ Wien, Prater
  @ Buenos Aires
  @ Brasília 
  @ Arena Fonte Nova, Salvador
  @ Arena Pantanal, Cuiabá
  @ Estádio do Maracanã, Rio de Janeiro
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
# Date       Fri Aug/15 2025 - Sun May/24 2026 (282d)
# Teams      20
# Matches    380

# Hugo Lloris saved a penalty from Ricardo Rodríguez at 55'.
```

#### Multi-line comments

You can use HTML-style comments, that is, `<!-- .. -->`. Example:

```
<!--
  1.AUSTRIA             3  2  0  1   6- 4   6
  2.FRANCE              3  1  2  0   2- 1   5
  3.NETHERLANDS         3  1  1  1   4- 4   4
  4.Poland              3  0  1  2   3- 6   1
-->
```


### Date (Header) Line


#### Date Formats

Many date formats supported incl. abbrevations for weekday and month names. Example:

```
## with month abbrev & day  (and year - yyyy only)
July 10
Jul 10
July 10 2026
Fri July 10
Fri July 10 2026
Friday July 10 2026
Fr July 10

Fr,     July 10 2026
Friday, July 10 2026
Fr,     July 10
        July 10, 2026
Fr,     July 10, 2026
Friday, July 10, 2026

## more max style
Monday, December 22, 2025
Wednesday, May 11, 2022
Tuesday, February 6, 2024

Monday,    December 22, 2025
Wednesday, May 11, 2022
Tuesday,   February 6, 2024


Sat, May 2
Sat, May 02
Sat, May 9
Sat, May 09
Sun, May 17
Sun, May 24


### with day and month_abbrev (and year  - yyyy or yy)
10 July
10 Jul
10 July 2026
10 July 26
Fri 10 July
Fri 10 July 2026
Fri 10 July 26
Friday 10 July 2026
Friday 10 July 26
Fr 10 July
Fr 10 July 2026
Fri     10 July 2026
Friday  10 July 2026
Fr      10 July
Fri,     10 July 2026
Friday, 10 July 2026
Fr,      10 July
Fri, 10 July 2026
Fri, 10 July 26
Friday, 10 July 2026
Friday, 10 July 26
Fr, 10 July

Sun  1 Mar
Sun 01 Mar

Wed  4 Mar
Wed 04 Mar
Sat 14 Mar
Sat 11 Apr



###############
## all numbers
10.07.2026
10.7.2026
10.07.26
10.7.26
10.07.
10.7.
Fri 10.07.2026
Fr 10.7.2026
Fr 10.07.26
Fr 10.7.26
Fr 10.07.
Fr 10.7.
Fri  10.07.2026
Fr   10.7.2026
Fri, 10.07.2026
Fr, 10.7.2026
Friday,  10.07.2026
Fr,  10.7.2026


###
# iso style
2026-07-10
2026-7-10

##  starting with day-month-year
07-10-2026
7-10-2026
Fri 07-10-2026
Fr 7-10-2026
Fri  07-10-2026
Fr    7-10-2026
Friday, 07-10-2026
Fri,  07-10-2026
Fr,    7-10-2026

###
#  use slash (/)
07/10/2026
7/10/2026
Fri 07/10/2026
Fr 7/10/2026
Fri  07/10/2026
Fr    7/10/2026
Friday, 07/10/2026
Fr,    7/10/2026

1/3/26
1/03/26
01/03/26
1/3
1/03
01/03
Su  1/3
Su 1/03
Su 01/03

We  4/3
Sa 14/3
Sa 11/4
Sa 11/04
```


### Score Formats

#### Basic (Final Result Only) Score Format

The "generic" score format is simply:

```
0-0
1-4
3-4
```

#### Score Formats for Half-Time, After-Extra-Time, Penalty-Shootout, & More 

For adding half-time, after-extra-time, penalty-shootouts, & more you have to format options - named (i) full & (i) fuller.

(i) Full-style samples:

```
Bayern München v Chelsea  1-1 aet, 3-4 pen
Bayern München v Chelsea  1-1 aet (1-1, 0-0) 3-4 pen
Bayern München v Chelsea  3-4 pen (1-1, 1-1, 0-0)
Bayern München v Chelsea  3-4 pen 1-1 aet (1-1, 0-0)
Bayern München v Chelsea  3-4 pen 1-1 aet

Bayern München  1-1 aet (1-1, 0-0) 3-4 pen  Chelsea
Bayern München  1-1 aet, 3-4 pen  Chelsea
Bayern München  3-4 pen (1-1, 1-1, 0-0)  Chelsea
Bayern München   3-4 pen 1-1 aet (1-1, 0-0)  Chelsea
Bayern München   3-4 pen. 1-1 a.e.t.   Chelsea

France  2-1 aet/gg Italy
France  2-1aet/gg Italy
France  2-1 a.e.t./g.g. Italy
France  2-1 agget Italy
France  2-1 asdet Italy

France  2-1 aet/gg (1-1, 1-0) Italy
France  2-1 aet/gg (1-1,) Italy
France  2-1 aet/gg (1-1) Italy
```

(ii) Fuller-style samples:

```
Bayern München 1-1 Chelsea (aet, win 3-4 on pens)
Bayern München 1-1 Chelsea (HT 0-0, FT 1-1, AET, PEN 3-4)

Barcelona 2-2 Chelsea  (win 2-3 on aggregate)
Real Madrid 2-1 Bayern München  (aet, agg 3-3, win 1-3 on pens)

Bayern München 2-1 Real Madrid  (HT 1-0)
Chelsea 1-0 Barcelona  (HT 1-0)
Barcelona 2-2 Chelsea  (HT 2-1, AGG 2-3)
Real Madrid 2-1 Bayern München  (HT 2-1, FT 2-1, AET, AGG 3-3, PEN 1-3)

Barcelona 4-1 Arsenal   (6-3 on agg)
Barcelona 4-1 Arsenal  (HT 3-1, AGG 6-3)

Manchester United 3-2 Bayern München  (agg 4-4, win 1-2 on away goals)
Manchester United 3-2 Bayern München  (HT 3-1, AGG 4-4, AWAY 1-2)

Bayern München 2-1 Manchester United  (HT 0-1)
Arsenal 2-2 Barcelona  (HT 0-0)

Germany  2-1 Czech Republic   (aet)
Germany  2-1 Czech Republic   (aet/gg)
Germany  2-1 Czech Republic   (a.e.t./g.g.)
Germany  2-1 Czech Republic   (a.e.t/g.g)
Germany  2-1 Czech Republic   (agget)
Germany  2-1 Czech Republic   (asdet)

Germany  v Czech Republic   2-1 (aet/gg)
Germany  v Czech Republic   2-1 (a.e.t./g.g.)
Germany  v Czech Republic   2-1 (a.e.t/g.g)
Germany  v Czech Republic   2-1 (agget)
Germany  v Czech Republic   2-1 (asdet)

France  2-1 Italy           (aet)
France  2-1 Italy           (aet/gg)


Greece  1-0 Czech Republic   (aet/sg)
Greece  1-0 Czech Republic   (a.e.t./s.g.)
Greece  1-0 Czech Republic   (asget)
```


### Goal (Scorer) Line

Goal (scorer) lines MUST be enclosed with parenthesis `()` AND start with `(`.
Note - the minute marker (`'`) is optional and you can split the 
goal (scorers) over multiple-lines 
and the commas (`,`) between players and/or minutes are optional 
e.g.

```
(Neymar 71'; Diego 56')
(Lavezzi 4' Luiz 61'og Pastore 90+3'; Hazard 27'pen)

   (Franck Ribéry 77, Ivica Olić 90+2;
             Wayne Rooney 2)
  (Franck Ribéry 77 Ivica Olić 90+2;
             Wayne Rooney 2)
  (Franck Ribéry 77
   Ivica Olić 90+2;
   Wayne Rooney 2)

        (Darron Gibson 3, Nani 7,41;
           Ivica Olić 43, Arjen Robben 74)

        (Darron Gibson 3
         Nani 7 41;
         Ivica Olić 43
         Arjen Robben 74)


        (Theo Walcott 69, Cesc Fàbregas 85pen;
               Zlatan Ibrahimović 46,59)

    (Lionel Messi 21,37,42,88; Nicklas Bendtner 18)

    (Diego Milito 35,70)
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





