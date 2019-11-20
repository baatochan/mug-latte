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

W ramach pracy zrealizowano następujące funkcjonalności:

* Możliwość przeglądania punktów w formie mapy i listy
* Możliwość dodawania, edycji i usuwania punktów
* Możliwość przeszukiwania bazy danych
* Połączenie z serwerem i synchronizacja danych
* Zapisywanie danych z serwera na urządzeniu, aby zminimalizować ilość zapytań

Jest to całkiem solidny zakres podstawowych funkcji umożliwiający na używanie aplikacji w założonych celach i jej dalszy rozwój.

Rozdział 1 stanowi wstęp do problemu i zakresu pracy. Rozdział 2 bardziej szczegółowo opisuje koncepcję aplikacji i jej użycie. Rozdział 3 przedstawia technologie wybrane do stworzenia programu. Rozdział 4 opisuje aspekty implementacji kodu oraz stanowi jego dokumentację. Rozdział 5 został wykorzystany do prezentacji i opisania interfejsu użytkownika aplikacji. W rozdziale 6 zamieszono podsumowanie pracy. Na końcu dokumentu znajdują się odwołania do literatury, z której korzystano w trakcie przygotowywania tej pracy.

## Opis koncepcji
