# CTF Collection Vol.2
## Zadanie

Welcome, welcome and welcome to another CTF collection. This is the second installment of the CTF collection series. For your information, the second serious focuses on the web-based challenge. There are a total of 20 easter eggs a.k.a flags can be found within the box. Let see how good is your CTF skill.

Now, deploy the machine and collect the eggs!

Warning: The challenge contains seizure images and background. If you feeling uncomfortable, try removing the background on style tag.

Note: All the challenges flag are formatted as THM{flag}, unless stated otherwise

## Kroki

Mamy stronę internetową z wieloma easter eggami, znajdzmy je wszystkie!

#1

![alt text](image.png)

Seems like user-agent manipulation, let's do it! 

*Easter 1*

![alt text](image-5.png)

Wchodzimy na `/robots.txt`, znajdujemy na końcu ciąg dwucyfrowych liczb szesnastkowych, wklejamy go w cyberchef'a i używamy From Hex, pierwsza flaga jest nasza!

![alt text](image-6.png)

*Easter 2*

Na `/robots.txt` mamy też scieżke w polu Disallow w base64, trik polega na tym że tekst ten jest czterokrotnie zakodowany base64. W tym celu czterokrotnie go dekodujemy i otrzymujemy ścieżkę 'DesKel_secret_base'.

![alt text](image-22.png)

Po przejściu na znalezioną podstronę, pod zdjęciem znajdziemy flagę zapisaną białym kolorem.

![alt text](image-23.png)

*Easter 3*

Wchodzimy na `/login`, otwieramy source code, tam znajdziemy pole hidden, gdy je rozwiniemy ukaże nam się flaga.

![alt text](image-21.png)

*Easter 4*

Strona `/login/` ma jeszcze jedną podatność, jest odkryta na atak SQL injection time-based, po przeprowadzeniu testów używając sqlmap, komendą która dała mi odpowiedź było: 

`sqlmap -u "http://10.10.143.77/login/" --data="password=pass&username=user" -D THM_f0und_m3 -T nothing_inside -C Easter_4 --dump`

![alt text](image-33.png)

*Easter 5*

Znów wykorzystujemy tę samą podatność, tym razem przeglądamy tabelę users, używamy do tego poniższej komendy:
`sqlmap -u "http://10.10.143.77/login/" --data="password=pass&username=user" -D THM_f0und_m3 -T user -C username,password --dump`

W rezultacie otrzymujemy w wyniku hash, który dekodujemy używając crackstation.net

![alt text](image-34.png)

Następnie logujemy się na `/login/` używając DesKel jako username, i odczytanego hasła jako password, w rezultacie otrzymujemy flagę!

![alt text](image-35.png)

*Easter 6*

Na stronie używając Burp Suite musimy kliknąc pod polem jednokrotnego wyboru i w odpowiedzi bedzie szósta flaga :)

![alt text](image-7.png)

*Easter 7*

Gdy podejrzymy sobie cookies wysyłane przez nas do strony widzimy że zawierają jeden parametr `invited` ustawiony na 0.

![alt text](image-30.png)

Gdy zmienimy tę wartośc na 1 i wyślemy zapytanie ponownie to otrzymamy flagę nr. 7 :)

![alt text](image-31.png)

*Easter 8*

W tym zadaniu musimy zmienić user-agent na "Mozilla/5.0 (iPhone; CPU iPhone OS 13_1_2 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.1 Mobile/15E148 Safari/604.1", żeby strona myślała że logujemy się z konkretnego iPhone z konkretną wersją. Po tym wysyłamy request ze spreparowanym user-agent i otrzymujemy flagę.

![alt text](image-32.png)

*Easter 9*

Kiedy w Burp Suite przejdziemy do `/ready/` to widzimy, że zanim pokaże się Easter 13, to pokazuje się Easter 9:

![alt text](image-36.png)

*Easter 10*

Klikając w baner o darmowej subskrypcji przenosi na do `/free_sub/`.

![alt text](image-28.png)

Aby spełnić powyższy warunek musimy dodać nagłówek `Referer: tryhackme.com` i powtórzyć request w Burp Suite.

![alt text](image-29.png)

*Easter 11*

Musimy znaleźć single selecta "select dinner" i wysłać request podmieniając nasz wybór na "egg", w rezultacie otrzymamy flagę!

*Easter 12*

W sources znajdziemy plik jquery-9.1.2.js, który podszywa się pod plik biblioteki jquery, zawiera ją funkcję `ahem()`, która wyświetla dwunastą flagę w konsoli.

![alt text](image-24.png)

![alt text](image-25.png)


*Easter 13*

Klikamy przycisk:

![alt text](image-3.png)

Kolejna flaga jest nasza!

![alt text](image-4.png)

*Easter 14*

![alt text](image-1.png)

Przeglądając kod źródłowy znalazłem w komentarzu HTML-owy odnośnik do zdjęcia zakodowanego w base64, usuńmy go z komentarza aby wyświetlić zdjęcie!

Flaga ukaże się niżej.

![alt text](image-2.png)

*Easter 15*

Na stronie głównej znajdziemy odnośnik o tytule **Game 1**, który przenosi nas do `/game1`, przechodzimy tam i jest tam prosta gra ze wskazówką, gra koduje wprowadzone znaki według określonego klucza, musimy więc poznać to kodowanie i wpisać odkodowaną wskazówkę.

![alt text](image-8.png)

Po wprowadzeniu 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz' otrzymujemy pełen klucz ponieważ pole przyjmuje TYLKO litery.

![alt text](image-9.png)

Po zmapowaniu okazuje się że w hint mamy zakodowane słowo 'GameOver', wpisujemy je i flaga jest nasza!

![alt text](image-10.png)

*Easter 16*

Mamy również odnośnik **Game 2**, po kliknięciu analogicznie przenosi nas do `/game2`, gra wymaga od nas kliknięcia 3 przycisków jednocześnie, początkowo próbowałem napisać skrypt JS pobierający przyciski po nazwach i klikający je niestety to nie pomogło.

![alt text](image-11.png)

Po sprawdzeniu request w Burp Suite, okazuje się, że kliknięcie powoduje przekazanie w requeście informacji który przycisk kliknęliśmy.

![alt text](image-12.png)

Spróbujmy przekonać stronę że kliknęliśmy wszystkie 3 na raz i prześlijmy w parametrach informację o trzech przyciskach.

Podziałało!

![alt text](image-13.png)

*Easter 17*

Znajdujemy przycisk 'Malfunction button', początkowo wywołuje on funkcję nyan(), która nie istnieje. Pod spodem jednak w polu script, mamy funkcje catz(), która wyświetla nam pod spodem ciąg binarny.

![alt text](image-16.png)

![alt text](image-17.png)

Ten ciąg kopiujemy i przeliczamy na system 16-stkowy, następnie otrzymany wynik tłumaczymy z hex na ASCII i flaga jest nasza!

![alt text](image-18.png)

*Easter 18*

![alt text](image-26.png)

Musimy wysłać zmodyfikowany request z nagłówkiem `egg: YES`, to wyświetli naszą flagę w odpowiedzi!

![alt text](image-27.png)

*Easter 19*

Trochę niżej widzimy w kodzie HTML, dziwnie cienki obraz:

![alt text](image-19.png)

Zmieniamy jego height na wyższą wartość i otrzymujemy flagę nr. 19 :)

![alt text](image-20.png)


*Easter 20*

Na stronie mamy taki napis, spróbujmy przesłać POST request z ustawionymi podanymi parametrami!

![alt text](image-14.png)

Ostatnia flaga jest nasza!

![alt text](image-15.png)

## Flaga

Flaga: ****