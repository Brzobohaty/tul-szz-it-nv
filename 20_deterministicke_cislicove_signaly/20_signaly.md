 # ��slicov� sign�ly, DTFT/DFT/STFT
> Deterministick� ��slicov� sign�ly � popis v �asov� oblasti, periodicita, DTFT/DFT spektrum, kr�tkodob� spektr�ln� anal�za (STFT) + vyu�it� ok�nkov�ch funkc�, vzorkovac� teor�m, kvantizace.

## Deterministick� ��slicov� sign�l

Sign�l je (matematick�) funkce, kter� reprezentuje informaci o v�voji n�jak� fyzik�ln� veli�iny.\
Takov� sign�l je v re�ln�m sv�t� obvykle spojit� (analogov�) - akustika, elektrick� sign�l, teplota, tlak, etc. Vzorkov�n�m (v�b�r vzorku v dan�ch intervalech) a kvantov�n�m (p�i�azen�m jedn� z kone�n�ho mno�stv� hodnot) vznik� ��slicov� sign�l.\
Deterministick� ��slicov� sign�l je pak ka�d� ��slicov� sign�l, u kter�ho lze v jak�mkoliv okam�iku zjistit hodnotu s absolutn� jistotou (lze je popsat exaktn�m matematick�m vzorcem, nap�. ![x[n] = sin(\omega n)](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20sin%28%5Comega%20n%29) - opakem jsou stochastick� sign�ly, kde jsou funkce pops�ny statistick�m vzorcem.

## Popis sign�lu v �asov� oblasti

Sign�l ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) - indexovan� nekone�n� posloupnost ��sel z ![R](https://latex.codecogs.com/png.latex?%5Cmathbb%7BR%7D) nebo ![C](https://latex.codecogs.com/png.latex?%5Cmathbb%7BC%7D). \
Vznik� bu� vzorkov�n�m spojit�ho sign�lu ![x(t)](https://latex.codecogs.com/png.latex?x%28t%29) v ekvidistantn�ch okam�ic�ch (![T_s](https://latex.codecogs.com/png.latex?T_s), vzorkovac� perioda -> ![1/T_s = F_s](https://latex.codecogs.com/png.latex?1/T_s%20%3D%20F_s), vzorkovac� frekvence)

![x[n] = x(nT_s)](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20x%28nT_s%29)

nebo p�irozen� diskr�tn� sekvenc� (denn� v�voj cenov�ch akci�). 

Sign�l lze v �asov� oblasti rozlo�it do jednodu���ch funkc�, nap�.\

jednotkov� puls

![\delta[n] = 1 pokud n = 0, 0 otherwise](https://latex.codecogs.com/png.latex?%5Cdelta%28n%29%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Cquad%20%5Ctext%7Bpokud%20%7D%20n%20%3D%200%5C%5C%200%20%26%20%5Cquad%20%5Ctext%7Bjinak%20%7D%5C%5C%20%5Cend%7Bcases%7D)

jednotkov� skok

![u[n] = 1 pokud n >= 0, 0 otherwise](https://latex.codecogs.com/png.latex?u%28n%29%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Cquad%20%5Ctext%7Bpokud%20%7D%20n%20%5Cgeq%200%5C%5C%200%20%26%20%5Cquad%20%5Ctext%7Bjinak%20%7D%5C%5C%20%5Cend%7Bcases%7D)

## Periodicita sign�lu

Pokud

![x[n] = x[n + N], \forall n, N \in \mathbb{Z}, N > 0](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20x%5Bn%20&plus;%20N%5D%2C%20%5Cforall%20n%2C%20N%20%5Cin%20%5Cmathbb%7BZ%7D%2C%20N%20%3E%200)

pak sign�l ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) je ![N](https://latex.codecogs.com/png.latex?N)-periodick�, hodnoty se opakuj� s periodou ![N](https://latex.codecogs.com/png.latex?N).


## DTFT (Discrete Time Fourier Transform)

### Z�kladem

Komplexn� exponenciela

![x[n] = e^{j \omega_0 n}, \omega_0 \in \mathbb{R}](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20e%5E%7Bj%20%5Comega_0%20n%7D%2C%20%5Comega_0%20%5Cin%20%5Cmathbb%7BR%7D)

kde ![\omega_0](https://latex.codecogs.com/png.latex?%5Comega_0) je ��slicov� frekvence

![obr�zek komplexn� exponenciely](http://m.eet.com/media/1068017/lyons_pt2_3.gif)

### DTFT

Zobrazen� z mno�iny posloupnosti prvk� (�asov� oblast) do mno�iny spojit�ch komplexn�ch funkc� re�ln� prom�nn� (frekven�n� oblast)

![X(e^{j\omega}) = \sum\limits_{n=-\infty}^{\infty}{x[n] e^{-j n \omega}}](https://latex.codecogs.com/png.latex?X%28e%5E%7Bj%5Comega%7D%29%20%3D%20%5Csum%5Climits_%7Bn%3D-%5Cinfty%7D%5E%7B%5Cinfty%7D%7Bx%5Bn%5D%20e%5E%7B-j%20n%20%5Comega%7D%7D)

kde ![\omega \in \mathbb{R}](https://latex.codecogs.com/png.latex?%5Comega%20%5Cin%20%5Cmathbb%7BR%7D) je ��slicov� frekvence

![X(e^{j\omega})](https://latex.codecogs.com/png.latex?X%28e%5E%7Bj%5Comega%7D%29) je spojit� komplexn� funkce re�ln�ho parametru ![\omega](https://latex.codecogs.com/png.latex?%5Comega). V bod� ![\omega_0](https://latex.codecogs.com/png.latex?%5Comega_0) se pak jedn� o korelaci sign�lu ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) a komplexn� exponenciely ![e^{j n \omega_0}](https://latex.codecogs.com/png.latex?e%5E%7Bj%20n%20%5Comega_0%7D) (v podstat� jak moc se sign�l podob� kosinusovce dan� frekvence)\
Ve v�sledku se jedn� o rozlo�en� sign�lu ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) na sou�et nekone�n� mnoha funkc� ![\cos(\omega n + \Phi(\omega))](https://latex.codecogs.com/png.latex?%5Ccos%28%5Comega%20n%20&plus;%20%5CPhi%28%5Comega%29%29), naz�v�me DTFT spektrum.

Rozd�luje se na *magnitudu* (m�ra podobnosti ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) a ![e^{j n \omega_0}](https://latex.codecogs.com/png.latex?e%5E%7Bj%20n%20%5Comega_0%7D))

![|X(e^{j n \omega_0})|](https://latex.codecogs.com/png.latex?%7CX%28e%5E%7Bj%20n%20%5Comega_0%7D%29%7C)

a f�zi (f�zov� posun mezi ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) a ![e^{j n \omega_0}](https://latex.codecogs.com/png.latex?e%5E%7Bj%20n%20%5Comega_0%7D))

![\Phi(\omega_0)](https://latex.codecogs.com/png.latex?%5CPhi%28%5Comega_0%29)

Dohromady

![X(e^{j n \omega_0}) = |X(e^{j n \omega_0})| e^{j \Phi \omega_0}](https://latex.codecogs.com/png.latex?X%28e%5E%7Bj%20n%20%5Comega_0%7D%29%20%3D%20%7CX%28e%5E%7Bj%20n%20%5Comega_0%7D%29%7C%20e%5E%7Bj%20%5CPhi%20%5Comega_0%7D)

### Inverze
Inverze je d�na jako

![x[n] = \frac{1}{2\pi} \int\limits_{-\pi}^{\pi} X(e^{j\omega}) e^{j n \omega} d\omega](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20%5Cfrac%7B1%7D%7B2%5Cpi%7D%20%5Cint%5Climits_%7B-%5Cpi%7D%5E%7B%5Cpi%7D%20X%28e%5E%7Bj%5Comega%7D%29%20e%5E%7Bj%20n%20%5Comega%7D%20d%5Comega)

### Vlastnosti

- Periodicita - DTFT je periodick� s periodou ![2\pi](https://latex.codecogs.com/png.latex?2%5Cpi) (��slicov� frekvence od ![-\pi](https://latex.codecogs.com/png.latex?-%5Cpi) do ![\pi](https://latex.codecogs.com/png.latex?%5Cpi))

- Linearita
 
  ![ax_1[n] + bx_2[n] \Leftrightarrow aX_1(e^{j \omega}) + bX_2(e^{j \omega})](https://latex.codecogs.com/png.latex?ax_1%5Bn%5D%20&plus;%20bx_2%5Bn%5D%20%5CLeftrightarrow%20aX_1%28e%5E%7Bj%20%5Comega%7D%29%20&plus;%20bX_2%28e%5E%7Bj%20%5Comega%7D%29)


- Oto�en� - oto�en� ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) v �ase vede k oto�en� ![X(e^{j\omega})](https://latex.codecogs.com/png.latex?X%28e%5E%7Bj%5Comega%7D%29) ve frekvenci, tedy

  ![x[-n] = X(e^{-j n \omega})](https://latex.codecogs.com/png.latex?x%5B-n%5D%20%3D%20X%28e%5E%7B-j%20n%20%5Comega%7D%29)
  

- Konvolu�n� teor�m - konvoluce dvou sign�l� v �asov� oblasti vede k vyn�soben� ve frekven�n� oblasti

  ![h[n]*x[n] \Leftrightarrow H(e^{j n \omega})X(e^{j n \omega})](https://latex.codecogs.com/png.latex?h%5Bn%5D*x%5Bn%5D%20%5CLeftrightarrow%20H%28e%5E%7Bj%20n%20%5Comega%7D%29X%28e%5E%7Bj%20n%20%5Comega%7D%29)

  Stejn� tak to plat� obr�cen� - n�soben� sign�l� v �ase je konvoluc� ve frekvenci
  
  ![h[n]x[n] \Leftrightarrow H(e^{j n \omega})*X(e^{j n \omega})](https://latex.codecogs.com/png.latex?h%5Bn%5Dx%5Bn%5D%20%5CLeftrightarrow%20H%28e%5E%7Bj%20n%20%5Comega%7D%29*X%28e%5E%7Bj%20n%20%5Comega%7D%29)

- Parseval�v teor�m - DTFT zachov�v� energii sign�lu, tedy

  ![\sum\limits_{n=-\infty}^{\infty}{|x[n]|^2} = \frac{1}{2\pi} \int\limits_{-\pi}^{\pi}{|X(e^{j \omega})|^2 d\omega}](https://latex.codecogs.com/png.latex?%5Csum%5Climits_%7Bn%3D-%5Cinfty%7D%5E%7B%5Cinfty%7D%7B%7Cx%5Bn%5D%7C%5E2%7D%20%3D%20%5Cfrac%7B1%7D%7B2%5Cpi%7D%20%5Cint%5Climits_%7B-%5Cpi%7D%5E%7B%5Cpi%7D%7B%7CX%28e%5E%7Bj%20%5Comega%7D%29%7C%5E2%20d%5Comega%7D)

## DFT (Discrete Fourier Transform)

### DFT

DTFT p�ev�d� nekone�nou diskr�tn� �adu ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) na spojitou funkci ��slicov� frekvence ![X(e^{j\omega})](https://latex.codecogs.com/png.latex?X%28e%5E%7Bj%5Comega%7D%29). Zp�tn� rekonstrukce sign�lu ze spektra je mo�n�, pokud zn�me hodnoty spektra pro v�echny ��slicov� frekvence \omega. Pokud je trv�n� �ady kone�n�, pak je mo�n� perfektn� rekonstrukce zn�me-li N vhodn� zvolen�ch frekven�n�ch bod�. V podstat� se jedn� o vhodn� ekvidistantn� navzorkov�n� DTFT spektra N vzorky tak, �e

![\omega[k] = \frac{2 \pi k}{N}, 0 \leq k \leq N-1](https://latex.codecogs.com/png.latex?%5Comega%5Bk%5D%20%3D%20%5Cfrac%7B2%20%5Cpi%20k%7D%7BN%7D%2C%200%20%5Cleq%20k%20%5Cleq%20N-1)

Vzorec DFT je tedy

![X[k] = \sum\limits_{n=0}^{N-1}{x[n] e^{-j 2 \pi n k / N}}, 0 \leq k < N-1](https://latex.codecogs.com/png.latex?X%5Bk%5D%20%3D%20%5Csum%5Climits_%7Bn%3D0%7D%5E%7BN-1%7D%7Bx%5Bn%5D%20e%5E%7B-j%202%20%5Cpi%20n%20k%20/%20N%7D%7D%2C%200%20%5Cleq%20k%20%3C%20N-1)

naz�v�me ![N](https://latex.codecogs.com/png.latex?N)-bodov� DFT.

Vybr�n�m ![N](https://latex.codecogs.com/png.latex?N) bod� sign�lu se v podstat� prov�d� operace n�soben� sign�lu obd�ln�kov�m ok�nkem (viz ��st o ok�nk�ch).

### Inverze

Inverzn� DFT je d�na jako

![x[n] = \frac{1}{N} \sum\limits_{k=0}^{N-1}{X[k] e^{j 2 \pi n k / N}}, 0 \leq n \leq N-1](https://latex.codecogs.com/png.latex?x%5Bn%5D%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%5Csum%5Climits_%7Bk%3D0%7D%5E%7BN-1%7D%7BX%5Bk%5D%20e%5E%7Bj%202%20%5Cpi%20n%20k%20/%20N%7D%7D%2C%200%20%5Cleq%20n%20%5Cleq%20N-1)

## STFT (Short Time Fourier Transform)

Kompromis mezi dobr�m rozli�en�m v �ase (v�m, kde je v sign�lu aktivita) a frekvenci (v�m, ze kter�ch kosinusovek se sign�l skl�d� - jsem schopen ho dob�e analyzovat).

Sign�l je nejprve rozd�len do r�mc� vhodn� velikosti (dle �lohy, nap�. pro zpracov�n� �e�i je vhodn� volit d�lku r�mce mezi 10 - 40 ms kv�li kvazi-stacionarit� �e�i), obvykle s p�ekryvem okolo 50 %. 

Sign�l v ka�d�m r�mci je vyn�sobem vhodnou ok�nkovac� funkc� (Hamming, Hann, Blackmann...), v�b�r op�t z�vis� na �loze. Na ka�d� r�mec je aplikov�na DFT.

Jednotliv� r�mce jsou pak naskl�d�ny za sebe, ��m� vznik� graf ukazuj�c� v�voj aktivity spektra v �ase - spektrogram (obvykle jenom pro magnitudu).

![spektrogram](http://newt.phys.unsw.edu.au/jw/graphics/didj_spectrogram.JPG)

STFT je v�hodn� hlavn� pro anal�zu sign�l� se siln� dynamickou povahou (nap�. �e�, hudba).

## Ok�nkovac� funkce a prosakov�n� spektra

Ok�nkovac� funkce je funkce umo��uj�c� vybrat ze sign�lu kone�n� dlouhou sekvenci prvk�. Sign�l je jednodu�e v �asov� oblasti zn�soben koeficienty dan�ho ok�nka (nap�. obd�ln�kov� ok�nko = 1 tam kde chci sign�l zachovat, 0 jinde).

N�soben� v �asov� oblasti v�ak odpov�d� kruhov� konvoluci v oblasti frekven�n�. V�sledkem je tedy kruhov� konvoluce spektra sign�lu a spektra ok�nkovac� funkce, viz obr�zek, tzv. prosakov�n� spektra (spectral leakage).

![porovn�n� DTFT a ok�nkovan� DTFT](https://upload.wikimedia.org/wikipedia/commons/7/72/Spectral_leakage_Sine.svg)

U spektra ok�nkov�ch funkc� se uv�d�j� dva hlavn� parametry - ���ka hlavn�ho laloku a �tlum postrann�ch lalok�. Ide�ln� je co nejmen�� ���ku hlavn�ho laloku a co nejv�t�� �tlum lalok� postrann�ch, re�ln� je to v�dycky kompromis.\
P�i vysok� ���ce hlavn�ho laloku m��e doj�t ke sl�v�n� bl�zk�ch frekven�n�ch komponent, p�i n�zk�m �tlumu postrann�ch lalok� m��e doch�zet k maskov�n� slab�ch frekven�n�ch komponent, viz obr�zek - kosinusovky na frekvenc�ch 1 kHz, 1,1 kHz a 3 kHz(slab�).

![obr�zek laloky dvou ok�nek](http://media.wiley.com/Lux/36/379636.image1.jpg)

Dal�� probl�m nast�v� p�i navzorkov�n� DTFT pomoc� DFT - Pokud nen� ok�nko zvoleno ve spr�vn� d�lce, tak bude DTFT navzorkov�no nevhodn�, viz obr�zek - perfektn� navzorkovan� DTFT

![perfect DTFT sampling](http://blogs.mathworks.com/images/steve/2014/frequency_bins_for_sinusoid_v2_05.png)

a nevhodn� navzorkovan� DTFT

![imperfect DTFT sampling](http://blogs.mathworks.com/images/steve/2014/frequency_bins_for_sinusoid_v2_07.png)

## Vzorkovac� teor�m

### Definice
Je-li ![\Omega_0](https://latex.codecogs.com/png.latex?%5COmega_0) nevy��� frekvenc� obsa�enou v analogov�m sign�lu ![x_a(t)](https://latex.codecogs.com/png.latex?x_a%28t%29) (sign�l je p�smov� omezen), pak ![x_a(t)](https://latex.codecogs.com/png.latex?x_a%28t%29) je mo�n� jednozna�n� rekonstruovat z jeho vzork� ![x_a(nT_s)](https://latex.codecogs.com/png.latex?x_a%28nT_s%29) pokud

![\Omega_s = \frac{2\pi}{T_s} \geq 2\Omega_0](https://latex.codecogs.com/png.latex?%5COmega_s%20%3D%20%5Cfrac%7B2%5Cpi%7D%7BT_s%7D%20%5Cgeq%202%5COmega_0)

![\Omega_0](https://latex.codecogs.com/png.latex?%5COmega_0) se naz�v� Nyquistova frekvence

### Prakticky
Nejvy��� frekvence obsa�en� v sign�lu nesm� b�t v�t�� ne� polovina vzorkovac� frekvence.

### Aliasing

P�i nedodr�en� vzorkovac�ho teor�mu doch�z� k aliasingu - p�ekl�d�n� frekvenc� ve spektru - a t�m k nejednozna�nosti rekonstrukce sign�lu, viz obr�zek.

![chirp aliasing](http://i.imgur.com/kvacDPJ.png)
Naho�e zvy�uj�c� se t�n od 0 do 2 kHz, vzorkovac� frekvence 4 kHz (spl�uje vzorkovac� teor�m). \
Dole zvy�uj�c� se t�n od 0 do 4 kHz, vzorkovac� frekvence 4 kHz (od poloviny trv�n� nespl�uje vzorkovac� teor�m a je p�elo�en (doslova)).

## Kvantizace

### Definice

Jedn� se o transformaci spojit�ch amplitud diskr�tn� (navzorkovan�) �ady ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) na diskr�tn� kone�nou mno�inu amplitud

![\hat{x}[n] = Q(x[n])](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D%5Bn%5D%20%3D%20Q%28x%5Bn%5D%29)

Spojit� amplituda je rozd�lena na ![L](https://latex.codecogs.com/png.latex?L) nep�ekr�vaj�c�ch se interval� ![l_k](https://latex.codecogs.com/png.latex?l_k) pomoc� ![L+1](https://latex.codecogs.com/png.latex?L&plus;1) rozhodovac�ch hladin ![x_1, x_2,...,x_{L+1}](https://latex.codecogs.com/png.latex?x_1%2C%20x_2%2C...%2Cx_%7BL&plus;1%7D)

![l_k = [x_k, x_{k+1}], k = 1, 2,..., L](https://latex.codecogs.com/png.latex?l_k%20%3D%20%5Bx_k%2C%20x_%7Bk&plus;1%7D%5D%2C%20k%20%3D%201%2C%202%2C...%2C%20L)

Pokud ![x[n]](https://latex.codecogs.com/png.latex?x%5Bn%5D) pat�� do intervalu ![l_k](https://latex.codecogs.com/png.latex?l_k), kvantizace p�i�ad� ![\hat{x}[n]](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D%5Bn%5D) hodnotu ![\hat{x}_k](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D_k)

### Prakticky

![\hat{x}[n] = round(x[n])](https://latex.codecogs.com/png.latex?%5Chat%7Bx%7D%5Bn%5D%20%3D%20round%28x%5Bn%5D%29)

Kvantiza�n� rozli�en� (���ka mezi rozhodovac�mi �rovn�mi) nem�nn�, po�et rozhodovac�ch hladin jako mocnina dvou (kv�li bin�rn�mu k�dov�n� po kvantizaci).

### Kvantiza�n� chyba a SQNR

Rozd�l mezi skute�nou a kvantovanou hodnotou

![e[n] = x[n] - Q(x[n])](https://latex.codecogs.com/png.latex?e%5Bn%5D%20%3D%20x%5Bn%5D%20-%20Q%28x%5Bn%5D%29)

SQNR - Signal to Quantization Noise Ratio, Odstup sign�lu od kvantiza�n�ho �umu

![SQNR = 10 \log{\frac{\sigma_x^2}{\sigma_e^2}} \approx 6.02 \text{ dB per bit}](https://latex.codecogs.com/png.latex?SQNR%20%3D%2010%20%5Clog%7B%5Cfrac%7B%5Csigma_x%5E2%7D%7B%5Csigma_e%5E2%7D%7D%20%5Capprox%206.02%20%5Ctext%7B%20dB%20per%20bit%7D)

tzn. p�id�n�m jednoho bitu se SQNR svy�uje o cca 6 dB (4x).



