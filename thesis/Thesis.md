# PRACA DYPLOMOWA INŻYNIERSKA
POLITECHNIKA WROCŁAWSKA  
WYDZIAŁ ELEKTRONIKI  
KIERUNEK: INFORMATYKA  
SPECJALNOŚĆ: SYSTEMY I SIECI KOMPUTEROWE  
Aplikacja mobilna na platformę Android umożliwiająca użytkowanie i uzupełnianie tworzonej społecznościowo bazy danych geoprzestrzennych
Mobile application for the Android platform facilitating use of and contribution to a crowdsourced geospatial database  
AUTOR: Bartosz Rodziewicz  
PROWADZĄCY PRACĘ: Dr inż. Paweł Trajdos, W4/K2  

## Spis treści
1. Wstęp
1. Opis koncepcji
1. Wybrane technologie
	1. Język
	1. Zewnętrzne biblioteki
	1. API
	1. Komunikacja z serwerem
	1. Środowisko deweloperskie
	1. Kontrola wersji
	1. System budowania
1. Dokumentacja i opis implementacji
1. Opis interfejsu użytkownika
1. Podsumowanie

Literatura  
<!--Indeks rycin/listingów-->

<!--(jezyk, zewnętrzne biblioteki, api (application programming interface), metoda komunikacji z serwerem, środowisko, kontrola wersji, system budowania)-->

## Wstęp
W dzisiejszych czasach praktycznie każdy posiada smartfon. Większość z nich jest wyposażona, najczęściej w stałe, połączenie z Internetem. Pozwoliło to na wykształcenie się na rynku wielu aplikacji, których celem jest pomoc użytkownikowi w znalezieniu konkretnych informacji, w tym również geolokalizacyjnych. Istnieje wiele aplikacji oferujących dostęp do map, ułatwiających znajdywanie firm, wyświetlających aktualne położenie autobusów komunikacji miejskiej czy umożliwiających zlokalizowanie publicznych toalet w okolicy.

Celem tej pracy było przygotowanie aplikacji na urządzenia z systemem Android umożliwiającej użytkownikom na łatwiejsze znajdywanie miejsc użyteczności publicznej, gdzie goście mają dostęp do energii elektrycznej, np. restauracji, w której można usiąść przy stoliku z laptopem i podłączyć się do prądu. Aplikacja miała być klientem do niezależnie rozwijanego serwera z bazą danych i oferować możliwość wyświetlania zebranych w niej danych oraz umożliwiać operowanie na nich w przystępny i szybki dla użytkownika sposób.

Program ten miał być pisany wykorzystując najlepsze wzorce projektowe oraz odpowiednią warstwę abstrakcji, tak by jego dalszy rozwój był łatwy, nawet dla innej osoby. Dodatkowo miało to umożliwić łatwą zmianę przechowywanych danych w bazie, jeśli w przyszłości byłaby taka konieczność bądź chciano by wykorzystać ten projekt do stworzenia aplikacji podobnego typu.

Rozdział 1 stanowi wstęp do problemu. Rozdział 2 bardziej szczegółowo opisuje koncepcję aplikacji, jej zastosowanie i to co zostało zrealizowane. Rozdział 3 przedstawia technologie wybrane do stworzenia programu. Rozdział 4 opisuje aspekty implementacji kodu oraz stanowi jego dokumentację. Rozdział 5 został wykorzystany do prezentacji i opisania interfejsu użytkownika aplikacji. W rozdziale 6 zamieszono podsumowanie pracy. Na końcu dokumentu znajdują się odwołania do literatury, z której korzystano w trakcie przygotowywania tej pracy.

## Opis koncepcji
Pomysł na aplikację powstał obserwując inne aplikacje użytkowe, jak te wymienione we wstępie. Głównie była ona bazowana na dwóch aplikacjach - aplikacji do wyszukiwania publicznych toalet (Flush) oraz publicznych sieci Wi-Fi (WiFi Map). W obu przypadkach głównym punktem wokół kręci się cała idea jest mapa z społecznie zbieranymi danymi przez użytkowników, którzy w założeniu sami dbają o poprawność i aktualność danych.

Tutaj też głównym miejscem miał być widok mapy umożliwiający w przyjazny dla użytkownika sposób przeglądanie danych. Dodatkowo dane miały być możliwe do wyświetlenia w kwestii listy, sortowanej rosnąco odległością od użytkownika.

Aby zmniejszyć obciążenie urządzenia oraz umożliwić pracę na dużej bazie danych klient miał pobierać punkty znajdujące się blisko lokalizacji użytkownika oraz te znajdujące się w zakresie widoku mapy, przeglądanej przez użytkownika. Z uwagi, że aplikacja prezentuje rzadko zmieniające się dane zmniejszenie zapytań do serwera miało być wykorzystane przez zapewnienie metody na buforowanie wyników zapytań na urządzeniu na jakiś czas, bądź do sytuacji gdy aplikacja przekroczy dozwolony rozmiar pamięci buforu. Aplikacja miała również oferować ręczne sterowanie, który obszar będzie zapisany lokalnie na urządzeniu, aby umożliwić dostęp do danych w trybie offline.

Baza miała przechowywać podstawowe dane o miejscu, jak jego lokalizacja, czy nazwa oraz bardziej specyficzne dla tego zastosowania dane, jak ilość publicznie dostępnych gniazdek, czy szkic poglądowy z zaznaczonymi gniazdkami na planie budynku (co np. w przypadku restauracji ułatwiło by klientowi wybranie odpowiedniego stolika, bez konieczności pytania obsługi). Planowana była też szersza integracja z Google Maps, aby miejsca w aplikacji można było przypisać do punktów POI (_Points of interests_) znajdujących się w tym serwisie.

W aplikacji miał być dostępny widok szczegółowy danego miejsca umożliwiający podejrzenie dodatkowych informacji o danym miejscu oraz historię ostatnich modyfikacji tego miejsca. Widok dodawania nowego miejsca miał umożliwić podanie wszystkich szczegółów dotyczących tego miejsca oraz miał ułatwiać naszkicowanie planu budynku ręcznie bądź umożliwić wgranie zdjęcia ręcznie wykonanego planu.

Klient miał oczywiście pozwalać również na edycje już istniejących punktów, jak i usuwanie błędnie stworzonych, bądź już nie istniejących. Planowane było też wprowadzenie kont użytkownika, aby śledzić kto dokonuje modyfikacji, oraz zablokować tych, którzy pogarszają jakość danych w aplikacji.

Do działania aplikacja potrzebowała by również internetowego serwera z bazą danych, jednak nie stanowi to przedmiotu tej pracy. Serwer miał być napisany w sposób umożliwiający tej aplikacji na połączenie się z nim oraz wykorzystując odpowiednią warstwę abstrakcji, by w przyszłości było możliwe stworzenie klientów na inne platformy (klient webowy, na system iOS, itp.)

Oczywiście powyższy opis konceptu przekracza to co było planowane w zakresie tej pracy, oraz przekracza to co udało się zrealizować. W trakcie realizacji pracy udało się stworzyć następujące funkcjonalności:

* Możliwość przeglądania punktów w formie mapy i listy
* Możliwość dodawania, edycji i usuwania punktów
* Możliwość przeszukiwania bazy danych
* Połączenie z serwerem i synchronizacja danych
* Zapisywanie danych z serwera na urządzeniu, aby zminimalizować ilość zapytań

Jest to całkiem solidny zakres podstawowych funkcji umożliwiający na używanie aplikacji w założonych celach i jej dalszy rozwój.

## Wybrane technologie
### Platforma
Z punktu widzenia projektu wybór platformy mobilnej był jedynym słusznym wyborem, ponieważ aplikacja dostarcza informacje, które użytkownikom są potrzebne gdy są w biegu, a nie siedzą w zaciszu swojego domu przed komputerem. Na rynku platform mobilnych aktualnie istnieje jedynie dwójka graczy, czyli Android od firmy Google, oraz iOS od firmy Apple, mając udziały w rynku odpowiednio 77% i 22%. Z tych danych wychodzi jasny obraz, że aby dotrzeć do jak największej liczby użytkowników należy wybrać platformę Android. Dodatkowym aspektem skłaniającym do wyboru tej platformy był fakt posiadania przez autora pracy urządzeń działających pod kontrolą tego systemu.

### Język programowania
Wybór platformy w dużej mierze uwarunkował wybór języka programowania. Istnieją oczywiście różne metody by pisać na Androida w wielu różnych językach (np. COBOL), jednak oficjalnie wspierane są następujące języki:
* Kotlin - nowy język, działający w JVM i będący w pełni interoperacyjny z Javą; od niedawna zalecany jako główny język dla nowych aplikacji przez Google
* Java - standardowy język, w którym od dawna powstają aplikację na tą platformę
* C++ - istnieje możliwość wykorzystania bibliotek napisanych w C++ za pomocą NDK udostępnionego przez Google, przydatne przy oprogramowaniu dla którego kluczowa jest wydajność, czyli np. gier
* HTML+CSS+JS - częściowo wspierane jest tworzenie nowoczesnych stron internetowych zachowujących się jako aplikacje wykorzystując PWA

Taka sytuacja sprowadza się do wyboru pomiędzy dwoma językami: Kotlinem i Javą. Mimo pewnego wcześniejszego doświadczenia autora pracy z Javą wybrany został język Kotlin, który jest traktowany przez Google jako przyszłość dla tej platformy, aby ułatwić w przyszłości rozwój tej aplikacji i poznać nieznaną dotąd dla siebie technologię.

### Zewnętrzne biblioteki















# Dokumentacja
* https://gs.statcounter.com/os-market-share/mobile/worldwide (@Platforma)
