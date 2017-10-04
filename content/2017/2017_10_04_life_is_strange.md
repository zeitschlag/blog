Title: Life Is Strange
Date: 4.10.2017, 7:48
Tags: [#lifeisstrange, #mathe]
filters: [markdown+mathml]

Am Wochenende — das dauerte dieses Mal von Donnerstag bis Dienstag, gerne mehr davon — habe ich das erste Mal [Life is Strange](https://de.wikipedia.org/wiki/Life_Is_Strange) gespielt, bisher habe ich die erste Episode geschafft. Mir gefällt die Musik unglaublich gut, eigentlich könnte man das Spiel starten, im Hauptmenü verweilen und einfach nur der Musik lauschen. Aber dann würde man ihm Unrecht tun.

In dem Spiel hat man Zugriff auf eine Art Tagebuch von Max, der Hauptfigur, in dem diverse Informationen abrufbar sind, unter anderem gibt es Interessantes zu den Charakteren zu lesen. Auf der Seite, die [Warren beschreibt](https://vignette.wikia.nocookie.net/rememberme/images/2/22/Warren_Entry.png/revision/latest?cb=20150209230731), sind einige mathematische Gleichungen zu sehen, beginnend mit:

${x-1}/4 - 4/(x-1)=0$

Als ich das sah, war mein Interesse geweckt. Auch wenn ich Informatik studiert habe, war ich nie besonders gut in Mathe. Es hat mir meistens Spaß gemacht, aber ich war eben nie besonders gut. Statistik und Stochastik sind mir bis heute beispielsweise ein Rätsel. Ich hatte das Bedürfnis, die Gleichung aus dem Spiel zu lösen — das, was in dem Buch stand, konnte nicht stimmen. Also kramte ich in meinem Kopf in einer Kiste mit der Aufschrift „Mathe 10. Klasse“ und begann, die beiden Brüche auf einen Nenner bringen, in dem ich jeden Bruch mit dem Nenner des anderen erweiterte:

$((x-1)(x-1))/(4(x-1)) - (4*4)/((x-1)4) = 0 $

Danach ziehe ich beide Brüche auf einen Bruchstrich ...

$((x-1)(x-1)-16)/(4(x-1)) = 0$

... um anschliessend die zweite binomische Formale auszumultiplizieren

$(x^2-2x+1-16)/(4(x-1))=0$

Nun multipliziere ich beide Seiten der Gleichung mit $4(x-1)$, um den Bruch aufzulösen.

$x^2-2x+1-16=0i => x^2-2x-15=0$

Diese beiden Schritte hätte ich auch in umgekehrter Reihenfolge machen können.

Hört ihr das? Wir haben eine [quadratische Gleichung](https://de.wikipedia.org/wiki/Quadratische_Gleichung), die nach der [pq-Formel](https://de.wikipedia.org/wiki/Quadratische_Gleichung#L.C3.B6sungsformel_f.C3.BCr_die_Normalform_.28p-q-Formel.29) mit $p=-2, q=-15$ schreit.

Wir müssen noch überprüfen, ob die Diskriminante $D$ negativ ist: $D=p^2-4q; p=-2, q=-15 => D = 4-4*(-15) = 4+60=64$, passt also, her mit der _normalen_ pq-Formel.

Der Rest ist einsetzen und ausrechnen oder einen Taschenrechner bemühen:

$x_{1,2} = (-p)/2 ± sqrt{(p/2)^2-q}; p=-2, q=-15$

$x_{1,2} = 2/2 ± sqrt{(-2/2)^2+15}$

$x_{1,2} = 1 ± sqrt{(-1)^2+15}$

$x_{1,2} = 1 ± sqrt{16}$

$x_{1,2} = 1 ± 4$

$x_1 = 5, x_2 = -3$

$q.e.d.$

In die Ursprungsgleichung eingesetzt, ergeben sowohl $x_1$, als auch $x_2$ eine wahre Aussage. Diese Rechnung weicht ein bisschen von der aus dem Spiel ab. Da mir im Matheunterricht regelmässig Flüchtigkeits- und/oder Vorzeichenfehler unterlaufen sind, war ich immer noch skeptisch. Ich schoss mit Kanonen auf Spatzen und schmiss ein CAS an. Auch das bestätigte mir meine beiden Ergebnisse und ich war zufrieden.

![Screenshot vom CAS](/img/Life_is_strange_CAS.png)

Warum die Gleichung mit Rechenfehlern auf der Seite von Warren in Max' Tagebuch stehen? Keine Ahnung, aber vielleicht erfährt man das irgendwann in einer der anderen Episoden.
