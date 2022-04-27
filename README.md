# php-exercises

# Podstawy PHP-notatki z lektury
## Znaczniki, zmienne i typy danych
## Umieszczanie skryptów w kodzie HTML

Skrypty PHP są wykonywane po stronie serwera, jednakże mogą być umieszczane w bezpośrednio w kodzie HTML. Służą do tego
znaczniki:

- kanoniczne
- typu SGML
- typu ASP
- skryptów HTML

### Znaczniki kanoniczne (klasyczne)

Znaczniki kanoniczne to standardowe znaczniki PHP i mają postać:

```php
<?php
  // kod skryptu
?>
```

Znaczniki te są rozpoznawane zawsze niezależnie od opcji włączonych w pliku konfiguracyjnym i są zalecane. Można opuścić
znacznik końcowy, jeśli mamy do czynienia li tylko z kodem php.

### Znaczniki HTML

Postać znaczników HTML:

```html
<script language="php">
// kod php
</script>
```

Postać ta została usunięta w wersji PHP 7, zatem począwszy od tej wersji, nie można, jej stosować.

## Proste wyświetlanie danych

Jeśli chcemy coś wysłać do przegladarki(potocznie wyświetlić) lub wyświetlić w konsoli stosujemy instrukcję `echo`
Ciąg znaków składający się na fragment kodu HTML wyślemy:

```php
echo "<h2 style='text-align:center'>Witamy na stronie!<h2>";
```

Można przesłać obliczoną wartość wyrażenia np.:

```php
echo 2 + 2 * 3; // 8
```

Wyrażenie możemy ująć w znaczniki HTML:

```php
<?php
echo "<b><i>";
echo 2 + 3 * 4;
echo "</i></b>"
?>
```

Lub tak:

```php
<b><i>
<?php
echo 2 + 3 * 4;
?>
</i></b>
```

Zamiast pisać:

```php
<?php echo wyrażenie ?>
```

można zastosować zapis:

```php
<?=wyrażenie ?>
```

Zatem przykład pokazany wyżej mógłby wygladać tak:

```php
<b><i>
<?=2 + 3 * 4 ?>
</i></b>
```

## Typy danych

W PHP występuje osiem podstawowych typów danych, które można podzielić na trzy różne rodzaje:

- skalarne
- złożone
- specjalne

### Typy skalarne

**Typy skalarne** (ang. scalar types) to inaczej **typy proste** (ang. primitive types). Dzielą się one na cztery
rodzaje:

- boolean
- integer
- float
- string

#### Typ boolean

Jest to typ logiczny, który może przyjmować tylko dwie wartości: true(prawda) i false(fałsz). Jest on wykorzystywany
przy konstruowaniu wyrażeń logicznych oraz sprawdzaniu warunków.

#### Typ integer

Jest to typ całkowitoliczbowy. Liczby te moagą być zapisane w następujących formatach:

- dziesiętnym
- ósemkowym (oktalnym) - liczbę ósemkową porzedzamy znakiem 0, np. 024 (20 dziesiętnie)
- szesnastkowym (heksadecymalnym) - liczbę szesnasnastkową poprzedzamy znakami 0x, np. 0xff (255 dziesiętnie)
- binarnym - liczbę dwójkową poprzedzamy zakami 0b, np. 0b0101 (5 dziesiętnie)

Maksymalny zakres typu całkowitego, zależy od platformy systemowo-sprzętowej. Dla systemów 32-bitowych typowo jest to
32-bitowa liczba ze znakiem, czyli zakres wartości można przedstawić od -2<sup>31</sup> do 2<sup>31</sup> - 1. Dla
systemów 64-bitowych jest to 64-bitowa liczba ze znakiem czyli zakres można przedstawić od -2<sup>63</sup> do 2<sup>
63</sup> - 1.

W przypadku przekroczenia zakresu wartość jest konwertowana na typ float.

Dla danego systemu można sprawdzić jaki jest rozmiar typu integer:

```php
echo PHP_INT_SIZE;
```

Maksymalną wartość odczytamy:

```php
echo PHP_INT_MAX;
```

#### Typ float

Typ float reprezentuje liczby rzeczywiste (zmiennoprzecinkowe). Zakres zależy od platformy systemowo-sprzętowej z reguły
są to wartości od -1,8&times;10<sup>308</sup> do 1.8&times;10<sup>308</sup>.

Typowy jest zapis z kropką. Można stosować zapis wykładniczy:

X.YeZ <=> X.Y&times;10<sup>z</sup>

lub taki:

X.YEZ

#### Typ string

Typ string to typ tekstowy zapamiętujący ciąg (łańcuch) znaków. Maksymalna długość ciągu to 2<sup>31</sup> -1 bajtów.
Ponieważ pojedynczy znak odpowiada zawsze jednemu bajtowi (nie występuje rozróżnienie między ciągami znakowymi bajtowymi

- napisy to ciągi bajtów, nie bezpośredniej obsługi standardu Unicode.

Łańcuch znaków można, utworzyć używając:

- apostrofów
- cudzysłowie
- składni heredoc
- składni nowdoc

##### Znaki apostrofu

Ciąg znaków ujęty w apostrofy nie jest interpretowany przez kompilator PHP, tzn że jeśli umieścimy w nich nazwę zmiennej
to nie zostanie ona zamieniona na wartość, którą reprezentuje.

```php
$var = 56;
echo '$var' . "<br>"; // $var
echo "$var" . "<br>"; // 56
```

##### Znaki cudzysłowu

Ciąg znaków ujęty w cudzysłów jest przetwarzany przez interpreter PHP wg zasad:

- jeśli zmienna jest typu znakowego, to zawarty w niej ciąg znaków jest wklejany do ciągu bieżącego;
- jeśli zmienna jest innego typu, następuje jej konwersja na typ string, a następnie jest wklejana do ciągu bieżącego;
- jeśli zmienna nie zawiera żadnej wartości, jest traktowana jak pusty ciąg znaków.

Dzięki temu, że ciagi ujęte w cudzysłów są interpretowane przez PHP, można stosować w nich sekwencje znaków specjalnych.

**Tabela** Kodowanie znaków specjalnych

| Sekwencje znaków | Znaczenie                                                           | Kod znaku |
| ---------------- | ------------------------------------------------------------------- | --------- |
| \t               | Tabulator poziomy (ang. _horizontal tab_)                           | 09 (0x09) |
| \n               | Nowa linia (ang. _new line_)                                        | 10 (0x0A) |
| \v               | Tabulator poziomy (ang. _vertical tab_)                             | 11 (0x0B) |
| \f               | Przewinięcie (wysunięcie) strony (ang. _form feed_)                 | 12 (0x0C) |
| \r               | Powrót karetki (powrót na początek wiersza, ang. _carriage return_) | 13 (0x0D) |
| \e               | _Escape_                                                            | 27 (0x1B) |
| \\\              | Lewy ukośnik (ang. _backslash_)                                     | 92 (0x5C) |
| \\$              | Znak dolara                                                         | 36 (0x24) |
| \\"              | Znak cudzysłowu                                                     | 34 (0x22) |

Jeśli liczbę poprzedzimy ukośnikiem zostanie potraktowana jak liczba ósemkowa.

Jeśli sekwencją \x (np. \xf \61) jako liczba szesnastkowa.

Do dyspozycji jest tylko 256 wartości (od 0 do 255) to też liczba ósemkowa może zawierać tylko trzy cyfry a szesnastkowa
dwie.

Sekwencje specjalne to \u{kod}, gdzie kod oznacza znak w formacie Unicode 16. Np. \u{017c} oznacza małą literę ż

```php
echo "Bez interpretacji sekwencji specjalnych: ";
echo  '\x61\x62\x63\x64\$\144\143\142\141';
//Bez interpretacji sekwencji specjalnych: \x61\x62\x63\x64\$\144\143\142\141

echo "Z interpretacją sekwencji specjalnych: ";
echo  "\x61\x62\x63\x64\$\144\143\142\141";
// Z interpretacją sekwencji specjalnych: abcd$dcba

echo "Z interpretacją sekwencji specjalnych Unicode: ";
echo "\u{017c}\u{00f3}\u{0142}\u{0107}";
// Z interpretacją sekwencji specjalnych Unicode: żółć
```

##### Składnia heredoc

Łańcych znakowy rozpoczyna się od sekwencji `<<<`, po której następuje identyfikator. Ten sam identyfikator powinien
sygnalizować koniec łańcucha. Linia kończąca może zawierać tylko indentyfikator i średnik.

```php
$caption = <<<idcaption
  Tu zaczyna się napis
  idcaption;

  echo $caption;
```

##### Składnia nowdoc

```php 
 $captionOne = <<<'idcaptionOne'
 Tu zaczyna się napis w składni 
 nowdoc
 idcaptionOne;
```

Poniższy przykład pokazuje różnicę między składnią heredoc a nowdoc. Ta pierwsza jest przetwarzana przez interpreter PHP
a ta druga nie.

```php
$num1 = 2;
$num2 = 3;

$result = $num1 + $num2;

$suma = <<<idsuma
$num1 + $num2 = $result
idsuma;

echo $suma; // 2 + 3 = 5

$suma = <<<'idsuma'
$num1 + $num2 = $result
idsuma;

echo $suma; // $num1 + $num2 = $result
```

### Typy złożone

Typy złożone dzielą się na:

* typ array (tablicowy)
* typ object (obiektowy)

Tablice oraz obiekty omówione w odpowiednich działach.

### Typy specjalne

Typy specjalne dzielą się na:

* typ resource
* typ null

#### Typ resource

Typ `resource` jest typem specjalnym wskazującym, że zmienna przechowuje odwołanie do zasobu zewnętrznego utworzonego za
pomocą specjalnej funkcji. Tu ten typ nie będzie omawiany.

#### Typ null

Typ `null` jest typem specjalnym informującym, że dana zmienna nie przechowuje żadnej wartości. Jeżeli chcemy ustawić
zmienna na `null`, piszemy:

```php
$variable = null;
```

Wielkość liter nie ma tu znaczenia. Prawidłowe są zatem zapisy: `null` `NULL` czy `Null`.

## Zmienne

Zmienna to konstrukcja programistyczna, która pozwala na przechowywanie danych posiadająca nazwę i typ. Nazwa to
jednoznaczny identyfikator, dzięki któremu możemy się odwołać do zmiennej w kodzie skryptu. Typ natomiast określa
jakiego rodzaju wartości zmienna może przechowywać.

Zmienną tworzymy, pisząc znak dolara $ a po nim nazwę zmiennej:

```php
$variableName = "variable";
```

Nazwa musi zaczynać od litery (także znaki o kodach od 127 do 255) lub znaku podkreślenia i może zawierać tylko litery,
cyfry i znaki podkreślenia.

Rozróżniane są małe i duże litery.

Praktyką jest stosowanie nazw angielskich.

### Tworzenie zmiennych

W PHP nie ma wymogu deklarowania zmiennej ani określania jej typu. Czynności te są wykonywane automatycznie.

Wartość przypisana zmiennej definiuje jednocześnie typ zmiennej. Jeśli przypiszemy zmiennej wartość typu `integer` to
typem tej zmiennej staje się `integer`:

```php
$number = 100;
```

jeśli przypiszemy typ `float` to typem zmiennej jest `float`

```php
$real = 1.55;
```

jeśli `string` to typem zmiennej staje się `string`:

```php
$caption = 'To jest przykładowy tekst';
```

Typ zmiennej może się zmieniać w trakcie działania skryptu.

```php
$variable = 100;
echo $variable; // 1000
    
$variable = 1.5;
echo $variable; // 1.5

$variable = "Przykładowy napis.";
echo $variable; // Przykładowy napis
```

### Jak wykryć typ zmiennej

Ponieważ typ zmiennej w trakcie działania skryptu może uleć zmianie, może zaistnieć sytuacja, w której będzie trzeba
sprawdzić typ zmiennej. Można to zrobić za pomocą jeden z funkcji zaprezentowanych w tabeli poniżej.

**Tabela** Funkcje kontrolujące typ zmiennej

| Nazwa funkcji   | Opis                                                                                          | Uwagi                              |
| --------------- | --------------------------------------------------------------------------------------------- | ---------------------------------- |
| `gettype()`     | Zwraca ciąg znaków określający typ zmiennej lub<br> ciąg `unknown`, gdy typ jest nieokreślony | Funkcja dostępna od PHP 3          |
| `is_array`      | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `array`           | j.w.                               |
| `is_bool()`     | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `boolean`         | Funkcja dostępna od PHP 4          |
| `is_double()`   | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `float`           | Jest to alias do funkcji is_float. |
| `is_float()`    | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `float`           | Funkcja dostępna od PHP 3          |
| `is_int()`      | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `integer`         | Funkcja dostępna od PHP 3          |
| `is_integer()`  | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `integer`         | Alias dla is_int                   |
| `is_long()`     | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `integer`         | Alias dla is_int                   |
| `is_null()`     | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `null`            | Funkcja dostępna od PHP 4.0.4      |
| `is_object()`   | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `object`          | Funkcja dostępna od PHP 3          |
| `is_real()`     | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `float`           | Alias dla is_float                 |
| `is_resource()` | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `resource`        | Funkcja dostępna od PHP 4          |
| `is_scalar()`   | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `skalarnego`      | Funkcja dostępna od PHP 4.0.5      |
| `is_string()`   | Zwraca wartość `true`, jeśli zmienna przekazana<br> jako argument jest typu `string`          | Funkcja dostępna od PHP 3          |

**Przykład działania funkcji gettype**

```php
$variable = 100;
echo "Wartość zmiennej = $variable";  //Wartość zmiennej = 100
echo "Typ zmiennej = " . gettype($variable);   //Typ zmiennej = integer

$variable = 1.5;
echo "Wartość zmiennej = $variable";  // Wartość zmiennej = 1.5
echo "Typ zmiennej = " . gettype($variable);  // Typ zmiennej = double

$variable = "Przykładowy napis.";  
echo "Wartość zmiennej = $variable"; // Wartość zmiennej = Przykładowy napis.
echo "Typ zmiennej = " . gettype($variable); // Typ zmiennej = string
```

Funkcja `var_dump($variable)` wyświetla w konsoli i przeglądarce wartość i typ zmiennej.

### Deklaracja typów zmiennej

PHP należy do języków o słabym typowaniu. To oznacza, że *typ* zmiennej nie musi być zadeklarowany przed jej użyciem, a
przy odwoływaniu się do tej zmiennej PHP zawsze potraktuje ją jako zmienną takiego typu, który wynika z kontekstu jej
zastosowania.

Istnieje np. możliwość przypisania do zmiennej długiej wielocyfrowej liczby i odczytania tylko n-tej jej cyfry przy
założeniu, że nie jest to liczba, lecz łańcuch tekstowy.

```php
<?php
$number = 23457 * 45678;

echo "<p>$number<br><p/>";

echo substr($number, 4, 1); 
```

Analogicznie może wyglądać zamiana łańcucha na liczbę i temu podobne operacje.

```php
// Kolejny przykład słabego typowania
echo "<br><br>";
$pi = "3.1415927";
$radius = 5;
echo $pi * ($radius * $radius);
```

W praktyce nie trzeba się zanadto przejmować deklarowaniem typów zmiennych. Wystarczy przypisywać im logiczne wartości,
a PHP w razie potrzeby dokona ich konwersji. Gdy będzie potrzeba skorzystania z wartości tych zmiennych, należy się po
prostu do nich odwołać (np. za pomocą instrukcji echo).

### Deklaracje zmiennych typu skalarnego

PHP 7 dodał deklarację dla typów skalarnych za pomocą słów kluczowych:

* `string` &mdash; dla łańcuchów znaków,
* `int` &mdash; dla liczb całkowitych,
* `float` &mdash; dla liczb zmiennoprzecinkowych,
* `boolean`

//TODO Dodano w poprzednich wersjach deklaracje dla klas, interfejsów, tablic i typu callable.

Sprawdzanie typów dostępne jest w dwóch wersjach:

1. Domyślnym `coercive` &mdash; dopuszczającym rzutowanie.
2. Dokładnym `strict` &mdash; dopuszczającym tylko dokładny typ

Sprawdzanie typów konfiguruje się dla każdego pliku osobno, w celu odblokowania trybu strict należy w na samej górze
pliku umieścić linię:

```php
<?php
declare(strict_types=1);
```

Gdy dopasowanie typu nie powiedzie się, zostanie rzucony wyjątek TypeError, co także jest nowością wprowadzoną w PHP7.

```php
<?php
declare(strict_types=1);

function multiply(float $x, float $y): float
{
    return $x * $y;
}

function add(int $x, int $y): int
{
    return $x + $y;
}

var_dump(multiply(2, 3.5)); // float(7)
//var_dump(add('2', 3)); // Fatal error: Uncaught TypeError: Argument 1 passed to add() must be of the type integer, 
string given...
```

Więcej przeczytać można w [RFC: Scalar Type Declarations](https://wiki.php.net/rfc/scalar_type_hints_v5)

### Dobre praktyki przy stosowaniu zmiennych

Refactoring kodu &mdash; ulepszanie kodu, poprawianie jego jakości.

* stosujemy opisowe nazwy zmiennych,
* nazwy zmiennych tworzymy w języku angielskim.
* dla nazw wieloczłonowych stosujemy notację wielbłądzią &mdash; camelCase (ang. *camel case*), która obecnie stała się
  niejako standardem.

### Zmienne superglobalne

W PHP istnieje zestaw zmiennych nazwanych **superglobalnymi** (ang. *superglobals*), które są dostępne w każdej części
skryptu. Większość z nich to tablice, pozwalające na uzyskanie informacji konfiguracyjnych oraz związanych z bieżącym
wywołaniem skryptu.

#### $_GLOBALS

Tablica zawierająca odniesienie do każdej zmiennej globalnej zdefiniowanej przez użytkownika. Kluczami są nazwy zmiennej
a wartościami wartości zmiennych

#### $_SERVER

Tablica zawierająca informacje ustawiane przez serwer WWW. Np. adres IP, port, wartość nagłówków HTTP.

#### $_GET

Tablica zawiera dane przekazane do serwera WWW za pomocą metody GET.

#### $_POST

Tablica zawiera dane przekazane do serwera za pomocą metody POST.

#### $_COOKIE

Tablica zawiera `cookies` przekazane z serwera WWW.

#### $_FILES

Tablica zawierająca elementy przekazane do skryptu za pomocą metody POST pod czas przesyłania plików do serwera.

#### $_ENV

Tablica zawierająca wartości zmiennych środowiskowych przekazanych z systemu, na którym działa PHP.

#### $_REQUEST

Tablica asocjacyjna zawierająca dane z $_GET, $_POST i $_COOKIE

#### $_SESSION

Tablica asocjacyjna zawierająca dane związane zbieżącą sesją.

## Stałe

**Stała** (ang. *constant*) jest konstrukcją, która nie może zmieniać swojej wartości podczas działania skryptu.

Zwyczajowo stałe pisze się dużymi literami. Gdy nazwa stałej jest wieloczłonowa, stosujemy konwencję (już teraz prawie
standard) snake_case (ang. *snake case*)

Stałych nie wolno poprzedzać znakiem $. Stałej musimy przypisać wartość przy jej deklarowaniu.

Stałe definiowane są za pomocą funkcji define:

```
define('constantName', constantValue);
```

Np.:

```php
define('PI', 3.14159265);
```

Można definiować stałą za pomocą słowa kluczowego `const`:

```php
const EULER_NUMBER = 2.7183;
```

Pamiętajmy, stałej możemy przypisać wartość tylko raz przy jej tworzeniu.

### Stałe predefined

W PHP istnieją **stałe predefined** (ang. *predefined constants*) nazywane **stałymi magicznymi** (ang. *magic
constants*)

**Tabela**. Wybrane stałe predefiniowane

| Nazwa stałej           | Znaczenie                                                                    |
| ---------------------- | ---------------------------------------------------------------------------- |
| `PHP_VERSION`          | Wersja PHP                                                                   |
| `PHP.OS`               | Wersja systemu operacyjnego                                                  |
| `DEFAULT_INCLUDE_PATH` | Ścieżka dostępu do plików dołączanych za pomocą instrukcji include i require |
| `PHP_EXTENSION_DIR`    | Katalog z bibliotekami PHP                                                   |
| `PHP_BINDIR`           | Katalog z plikami wykonywalnymi PHP                                          |
| `__LINE__`             | Bieżąca linia skryptu                                                        |
| `__FILE__`             | Nazwa pliku ze skryptem wraz z ścieżką dostępu                               |
| `__FUNCTION__`         | Nazwa bieżącej funkcji                                                       |
| `__METRHOD__`          | Nazwa bieżącej metody                                                        |
| `__DIR__`              | Katalog z plikiem skryptu                                                    |
| `__NAMESPACE__`        | Nazwa bieżącej przestrzeni nazw                                              |

## Operatory

Na zmiennych można wykonywać różne operacje, np. dodawania, dzielenia itp. za pomocą operatorów takich jak np. `+`
czy `/`.

Operatory można podzielić na następujące kategorie:

* arytmetyczne
* bitowe
* logiczne
* przypisania
* relacyjne (porównania)
* inkrementacji i dekrementacji
* pozostałe

[Lista operatorów jest bardzo długa.](https://www.php.net/manual/en/language.operators.php)

### Operatory arytmetyczne

Operatory arytmetyczne służą do wykonywania operacji arytmetycznych.

**Tabela**. Operatory arytmetyczne w PHP

| Operator | Wykonywane działania                  |
| -------- | ------------------------------------- |
| `*`      | mnożenie                              |
| `/`      | dzielenie                             |
| `+`      | dodawanie                             |
| `-`      | odejmowanie                           |
| `%`      | dzielenie modulo (reszta z dzielenia) |
| `**`     | potęgowanie                           |

**Działanie operatora modulo:**

 ```php
   $z = 34 % 8; // 2 bo 4 X 8 + 2 = 34
 ```

**Działanie operatora potęgowania:**

```php
$z = 2.5 ** 3.2 // <=> 2.5<sup>3.2</sup> = 18.76756928096 
$z = 4 ** 0.5 //  2
```

2.5 ** 3.2 <=> 2.5<sup>3.2</sup>

4 ** 0.5 <=> 4<sup>1/2</sup> <=> &radic;4

16 ** 1.75 = 128 <=> &#8732;16<sup>7</sup>

### Operatory inkrementacji i dekrementacji

Operator inkrementacji, czyli zwiększania (++) zwiększa wartość zmiennej o jeden. Występuje w dwóch formach:

1. Przedrostkowej (tzw. preinkrementacja), która ma postać: `++$variable` &ndash; zwiększenie wartości następuje przed
   użyciem zmienne.
2. Przyrostkowej (tzw. postinkrementacja), która ma postać `$variable++` &ndash; zwiększenie wartości następuje po
   użyciu zmiennej.

Operator dekrementacji, czyli zmniejszania (--) zmniejsza wartość zmiennej o jeden. Występuje w dwóch formach:

1. Przedrostkowej (tzw. predekrementacja), która ma postać: `--$variable` &ndash; zmniejszenie wartości następuje przed
   użyciem zmienne.
2. Przyrostkowej (tzw. postdekrementacja), która ma postać `$variable--` &ndash; zmniejszenie wartości następuje po
   użyciu zmiennej.

// TODO przykłady i ćwiczenia

### Operatory bitowe

Operatory bitowe wykonują operacje na bitach.

**Tabela**. Operatory bitowe.

| Operator | Wykonywane działanie            |
| -------- | ------------------------------- |
| &        | Iloczyn (koniunkcja) bitowy AND |
| \|       | Suma (alternatywa) bitowa OR    |
| ~        | Negacja bitowa NOT              |
| ^        | Bitowa różnica symetryczna XOR  |
| > >       | Przesunięcie bitowe w prawo     |
| <<       | Przesunięcie bitowe w lewo      |

Każda liczba nieparzysta ma ostatni najmniej znaczący bit równy jeden. Przesunięcie w lewo jest równoznacze z
pomnożeniem liczby przez wielokrotność dwa, a w prawa to podzielenie liczby przez wielokrotność.

// TODO inne operacje bitowe takie jak rotacja itp.

### Operatory logiczne

Operacje logiczne można wykonywać na argumentach (operandach), które posiadają wartość logiczną: prawda (ang. *true*)lub
fałsz (ang. *false*).

**Tabela**. Operatory logiczne w PHP

| Operator | Wykonywane działania              |
| -------- | --------------------------------- |
| and      | iloczyn logiczny (1)              |
| or       | suma logiczna (1)                 |
| xor      | logiczna alternatywa wykluczająca |
| !        | negacja logiczna                  |
| &&       | iloczyn logiczna (2)              |
| \| \|    | suma logiczna (2)                 |

Występujące w tabeli dwa rodzaje iloczynu logicznego i sumu logicznej wykonują takie same operacje, mają jednak różny
priorytet.

#### Iloczyn logiczny

#### Suma logiczna

#### Logiczna alternatywa wykluczająca

#### Negacja logiczna

### Operatory relacyjne (porównania)

**Tabela**. Operatory relacyjne

| Operator | Opis                                                              |
| -------- | ----------------------------------------------------------------- |
| ==       | Jeśli argumenty są równe, wynikiem jest *true*                     |
| ===      | Jeśli argumenty są tego samego typu i równe, wynikiem jest *true* |
| <>       | Wynikiem jest true, jeśli argumenty są różne                     |
| !=       | j.w.                                                              |
| !==      | Wynikiem jest true, jeśli argumenty sa różnych typów i różne     |

<!-- TODO dwa nowe operatory z tej grupy -->

### Operator Łańcuchowy

Operatorem konkatenacji, czyli łączenia łańcuchów znakowych (napisów) jest . (kropka).

**Przykład użycia operatora konkatenacji:**

```php
$str1 = "Pierwszy tekst";
$str2 = "Drugi tekst";

echo $str1.$str2;
echo "<br>";

$str3 = $str1 . "Trzeci tekst";
echo $str3;
```

### Operatory przypisania

Operatora przypisania reprezentuje znak równości &bdquo;=&rdquo;. Poniższe działanie czytam od prawej strony do lewej.
String 'bar' zostaje przypisany do zmiennej `$foo`.

```php
$foo = 'bar';
```

Operator przypisania może być użyty wielokrotnie w jednej linii kodu i w tym przypadku również czytamy od prawej strony
do lewej, czyli `string` 'lorem' zostaje przypisany do zmiennej `$lorem` a następnie wartość, które znajduje się pod
zmienną `$lorem` zostaje przypisane do zmiennej `$foo`. Finalnie zmienna `$lorem` i zmienna `$foo` zawierają tę samą
wartość.

Warto zwrócić uwagę na fakt, że modyfikując dalej zmienną `$foo` modyfikujemy tylko wartość przypisaną do niej. Wartość
przypisana do zmiennej `$lorem` zostaje niezmieniona.

```php
$foo = $lorem = 'lorem';
var_dump($foo);
var_dump($lorem);

$foo = 'new string';
var_dump($foo);
var_dump($lorem);
```

Operacje przypisania są dwuargumentowe i powodują przypisanie argumentu prawostronnego argumentowi lewostronnemu. Odbywa
się to za pomocą operatora = (równa się). Jeśli napiszemy `$a = 5`, oznacza to, że zmiennej `$a` przypisaliśmy
wartość `5`.

Oprócz tego występuje szereg operatorów łączonych, tzn. takich, w których przypisaniu towarzyszy dodatkowa operacja
&mdash; arytmetyczna, logiczna czy łańcuchowa.

Przykładowy napis `$a += $b` jest równoważny takiemu: `$a = $a + $b`.

Schematyczny zapis dla złożonych operatorów przypisania wygląda tak: `argOne operator= argTwo` i oznacza
działanie `argOne = argOne operator argTwo`

**Tabela** Operatory przypisania

| argument1 | operator | argument2 | znaczenie     |
| --------- | -------- | --------- | ------------- |
| $x        | =        | $y        | $x = $y       |
| $x        | +=       | $y        | $x = $x + $y  |
| $x        | -=       | $y        | $x = $x - $y  |
| $x        | *=       | $y        | $x = $x * $y  |
| $x        | /=       | $y        | $x = $x / $y  |
| $x        | %=       | $y        | $x = $x % $y  |
| $x        | .=       | $y        | $x = $x . $y  |
| $x        | <<=      | $y        | $x = $x << $y |
| $x        | > > =      | $y        | $x = $x >> $y |
| $x        | &=       | $y        | $x = $x & $y  |
| $x        | \|=      | $y        | $x = $x \| $y |
| $x        | ^=       | $y        | $x = $x ^ $y  |

### Operatory tablicowe

#### Operator łączenia tablic

Operatorem łącznia tablic jest plus (+). Do tablicy znajdującej się po lewej stronie operatora zostanie dodana zawartość
tablicy umieszczonej po stronie prawej. Jeżeli w obu tablicach znajdują się elementy o takich samych indeksach
(kluczach), to w nowej tablicy zachowane zostaną wartości z lewostronnego argumentu.

**Przykład użycia operatora łączenia tablic**:

```php
 $a = array(
    1 => 1,
    2 => 2,
    3 => 3
  );
  $b = array(
    3 => "trzy",
    4 => "cztery",
    5 => "pięć"
  );

  $c = $a + $b;
  print_r($c);
  
  echo "<br>";

  $arrayOne = [1, 3, 5, 6, 7, 8];
  $arrayTwo = [16, 17, 18, 9, 11, 13];
  $arrayThree = array(6 => 33, 7 => 44, 8 => 55);

  $newArray = $arrayOne + $arrayTwo;
  print_r($newArray); //

  echo "<br>";

  $newArray = $arrayOne + $arrayThree;
  print_r($newArray);
```

#### Operator indeksowania tablic

### Pozostałe operatory

#### Operator warunkowy

#### Operator kontroli błędów

#### Operator wykonania zewnętrznego

#### Operator konwersji (rzutowania) typów

#### Operatory obsługi obiektów

#### Operator rozdzielania wyrażeń

# Instrukcje sterujące i funkcje

## Instrukcje warunkowe

### Instrukcja if...else

Ogólna postać instrukcji warunkowej:

```php
if(warunek) {
  // Instrukcje do wykonania, gdy warunek prawdziwy
} else {
  // Instrukcje do wykonania, gdy warunek fałszywy
}
```

Blok `else` jest opcjonalny, zatem prawidłowa jest również konstrukcja:

```php
if(warunek){
   // Instrukcje do wykonania, gdy warunek prawdziwy
}
```

### Instrukcje if...else if

Po bloku `if` może wystapić dowolna liczba bloków `else if`.

**Przykład użycia instrukcji `if...else if`**

```php
<?php
  $liczba = 40;
  if ($liczba == 10) {
    echo "Zmienna liczba ma wartość 10.";
  }
  else if ($liczba == 20) {
    echo "Zmienna liczba ma wartość 20.";
  }
  else if ($liczba == 30) {
    echo "Zmienna liczba ma wartość 30.";
  }
  else {
    echo "Zmienna liczba nie jest równa ani 10, ani 20, ani 30.";
  }
?>
```

W PHP instrukcję if...else if można zapisać tak, że `elseif` jest jednym słowem.

### Zagnieżdżanie się instrukcji warunkowych

<!-- TODO równanie kwadratowe -->

## Wyrażenia warunkowe

## Operator warunkowy

## Instrukcja wyboru switch

## Pętle

## Składnia alternatywna

Tak pętle, jak i instrukcje warunkowe mogą mieć w PHP zarówno postać klasyczną, jak i postać alternatywną, zwaną
**składnią alternatywną** (ang. *alternative syntax*), której postać ogólna poniżej:

```
 instrukcja(wyrażenie):
    blok instrukcji;
 endinstrukcja;
```

Ze względu na wyraźne wyróżnienie tego, gdzie i jaka instrukcja się kończy, ten często niedoceniany sposób zapisu jest
wygodny, gdy w kodzie strony wielokrotnie przeplatane są instrukcje HTML i PHP.

### Instrukcje warunkowe

#### Instrukcja if

Zwykłą instrukcję if w przykładowej, klasycznej postaci:

```php
$a = 5.6, $b = 6.8;

if($a < $b){ 
  echo "a jest mniejsze od b"; 
}
```

Można zapisać:

```php
$a = 5.6, $b = 6.8;

if($a < $b): 
  echo "a jest mniejsze od b";
endif;
```

#### Instrukcja if...else

```php
$a = 5.6, $b = 6.8;

if($a < $b): 
  echo "a jest mniejsze od b"; 
else: echo "a nie jest mniejsze od b"; 
endif;
```

#### Instrukcja if...else if

```php
$a = 6; $b = 7;
if($a < $b): 
  echo "a jest mniejsze od b"; 
  elseif($a > $b): echo "a jest większe od b"; 
  else: echo "a jest równe b"; 
endif;
```

### Instrukcja switch

```php
$liczba = 0;
switch($liczba): 
  case 10 : echo "Zmienna liczba = 10"; 
    break; 
  case 20 : echo "Zmienna liczba = 20"; 
    break; 
  default : echo "Zmienna liczba nie jest równa ani 10, ani 20."; 
endswitch;
```

### Pętle

#### Pętla for

```php
for($i = 0; $i < 10; $i++): 
  echo "$i <br>"; 
endfor;
```

#### Pętla foreach

```php
$tab = array();
foreach($tab as $key => $v): 
  echo "tab[$key] = $v <br>"; 
endforeach;
```

#### Pętla while

```php
while($i < 10): 
  echo "$i <br>"; $i++; 
endwhile;
```

## Instrukcje break i continue

## Funkcje

### Budowa funkcji

Funkcję tworzymy za pomocą słowa kluczowego `function`:

```php
function functionName(){
  // instrukcje
}

// Funkcję wywołujemy:
fuctionName();
```

### Argumenty funkcji

```php
function functionName($param1, $param2, ... $paramN){
  // instrukcje
}
```

**Przykłady funkcji:**

```php
function timesTwo($x){
  $result = $x * 2;
  echo "$x * 2 = $result";
}

timesTwo(5);  // 5 * 2 = 10
```

```php
function add($num1, $num2) {
  $result = $num1 + $num2;
  echo "$num1 + $num2 = $result";
}

add(4, 6); // 4 + 6 = 10
```

### Zwracanie wartości

```php
function multiply($a, $b){
  return $a * $b;
}

$num1 = 7;
$num2 = 8;
$result = multiply($num1, $num2);

echo "$num1 * $num2 = $result";
```

Instrukcji `return` można użyć bez żadnej wartości. Powoduje ona wtedy jedynie przerwanie działania funkcji.

Można zadeklarować typ zwracanej wartości z funkcji:

```php
function functionName():typeName {
  // instrukcje
}
```

Jeżeli funkcja zwróci inny typ niż zadeklarowany, to nastąpi konwersja do typu zadeklarowanego, gdy na początku skryptu
nie będzie instrukcji:

`declare(strict_type=1)`

W przeciwnym razie będzie zgłoszony błąd TypeError.

### Zasięg zmiennych

Zasięg zmiennej to miejsca w skrypcie, w których jest ona dostępna. Zmienne w PHP mogą być:

* lokalne dostępne wewnątrz funkcji,
* globalne dostępne w całym skrypcie z wyjątkiem wnętrz funkcji,
* superglobalne.

Wewnątrz funkcji możemy uzyskać dostęp do zmiennych globalnych na dwa sposoby:

1. Poprzez użycie słowa kluczowego `globals`:

```php
<?php
  $a = 1;

  function funkcja(){
    global $a;
    echo "Wartość a = $a <br>";
  }

  funkcja();

  echo "Wartość a = $a <br>";
?>
```

2. Przez odwołanie się do zmiennej superglobalnej $GLOBALS:

```php
<?php
  $a = 1;

  function funkcja(){
    $a = $GLOBALS["a"];
    echo "Wartość a = $a <br>";
  }

  funkcja();

  echo "Wartość a = $a <br>";
?>
```

### Argumenty funkcji raz jeszcze

#### Sposoby przekazywania argumentów

Argumenty funkcji mogą być przekazywane:

* **przez wartość** (ang. *by value*) &mdash; funkcja otrzymuje kopię argumentu i wszystkie operacje wykonuje na tej
  kopii, stąd nie może się zmienić stan argumentu poza funkcją.
* **przez referencję** (ang. *reference*, inaczej odniesienie) &mdash; przed nazwą argumentu dodajemy znak & (ang. *
  ampersand*), wtedy jest możliwa zmiana argumentu poza funkcją:

```php
<?php
  function dodajJeden(&$liczba){
    $liczba = $liczba + 1;
  }
  
  $liczba = 1;

  echo "Przed wywołaniem funkcji liczba = $liczba <br>";

  dodajJeden($liczba);

  echo "Po wywołaniu funkcji liczba = $liczba <br>";
?>
```

#### Argumenty domyślne

Argumenty przekazywane funkcji mogą mieć wartości domyślne. Jeśli w wywołaniu funkcji nie będą podane wartości tych
argumentów to, przyjmą one wartości, które są ustawione jako domyślne.

Ogólna postać takiej funkcji wygląda następująco:

```php
function functionName ($argument1 = value1 , $argument2 = value2 , ..., $argumentN = valueN ){
   // Treść funkcji
}
```

#### Zmienna lista argumentów

PHP umożliwia wywołanie funkcji ze zmienną listą argumentów za pomocą wbudowanych funkcji:

* `func_nun_args` &mdash; udostępnia faktyczną liczbę argumentów,
* `func_get_arg` &mdash; argument o podanym numerze,
* `func_get_args` &mdash; listę wszystkich argumentów w postaci tablicy

```php
<?php
  function func(){
    $liczba_arg = func_num_args();
    echo "Liczba argumentów funkcji = $liczba_arg";
    echo "<br>";
  }
  
  func(1);
  func(1, 2);
  func("x", "y", "z");
?>
```

Wynik:

```
Liczba argumentów funkcji = 1
Liczba argumentów funkcji = 2
Liczba argumentów funkcji = 3
```

```php
<?php
  function func(){
    $liczba_arg = func_num_args();
    $str = "";
    for($i = 0; $i < $liczba_arg; $i++){
      $str .= (string) func_get_arg($i);
    }
    return $str;
  }
  
  echo func("To ", "jest ", "przykład nr ", 1);
?>
```

Wynik:

```
To jest przykład nr 1
```

Dostępny jest następujący sposób przekazania zmiennej liczby argumentów:

```php
function nazwa_funkcji (...$ dane ){
   // Treść funkcji
}
```

```php
<?php 

function func(...$dane){ 
  $str = ""; 
  
  foreach($dane as $d){ 
    $str .= $d; 
  } 
  
  return $str; 
} 

echo func("To ", "jest ", "przykład nr ", 1); 

?>
```

#### Typ danych

Aby wskazać, że dany argument ma mieć konkretny typ, należy nazwę argumentu poprzedzić nazwą typu, schematycznie:

```php
function nazwa_funkcji ( typ1 argument1 , typ2 argument2 , ... , typN argumentN ){ 
  // Instrukcje wnętrza funkcji 
}
```

```php
function mnozenie(int $arg1, int $arg2 = 2){ 
  return $arg1 * $arg2; 
}
```

Przykładowe wywołania:

```php
echo mnozenie(2, 3); 
echo mnozenie(2);
```

Można też będzie zastosować instrukcje:

```php
echo mnozenie(2.1, 3.1); 
echo mnozenie(2.2);
```

Argumenty typu zmiennoprzecinkowego (float) zostaną skonwertowane do typu całkowitoliczbowego (int).Tym samym wynikiem
ponownie będzie 6 i 4, natomiast po włączeniu trybu ścisłego zostanie wygenerowany błąd.

Dopuszczalne będą też odwołania typu:

```php
echo mnozenie("22", 2); 
echo mnozenie("2.1", "2.2"); 
```

W pierwszym przypadku napis zostanie skonwertowany do liczby całkowitej, która następnie będzie użyta jako argument
funkcji, natomiast w przypadku drugim napisy zostaną najpierw skonwertowane na wartości zmiennoprzecinkowe, które
następnie utracą części ułamkowe i dopiero tak przetworzone będą użyte jako wartości argumentów.

Z nieco inną sytuacją będziemy mieli do czynienia, jeżeli argumenty będą ciągami zawierającymi źle sformowane liczby,
np.:

```php
echo mnozenie("2abc", "1xyz"); 
echo mnozenie("abc", "xyz");
```

W pierwszym przypadku oba ciągi zaczynają się od prawidłowych liczb, po których występują inne znaki. W takiej sytuacji
ze znaków składających się na liczby zostaną przygotowane wartości przekazywane funkcji, ale jednocześnie zostaną
wygenerowane błędy najniższego rzędu (noty informacyjne, ang. notice ; ich pojawienie się zależy od konfiguracji
środowiska PHP). W drugim przypadku żaden z ciągów nie reprezentuje poprawnej dla PHP liczby, co w wyniku spowoduje
pojawienie się błędu

### Deklaracje typów wartości zwracanych

Kolejną przełomową zmianą w PHP7 jest wprowadzenie deklaracji dla typów zwracanych. Dostępny jest szereg typów, które są
obsługiwane: ciągi znaków (string), liczby całkowite (int) i zmiennoprzecinkowe (float), typy logiczne (bool), tablice (
array), typ callable, typ self (tylko dla metod), typ parent (tylko dla metod), domknięcia (Closure), a także klasy i
interfejsy.

Deklaracje dla typów zwracanych, podobnie jak dla typów skalarnych posiadają dwa tryby: coercive – dopuszczającym
rzutowanie i strict – tylko dokładny typ, konfigurowane analogicznie jak w poprzednim przypadku.

Deklaracji typu zwracanego dokonuje się poprzez umieszczenie dwukropka i nazwy typu po liście argumentów funkcji:

```php
function add(int $x, int $y) : int
{
    return $x + $y;
}
```

Gdy dopasowanie typu nie powiedzie się, podobnie jak w przypadku deklaracji dla typów statycznych, zostanie rzucony
wyjątek TypeError.

```php
<?php
declare(strict_types=1);

function multiply(float $x, float $y) : float
{
    return $x * $y;
}

function add(int $x, int $y) : string
{
    return $x + $y;
}

var_dump(multiply(2, 3.5)); // float(7)

var_dump(add(2, 3)); // Fatal error: Uncaught TypeError: Return value of add() must be of the type string, integer returned
```

Więcej przeczytać można w [RFC: Return Type Declarations.](https://wiki.php.net/rfc/return_types)

# Tablice

## Rodzaje tablic w PHP

Tablice (ang *arrays) to struktury pozwalające na przechowywanie zbioru danych określonego typu. W PHP tablice mogą być
indeksowane klasycznie (numerowane) oraz asocjacyjnie

> W rzeczywistości w PHP tablica jest uporządkowaną mapą, zbiorem par klucz – wartość, przy czym klucz może być wartością całkowitą lub wartością typu string. Z formalnego punktu widzenia nie ma zatem różnicy między tablicami indeksowanymi numerycznie, a tablicami asocjacyjnymi.

### Tablice indeksowane numerycznie

Aby utworzyć prostą tablicę indeksowaną numerycznie, należy użyć słowa kluczowego array w schematycznej postaci:

```php
$ tablica = array( wartość1 , wartość2 ,..., wartośćN );
```

```php
<?php 

$kolory = array("czerwony", "zielony", "niebieski");

echo "kolory[0] = $kolory[0] <br>";
echo "kolory[1] = $kolory[1] <br>"; 
echo "kolory[2] = $kolory[2] <br>"; 

?>

```

Wykorzystanie pętli for do wyświetlenia zawartości tablicy:

```php
 <?php 

 $kolory = array("czerwony", "zielony", "niebieski"); 
 
 for($i = 0; $i < 3; $i++){ 
   echo "kolory[$i] = $kolory[$i] <br>"; 
 } 
 
 ?>
 ```

Tablica może zostać również utworzona poprzez bezpośrednie przypisywanie wartości jej komórkom. Przykładowo zamiast
pisać:

 ```php
 $kolory = array("czerwony", "zielony", "niebieski"); 
 ```

można wykorzystać serię instrukcji w postaci:

 ```php
 $kolory[0] = "czerwony"; $kolory[1] = "zielony"; $kolory[2] = "niebieski";
```

W celu uniknięcia niejednoznaczności w tego typu skryptach (gdzie przypisania wartości indeksów odbywają się w osobnych
instrukcjach) dodaje się na początku instrukcję tworzącą pustą tablicę:

```php
$kolory = array();
```

### Tablice asocjacyjne

W PHP indeksem tablicy może być także dowolny ciąg znaków wtedy tablica nazywa się asocjacyjna (ang. associative array)
.Każdy indeks otrzymuje unikatową nazwę, a indeks zwiemy kluczem (ang. *key*).

Mówimy zatem, że w tablicy asocjacyjnej występują pary klucz – wartość (ang. *key - value*), w których każdy **klucz**
jednoznacznie identyfikuje przypisaną mu wartość. Tablicę tego typu tworzy się schematycznie tak:

```php
array ( 

  klucz1 => wartość1,
  klucz2 => wartość2, 
  ... 
  kluczN => wartośćN 
  
);
```

Utworzenie tablicy asocjacyjnej:

```php
<?php
  $kolory = array
  (
    "kolor1" => "czerwony",
    "kolor2" => "zielony",
    "kolor3" => "niebieski"
  );
  
  echo "Zawartość tablicy:<br>";
  echo "kolory['kolor1'] = ";
  echo $kolory['kolor1'];

  echo "<br>kolory['kolor2'] = ";
  echo $kolory['kolor2'];

  echo "<br>kolory['kolor3'] = ";
  echo $kolory['kolor3'];
?>
```

Wynik:

```
Zawartość tablicy:
kolory['kolor1'] = czerwony
kolory['kolor2'] = zielony
kolory['kolor3'] = niebieski
```

Po zastosowaniu konstrukcji w schematycznej postaci:

```php
nazwa_tablicy [' nazwa_klucza '] 
```

otrzymujemy wartość odpowiadającą danemu kluczowi.

Drugim ze sposobów tworzenia tablicy asocjacyjnej jest użycie składni z nawiasem kwadratowym:

```php
nazwa_tablicy [' nazwa_klucza '] = wartość_klucza ;
```

```php
<?php
  $kolory['kolor1'] = "czerwony";
  $kolory['kolor2'] = "zielony";
  $kolory['kolor3'] = "niebieski";

  echo "Zawartość tablicy:<br>";
  echo "kolory['kolor1'] = ";
  echo $kolory['kolor1'];

  echo "<br>kolory['kolor2'] = ";
  echo $kolory['kolor2'];

  echo "<br>kolory['kolor3'] = ";
  echo $kolory['kolor3'];
?>

```

Tablice asocjacyjne są obsługiwane przez pętle typu foreach:

```php
<?php
  $kolory['kolor1'] = "czerwony";
  $kolory['kolor2'] = "zielony";
  $kolory['kolor3'] = "niebieski";

  echo "Zawartość tablicy:<br>";
  foreach($kolory as $kolor){
    echo $kolor;
    echo "<br>";
  }
?>
```

W ten sposób uzyskamy jednak jedynie wartości kluczy, nie zaś nazwy kluczy. Jeśli również ta informacja jest potrzebna,
trzeba zastosować drugą wersję pętli foreach:

```php
<?php
$kolory['kolor1'] = "czerwony";
$kolory['kolor2'] = "zielony";
$kolory['kolor3'] = "niebieski";

echo "Zawartość tablicy:<br>";
foreach($kolory as $klucz => $kolor){
  echo "kolory['$klucz'] = $kolor";
  echo "<br>";
}
?>
```

## Tablice wielowymiarowe

### Tworzenie tablic wielowymiarowych

### Tablice nieregularne

## Operacje na tablicach

### Sortowanie tablic klasycznych

### Sortowanie tablic asocjacyjnych

### Implozja i eksplozja

## Operacje na elementach tablic

### Zmiana kolejności elementów

### Poruszanie się po tablicy

### Poruszanie się po tablicy

### Dodawanie i pobieranie elementów

## Liczba elementów tablicy

# Programowanie obiektowe

PHP umożliwia *programowanie obiektowe* (ang. OOP &mdash; *Object Oriented Programming*). Przedstawione tu będą jedynie
podstawowe koncepcje oraz ich realizacja w PHP. Mechanizmy obiektowe dostępne W PHP posiadają wszystkie własności,
jakich się oczekuje od języka w pełni obiektowego.

## Podstawy programowania obiektowego

### KLasy i obiekty

Programowanie obiektowe zostało zaprojektowane jako zbiór obiektów z atrybutami i operacjami, które wchodzą w
interakcje. Atrybuty to właściwości bądź zmienne obiektu. Operacje to metody, działania lub funkcje, które obiekt może
podejmować w celu modyfikacji siebie lub zewnętrznego efektu.

Jedną z koncepcji programowania obiektowego jest **hermetyzacja** czyli ukrywanie danych co oznacza, że dostęp do danych
jest możliwy jedynie przez operacje obiektu, nazwane jego interfejsem.

Możliwości funkcjonalne obiektu są związane z używanymi przez niego danymi. Możliwa jest łatwa zmiana szczegółów
implementacji obiektu w celu poprawienia wydajności, dodania nowych własności lub naprawienia błędów bez
*konieczności zmiany interfejsu*, która mogłaby poważnie wpłynąć na cały projekt. Dzięki enkapsulacji możliwe jest
dokonywanie zmian i naprawianie błędów bez wpływania na pozostałe części projektu.

Programowanie obiektowe stało się już normą, a programowanie proceduralne oparte na funkcjach uważa się za przestarzałe.
Jednak większość aplikacji internetowych jest wciąż niestety projektowana i tworzona według metodologii zorientowanej na
funkcje.

Obiekt jest unikatowym i identyfikowalnym zbiorem zapisanych danych i operacji pracujących na tych danych. Na każdym z
nich można pracować oddzielnie, ponieważ posiadają specjalną zmienną, tak zwany uchwyt (niepowtarzalny identyfikator).

Obiekty mogą być pogrupowane w klasy. Klasy reprezentują zbiór obiektów, które mogą różnić się nieco między sobą, lecz
posiadają określoną liczbę podobieństw. Klasa zawiera obiekty posiadające takie same operacje, działające w identyczny
sposób, i takie same atrybuty, opisujące identyczne własności, chociaż wartości tych atrybutów mogą różnić się pomiędzy
poszczególnymi obiektami.

### Polimorfizm

### Dziedziczenie

### Tworzenie klas

Obiekt jest traktowany jako byt programistyczny, który może przechowywać pewne dane (atrybuty, właściwości) i wykonywać
pewne zadania (funkcje). W Obiekcie zawieramy zmienne przechowujące dane oraz funkcje realizujące przypisanie obiektowi
zadania.

Zmienne zawarte w obiekcie nazywamy polami (ang. *fields*), właściwościami (ang. *properties*) <a href="#1">[1]</a> lub
atrybutami (ang. *attributes*), natomiast funkcje — metodami (ang. *methods*). Postać obiektu opisuje konstrukcja
nazywana klasą (ang. class). Pola i metody określamy natomiast jako składowe klasy (ang. class members).

Od PHP 7.4.0 definicje właściwości mogą zawierać deklaracje typu, z wyjątkiem wywoływanych.

Ogólna postać klasy to:

```php
class className { 
  public  type $propertyNameOne; 
  public  type $propertyNameToo; 
  //... 
  public type $propertyNameN;

  public function functionName ($arguments) {
   // wnętrze metody
  }
}
```

Przy czym słowo public to tzw. specyfikator dostępu oznaczający, że dostęp do wymienionego pola nie jest niczym
ograniczony. Przy metodach możemy je pominąć.

Przykład prostej klasy

```php
<?php
class Person {
  private string $name;
  private string $surname;
  
  function display(string $name, string $surname ){
    echo "Twoje imię to $name a nazwisko to $surname";
  }
}
```

Umieszczenie klasy w kodzie oznacza utworzenie nowego typu danych oraz możliwość korzystania z obiektów tego typu.

### Tworzenie obiektów

Gdy jest zdefiniowana klasa (czyli nowy typ danych), można na jej podstawie tworzyć obiekty, tj. konkretne egzemplarze
tej klasy. Mówi się, że obiekt jest instancją (wystąpieniem) danej klasy.

Aby utworzyć obiekt, należy użyć operatora `new` w postaci:

```
 $zmienna = new nazwa_klasy ();
```

### Odwołania do składowych

Dostęp do składowych klasy uzyskuje się, stosując operator ->.

```
$object -> filedName;
$object -> methodName(arguments)
```

Przykład:

```php
<?php

class Person {
  public string $name;
  public string $surname;

  function test(): string {
    return "Test metody test";
  }
}

$person = new Person();
$person -> name = 'Jan';
$person -> surname = 'Kowalski';
$person -> show();

echo "Masz na imię: $person->name <br>";
echo "Nazywasz się: $person->surname <br>";
echo "Testujemy metodę: ";
$display = $person -> test();
echo "$display";
```

Przykład. Wiele obiektów jednej klasy:

```php
<?php
require "Person.php";
$persons = array();

for ($i = 0; $i < 3; $i++) {
  $persons[$i] = new Person();
}

$persons[0]->name = 'Jan';
$persons[0]->surname = 'Kowalski';

$persons[0]->name = 'Tadeusz';
$persons[0]->surname = 'Nowak';

$persons[0]->name = 'Ewa';
$persons[0]->surname = 'Demarczyk';
?>

<table>
  <caption>Zawartość tablicy $osoby</caption>
  <tr>
    <th>Imię</th>
    <th>Nazwisko</th>
  </tr>
<!-- (***) -->
  <?php
  for ($i = 0; $i < 3; $i++) {
    echo "<tr>";
    echo "<td>" . $persons[$i]->name . "</td>";
    echo "<td>" . $persons[$i]->surname . "</td>";
    echo "</tr>";
  }
  ?>
```

Zamiast pętli for można by również zastosować pętlę foreach, o ile tylko chcemy odczytywać wszystkie dane z tabeli:

```php
<?php
  foreach($osoby as $osoba){
    echo "<tr>";
    echo "<td>$osoba->imie</td>";
    echo "<td>$osoba->nazwisko</td>";
    echo "</tr>";
  }
?>
```

Dla złożonych odwołań może się okazać, że należy zastosować składnię z nawiasami klamrowymi, aby dla interpretera PHP
wyraźniej zaznaczyć miejsce, wstawianej wartości do łańcucha znaków:

```
"napis {złożone odwołanie} napis"
```

Np. :

```php
echo "<td>{person->name}</td>";
```

W praktyce dąży się również do tego, aby maksymalnie oddzielać treść PHP od HTML. Zatem również w pętli generującej
wiersze tabeli warto zastosować przeplatanie trybów PHP i HTML.

```php
<?php

<table>
  <caption>Zawartość tablicy $osoby</caption>
     <tr>
        <th>Imię</th>
        <th>Nazwisko</th>
     </tr>

      <?php
        foreach($osoby as $osoba):
      ?>
        <tr>
          <td><?php echo $osoba->imie ?></td>
          <td><?php echo $osoba->nazwisko ?></td>
        </tr>
      <?php
        endforeach;
      ?>

</table>
?>
```

Forma skrócona instrukcji `echo` wygląda tak:

```
<?=value?>
```

Użycie składni skróconej:

```php
<?php
  $osoby = array();
  foreach($osoby as $osoba):
?>
<tr>
  <td><?=$osoba->imie?></td>
  <td><?=$osoba->nazwisko?></td>
</tr>
<?php 
  endforeach;
?>
```

### Wskazanie this

Aby wewnątrz klasy odwołać się do jej pól, trzeba użyć słowa `this`. Jest to specjalne odwołanie wskazujące na bieżący
obiekt. A zatem odwołanie w postaci:

```
$this->fieldName
```

oznacza pole znajdujące się w aktualnym obiekcie.

```php
<?php

class Person {
  public string $name;
  public string $surname;

  function show() {
    echo "Imię: $this->name <br>";
    echo "Nazwisko: $this->surname <br>";
  }
}

$person = new Person();
$person->name = "Anna";
$person->surname = "Malinowska";

$person->show();
```

## Konstruktory i destruktory

### Budowa konstruktora

**Konstruktor** (ang. *constructors*) jest wywoływany przy tworzeniu obiektu, może zatem nadawać atrybutom sensowne
wartości początkowe oraz ewentualnie tworzyć inne obiekty wymagane przez ten obiekt.

Po utworzeniu obiektu jego pola są puste, nie mają przypisanych żadnych wartości. To wręcz dobry obyczaj
programistyczny, aby inicjować pola obiektu wartościami domyślnymi.

Konstruktor jest deklarowany w identyczny sposób jak inne operacje, ale ma specjalną nazwę __construct()

```php
class className { 
  function __construct($param) { 
    echo "Konstruktor wywołany z parametrem ".$param."<br />"; 
  } 
}
```

Przykład klasy zawierającej konstruktor:

```php
<?php
namespace persons;

class Person {
  private string $name;
  private string $surname;

  function __construct($name, $surname){
    $this->name = $name;
    $this->surname = $surname;
  }

  function showPerson() {
    echo "Imię: $this->name <br>";
    echo "Nazwisko: $this->surname <br>";
  }
}
```

Przykład użycia klasy z konstruktorem:

```php
<?php
require "Person.php";

$person = new persons\Person('Jan', 'Kowalski');

$person->showPerson();
```

## Kontrola dostępu przy użyciu modyfikatorów

PHP udostępnia trzy modyfikatory:

1. Modyfikator *public* jest ustawieniem domyślnym, więc jeśli nie zostanie użyty jawnie żaden modyfikator dostępu w
   deklaracji atrybutu lub metody to zostanie zastosowany. Elementy poprzedzone tym modyfikatorem są *publiczne* czyli
   dostępne dla kodu spoza klasy.

2. Modyfikator *private*. Składowe klasy z tym modyfikatorem są dostępne wyłącznie wewnątrz danej klasy. Za jego pomocą
   możliwe jest ukrywanie danych. Także niektóre pomocnicze metody, które są wykorzystywane tylko wewnątrz klasy,
   powinny być opatrzone tym modyfikatorem. Składowe prywatne nie są dziedziczone.

3. Modyfikator dostępu *protected* oznacza, że dostęp do elementów będzie możliwy wewnątrz danej klasy i w klasach
   pochodnych.

Przykład użycia modyfikatorów dostępu:

```php
class Manners { 
  private string $greeting = 'Witaj'; 
  
  public function welcome($name) { 
    echo "$this->greeting, $name"; 
  } 
}
```

Modyfikator public można by pominąć, gdyż jest on stosowany domyślnie, jednak jeśli w kodzie są używane inne
modyfikatory dostępu, to stosowanie także modyfikatora public sprawi, że kod będzie łatwiejszy do zrozumienia.

## Pisanie funkcji dostępowych

Jeśli zrezygnujemy z bezpośredniego dostępu do atrybutów klasy i zdefiniujemy je jako prywatne lub chronione, a
dodatkowo uzupełnimy o odpowiednie funkcje dostępowe (ang. *accessor functions*), to cały dostęp do tych atrybutów
będzie mógł być realizowany przy użyciu określonego fragmentu kodu. W ten sposób wymusimy hermetyzację danych, co należy
do dobrych praktyk programistycznych.

```php
class PrivateTest {
  private string attribute;
  function __get($name){
    return $this->$name;
  }
  function __set($name, $value){
    if($name="attribute" && $value >= 0 && $value <= 100){
      $attribute = $value;
    }
  }
}

$test = new PrivateTest();
$test->attribute = 5; // zostanie automatycznie wywołany seter
$test->attribute; // automatyczne wywołanie getera
```

Powyższe metody dostępowe do `magic method`

```php
class Calculator
{
  private float $paramOne;
  private float $paramTwo;


  public function getParamOne(): float
  {
    return $this->paramOne;
  }

  public function setParamOne(float $paramOne): void
  {
    $this->paramOne = $paramOne;
  }


  public function getParamTwo(): float
  {
    return $this->paramTwo;
  }

  public function setParamTwo(float $paramTwo): void
  {
    $this->paramTwo = $paramTwo;
  }

  function add(): float
  {
    return $this->paramOne + $this->paramTwo;
  }

  function multiply(): float
  {
    return $this->paramOne * $this->paramTwo;
  }

```

## Metody statyczne

Metodę można zdefiniować jako statyczną (ang. *static*), co oznacza, że jest ona wywoływana względem klasy, a nie
obiektu. Metoda statyczna nie ma dostępu do żadnych właściwości obiektu.

```php
// User.php
namespace netUser;

class User
{
  static function pwdString(){
    echo "Proszę wpisać hasło";
  }
}
```

```php
// index.php
<?php

include "User.php";

netUser\User::pwdString();
```

Klasę wraz z metodą statyczną wywołuje się za pomocą podwójnego dwukropka (niekiedy nazywa się go *operatorem zasięgu*),
a nie znaków `->`. Funkcje statyczne przydają się do wykonywania działań na samej klasie, a nie na konkretnych
obiektach.

Próba uzyskania dostępu do $this->property albo innych właściwości obiektu z poziomu funkcji statycznej wywoła błąd.

## Deklarowanie stałych

Stałe w klasie definiujemy za pomocą słowa kluczowego `const`. Wewnątrz klasy do stałej odwołujemy się za pomocą
słowa `self` i podwójnego dwukropka.

```php
<?php

class SomeClass {
  const BAR = 'bar'; // publiczna
  public const FOO = 'foo';
  private const ZAZ = 'zaz';
  
  public function doSomething() : void {
    echo self::ZAZ;
  }
  
}
```

```php
echo SomeClass::FOO . "\n";
echo SomeClass::ZAZ . "\n";

$object = new SomeClass();
var_dump($object);
$object->doSomething();
var_dump(SomeClass::ZAZ); // error
```

Od wersji 7.1 możemy używać modyfikatorów dostępu. Jeśli nie użyjemy żadnego, to stała domyślnie jest publiczna.

Do stałej musimy przypisać konkretną wartość np. string, tablica, nie mogą to być jednak wyrażenia, czyli zmienne,
właściwości czy rezultat zwrócony przez wywołanie funkcji (metody).

Do stałej odwołujemy się przez nazwę klasy oraz użycie podwójnego dwukropka "::" Z wnętrza klasy do stałej odwołujemy
się za pomocą słowa "self", które wskazuje na nazwę klasy. Istotny jest fakt, że nie potrzebujemy używać znaku dolara "
$" przed nazwą stałej.

Stałe są inicjalizowane tylko raz, gdy PHP wczyta kod klasy, a nie za każdym razem, gdy tworzymy nowy obiekt danej
klasy.

## Dziedziczenie

### Konstruktory i dziedziczenie

W klasie potomnej zawsze możemy nadpisać metodę lub właściwość pochodzącą z klasy rodzica. W tym przypadku jest to
konstruktor.

Za pomocą słowa kluczowego `parent` możemy się odwołać w klasie potomnej do składowych klasy rodzica, w tym także do
konstruktora.

```php
class Dziecko extends Rodzic
{
    public function __construct(string $nazwa, int $numer)
    {
        parent::__construct($nazwa);
    }

    private function doSomethin(int $count): string
    {
        // ...
    }
}
```

Jeśli wprowadzone przez nas zmiany w deklaracji metody, którą nadpisujemy, zmienią ją na tyle, że PHP uzna, że nie
jest "kompatybilna" z deklaracji rodzica to zostaniemy o tym poinformowani stosownym komunikatem o błędzie.

Możemy bez konsekwencji zmieniać listę łącznie z typami argumentów przekazywanymi do konstruktora.

Dobrą zasadą jest, aby utrzymywać jak największa spójność deklaracji konstruktora w dziecku z rodzicem. Mimo że możemy
go całkiem zmienić, to jednak przykładowo, jeśli potrzebujemy dodać nowy argument, to dodajmy go na końcu listy
argumentów.

## Wyjątki
```php
<?php
/*
interface Throwable {}

class Error implements Throwable {}

class Exception implements Throwable {}
*/
?>
```

```php
<?php
try {
  echo "jesteśmy w try - start<br>";

  throw new Exception('To jest error', 100);
} catch (Exception $e){
  echo "jesteśmy w catch - start<br>";

  dump($e->getMessage());
  dump($e->getCode());
  dump($e->getLine());
  dump($e->getFile());

  echo "jesteśmy w catch - end<br>"; 
}

```

**Wyjątki** (ang. *exception*) to konstrukcje programistyczne służące do obsługi błędów pozwalające na zmniejszenie
liczby instrukcji warunkowych oraz pomijanie całych bloków kodu.

### Zgłaszanie wyjątków

Zgłoszenie wyjątku to po prostu informacja dla Aby sprawdzić, jak zareaguje PHP na wykonanie instrukcji throw, wystarczy
uruchomić poniższy skrypt:

Wyjątek może zostać zgłoszony za pomocą instrukcji `throw` (ang. throw &ndash; rzucać) informując aparatu wykonawczy
PHP, że wystąpiła sytuacja nadzwyczajna, która wymaga specjalnej obsługi. Z reguły jest to informacja o błędzie. Możemy
sprawdzić, jak zareaguje PHP na wykonanie instrukcji `throw`, wystarczy uruchomić poniższy skrypt:

```php
<?php
  throw new Exception();
?>
```
W przeglądarce zobaczymy taki widok:

![img.png](img.png)

Wykonanie powyższego skryptu spowoduje wystąpienie błędu krytycznego (ang. *fatal error*) i zakończenie działania kodu.
Tak wygenerowany wyjątek można przechwycić i wykonać kod obsługi błędu.

Wyjątek to obiekt klasy Exception lub pochodnej zgłoszony za pomocą instrukcji `throw`.



## Klasy anonimowe

Klasy anonimowe są dostępne w PHP7. Pozwalają one na utworzenie instancji klasy w miejscu i natychmiastowe przekazanie
obiektu, na przykład do funkcji. Są wyjątkowo użyteczne, gdy instancja obiektu wykorzystywana jest w jednym miejscu.

## Zasady tworzenia klas &mdash; dobre praktyki programistyczne

```php
class SomeClass
{
  // Stałe publiczne  
  // Stałe prywatne
  
  // Właściwości statyczne publiczne
  // Właściwości statyczne prywatne 
  
  // Metody statyczne publiczne 
  // Metody statycznie prywatne 

  // Właściwości publiczne
  // Właściwości prywatne

  // Konstruktor

  // Metody publiczne
  // Metody prywatne
}
```

# Przetwarzanie danych z przeglądarki

Definicja formularza ma schematyczną postać:

```html

<form action="adres_skryptu ">
  <!-- Tutaj definicje elementów formularza -->
</form>
```

Parametr `action` określa lokalizację skryptu, do którego mają zostać wysłane dane zebrane z formularza. Określenie to
może zawierać:

* pełny adres URL, np. http://www.mojadomena wtedy można wywoływać skrypty umieszczone w dowolnej domenie pod dowolnym
  adresem,

* jego część, np. /skrypt/scrypt.php wtedy jest to adres względny, skrypt znajduje się w folderze skrypty, który jest w
  katalogu głównych serwera.

Znacznik `<form>` może zawierać również opcjonalne atrybuty, m.in.:

* accept-charset &mdash; sposoby kodowania znaków w przesyłanych danych (np. utf-8, ISO - 8852-2),
* enctype &mdash; sposób kodowania danych wysyłanych do serwera (zwykle application/x-www-form-urlencoded, multipart
  /form-data lub text/plain)

* metod &mdash; metoda wysyłania danych (z reguły get lub post)

Elementami składowymi formularza mogą być m.in.:

* button — klasyczny przycisk,

* checkbox — pole wyboru,

* file — pole wyboru pliku,
* hidden — element ukryty,
* image — obraz,
* password — pole tekstowe do wpisywania haseł,
* radio — pole wyboru,
* reset — przycisk reset,
* select — lista wyboru,
* submit — przycisk submit,
* text — pole tekstowe,
* textarea — rozszerzone pole tekstowe.

Każdy z tych elementów powinien mieć określony atrybut `name`, dzięki któremu będzie możliwa jego identyfikacja w
skrypcie PHP.

## Metoda GET

Metoda GET służy do przesyłania niewielkich ilości danych, np. z formularzy tekstowych w adresie URL, który będzie miał
wtedy schematyczną postać:

```html
http://adres.serwera/skrypt.php?parametr1=wartość1&parametr2=wartość2
```

Z reguły metoda ta używana jest do wywoływania skryptów generujących dane.

Jeśli do pola tekstowego zostanie wprowadzony przykładowy ciąg znaków, np. test, po kliknięciu przycisku `Wyślij` będzie
wywołany ciąg URL w postaci http://localhost/skrypt.php?pole1=test. Przy założeniu, że atrybut formularza `action`
jest równy http://localhost/skrypt.php a atrybut `name` pola tekstowego równa się pole1.

Dostęp do danych z formularza jest możliwy za pośrednictwem globalnej (superglobalnej) tablicy `$_GET`:

```php
 $variable = $_GET['fieldName'];
```

Przydatna jest funkcja `isset()`, która pozwala stwierdzić, czy dana zmienna, pole obiektu lub też klucz tablicy, są
ustawione.

W praktyce należy zawsze weryfikować, czy otrzymane dane zgadzają się z oczekiwanymi. Poniżej przykład takiego
sprawdzenia:

```php
<?php
if (isset($_GET['year']) &&
  ($_GET['year'] == '1985'
    || $_GET['year'] == '1986'
    || $_GET['year'] == '1983'
  )
) {
  if ($_GET['year'] == '1986') {
    echo "Gratulacje, prawidłowa odpowiedź";
  } else {
    echo "Przykro mi, ale odpowiedź jest nie prawidłowa.";
  }
} else {
  echo "Nie zaznaczono żadnej pozycji";
}

?>
```

W tym przypadku po zbadaniu, że istnieje indeks `year`, jest sprawdzane, czy zapisana pod nim wartość jest zgodna z
listą opcji zawartą w formularzu.

## Metoda POST

Metoda POST to drugi sposób przesyłania danych do serwera:

* możliwość przesłania większej ilości danych (np. plików binarnych); domyślnie 8 MB, ale można to zmienić ustawiając
  opcję konfiguracyjną PHP `post_max_size`.
* nie można ich zobaczyć na polu adresu przeglądarki.

Wartości z formularza można odczytać w skrypcie przetwarzającym dane. Jako indeks tablicy należy zastosować nazwę pola
formularza, z którego chce się odczytać dane. Schematycznie konstrukcja taka ma postać:

```php
$variable = $_POST['fieldName'];
```

## Tablica REQUEST

Tablica $_REQUEST zawiera wszystkie dane z tablic $_GET, $_POST i $COOKIE.

## Wysyłanie pliku na serwer (upload)

Aby możliwe było, wysłanie plik z komputera użytkownika na serwer potrzebny jest:

* formularz HTML umożliwiający wybór pliku oraz skrypt PHP, który ten plik odbierze,
* odpowiednio skonfigurowany plik `php.ini`:
  * włączona opcja `file_uploads`,
  * zmienna `upload_tmp_dir` wskazująca na katalog tymczasowy, w którym będą zapisywane dane tymczasowe podczas ich
    pobierania, jeśli nie będzie podany, to zostaną wykorzystane ustawienia systemowe,

  * zmienna `upload_max_filesize` powinna wskazywać na maksymalny rozmiar pojedynczego pliku (standardowo 2 MB),
  * maksymalna wielkość pliku zależy również od opcji `post_max_size` (standardowo 8 MB),
  * `m_input_time` (maksymalny czas przetwarzania danych wejściowych; standardowo bez ograniczeń).

Znacznik form w kodzie HTML powinien zawierać następujące parametry:

* name — zawiera nazwę formularza;
* enctype — określa typ kodowania MIME, w tym przypadku będzie to multipart/form-data;
* action — zawiera adres skryptu PHP;
* method — określa metodę wysyłania danych, w tym przypadku będzie to metoda POST.

Polu typu file, służącemu do wyboru pliku, zostanie nadana nazwa (parametr name), która pozwoli na zidentyfikowanie
danych z tego pola w skrypcie PHP.

Skrypt odbierający uzyska dostęp do globalnej tablicy $_ FILES, która zawiera informacje dotyczące przesłanych danych.
Jest to tablica asocjacyjna, w której plik identyfikowany jest przez nazwę pola <input> typu file. W naszym przypadku
nazwą tą jest `pliki`:

* $_ FILES ['plik1']['name'] — oryginalna nazwa pliku (którą plik miał w komputerze użytkownika);
* $_FILES [' plik1 '][' type '] — typ MIME pliku (o ile przeglądarka dostarczyła tę informację);
* $_FILES [' plik1 '][' size '] — wielkość pliku w bajtach;
* $_ FILES ['plik1']['tmp_name '] — nazwa tymczasowa, pod jaką plik został zapisany na serwerze;
* $_ FILES ['plik1 '][' error '] — status operacji, kod błędu. Pole error może przyjmować jedną z wartości:
* UPLOAD _ ERR _ OK — brak błędu, operacja zakończona sukcesem.
* UPLOAD _ ERR _ INI _ SIZE — wielkość pliku przekracza wielkość maksymalną zdefiniowaną w pliku php.ini (zmienna upload
  _ max _ filesize ).

* UPLOAD_ERR_FORM _ SIZE — wielkość pliku przekracza wielkość maksymalną zdefiniowaną w formularzu HTML.
* UPLOAD _ ERR _PARTIAL — została odebrana jedynie część pliku.
* UPLOAD _ ERR _ NO _ FILE — plik nie został przesłany.
* UPLOAD_ERR_NO_TMP_DIR — niedostępny katalog tymczasowy (dostępny od wersji PHP 5.0.3).

* UPLOAD _ ERR _ CANT _ WRITE — wystąpił błąd przy próbie zapisu pliku na dysku (dostępny od wersji PHP 5.1.0).
* UPLOAD_ERR_EXTENSION — ładowanie pliku zostało przerwane przez jedno z rozszerzeń PHP (dostępny od wersji PHP 5.2.0).

Przykład scryptu odbierającego plik:

```php
 <?php
      $uploadDir = 'pliki/';

      if($_FILES['plik1']['error'] == UPLOAD_ERR_OK){
        $new_name = $uploadDir . $_FILES['plik1']['name'];
        $temp_name = $_FILES['plik1']['tmp_name'];
        if(move_uploaded_file($temp_name, $new_name)){
          echo "Plik został załadowany.";
        }
        else{
          echo "Nieprawidłowy plik.";
        }
      }
      else{
        echo "Wystąpił błąd: ";
        echo match ($_FILES['plik1']['error']) {
          UPLOAD_ERR_INI_SIZE, UPLOAD_ERR_FORM_SIZE => "Przekroczony maksymalny rozmiar pliku!",
          UPLOAD_ERR_PARTIAL => "Odebrano tylko część pliku!",
          UPLOAD_ERR_NO_FILE => "Plik nie został pobrany!",
          UPLOAD_ERR_NO_TMP_DIR => "Brak dostępu do katalogu tymczasowego!",
          UPLOAD_ERR_CANT_WRITE => "Nie udało się zapisać pliku na dysku serwera!",
          UPLOAD_ERR_EXTENSION => "Ładowanie pliku przerwane przez rozszerzenie PHP!",
          default => "Nieznany typ błędu!",
        };
      }
    ?>
```

## Wysyłanie wielu plików naraz

Formularz HTML można przygotować w taki sposób, aby umożliwiał wskazanie kilku plików, które zostaną wysłane do serwera
w jednym żądaniu. Należy wtedy umieścić w kodzie serię znaczników < input > o typie file i takiej samej nazwie, przy
czym nazwa ta powinna być uzupełniona o znaki [] . Schemat budowy takiego znacznika będzie więc następujący:

```html
<input type="file" name="nazwa[]">
```

