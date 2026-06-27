# Enerji Tuketimi Odakli Benchmark Degerlendirme Raporu

## 1. Raporun Amaci

Bu rapor, buyuk dil modellerinin farkli yapilandirilmis cikti formatlari ile gorevleri yerine getirirken ortaya cikan enerji tuketimi farklarini incelemek amaciyla hazirlanmistir. Degerlendirme, calisma klasorundeki `summary_*.csv` ve `timeseries_*.csv` dosyalarindan otomatik olarak yuklenen benchmark sonuclarina dayanmaktadir.

Analizde 7 model, 4 cikti formati ve 81 ozet kayit yer almaktadir. Raporun temel odagi model kalitesi degil, ayni gorev kosullarinda format, model ve gorev karmasikliginin enerji tuketimi uzerindeki etkisidir.

Bu raporda syntax ve semantic basari tum modeller ve formatlar icin tam kabul edilmistir. Bu nedenle kalite skoru farki yaratilmamis, tum yorumlar enerji, guc tuketimi, token sayisi ve yanit uzunlugu uzerinden yapilmistir.

## 2. Temel Bulgular

- Format secimi enerji tuketimini belirgin sekilde etkilemektedir.
- Ortalama enerji tuketimi en dusuk formatlar TONL ve XML olarak gorunmektedir.
- YAML, ozellikle karmasik gorevlerde en yuksek enerji tuketimine sahip formattir.
- Model bazinda qwen2.5-14b en dusuk ortalama enerji tuketimini gostermektedir.
- Deepseekr1-qwen14, llama3.2-1b ve gpt-oss-20b-MXFP4-Q8 daha yuksek enerji maliyetine sahiptir.
- Enerji artisinin en belirgin oldugu gorev grubu highly-nested-multimodal gorevlerdir.
- Token sayisi ve yanit uzunlugu arttikca enerji tuketimi de belirgin bicimde artmaktadir.

## 3. Formatlarin Enerji Tuketimi Karsilastirmasi

| Format | Kayit Sayisi | Ortalama Enerji (mWh) | Medyan Enerji (mWh) | Toplam Enerji (mWh) | Ortalama Token | Ortalama Yanit Karakteri |
|---|---:|---:|---:|---:|---:|---:|
| TONL | 21 | 1.8061 | 0.8928 | 32.5107 | 511.7 | 586.3 |
| XML | 21 | 2.0360 | 0.9141 | 42.7567 | 472.5 | 779.1 |
| TOML | 21 | 3.4152 | 1.0498 | 71.7198 | 541.8 | 623.1 |
| YAML | 21 | 8.2454 | 0.9595 | 173.1531 | 2343.0 | 5512.3 |

Format ortalamalari incelendiginde TONL en dusuk ortalama enerji tuketimine sahiptir. XML, TONL'ye cok yakin bir enerji profili sunmakta ve toplam enerji acisindan da makul bir seviyede kalmaktadir. TOML orta seviyede enerji tuketirken, YAML acik sekilde en yuksek ortalama ve toplam enerji degerlerine sahiptir.

YAML'in medyan enerji degeri dusuk olmasina ragmen ortalama ve toplam enerji degerlerinin cok yuksek olmasi, belirli gorevlerde veya model-format kombinasyonlarinda enerji tuketiminin asiri yukseldigini gostermektedir. Bu durum ozellikle karmasik gorevlerde ortaya cikmaktadir.

## 4. Gorev Karmasikligina Gore Format Etkisi

| Gorev Karmasikligi | Format | Ortalama Enerji (mWh) | Ortalama Token | Ortalama Yanit Karakteri |
|---|---|---:|---:|---:|
| simple | TOML | 1.2942 | 296.6 | 192.1 |
| simple | XML | 1.4762 | 278.7 | 245.0 |
| simple | TONL | 1.4949 | 336.7 | 263.0 |
| simple | YAML | 2.0596 | 221.7 | 113.1 |
| nested | TONL | 1.2861 | 315.2 | 113.7 |
| nested | XML | 1.4219 | 211.3 | 140.1 |
| nested | TOML | 1.8312 | 294.0 | 151.1 |
| nested | YAML | 2.5445 | 215.1 | 92.6 |
| highly-nested-multimodal | TONL | 2.6375 | 883.2 | 1382.2 |
| highly-nested-multimodal | XML | 3.2099 | 927.4 | 1952.3 |
| highly-nested-multimodal | TOML | 7.1202 | 1034.9 | 1526.0 |
| highly-nested-multimodal | YAML | 20.1320 | 6592.0 | 16331.1 |

Gorev karmasikligi arttikca formatlar arasindaki enerji farki buyumektedir. Simple gorevlerde formatlar arasindaki fark gorece sinirliyken, highly-nested-multimodal gorevlerde YAML enerji tuketimi bakimindan diger formatlardan belirgin sekilde ayrilmaktadir.

Highly-nested-multimodal gorevlerde YAML'in ortalama enerji tuketimi 20.1320 mWh seviyesine cikmistir. Bu deger, ayni gorev grubundaki TONL degerinin yaklasik 7.6 kati, XML degerinin yaklasik 6.3 kati ve TOML degerinin yaklasik 2.8 katidir.

Bu bulgu, karmasik ve uzun cikti gerektiren gorevlerde format seciminin enerji maliyeti uzerindeki etkisinin kritik hale geldigini gostermektedir.

## 5. Model Bazinda Enerji Tuketimi

| Model | Kayit Sayisi | Ortalama Enerji (mWh) | Medyan Enerji (mWh) | Toplam Enerji (mWh) | Ortalama Token | Ortalama Yanit Karakteri |
|---|---:|---:|---:|---:|---:|---:|
| qwen2.5-14b | 12 | 0.6966 | 0.4088 | 8.3590 | 164.5 | 533.7 |
| gemma3-4b | 12 | 0.8537 | 0.5510 | 10.2445 | 281.0 | 745.7 |
| qwen3-0.6b-8bit | 12 | 1.1177 | 0.9952 | 13.4128 | 582.8 | 494.8 |
| mistral7b | 12 | 2.3296 | 1.2367 | 27.9558 | 240.7 | 609.3 |
| gpt-oss-20b-MXFP4-Q8 | 12 | 6.0452 | 3.5851 | 72.5428 | 1866.3 | 669.8 |
| llama3.2-1b | 12 | 7.4549 | 0.3810 | 89.4593 | 2852.3 | 9451.7 |
| deepseekr1-qwen14 | 12 | 10.9073 | 10.2682 | 98.1660 | 873.6 | 633.2 |

Model bazinda en dusuk ortalama enerji tuketimi qwen2.5-14b modelinde gorulmektedir. Bu model ayni zamanda dusuk token sayisi ile kontrollu bir cikti profili sunmaktadir. Gemma3-4b ve qwen3-0.6b-8bit de dusuk enerji grubunda yer almaktadir.

Deepseekr1-qwen14 en yuksek ortalama enerji tuketimine sahiptir. Llama3.2-1b'nin medyan enerji degeri dusuk gorunmesine ragmen ortalama ve toplam enerji degerleri yuksektir; bu durum bazi gorevlerde cok uzun cikti uretmesinden kaynaklanmaktadir.

## 6. Model-Format Kombinasyonlari

| Model | En Dusuk Enerjili Format | Ortalama Enerji (mWh) | En Yuksek Enerjili Format | Ortalama Enerji (mWh) | Yorum |
|---|---|---:|---|---:|---|
| deepseekr1-qwen14 | XML | 6.6699 | TOML | 13.6029 | Bu modelde format secimi enerji maliyetini iki kata yakin degistirmektedir. |
| gemma3-4b | XML | 0.4679 | TOML | 1.2606 | XML bu model icin en verimli formattir. |
| gpt-oss-20b-MXFP4-Q8 | XML | 2.9600 | YAML | 11.5717 | YAML enerji maliyetini belirgin sekilde artirmaktadir. |
| llama3.2-1b | TONL | 0.2290 | YAML | 28.7000 | YAML bu modelde asiri yuksek enerji maliyetine yol acmistir. |
| mistral7b | XML | 1.9293 | TOML | 2.6574 | Format farki vardir, ancak diger modellere gore daha sinirlidir. |
| qwen2.5-14b | TONL | 0.4588 | XML | 0.9344 | Tum formatlarda dusuk enerji profili korunmaktadir. |
| qwen3-0.6b-8bit | TONL | 0.9240 | YAML | 1.4534 | Format farki sinirli fakat TONL daha verimlidir. |

Model-format karsilastirmasi, format etkisinin modelden modele degistigini gostermektedir. En carpici fark llama3.2-1b modelinde gorulmektedir: TONL formatinda ortalama enerji 0.2290 mWh iken YAML formatinda 28.7000 mWh seviyesine cikmaktadir.

Benzer sekilde gpt-oss-20b-MXFP4-Q8 modelinde XML 2.9600 mWh ile en verimli format iken YAML 11.5717 mWh ile cok daha maliyetlidir. Bu nedenle format secimi, yalnizca genel ortalamalarla degil, model bazli olarak da degerlendirilmelidir.

## 7. Guc Tuketimi ve Enerji Iliskisi

| Format | Ortalama CPU Power (mW) | Ortalama GPU Power (mW) | Ortalama Enerji (mWh) |
|---|---:|---:|---:|
| TONL | 270.1 | 65.1 | 1.8061 |
| XML | 252.5 | 75.9 | 2.0360 |
| TOML | 306.9 | 89.9 | 3.4152 |
| YAML | 275.5 | 157.5 | 8.2454 |

GPU guc tuketimi ile toplam enerji arasinda belirgin bir iliski vardir. YAML, ortalama GPU gucu en yuksek format olarak gorulmekte ve ayni zamanda en yuksek ortalama enerji tuketimine sahiptir.

XML ve TONL daha dusuk GPU gucu ve daha dusuk enerji profili sunmaktadir. Bu nedenle GPU enerjisi veya termal butce kritik olan sistemlerde XML ve TONL daha avantajli formatlar olarak degerlendirilebilir.

## 8. Sonuc

Enerji odakli degerlendirme, format seciminin benchmark maliyetini dogrudan etkiledigini gostermektedir. Genel ortalamalara gore TONL ve XML en verimli formatlar olarak one cikmaktadir. TOML orta seviyede kalirken, YAML ozellikle karmasik gorevlerde ve belirli modellerde enerji maliyetini ciddi bicimde artirmaktadir.

Model bazinda qwen2.5-14b en dusuk ortalama enerji tuketimine sahiptir. Gemma3-4b ve qwen3-0.6b-8bit de dusuk enerji profiliyle uygun alternatiflerdir. Deepseekr1-qwen14, llama3.2-1b ve gpt-oss-20b-MXFP4-Q8 ise ayni kalite varsayiminda daha yuksek enerji maliyetine sahiptir.

Bu sonuclar, yapilandirilmis cikti benchmarklarinda enerji verimliligi icin yalnizca model seciminin yeterli olmadigini, format seciminin de kritik bir parametre oldugunu gostermektedir.

## 9. Enerji Odakli Oneriler

- Genel enerji verimliligi icin ilk tercih: qwen2.5-14b.
- Dusuk enerji isteyen uygulamalar icin alternatif modeller: gemma3-4b ve qwen3-0.6b-8bit.
- Format seciminde dusuk enerji icin: TONL veya XML.
- Karmasik gorevlerde YAML kullanimi enerji maliyeti nedeniyle dikkatle degerlendirilmelidir.
- Model-format secimi her model icin ayri incelenmelidir; ayni format farkli modellerde cok farkli enerji maliyeti dogurabilir.
- Enerji butcesi sinirli sistemlerde uzun yanit ureten modeller ve formatlar kontrollu kullanilmalidir.
