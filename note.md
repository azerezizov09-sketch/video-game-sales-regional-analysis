# Regional Sales Breakdown and Genre Trends in Video Game Market

## 1. Dataset və alətlər

- **Dataset:** `vgsales.csv` (Kaggle: gregorut/videogamesales), **16 598 oyun, 11 sütun** (`Rank, Name, Platform, Year, Genre, Publisher, NA_Sales, EU_Sales, JP_Sales, Other_Sales, Global_Sales`).
- **Alətlər:** R (`tidyverse`: `dplyr`, `tidyr`, `readr`; `ggplot2`; `scales`), R Markdown ilə hazırlanmış hesabat. Tapşırıqda göstərilən pandas/matplotlib/seaborn əvəzinə R istifadə olunub, funksionallıq eynidir.
- **Vahid:** bütün satış rəqəmləri **milyon ədəd** ilə verilir.

## 2. Metodologiya

1. **Yükləmə:** `read_csv` ilə, `"N/A"` mətni çatışmayan dəyər (NA) kimi oxundu.
2. **Çatışmayan dəyərlər:**
   - `Year` sütununda **271** NA var idi və bu sətirlər **silindi** (16 598 → **16 327** sətir).
   - `Publisher` sütununda **58** NA var idi və **"Unknown"** ilə dolduruldu.
   - Təmizləmədən sonra heç bir sütunda NA qalmadı.
3. **Qlobal satış** `Genre`, `Platform` və `Publisher` üzrə cəmləndi, top 10 seçildi.
4. **Regional pay:** NA, EU və JP satışı `Global_Sales`-ə bölünüb 100-ə vuruldu, həm ümumi bazar, həm də hər janr üçün.
5. **Hər regionun ən populyar janrı** regionun janr üzrə cəmi satışına görə müəyyən edildi.
6. **İllik trend** yalnız 1980–2016 üçün hesablandı (37 il). 2017 və 2020 üçün datasetdə cəmi bir neçə sətir var, bu illər natamamdır.
7. **Top 10 oyun** `Global_Sales`-ə görə sıralandı. Dataset hər oyunu platforma üzrə ayrı sətir kimi saxlayır, ona görə nəticə "oyun + platforma" kombinasiyasıdır.
8. **Bonus:** onilliklər üzrə oyun başına orta satış və top 5 janr üçün grouped bar chart.
9. **Qrafiklər** `plots/` qovluğuna saxlandı: stacked bar, illik trend, top 10 publisher, onilliklər, grouped bar.

## 3. Əsas nəticələr

**Janr üzrə qlobal satış (top 5):** Action (1 723), Sports (1 309), Shooter (1 026), Role-Playing (924), Platform (829). Ardınca Misc (798), Racing (727), Fighting (444), Simulation (390) və Puzzle (242) gəlir.

**Platforma üzrə qlobal satış (top 5):** PS2 (1 233), X360 (970), PS3 (949), Wii (910), DS (819).

**Publisher üzrə qlobal satış (top 5):** Nintendo (1 784), Electronic Arts (1 093), Activision (721), Sony Computer Entertainment (607), Ubisoft (474).

**Ümumi regional paylar (Global-a görə):**

| Region | Pay |
|---|---|
| NA | 49.1% |
| EU | 27.3% |
| JP | 14.6% |
| Other | 8.9% |

**Hər regionun ən populyar janrı:** NA: Action, EU: Action, JP: Role-Playing.

**İllik trend:** satış 1995-ə qədər aşağı səviyyədə qalıb (1995-də 88.1), 1996-da 199-a sıçrayıb, 2008-də **678.9 mln** ilə pik həddə çatıb. Sonra azalma başlayıb: 2012-də 364, 2015-də 264, 2016-da 70.9. 2016 ilinin kəskin düşüşü real azalma yox, datanın natamamlığı ola bilər.

**Top 10 oyun:**

| # | Oyun | Platforma | Janr | İl | Satış |
|---|---|---|---|---|---|
| 1 | Wii Sports | Wii | Sports | 2006 | 82.7 |
| 2 | Super Mario Bros. | NES | Platform | 1985 | 40.2 |
| 3 | Mario Kart Wii | Wii | Racing | 2008 | 35.8 |
| 4 | Wii Sports Resort | Wii | Sports | 2009 | 33.0 |
| 5 | Pokemon Red/Pokemon Blue | GB | Role-Playing | 1996 | 31.4 |
| 6 | Tetris | GB | Puzzle | 1989 | 30.3 |
| 7 | New Super Mario Bros. | DS | Platform | 2006 | 30.0 |
| 8 | Wii Play | Wii | Misc | 2006 | 29.0 |
| 9 | New Super Mario Bros. Wii | Wii | Platform | 2009 | 28.6 |
| 10 | Duck Hunt | NES | Shooter | 1984 | 28.3 |

**Bonus: onilliklər üzrə oyun başına orta satış:**

| Onillik | Orta satış (mln) | Oyun sayı |
|---|---|---|
| 1980-lər | **1.84** | 205 |
| 1990-lar | 0.72 | 1 769 |
| 2000-lər | 0.50 | 9 208 |
| 2010-lar | 0.49 | 5 141 |

Oyun başına orta satış ən yüksək **1980-lərdədir**. Səbəb, o dövrdə datasetdə az oyun olması və onların çoxunun hit olmasıdır. Sonrakı onilliklərdə oyun sayı kəskin artdıqca orta satış azalıb.

## 4. Regional bazar üstünlükləri: 4 insight

1. **NA və EU oxşar zövqə malikdir, JP isə fərqlidir.** Hər iki Qərb bazarında birinci janr Action-dır (NA-da bazarın 19.9%-i, EU-da 21.4%-i), ardınca Sports (15.5% və 15.4%) və Shooter (13.3% və 12.9%) gəlir. Yaponiyada isə birinci janr **Role-Playing**-dir (bazarın 27.3%-i), Action ikinci (12.4%) və Sports üçüncüdür (10.5%).

2. **Shooter və Racing Qərb janrlarıdır.** Shooter-in satışının 56.0%-i NA-dan, 30.3%-i EU-dan, cəmi 3.7%-i JP-dən gəlir. Racing-in JP payı cəmi 7.8%-dir, EU payı isə 32.5% ilə bütün janrlar arasında ən yüksəkdir.

3. **Role-Playing, Strategy və Puzzle Yaponiyada ümumi ortalamadan çox satılır.** JP-nin bütün bazarda payı 14.6%-dir, amma Role-Playing-də 37.9% (bu, NA-nın 35.3%-lik payından da çoxdur), Strategy-də 28.3%, Puzzle-da 23.4%-dir.

4. **Nintendo hər üç regionda birincidir, amma Yaponiyada rəqibləri daha zəifdir.** Nintendo NA-da 816, EU-da 418, JP-də 455 mln satış edib. NA-da ikinci Electronic Arts (584), EU-da da Electronic Arts (367) gəlir. JP-də isə ikinci Namco Bandai (127) və üçüncü Konami (90.9) Nintendo-dan çox geridədir. Platforma baxımından NA-da X360 (594), EU-da PS3 (340) liderdir, JP-də isə DS (175) birinci, PS (140) və PS2 (138) ardınca gəlir.

## 5. Məhdudiyyətlər

- Dataset 2016-dan sonrakı illəri tam əhatə etmir. 2016 ili natamamdır (satış 70.9 mln, 2015-də 264 mln), ona görə son illərdəki azalma real azalmadan çox ola bilər.
- Dataset yalnız fiziki satışları (retail) əhatə edir, rəqəmsal satışlar yoxdur.
- "Other" regionu NA/EU/JP-dən kənar bütün bazarları birləşdirir.
- Top 10 oyun cədvəli "oyun + platforma" kombinasiyasıdır. Eyni oyun fərqli platformalarda ayrı sətir kimi sayılır.
