# Canvas-Workshop
## The game's HTML
### Del 1
Spillets HTML
HTML-dokumentstruktur er ganske enkel, som spillet bliver gengivet helt på elementet < lærred > . Ved hjælp af din foretrukne teksteditor, oprette en ny HTML-dokument, gemme det som en fornuftig beliggenhed og tilføje følgende kode til det:index.html

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Gamedev Canvas Workshop</title>
    <style>
    	* { padding: 0; margin: 0; }
    	canvas { background: #eee; display: block; margin: 0 auto; }
    </style>
</head>
<body>

<canvas id="myCanvas" width="480" height="320"></canvas>

<script>
/*JavaScript code goes here */
</script>

</body>
</html>
```

We have a charset defined, title and some basic CSS in the header. The body contains canvas and script elements — we will render the game inside the first one and write the JavaScript code that controls it in the second one. The canvas element has an id of myCanvas to allow us to easily grab a reference to it, and it is 480 pixels wide and 320 pixels high. All the JavaScript code we will write in this tutorial will go between the opening script and closing /script tags.

## Canvas basics

Vi har en defineret, < titel > og nogle grundlæggende CSS i hovedet. Kroppen indeholder < lærred > og < script > elementer – vi vil gøre spillet inde den første sig og skrive den JavaScript-kode, der styrer det i den anden. Elementet < lærred > har en af så vi kan nemt få fat i en henvisning til det, og det er 480 pixel bred og 320 pixel høj. Alle de JavaScript-kode, vi vil skrive i denne tutorial vil gå mellem start- og slutkoder.charsetidmyCanvas<script></script>

Lærred basics
Du kan faktisk være i stand til at gøre grafik på elementet < lærred > , skal vi først få fat i en henvisning til det i JavaScript. Tilføj følgende under din åbning tag.<script>

```javascript
var canvas = document.getElementById("myCanvas");
var ctx = canvas.getContext("2d");
```

Her vi lagring af en henvisning til elementet < lærred > til variablen. Så vi skaber variablen for at gemme 2D rendering forbindelse — den faktiske værktøj, vi kan bruge til at male på lærred.canvasctx
Lad os se en eksempel stykke kode, der udskriver en rød firkant på lærredet. Tilføje dette under din tidligere linjer af JavaScript, så indlæse din i en gennemser hen til prøve sig ud.index.html

```javascript
ctx.beginPath();
ctx.rect(20, 40, 50, 50);
ctx.fillStyle = "#FF0000";
ctx.fill();
ctx.closePath();
```

Alle anvisninger er mellem metoderne beginPath() og closePath() . Vi definerer et rektangel ved hjælp af rect(): de første to værdier angiver koordinaterne for det øverste venstre hjørne af rektanglet på lærredet, mens de anden to angive bredden og højden af rektanglet. I vores tilfælde rektanglet er malet 20 pixels fra venstre side af skærmen og 40 pixels fra oversiden, og er 50 pixel bred og 50 pixel høj, hvilket gør det til et perfekt kvadrat. Egenskaben fillStyle gemmer en farve, der bruges af metoden fill() til at male pladsen i vores tilfælde, rød.
Vi er ikke begrænset til rektangler – her er et stykke kode til udskrift en grøn cirkel. Prøv at tilføje dette til bunden af din JavaScript besparelse og forfriskende:

```javascript
ctx.beginPath();
ctx.arc(240, 160, 20, 0, Math.PI*2, false);
ctx.fillStyle = "green";
ctx.fill();
ctx.closePath();
```

Som du kan se bruger vi metoderne beginPath() og closePath() igen. Mellem dem er den vigtigste del af koden ovenfor arc() metoden. Det tager seks parametre:
x og koordinater af arc's centery
ARC radius
Start vinkel og vinklet afslutning (hvad vinkel at starte og afslutte tegning cirkel, i radianer)
retning af tegning (for uret, standard, eller for mod uret.) Denne sidste parameter er valgfri.falsetrue
Egenskaben fillStyle ser anderledes ud end før. Dette er da bare med CSS, farve kan være angivet som en hexadecimal værdi, en farve nøgleord, funktionen, eller nogen af de andre metoder, tilgængelig farve.rgba()
I stedet for ved hjælp af fill() og fylde figurer med farver, kan vi bruge stroke() til at kun farve den ydre slagtilfælde. Prøv at tilføje denne kode til din JavaScript for:

```javascript
ctx.beginPath();
ctx.rect(160, 10, 100, 40);
ctx.strokeStyle = "rgba(0, 0, 255, 0.5)";
ctx.stroke();
ctx.closePath();
```

Ovenstående kode udskriver en blå-strøg tomt rektangel. Takket være alfakanalen i funktionen er den blå farve semi gennemsigtige.rgba()

Næste trin
Nu vi har defineret den grundlæggende HTML og lært lidt om lærred, kan fortsætte med at det andet kapitel og arbejde ud af at flytte bolden i vores spil.

### Del 2

Det er 2 skridt ud af 10 af Gamedev lærred tutorial. Du kan finde kildekoden, som det skal se efter endt denne lektion på Gamedev-lærred-workshop/lesson2.html.

Du kender allerede hvordan man tegner en bold fra arbejde gennem den foregående artikel, så nu, lad os gøre det gå. Teknisk, vi vil male bolden på skærmen, fjerne det og derefter male den igen i en lidt anden position hver ramme for at gøre indtryk bevægelighed — ligesom hvordan bevægelse arbejder med film.

### Definere en tegning løkke

For at holde konstant opdaterer lærredet tegning på hver ramme, vi har brug at definere en tegning funktioner, der vil køre igen og igen med et andet sæt af variable værdier hver gang for at ændre sprite holdninger, osv. Igen og igen ved hjælp af en JavaScript timing funktion som setInterval () eller requestAnimationFrame(), kan du køre en funktion.
Slette alle de JavaScript, du har i øjeblikket inde i din HTML-fil med undtagelse af de to første linjer, og Tilføj følgende under dem. Funktionen udføres inden for hver 10 miliseconds:draw()setInterval

```javascript

function draw() {
    // drawing code
}
setInterval(draw, 10);
```

Takket være den uendelige karakter af funktionen vil blive kaldt hver 10 millisekunder for evigt, eller indtil vi stoppe den. Nu, lad os trække bolden — skal du tilføje følgende i din funktion:setIntervaldraw()draw()

```javascript
ctx.beginPath();
ctx.arc(50, 50, 10, 0, Math.PI*2);
ctx.fillStyle = "#0095DD";
ctx.fill();
ctx.closePath();
```

### Få den til at bevæge sig

Du vil ikke mærke bolden bliver malet hele tiden i øjeblikket, da det ikke er i bevægelse. Lad os ændre. Først, i stedet for en hardcodede position på (50,50) vi vil definere et udgangspunkt på den nederste midterste del af lærredet i variabler hedder og derefter bruge dem til at definere positionen cirklen er tegnet på.xy
Først, sammenlægge den næste to linier over din funktion, at definere og:draw()xy

```javascript
var x = canvas.width/2;
var y = canvas.height-30;
```

Næste opdatere funktionen til brug af x og y variabler i metoden arc() , som vist i den følgende markerede linje:draw()

```javascript
function draw() {
    ctx.beginPath();
    ctx.arc(x, y, 10, 0, Math.PI*2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
}
```

Nu kommer den vigtige del: vi ønsker at tilføje en lille værdi og efter hver frame er udarbejdet for at gøre det ud til, at bolden er i bevægelse. Lad os definere disse små værdier som og og sat deres værdier til 2 og -2 henholdsvis. Tilføj følgende under din x og y variable definitioner:xydxdy

```javascript
var dx = 2;
var dy = -2;
```

Den sidste ting at gøre er at opdatere og med vores og variable på hver ramme, så bolden vil være malet i den nye stilling på hver opdatering. Tilføj følgende to nye linjer angivet nedenfor for at din funktion:xydxdydraw()

```javascript
function draw() {
    ctx.beginPath();
    ctx.arc(x, y, 10, 0, Math.PI*2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
    x += dx;
    y += dy;
}
```

Gem din kode igen og prøve det i din browser. Det virker ok, selv om det synes at bolden forlader en trail bag det:

### Clearing lærred før hver ramme

Bolden er efterlader et spor, fordi vi maler en ny cirkel på hver ramme uden at fjerne den tidligere en. Må ikke bekymre dig, fordi der er en metode til at rydde lærred indhold: clearRect(). Denne metode tager fire parametre: x og y koordinater for den øverste venstre hjørne af et rektangel, og x og y koordinater i nederste højre hjørne af et rektangel. Hele området er omfattet af dette rektangel ryddes af indhold tidligere malet der.
Tilføj følgende fremhævet nye linje til funktionen:draw()

```javascript
function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.beginPath();
    ctx.arc(x, y, 10, 0, Math.PI*2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
    x += dx;
    y += dy;
}
```

Gem din kode og prøv igen, og denne gang du vil se bolden bevæge sig uden et spor. Hver 10 millisekunder lærredet er ryddet, den blå cirkel (vores bold) vil blive trukket på en given position og den og værdier vil blive opdateret til den næste ramme.xy

### Ryd op i vores kode

Vi vil være tilføjer mere og mere kommandoer til at fungere i næste par artikler, så det er godt at holde det så simpelt og ren som muligt. Lad os starte ved at flytte bolden tegning kode til en særskilt funktion.draw()
Erstatte funktionen eksisterende draw() med de følgende to funktioner:

```javascript
function drawBall() {
    ctx.beginPath();
    ctx.arc(x, y, 10, 0, Math.PI*2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawBall();
    x += dx;
    y += dy;
}
```
Øvelse: Prøv at ændre hastigheden på den bevægelige bold, eller den retning, den bevæger sig i.

Næste trin
Vi har trukket vores bold og fået det bevæger sig, men det holder forsvinde ud over kanten af lærredet. I det tredje kapitel vil vi undersøge, hvordan at gøre det hoppe fra væggene.

### Del 3

Simpel sammenstød afsløring
At opdage de sammenstød, vi vil kontrollere, om bolden rører (kolliderede med) muren, og hvis så, vi vil ændre retningen af dens bevægelse i overensstemmelse hermed.
For at gøre beregningerne lettere Lad os definere en variabel kaldet, der vil holde radius af den tegnede cirkel og bruges til beregninger. Tilføj dette til din kode, et sted under de eksisterende variable erklæringer:ballRadius

```javascript
ctx.arc(x, y, ballRadius, 0, Math.PI*2);
```

### Hoppe fra top og bund

Der er fire vægge til at hoppe bolden ned — Lad os fokusere på den øverste ene først. Vi skal tjekke på hver frame, uanset om bolden rører den øverste kant af lærredet – hvis ja, vi vil vende bevægelsen bold, så vil det begynde at bevæge sig i den modsatte retning og holde sig inden for de synlige grænser. At huske at koordinatsystemet begynder fra øverst til venstre, kan vi komme med noget som dette:

```javascript
if(y + dy < 0) {
    dy = -dy;
}
```

Hvis bolden position er lavere end nul, ændre retningen af bevægelse på aksen ved at angive det lig med sig selv, tilbageføres. Hvis bolden bevæger sig opad med en hastighed på 2 pixels pr. ramme, vil nu det være omflytning "op" med en hastighed på-2 pixels, hvilket faktisk svarer til bevæger sig ved en hastighed på 2 pixels pr frame.yy
Ovenstående kode vil beskæftige sig med bolden hoppe fra den øverste kant, så nu lad os tænke over den nederste kant:

```javascript
if(y + dy > canvas.height) {
    dy = -dy;
}
```

Hvis boldens position er større end højden af lærredet (Husk at vi tæller værdier fra øverst til venstre, så den øverste kant starter ved 0 og den nederste kant er på 480 pixels, lærred højde), derefter hoppe det ud den nederste kant ved at vende den akse bevægelse en s før.yyy
Vi kunne sammenlægge de to udsagn i sig at spare på kode verbosity:

```javascript
if(y + dy > canvas.height || y + dy < 0) {
    dy = -dy;
}
```

Hvis en af de to erklæringer, vende bevægelsen af bolden.true

### Hoppe fra venstre og højre

Vi har den øverste og nederste kant er dækket, så lad os tænke på venstre og højre ones. Det er faktisk meget lig alt du skal gøre, er at gentage sætninger for i stedet for:xy

```javascript
if(x + dx > canvas.width || x + dx < 0) {
    dx = -dx;
}

if(y + dy > canvas.height || y + dy < 0) {
    dy = -dy;
}
```

På dette tidspunkt bør du indsætte kodeblokken ovenfor i funktionen draw(), lige før den afsluttende klammeparentes.

### Bolden holder forsvinde ind i væggen!

Teste din kode på dette punkt, og du vil blive imponeret – nu har vi en bold, der prellede alle fire kanter på lærred! Vi har et andet problem dog — når bolden rammer hver væg, det synker ind i det lidt før du ændrer retning:

Dette er fordi vi beregner kollision punkt i væggen og midten af bolden, mens vi skal gøre det for sin omkreds. Bolden skal hoppe lige efter if rører væggen, ikke når det er allerede halvvejs i væggen, så lad os justere vores erklæringer en smule at medtage der. Opdatere den sidste kode, du har tilføjet til dette:

```javascript
if(x + dx > canvas.width-ballRadius || x + dx < ballRadius) {
    dx = -dx;
}
if(y + dy > canvas.height-ballRadius || y + dy < ballRadius) {
    dy = -dy;
}
```

Når afstanden mellem midten af bolden og kanten af væggen er nøjagtig den samme som radiussen af bolden, vil det ændre den bevægelsesretning. Fratrække radius fra én kant bredde og tilføje det på den anden giver os indtryk af den korrekte kollisions-bolden hopper fra væggene som den bør gøre.

Næste trin
Vi har nu fået til den fase, hvor vores bold både flytte og opholder sig på brættet. I det fjerde kapitel vil vi kigge på at gennemføre en kontrollerbar pagaj — Se pagaj og tastatur kontrol.

### Del 4

Bolden er hoppende off vægge frit, og du kan se det på ubestemt tid, men i øjeblikket er der ingen interaktivitet. Det er ikke et spil, hvis du ikke kan styre det! Så lad os tilføje nogle brugerinteraktion: en kontrollerbar pagaj.

### Definere en pagaj for at ramme bolden

Så, vi har brug for en pagaj at ramme bolden — Lad os definere et par variabler for at. Tilføj følgende variabler nær toppen af din kode, ved siden af dine andre variabler:

```javascript
var paddleHeight = 10;
var paddleWidth = 75;
var paddleX = (canvas.width-paddleWidth)/2;
```

Her definerer vi højden og bredden af pagajen og sit udgangspunkt på aksen, til brug i beregninger yderligere på ned koden. Lad os oprette en funktion, der vil trække padle på skærmen. Tilføj følgende lige under din funktion:xdrawBall()

```javascript
function drawPaddle() {
    ctx.beginPath();
    ctx.rect(paddleX, canvas.height-paddleHeight, paddleWidth, paddleHeight);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
}
```

### Tillader brugeren at styre pagajen

Vi kan trække pagajen, uanset hvor vi ønsker, men det bør reagere på brugerens handlinger — det er tid til at gennemføre nogle tastatur kontrol. Vi får brug for:
To variabler til at gemme oplysninger på om venstre eller højre Ctrl-knappen er trykket.
To begivenhed lyttere til og events – vi ønsker at køre nogle kode for at håndtere padle bevægelse, når der trykkes på knapperne.keydownkeyup
To funktioner håndtering af og begivenheder den kode, der køres, når der trykkes på knapperne.keydownkeyup
Evnen til at flytte padle, venstre og højre
Pressede knapper kan defineres og initialiseres med boolean variabler, som så. Tilføje disse linjer et sted i nærheden af resten af dine variabler:

```javascript
var rightPressed = false;
var leftPressed = false;
```

Standardværdien for begge er fordi i begyndelsen betjeningsknapperne ikke er presset. Hvis du vil lytte til tastetryk, vil vi oprette to begivenhed lyttere. Tilføj følgende linjer lige over linjen nederst i din JavaScript:falsesetInterval()

```javascript
document.addEventListener("keydown", keyDownHandler, false);
document.addEventListener("keyup", keyUpHandler, false);
```

Når hændelsen er fyret på en af tasterne på tastaturet (når de presses), udføres funktionen. Det samme mønster gælder for den anden lytter: begivenheder vil brand funktionen (når tasterne holder op med at være trykket). Tilføje disse til din kode nu, under linjerne:keydownkeyDownHandler()keyupkeyUpHandler()addEventListener()

```javascript
function keyDownHandler(e) {
    if(e.keyCode == 39) {
        rightPressed = true;
    }
    else if(e.keyCode == 37) {
        leftPressed = true;
    }
}

function keyUpHandler(e) {
    if(e.keyCode == 39) {
        rightPressed = false;
    }
    else if(e.keyCode == 37) {
        leftPressed = false;
    }
}
```

Når vi trykker på en tast nede, gemmes oplysningerne i en variabel. Den relevante variabel i hvert enkelt tilfælde er indstillet til. Når nøglen er frigivet, er variablen sat tilbage.truefalse
Begge funktioner tage en begivenhed som en parameter, repræsenteret af variablen. Fra at du kan få nyttige oplysninger: lastrum oplysninger om den nøgle, der blev trykket på. For eksempel nøglen kode 37 er den venstre markørknap og 39 er højre-cursoren. Hvis venstre markøren er trykket, derefter variablen er indstillet til, og når det er frigivet variablen er angivet til. Det samme mønster følger med højre-cursoren og variablen.ekeyCodeleftPressedtrueleftPressedfalserightPressed

### Padle bevægelse logik

Vi har nu variabler til at gemme info om tasteanslag, begivenhed lyttere og relevante funktioner sat op. Nu får vi ind på selve koden til at bruge alle den og flytte padle på skærmen. Inde i funktionen, vil vi kontrollere, hvis venstre eller højre cursor-tasterne er presset når hvert billede gengives. Vores kode kunne ligne dette:draw()

```javascript
if(rightPressed) {
    paddleX += 7;
}
else if(leftPressed) {
    paddleX -= 7;
}
```

Hvis venstre markøren er trykket, padle vil flytte 7 pixels til venstre, og hvis trykkes på højre-cursoren pagajen vil flytte 7 pixel til højre. Dette i øjeblikket virker ok, men padle forsvinder ud over kanten af lærredet hvis vi nede enten alt for længe. Vi kunne forbedre, og flytte padle kun inden for grænserne af lærredet ved at ændre koden som følger:

```javascript
if(rightPressed && paddleX < canvas.width-paddleWidth) {
    paddleX += 7;
}
else if(leftPressed && paddleX > 0) {
    paddleX -= 7;
}
```

Den holdning, vi bruger vil flytte mellem den venstre side af lærredet og på højre side, som vil arbejde præcis som vi ønsker det.paddleX0canvas.width-paddleWidth

Tilføje kodeblokken ovenfor i funktionen nederst lige over den afsluttende klammeparentes.draw()

Den eneste ting tilbage at gøre er nu kalde funktionen fra i funktionen faktisk udskrive det på skærmen. Tilføj følgende linje i din funktion, lige under den linje, der kalder:drawPaddle()draw()draw()drawBall()

```javascript
drawPaddle();
```

Næste trin
Nu har vi noget, der ligner et spil; de eneste problemer er nu, at du bare kan fortsætte med at ramme bolden med pagajen for evigt. Dette vil alle ændre i det femte kapitel, Game over, når vi begynder at tilføje i et slutspil state for vores spil.

### Del 5

### Gennemføre game over

Lad os forsøge at gennemføre spillet i vores spil. Her er stykket kode fra den tredje lektion, hvor vi lavede bolden hoppe fra væggene:

```javascript
if(x + dx > canvas.width-ballRadius || x + dx < ballRadius) {
    dx = -dx;
}

if(y + dy > canvas.height-ballRadius || y + dy < ballRadius) {
    dy = -dy;
}
```

I stedet for at lade bolden til at hoppe fra alle fire vægge, lad os tillader kun tre nu – højre, top og venstre. At ramme bunden muren vil afslutte spillet. Vi vil redigere den anden hvis blok så det er en hvis anden blok, der vil udløse vores "game over" tilstand på kuglen kolliderede med den nederste kant af lærredet. For nu vil vi holde det simpelt, viser en advarselsmeddelelse og genstarte spillet ved genindlæsning af siden. Erstatte den anden hvis-sætning med følgende:

```javascript
if(y + dy < ballRadius) {
    dy = -dy;
} else if(y + dy > canvas.height-ballRadius) {
    alert("GAME OVER");
    document.location.reload();
}
```

### At lade pagajen ramme bolden

Den sidste ting at gøre i denne lektion er at skabe en slags kollisions mellem bolden og pagaj, så det kan hoppe ud det og komme tilbage i afspilningsområdet. Den nemmeste ting at gøre er at kontrollere, om midten af bolden er mellem venstre og højre kanter af pagajen. Opdatere den sidste bid af kode du ændret igen, til følgende:

```javascript
if(y + dy < ballRadius) {
    dy = -dy;
} else if(y + dy > canvas.height-ballRadius) {
    if(x > paddleX && x < paddleX + paddleWidth) {
        dy = -dy;
    }
    else {
        alert("GAME OVER");
        document.location.reload();
    }
}
```

Hvis bolden rammer den nederste kant af lærredet nødt vi til at tjekke om den rammer pagajen. Hvis ja, så springer det ud ligesom du ville forvente; Hvis ikke så er spillet slut som før.

Næste trin
Vi laver ganske godt hidtil og vores spil er begyndt at føle en masse mere værd at spille nu du kan tabe! Men det stadig mangler noget. Lad os gå videre til den sjette kapitel — bygge feltet mursten — og skabe nogle mursten for bolden at ødelægge.

### Del 6

### Opsætning af mursten variabler

Det overordnede formål med denne lektion er at gøre et par linjer kode for mursten, ved hjælp af en indlejret løkke, der virker gennem en todimensional matrix. Første men vi har brug at oprette nogle variabler til at definere oplysninger om mursten som deres bredde og højde, rækker og kolonner, osv. Føj følgende linjer til din kode under de variabler, som du har tidligere anmeldt i dit program.

```javascript
var brickRowCount = 3;
var brickColumnCount = 5;
var brickWidth = 75;
var brickHeight = 20;
var brickPadding = 10;
var brickOffsetTop = 30;
var brickOffsetLeft = 30;
```

Her har vi defineret antallet af rækker og kolonner af mursten, deres bredde og højde, polstring mellem mursten så de ikke vil røre hinanden og en top og venstre forskydning, så de ikke vil starte trækkes lige fra kanten af lærredet.

Vi vil holde alle vores mursten i en todimensional matrix. Den vil indeholde kolonnerne mursten (c), som igen vil indeholde de mursten rækker (r), som igen hver indeholder et objekt, der indeholder den og holdning til at male hver mursten på skærmen. Tilføj følgende lige under dine variabler:xy

```javascript
var bricks = [];
for(c=0; c<brickColumnCount; c++) {
    bricks[c] = [];
    for(r=0; r<brickRowCount; r++) {
        bricks[c][r] = { x: 0, y: 0 };
    }
}
```

Ovenstående kode vil sløjfe igennem de rækker og kolonner og oprette nye mursten. Bemærk at mursten objekter bruges også til sammenstød afsløring formål senere.

### Mursten tegning logik

Lad os nu oprette en funktion til at sløjfe igennem alle murstenene i matrixen og tegne dem på skærmen. Vores kode kunne ligne dette:

```javascript
function drawBricks() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            bricks[c][r].x = 0;
            bricks[c][r].y = 0;
            ctx.beginPath();
            ctx.rect(0, 0, brickWidth, brickHeight);
            ctx.fillStyle = "#0095DD";
            ctx.fill();
            ctx.closePath();
        }
    }
}
```

Igen, vi looping gennem rækkerne og kolonnerne for at indstille den og placeringen af hver mursten, og vi også male en mursten på lærredet – størrelse x — med hver løkke iteration. Problemet er at vi maler dem alle på ét sted på koordinater. Hvad vi behøver at gøre er omfatter nogle beregninger, der vil træne på og placeringen af hver mursten for hver sløjfe iteration:xybrickWidthbrickHeight(0,0)xy

```javascript
var brickX = (c*(brickWidth+brickPadding))+brickOffsetLeft;
var brickY = (r*(brickHeight+brickPadding))+brickOffsetTop;
```

Hver stilling er arbejdede som + multipliceret med kolonnenummeret, plus den; logik for den mekaniker er identiske, bortset fra at det bruger værdierne for rækkenummer,,, og. Nu hver enkelt mursten kan placeres i det korrekte sted række og kolonne, med polstring mellem hver mursten, trukket på en forskydning fra venstre og øverste lærred kanter.brickXbrickWidthbrickPaddingcbrickOffsetLeftrbrickHeightbrickOffsetTop

Den endelige version af funktionen efter tildeling af og værdier som koordinater i stedet for hver gang, vil ligne indeværende — Tilføj dette til din kode under funktionen:drawBricks()brickXbrickY(0,0)drawPaddle()

```javascript
function drawBricks() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var brickX = (c*(brickWidth+brickPadding))+brickOffsetLeft;
            var brickY = (r*(brickHeight+brickPadding))+brickOffsetTop;
            bricks[c][r].x = brickX;
            bricks[c][r].y = brickY;
            ctx.beginPath();
            ctx.rect(brickX, brickY, brickWidth, brickHeight);
            ctx.fillStyle = "#0095DD";
            ctx.fill();
            ctx.closePath();
        }
    }
}
```

### Faktisk tegning mursten

Den sidste ting at gøre i denne lektion er at tilføje et opkald til et sted i funktionen, helst i begyndelsen, mellem clearing af lærredet og tegning bolden. Tilføj følgende lige over opkaldet:drawBricks()draw()drawBall()

```javascript
drawBricks();
```

Næste trin
Så nu har vi mursten! Men bolden er ikke interagere med dem på alle – vil vi ændre, som vi fortsat den syvende kapitel: sammenstød afsløring.

### Del 7

Vi har de mursten, der vises på skærmen allerede, men spillet er stadig ikke at interessant da kuglen går igennem dem. Vi skal tænke om at tilføje sammenstød afsløring, så det kan hoppe ud murstenene og bryde dem.
Det er vores beslutning om hvordan man gennemfører dette, selvfølgelig, men det kan være svært at beregne om bolden rører rektanglet eller ikke fordi der er ingen hjælpefunktioner i lærred for dette. Af hensyn til denne tutorial vil vi gøre det lettest muligt. Vi vil kontrollere hvis midten af bolden kolliderede med nogen af de givne mursten. Dette vil ikke give et perfekt resultat hver gang, og der er meget mere avancerede måder at gøre sammenstød afsløring, men dette vil fungere fint til at lære dig de grundlæggende begreber.

### Et sammenstød afsløring funktion

For at sparke det ønsker alle off vi at skabe en kollision bevægelsesdetektering funktion, der vil sløjfe igennem alle murstenene og sammenligne hver enkelt mursten position med boldens koordinater, som hvert billede tegnes. For bedre læsbarhed af koden vil vi definere variabel til at gemme objektet mursten i hver løkke af sammenstød afsløring:b

```javascript
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            // calculations
        }
    }
}
```

Hvis kuglen ligger inde koordinaterne for en af vores mursten, vil vi ændre retningen af bolden. For midten af bolden til at være inde i mursten, skal alle fire af følgende udsagn være sandt:
X-position af bolden er større end x-position af mursten.
X-position af bolden er mindre end x-position af mursten plus dens bredde.
Y placeringen af bolden er større end y position af mursten.
Y placeringen af bolden er mindre end y position mursten plus dens højde.
Lad os skrive det i kode:

```javascript
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            if(x > b.x && x < b.x+brickWidth && y > b.y && y < b.y+brickHeight) {
                dy = -dy;
            }
        }
    }
}
```

### Få mursten til at forsvinde, når de rammes

Ovenstående kode vil arbejde som ønsket og bolden skifter sin retning. Problemet er, at mursten bor hvor de er. Vi er nødt til at regne ud en måde at slippe af dem, vi allerede har ramt med bolden. Vi kan gøre ved at tilføje en ekstra parameter til at angive, om vi ønsker at male hver mursten på skærmen eller ej. I del af den kode, hvor vi initialisere mursten, lad os tilføje en ejendom til hver mursten objekt. Opdatere den følgende del af koden, som angivet af den fremhævede linje:status

```javascript
var bricks = [];
for(c=0; c<brickColumnCount; c++) {
    bricks[c] = [];
    for(r=0; r<brickRowCount; r++) {
        bricks[c][r] = { x: 0, y: 0, status: 1 };
    }
}
```

Næste vi vil kontrollere værdien af hver mursten ejendom i funktionen før tegning det — hvis er, så tegner det, men hvis det er, så det blev ramt af bolden og vi ikke længere vil have det på skærmen. Opdater din funktion som følger:statusdrawBricks()status10drawBricks()

```javascript
function drawBricks() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            if(bricks[c][r].status == 1) {
                var brickX = (c*(brickWidth+brickPadding))+brickOffsetLeft;
                var brickY = (r*(brickHeight+brickPadding))+brickOffsetTop;
                bricks[c][r].x = brickX;
                bricks[c][r].y = brickY;
                ctx.beginPath();
                ctx.rect(brickX, brickY, brickWidth, brickHeight);
                ctx.fillStyle = "#0095DD";
                ctx.fill();
                ctx.closePath();
            }
        }
    }
}
```

### Sporing og opdatere status i sammenstød afsløring funktion

Nu skal vi inddrage egenskaben mursten i funktionen: hvis mursten er aktive (dens status er) vil vi kontrollere, om kollisionen sker; Hvis en kollision opstÃ ¥ vi vil angive status for den givne mursten til, så det ikke vil være malet på skærmen. Opdater din funktion som angivet nedenfor:statuscollisionDetection()10collisionDetection()

```javascript
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            if(b.status == 1) {
                if(x > b.x && x < b.x+brickWidth && y > b.y && y < b.y+brickHeight) {
                    dy = -dy;
                    b.status = 0;
                }
            }
        }
    }
}
```

### Aktivering af vores sammenstød afsløring

Den sidste ting at gøre er at tilføje et kald til funktionen til vores vigtigste funktion. Tilføj følgende linje til funktionen, lige under opkaldet:collisionDetection()draw()draw()drawPaddle()

```javascript
collisionDetection();
```

Næste trin
Vi helt sikkert får der nu; Lad os gå videre! I det ottende kapitel vil vi se på hvordan man kan spore scoren og vinde.

### Del 8

### Tælle score

Hvis du kan se din score hele spillet, kan til sidst du imponere dine venner. Du har brug for en variabel til at optage scoren. Tilføj følgende i din JavaScript, efter resten af dine variabler:

```javascript
var score = 0;
```

Du skal også en funktion til at oprette og opdatere visningen score. Tilføj følgende efter funktion:drawScore()collisionDetection()

```javascript
function drawScore() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#0095DD";
    ctx.fillText("Score: "+score, 8, 20);
}
```

Tegning tekst på et lærred er lig tegne en figur. Den skrifttype definition ser ud præcis som i CSS – du kan angive den størrelse og skrifttype type i metoden skrifttype() . Brug derefter fillStyle() til at angive farven på den skrifttype og fillText() til at angive den faktiske tekst, som vil blive placeret på lærredet, og hvor det skal placeres. Den første parameter er selve teksten — den kode ovenfor viser det aktuelle antal point – og de sidste to parametre er koordinaterne hvor teksten vil blive placeret på lærredet.
For at tildele en score hver gang en mursten er ramt, skal du tilføje en linje til funktion at forøge værdien af variablen score hver gang en kollision er opdaget. Tilføj den følgende markerede linje til din kode:collisionDetection()

```javascript
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            if(b.status == 1) {
                if(x > b.x && x < b.x+brickWidth && y > b.y && y < b.y+brickHeight) {
                    dy = -dy;
                    b.status = 0;
                    score++;
                }
            }
        }
    }
}
```

Kald af funktionen holder score ajour med hver ny ramme — Tilføj følgende linje inde, lige under opkaldet:drawScore()draw()draw()drawPaddle()

```javascript
drawScore();
```

### Vise en vindende besked, når alle mursten er blevet ødelagt.

Indsamle punkterne, der fungerer godt, men du vil ikke være tilføjer dem for evigt – hvad med når alle brikkerne er blevet ødelagt? Det er det vigtigste formål med spillet, så du skal vise en vindende besked, hvis alle tilgængelige punkter er blevet indsamlet. Tilføj den følgende markerede afsnit i din funktion:collisionDetection()

```javascript
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            if(b.status == 1) {
                if(x > b.x && x < b.x+brickWidth && y > b.y && y < b.y+brickHeight) {
                    dy = -dy;
                    b.status = 0;
                    score++;
                    if(score == brickRowCount*brickColumnCount) {
                        alert("YOU WIN, CONGRATULATIONS!");
                        document.location.reload();
                    }
                }
            }
        }
    }
}
```

Takket være dette, kan dine brugere faktisk vinder spillet, når de ødelægge alle murstenene, der er ret vigtigt, når det kommer til spil. Funktionen genindlæser siden og starter spillet igen, når der klikkes på knappen alarm.document.location.reload()

Næste trin
Spillet ser temmelig godt på dette punkt. I næste lektion vil du udvide spillets appel ved at tilføje mus kontrol.

### Del 9

### Lytte til musen bevægelse

Lytte til musen er endnu nemmere end at lytte til tastetryk: alt hvad vi behøver er lytteren til begivenheden. Tilføj følgende linje i nærheden af en anden begivenhed lyttere, lige under den:mousemovekeyup event

```javascript
document.addEventListener("mousemove", mouseMoveHandler, false);
```

### Forankring padle bevægelse til musen bevægelse

Vi kan opdatere pagaj holdning baseret på markøren koordinater-funktionen følgende handleren vil gøre netop dette. Tilføj følgende funktion til din kode, under den foregående linje du tilføjede:

```javascript
function mouseMoveHandler(e) {
    var relativeX = e.clientX - canvas.offsetLeft;
    if(relativeX > 0 && relativeX < canvas.width) {
        paddleX = relativeX - paddleWidth/2;
    }
}
```

I denne funktion vi først udarbejde en værdi, som er lig med vandrette mus holdning i viewport () minus afstanden mellem venstre kant af lærredet og venstre kant af viewport () — effektivt det er lig med afstanden mellem lærred venstre kant en d musemarkøren. Hvis relative X pointer holdning er større end nul og mindre end lærred bredden, markøren er inden for lærredsgrænserne, og positionen (forankret på den venstre kant af pagajen) er angivet til værdien minus halvdelen af bredden af pagajen , således at bevægelsen vil faktisk være i forhold til midten af pagajen.relativeXe.clientXcanvas.offsetLeftpaddleXrelativeX
Padle vil nu følge placeringen af musen, men da vi begrænse bevægelse til størrelsen af lærredet, det vil ikke forsvinde helt fra begge sider.

Næste trin
Nu har vi en komplet spil vi vil afslutte vores serier af lektioner med nogle flere små tweaks — prikken over op.

### Del 10

Der er altid plads til forbedringer i ethvert spil, vi skriver. For eksempel, kan vi tilbyde mere end ét liv til spilleren. De kunne gøre en fejl eller to og stadig være i stand til at afslutte spillet. Vi kunne også forbedre vores kode rendering.

### Giver spilleren nogle liv

Gennemføre liv er helt ligetil. Lad os først tilføje en variabel til at gemme antallet af liv i det samme sted, hvor vi erklærede vores andre variabler:

```javascript
var lives = 3;
```

Tegning tælleren liv ser næsten det samme som tegning score tæller – tilføje følgende funktion til din kode, under funktionen:drawScore()

```javascript
function drawLives() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#0095DD";
    ctx.fillText("Lives: "+lives, canvas.width-65, 20);
}
```

Stedet for at afslutte spillet straks, vil vi reducere antallet af liv, indtil de er ikke længere tilgængelig. Vi kan også nulstille bolden og pagaj positioner, når spilleren begynder med deres næste liv. Så, i funktionen erstatte den næste to linier:draw()

```javascript
alert("GAME OVER");
document.location.reload();
```

Med dette, kan vi tilføje lidt mere kompleks logik at det som angivet nedenfor:

```javascript
lives--;
if(!lives) {
    alert("GAME OVER");
    document.location.reload();
}
else {
    x = canvas.width/2;
    y = canvas.height-30;
    dx = 2;
    dy = -2;
    paddleX = (canvas.width-paddleWidth)/2;
}
```

Nu, når bolden rammer den nederste kant af skærmen, vi fratrækker et liv fra variablen. Hvis der er ingen liv tilbage, er spillet tabt; Hvis der er stadig nogle liv venstre, derefter placeringen af bolden og padle nulstilles, sammen med bevægelsen af bolden.lives

### Rendering liv display

Nu skal du tilføje et kald til funktionen og tilføje det under opkaldet.drawLives()draw()drawScore()

```javascript
drawLives();
```

Forbedre præstationen med requestAnimationFrame()
Nu lad os arbejde på noget, der ikke er forbundet med spillets mekanik, men måde, at det gengives. requestAnimationFrame hjælper browseren gøre spillet bedre end den faste framerate, vi i øjeblikket har implementeret ved hjælp af setInterval (). Erstatte den følgende linje:

```javascript
setInterval(draw, 10);

//med blot:

draw();
```

Derefter, på bunden af funktionen (lige før den afsluttende klammeparentes), tilføje i den følgende linje, som medfører, at funktionen til at kalde sig selv igen og igen:draw()draw()

```javascript
requestAnimationFrame(draw);
```

Funktionen er nu at få udført igen inden for en loop, men i stedet for den faste 10 millisekunder frame rate, vi giver kontrol over frameraten tilbage til browseren. Det vil synkronisere frameraten i overensstemmelse hermed og render figurer, når det behøves. Dette giver en mere effektiv, mere smidig animation løkke end den ældre metode.draw()requestAnimationFrame()setInterval()

## ================================

Compare your code:

```javascript
var canvas = document.getElementById("myCanvas");
var ctx = canvas.getContext("2d");
var ballRadius = 10;
// // to move
var x = canvas.width/2;
var y = canvas.height-30;
var dx = 2;
var dy = -2;
// Definere pagaj for at ramme bolden
var paddleHeight = 10;
var paddleWidth = 75;
var paddleX = (canvas.width-paddleWidth)/2;
var rightPressed = false;
var leftPressed = false;
// Opsætning af mursten variabler
var brickRowCount = 5;
var brickColumnCount = 3;
var brickWidth = 75;
var brickHeight = 20;
var brickPadding = 10;
var brickOffsetTop = 30;
var brickOffsetLeft = 30;
var score = 0;
var lives = 3;

var bricks = [];
for(c=0; c<brickColumnCount; c++) {
    bricks[c] = [];
    for(r=0; r<brickRowCount; r++) {
        bricks[c][r] = { x: 0, y: 0, status: 1 };
    }
}

document.addEventListener("keydown", keyDownHandler, false);
document.addEventListener("keyup", keyUpHandler, false);
document.addEventListener("mousemove", mouseMoveHandler, false);
// ====== keyDownHandler ==================
function keyDownHandler(e) {
    if(e.keyCode == 39) {
        rightPressed = true;
    }
    else if(e.keyCode == 37) {
        leftPressed = true;
    }
}
// ====== keyDownHandler ==================
function keyUpHandler(e) {
    if(e.keyCode == 39) {
        rightPressed = false;
    }
    else if(e.keyCode == 37) {
        leftPressed = false;
    }
}
// ====== mouseMoveHandler ==================
function mouseMoveHandler(e) {
    var relativeX = e.clientX - canvas.offsetLeft;
    if(relativeX > 0 && relativeX < canvas.width) {
        paddleX = relativeX - paddleWidth/2;
    }
}
// ====== collisionDetection ==============
function collisionDetection() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            var b = bricks[c][r];
            if(b.status == 1) {
                if(x > b.x && x < b.x+brickWidth && y > b.y && y < b.y+brickHeight) {
                    dy = -dy;
                    b.status = 0;
                    score++;
                    if(score == brickRowCount*brickColumnCount) {
                        alert("Tillykke Du Vandt!");
                        document.location.reload();
                    }
                }
            }
        }
    }
}
// ====== darwBall ========================
function drawBall() {
    ctx.beginPath();
    ctx.arc(x, y, ballRadius, 0, Math.PI*2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
}
// ====== darwPaddle ======================
function drawPaddle() {
    ctx.beginPath();
    ctx.rect(paddleX, canvas.height-paddleHeight, paddleWidth, paddleHeight);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
}
// ====== drawBricks ==================
function drawBricks() {
    for(c=0; c<brickColumnCount; c++) {
        for(r=0; r<brickRowCount; r++) {
            if(bricks[c][r].status == 1) {
                var brickX = (r*(brickWidth+brickPadding))+brickOffsetLeft;
                var brickY = (c*(brickHeight+brickPadding))+brickOffsetTop;
                bricks[c][r].x = brickX;
                bricks[c][r].y = brickY;
                ctx.beginPath();
                ctx.rect(brickX, brickY, brickWidth, brickHeight);
                ctx.fillStyle = "#0095DD";
                ctx.fill();
                ctx.closePath();
            }
        }
    }
}
// ====== drawScore ================
function drawScore() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#0095DD";
    ctx.fillText("Score: "+score, 8, 20);
}
// ====== drawLives ================
function drawLives() {
    ctx.font = "16px Arial";
    ctx.fillStyle = "#0095DD";
    ctx.fillText("Lives: "+lives, canvas.width-65, 20);
}
// ====== draw ================
function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawBricks();
    drawBall();
    drawPaddle();
    drawScore();
    drawLives();
    collisionDetection();
    if(x + dx > canvas.width-ballRadius || x + dx < ballRadius) {
        dx = -dx;
    }
    if(y + dy < ballRadius) {
        dy = -dy;
    }
    else if(y + dy > canvas.height-ballRadius) {
        if(x > paddleX && x < paddleX + paddleWidth) {
            dy = -dy;
        }
        else {
            lives--;
            if(!lives) {
                alert("GAME OVER");
                document.location.reload();
            }
            else {
                x = canvas.width/2;
                y = canvas.height-30;
                dx = 3;
                dy = -3;
                paddleX = (canvas.width-paddleWidth)/2;
            }
        }
    }
    if(rightPressed && paddleX < canvas.width-paddleWidth) {
        paddleX += 7;
    }
    else if(leftPressed && paddleX > 0) {
        paddleX -= 7;
    }
    x += dx;
    y += dy;
    requestAnimationFrame(draw);
}

draw();
```

### Game over - for nu!

Du har afsluttet alle lektionerne - tillykke! Ved dette punkt, bør du nu vide grundlæggende i lærred manipulation og logikken bag simple 2D spil. Nu er det et godt tidspunkt at lære nogle rammer og fortsætte spillets udvikling. Du kan tjekke ud denne serie modstykke, 2D breakout spil ved hjælp af Phaser eller Cyber Orb bygget i Phaser tutorial. Du kan også se gennem spil sektion på MDN for inspiration og mere viden.

Du kan også gå tilbage til denne tutorial serie indeksside.

Have det sjovt med kodning!