## Gettext-Nedir? .mo-.po-UzantiliDosyalarNedir?

Yazılım dillerine çoklu dil desteği sağlamak için çevirilerinin yapılması gerekir. Yazılımın hangi dilde çalışacağına kullanıcı karar verir ve dil seçimini yapar. Yazılımda belli bazı işlemler ve dosyalarla arayüzde istenilen dil ile kullanıcının rahat bir şekilde işlem yapması sağlanır.

Yazılım İngilizce olarak hazırlandığını varsayarsak, başka bir dilde çalışması için istenilen dil çevirisinin bulunması ve bunun çalıştırılması gerekmektedir. Burada kullanılacak olan farklı dillerde yazılmış olan mesajlar veya dökümantasyonlar .mo uzantılı dosyanın içinde bulunurlar. Bu dosyalar bir editör yardımıyla düzenlenebilen .po uzantılı dosyalardan oluşurlar. Kısaca .mo uzantılı dosyalar .po uzantılı dosyaların derlenmiş halidir. 


### Gettext, jinja ile nasıl kullanılır?

#### Eğer çevirilecek cümle kısa ise => 
```
{{ _(‘Daha fazlası için tıkla') }}
````
#### Eğer çevirilecek cümle kısa ise => 
````
 {% trans -%}
    Ağaç kabuklarının ve yosunların dokusundan ilham alınarak tasarlanan trikolar, sezonun kurtarıcı parçaları olarak gardırobunuzda kendine yer edinmeye kararlı.
    {%- endtrans %}
