# Analiza sentimenta tvitova na ruskom jeziku
Projekat iz predmeta Osnove računarske inteligencije

## Potreban softver za pokretanje projekta
- Za ovaj projekat nije potrebno instalirati nikakav softver.
Sve što treba uraditi jeste otvoriti priloženi jupyter fajl u google colab okruženju i pokrenuti postojeće ćelije.
- Ćelije je potrebno pokretati onim redom kojim su navedene

## O radu
- Rad je osmišljen da prouči algoritme za analizu sentimenta kratkih tekstova kao što su tvitovi
- Implementiran je algoritam neuronske mreže sa vežbi i neuronske mreže koje nudi tensor flow 
- Zadatak se svodi na predprocesiranje tvitova, obučavanje neuronske mreže i testiranje na nepoznatim tvitovima

## Predprocesiranje
- Tvitovi se učitavaju iz priloženih csv fajlova. positive.csv sadrži pozitivne tvitove, a negative.csv negativne
- Kako sesija ne bi pukla zbog velike količine podataka, učitava se samo deo tvitova: 50,000 pozitivnih i 50,000 negativnih
- Ucitani tvitovi prolaze kroz predprocesiranje, koje uključuje tokenizaciju, izbacivanje karaktera koji nisu ruska ćirilica, stemovanje (svodjenje reči na osnovni oblik).
- Pronađene reči se smeštaju u vokabular i pridružuje im se broj koji označava koliko puta se javljaju u podacima.
- Uzima se 5000 najčešćih reči
- Obrađene su dve metode pripremanja podataka za obučavanje:
    - Tvit se pretvara u vektor nula i jedinica, gde nula označava da se odgovarajuća reč ne nalazi u tvitu, a jedinica suprotno. Svi vektori su dužine 5000
    - Tvit se pretvara u vektor gde se svaka reč zamenjuje brojem koji je pridružen toj reči u vokabularu. Vektori su dužine broja reči u tvitu, pa je potrebno sve tvitove svesti na istu dužinu - dodati padding ili oduzeti višak reči
    
## Treniranje
- Nakon predprocesiranja, bilduje se model neuronske mreže. Dodaju joj se unutrašnji slojevi, a ulaz predstavlja tvit pretvoren u vektor. 
- Određuju se hiperparametri, skup za treniranje, testiranje, kao i labele koje predstavljaju stvaran sentiment odgovarajućeg tvita
- Na osnovu ovih parametara, vrši se obučavanje mreže na obučavajućem skupu, validacija na delu obučavajućeg skupa i zatim testiranje na testirajućem skupu

## Testiranje na mreži nepoznatim tvitovima
- Nakon obučavanja sledi real life testiranje
- Tvitovi se upisuju u listu i za svaki tvit se vrši predikcija pripadnosti određenoj klasi
