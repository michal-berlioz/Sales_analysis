Sklep X
================
Michał Lewsza
2020-12-29

## Analiza sprzedaży i wydatków reklamowych

### Korelacja

<br>

<div class="text-justify">

     Badaniu korelacji zostaną poddane parametry ilościowe opisujące
natężenie kampanii*(e.g. budżet, wyświetlenia, zasięgi, klikniecia)* i
wyniki sprzedaży *(przychód, liczba dokonanych zamówień, liczba
sprzedanych produktów)*. Dodatkowo, parametry natężenia kampanii zostaną
opóźnione w celu zbadania opóźnionego efektu na sprzedaż:

</div>

<br>

    ## # A tibble: 14 x 4
    ##    variable         liczba_zam liczba_prod przychod
    ##    <chr>                 <dbl>       <dbl>    <dbl>
    ##  1 zasieg                0.672       0.666    0.671
    ##  2 wyswietlenia          0.673       0.667    0.671
    ##  3 budzet                0.757       0.749    0.749
    ##  4 kliki                 0.800       0.790    0.796
    ##  5 zakupy_fb             0.846       0.845    0.843
    ##  6 komenty_post          0.720       0.700    0.705
    ##  7 reakcje_post          0.795       0.789    0.797
    ##  8 przychod              0.985       0.999    1    
    ##  9 liczba_prod           0.985       1        0.999
    ## 10 liczba_zam            1           0.985    0.985
    ## 11 nowe_zakazenia       -0.194      -0.176   -0.182
    ## 12 przyrost_zakazen      0.134       0.131    0.141
    ## 13 zakazenia_lag1       -0.255      -0.235   -0.245
    ## 14 temp                  0.248       0.229    0.240

<div class="text-justify">

     Wskaźniki korelacji wykazują silną, pozytywną(\>0,5) korelację
pomiędzy intensywnością kampanii a wynikami sprzedaży. Można
stwierdzić, że istnieje silna bezpośrednia zależność między wydatkami
reklamowymi a przychodem ze sprzedaży (korelacja: 0.749).

Równie silna zależność w kontekście przychodów występuje w przypadku
takich parametrów jak: ‘kliknięcia’, ‘komentarze postow’, ‘reakcje na
posty’.

</div>

<br>

<div class="text-justify">

     Poniższy wykres obrazuje korelację wydatków na reklamę z przychodem
w zależności od rzędu opóźnienia *(e.g. korelacja dla rzędu = 2 mówi
jaki związek mają przedwczorajsze wydatki z dzisiejszym przychodem)* Z
każdym kolejnym opóźnieniem korelacja maleje, co znaczy, że **wydatki na
reklamę mają największe przełożenie na przychód tego samego dnia.**

<br>

</div>

![](Kiowi_R_files/figure-gfm/lagging-1.png)<!-- -->

<div class="text-justify">

     Wydatki z kolejnymi opóźnieniami cechują się również wysokimi
wskaźnikami korelacji. Jednak może to dawać złudny obraz, ponieważ sam
szereg czasowy wydatków na reklamę cechuje się silną autokorelacją o
czym świadczy poniższy wykres:

</div>

<br>

![](Kiowi_R_files/figure-gfm/acf-1.png)<!-- -->

<div class="text-justify">

     **Podsumowując: **najrozsądniej jest przyjąć hipotezę, mówiącą, że
wydatki na reklamę mają silny wpływ na przychód **tego samego dnia.**

</div>

<br> <br>

### Kolor czapek

<div class="text-justify">

     W tej zakładce odpowiemy graficznie na proste pytania związane ze
sprzedażą czapek ze względu na
kolor:

<br>

</div>

<img src="Kiowi_R_files/figure-gfm/kolor_czapek-1.png" width="80%" />

<img src="Kiowi_R_files/figure-gfm/kolor_czapek_procenty-1.png" width="80%" />

<br> <br>

### Efekt dnia tygodnia

Czy dzień tygodnia ma wpływ na sprzedaż czapek Kiowi?

<br>

![](Kiowi_R_files/figure-gfm/plotting_prod_zam-1.png)<!-- --> <br>

<div class="text-justify">

Wtorki i soboty to dni kiedy klienci najchętniej składają zamówienia.
Nie można wyróżnić jednego dnia z istotnie najniższą liczbą zamówień.
Bardziej szczegółowych danych dostarczy nam wizualizacja na wykresie
pudełkowym.

</div>

<br>

![](Kiowi_R_files/figure-gfm/boxplot_wday-1.png)<!-- -->

<br>

<div class="text-justify">

Liczba zamówień na wykresie pudełkowym obrazuje, że wszystkie dni mają
medianę na podobynm poziomie (3-4 zamówienia). Jednak wtorek, sobota i
niedziela są bardziej podatne na odchylenia w kierunku większej ilości
zamówień (długie wąsy górne)

</div>

<br>

Spróbujemy wykluczyć hipotezę, że na te odchylenia miały wpływ jedynie
dni tygodnia, bez udziału wpływu budżetu reklamowego.

![](Kiowi_R_files/figure-gfm/outliers-1.png)<!-- -->

     Widzimy, że obserwacje odchylone i odstające w sobotę i niedzielę
wiązały się z największymi nakładami reklamowymi (4 maksymalnie
wychylone punkty względem osi poziomej) Dlatego hipoteza, że to nakłady
reklamowe decydowały o odchyleniach w wyżej wspomnianych dniach tygodnia
wydaje się bliższa rzeczywistości, niż hipoteza o efekcie tygodnia,
którą najprawdopodbiej odrzucimy.

     Aby zweryfikować hipotezy o wpływie dni tygodnia przeprowadzimy
dwuczynnikową analizę wariancji z interakcją. Zbadaniu wpływu na liczbę
zamówień zostaną poddane trzy czynniki: dzień tygodnia, budżet oraz
interakcja dnia tygodnia z budżetem (być może tylko któryś dzień
tygodnia w połączeniu z budżetem daje istotnie różne wyniki)

    ##                  Df Sum Sq Mean Sq F value   Pr(>F)    
    ## dzien_tyg         6   19.8     3.3   0.195    0.977    
    ## budzet            1 1917.1  1917.1 113.244 2.83e-16 ***
    ## dzien_tyg:budzet  6  121.5    20.2   1.196    0.319    
    ## Residuals        70 1185.0    16.9                     
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

<div class="text-justify">

<br> Wyniki analizy wariancji mówią nam, że **jedynie czynnik budżetu
istotnie wpływa na liczbę zamówień.** Ostatecznie odrzucamy hipotezę
mówiącą o efekcie dnia tygodnia.

<br>

     Zarówno w tym teście jak i poprzednim rozdziale o korelacji,
zauważyliśmy, że budżet reklamowy ma istotny, i silny wpływ na
zamówienia. Mimo to, musimy założyć, że ten wpływ ma swój ograniczony
zakres. Dlatego zakładamy, że istnieje punkt przegięcia - punkt w którym
dodatkowe nakłady nie dają proporcjonalnych korzyści. Poniższe dwa
wykresy mogą stanowić ku temu przesłankę.

</div>

<br>

![](Kiowi_R_files/figure-gfm/plotting_dni_tyg-1.png)<!-- -->

     Widzimy, że zwiększone wydatki w niedziele nie znalazły
odzwierciedlenia w liczbie zamówień.

<br>

![](Kiowi_R_files/figure-gfm/zam_budzet_ratio-1.png)<!-- -->

W efekcie wskaźnik efektywności (iloraz: zamówienia/budżet) jest
najniższy właśnie dla niedzieli. Zagadnienie punktu przegięcia będzie
rozwijane w kolejnych zakładkach. <br> <br> <br> <br>

### Pogoda i zakażenia

<br>

<div class="text-justify">

     Do analizy włączmy inny czynnik, który być może, okaże się również
istotny: kolor punktów będzie reprezentował liczbę odnotowanych
pozytywnych przypadków COVID w Polsce.

</div>

<br>

![](Kiowi_R_files/figure-gfm/scatterplot_cov-1.png)<!-- -->

<br>

<div class="text-justify">

     Po kolorze punktów, widzimy, że wysoka liczba zachorowań wcale nie
znajdowała odbicia w zwiększonych przychodach. Najbardziej przychodowe
dni przypadały wtedy, gdy liczba zachorowań oscylowała w przedziale 5-10
tys nowych zakażeń. Mogło to być związane z wpływem psychologicznym i
niepokojem, kiedy liczba zakażeń zaczęła gwałtownie rosnąć, a może to
efekt sezonu, kiedy czapki z daszkiem najlepiej nadają się do noszenia.
Spróbujmy stworzyć ten sam wykres, ale tym razem kolor będzie
reprezentował miesiąc.

</div>

![](Kiowi_R_files/figure-gfm/scatterplot_mm-1.png)<!-- -->

Widzimy, że największe przychody są ściśle przywiązane do października.

<br>

![](Kiowi_R_files/figure-gfm/plot_line_mm-1.png)<!-- -->

Powyższy wykres potwierdza, że sklep miał największy ruch w październiku

<br>

![](Kiowi_R_files/figure-gfm/plot_line_facet-1.png)<!-- -->

<br>

Na powyższych wykresach widzimy, że przychód zaczyna spadać w drugiej
połowie października, a w tym momencie:

  - temperatura zaczyna łagodnie spadać
  - nowe zakażenia osiągają maxima, chwilowo spadają, by potem ponownie
    zaliczyć gwałtowny przyrost
  - utrzymywane są nakłady reklamowe

<br>

Ten sam wykres z “zoomem” na październik:
![](Kiowi_R_files/figure-gfm/plot_line_facet_2-1.png)<!-- --> <br> <br>

*źródła: baza danych Michała Rogalskiego; stacja pomiarowa w Poznaniu
<http://www.pimr.poznan.pl/>*

### Sezonowość

<br>

<div class="text-justify">

     W poprzednim rozdziale zauważyliśmy, że mimo utrzymania wydatków
reklamowych i wzrostu liczby zakażeń, przychody ze sprzedaży zaczęły
gwałtownie spadać w drugiej połowie października. Fakt, że tak silnie
skorelowana zmienna jak wydatki reklamowe przestały stymulować popyt,
oznacza, że musimy poszukać innego czynnika, który wyjaśniałby
zachowanie przychodów. W związku ze spadkiem temparatur i liczbie
słonecznych dni, racjonalną hipotezą jest twierdzenie o sezonowości w
sprzedaży czapek. Aby zweryfikować tę hipotezę posłużymy się testem
Chowa. Idea testu polega na arbitralnym wyborze punktu zwrotnego w
czasie i sprawdzenie, czy parametry modelów przed i po tym punkcie
istotnie różnią się od siebie.**Hipotezę zerową dla naszego przypadku
możemy sformułować następująco: model opisujący relację między
wydatkami a przychodami jest taki sam dla okresu do 21 października
(on-season) jak dla okresu od 22 października (off-season) **

</div>

<br> Test Chowa:

    ##      F value        d.f.1        d.f.2      P value 
    ## 2.075897e+01 2.000000e+00 6.700000e+01 9.642807e-08

<div class="text-justify">

Wynik testu daje nam podstawy do odrzucenia hipotezy zerowej mówiącej o
braku sezonowości. Zatem zasadne jest osobne spojrzenie na relację
wydatki - przychód w on-seasonie i off-seasonie. Spróbujmy opisać tę
relację w tych dwóch przypadkach:

</div>

<br> <br> **Model regresji liniowej: przychód \~ wydatki On-season**

    ## 
    ## Call:
    ## lm(formula = przychod_on ~ budzet_on, data = onseason)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1149.85  -277.77   -87.31   132.46  1234.78 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -230.583    216.027  -1.067    0.296    
    ## budzet_on      8.116      1.013   8.009  2.3e-08 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 595.9 on 25 degrees of freedom
    ## Multiple R-squared:  0.7196, Adjusted R-squared:  0.7083 
    ## F-statistic: 64.14 on 1 and 25 DF,  p-value: 2.302e-08

![](Kiowi_R_files/figure-gfm/lr_on-1.png)<!-- -->

<br>

<div class="text-justify">

**Interpretacja:** W powyższym modelu regresji liniowej, zmienność
wydatków na reklamę wyjaśnia zmiany w przychodach w 72% (wskaźnik
determinacji R^2 = 0.7196), co można ocenić na bardzo dobre dopasowanie
modelu. Współczynnik regresji *beta = 8.116* mówi, że w on-season’ie
wzorst wydatków reklamowych o 100 zł przynosi wzrost dochodów o 811.6 zł

</div>

<br> <br> **Model regresji liniowej: przychód \~ wydatki Off-season **

    ## 
    ## Call:
    ## lm(formula = przychod_off ~ budzet_off, data = offseason)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -559.45 -187.32    1.14  183.78  651.10 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)   
    ## (Intercept) 181.5593   106.8390   1.699  0.09665 . 
    ## budzet_off    2.2123     0.7062   3.133  0.00315 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 297.9 on 42 degrees of freedom
    ## Multiple R-squared:  0.1894, Adjusted R-squared:  0.1701 
    ## F-statistic: 9.813 on 1 and 42 DF,  p-value: 0.003154

![](Kiowi_R_files/figure-gfm/lr_off-1.png)<!-- --> <br>

<div class="text-justify]">

**Interpretacja:** W powyższym modelu regresji liniowej dla
**off-seasonu**, zmienność wydatków na reklamę wyjaśnia zmiany w
przychodach w 19% (wskaźnik determinacji R^2 = 0.1894), co oceniamy na
bardzo niskie dopasowanie, a tym samym uznajemy, że model ten nie jest
satysfakcjonującym narzędziem do opisu rzeczywistości. Można zatem
twierdzić, że wydatki na reklamę mają bardzo słaby wpływ na przychody w
off-season’ie.

</div>
