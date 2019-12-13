# Gettext-Transtag_.mo_.po

Yazılım dillerine çoklu dil desteği sağlamak için çevirilerinin yapılması gerekir. Yazılımın hangi dilde çalışacağına kullanıcı karar verir ve dil seçimini yapar. Yazılımda belli bazı işlemler ve dosyalarla arayüzde istenilen dil ile kullanıcının rahat bir şekilde işlem yapması sağlanır.

Yazılım İngilizce olarak hazırlandığını varsayarsak, başka bir dilde çalışması için istenilen dil çevirisinin bulunması ve bunun çalıştırılması gerekmektedir. Burada kullanılacak olan farklı dillerde yazılmış olan mesajlar veya dökümantasyonlar .mo uzantılı dosyanın içinde bulunurlar. Bu dosyalar bir editör yardımıyla düzenlenebilen .po uzantılı dosyalardan oluşurlar. Kısaca .mo uzantılı dosyalar .po uzantılı dosyaların derlenmiş halidir. 


## transtag HTML'de nasıl kullanılır?

####   => Eğer çevirilecek cümle kısa ise =>
```
{{ _(‘Daha fazlası için tıkla') }}
```
####   => Eğer uzun paragraf çevirilecek ise =>

```
{% trans -%}
Koleksiyonun odak noktasında yer alan Pierre Cardin trikolar, yeni sezonda daha koyu ve daha derin.
Eski dostu tam balıkçı yakalar ile tekrar buluşan trikolara, şehirli erkeğin kayıtsız kalması ise imkansız!
Koleksiyonun odak noktasında yer alan Pierre Cardin trikolar, yeni sezonda daha koyu ve daha derin.
Eski dostu tam balıkçı yakalar ile tekrar buluşan trikolara, şehirli erkeğin kayıtsız kalması ise imkansız!
{%- endtrans %}
```
####   => .format referans vererek kullanım;

````
{{ _('{}Ön Bilgilendirme Koşulları`nı{} ve {}Uzaktan Satış
Sözleşmesi`ni{} okudum ve kabul ediyorum.'.format('<a href="/orders/contract/?contract_name=info"
class="js-ajax-popup">','</a>',
'<a href="/orders/contract/?contract_name=sales" class="js-ajax-popup">','</a>'))}}
````

````
{% trans link=url('account-contact') -%}
  Görüş, öneri ya da şikayetinizi paylaşmak isterseniz, <a href="{{ link }}">İletişim Formu</a>’nu 
  doldurarak bize ulaştırabilirsiniz.
 {%- endtrans %}
````
####   => if loop kullanımı

```
 {{ _('adlı {} stokta kalmadığı için sepetinizden çıkarıldı!').format(
      _('ürünler') if products|length > 1 else _('ürün')
 ) }}
```

##  gettext js dosyasına dahil etme
örnek olarak;
````
import gettext from 'dosya-konumu/gettext';

 results.forEach(function (el) {
    template += `<li>
      <a href="${el.id}">
        <span>${gettext('Sipariş')} : <b>${el.number}</b></span> 
        <span>${el.amount} ${el.currency.label </span>
      </a></li>`;
});
````

### setting.py için örnek kod ayarlamaları
````
LANGUAGE_CODE = 'tr-tr' 	* Asıl yazılan, varsayılan dil

LANGUAGES = [  			* UI'da kullanıcını seçeceği ve gerekli .po dosyalarının bulunduğu, dil seçeneği.  
    ('tr-tr', u'Türkçe'),      
    ('us-en', u'İngilizce'),
    ('fr-fr', u'Fransızca'),
    ('ru-ru', u'Rusça'),
    ('es-es', u'İspanyolca'),
]
````

## Genel olarak yukarıda verilen bilgiler ile HTML veya js'te yapılacak uygulamalardan sonra;

#### Terminalde sırasıyla (Örnek çeviri İngilizce - Türkçe) ;

  ### HTML .po dosyasını çıkarmak için;
   #### A-1 => 

       ````
       sudo python manage.py makemessages —locale=en_US
       sudo python manage.py makemessages --locale=tr_TR
       ````
       Komut uygulaması ile .po dosyası oluşturuluyor.

   #### A-2 =>
      .po dosyası oluşturulduktan sonra,
      ````
      sudo python manage.py compilemessages --locale=en_US
      sudo python manage.py compilemessages --locale=tr_TR
      ````
      Komut uygulaması ile compile messagess oluşturuluyor.


 ### JS .po dosyasını çıkarmak için;
 
   #### B-1 İngilizce dili için çıkarılacak .po için => 
        
       ````
        python manage.py jsmakemessages --locale=en_US -d djangojs --ignore=node_modules
        --ignore=bundle.js --settings=shomnipro.settings --localedir=/file/patch/project/locale
       ````
       Komut uygulaması ile .po dosyası oluşturuluyor.
   
   #### B-2 Türkçe dili için çıkarılacak .po için => 
        
       ````
        python manage.py jsmakemessages --locale=tr_TR -d djangojs --ignore=node_modules
        --ignore=bundle.js --settings=shomnipro.settings --localedir=/file/patch/project/locale
       ````
       Komut uygulaması ile .po dosyası oluşturuluyor.
   
   #### B-3 compilemessages için =>
   
       ````
       python manage.py jscompilemessages --locale=en_US
       python manage.py jscompilemessages --locale=tr_TR
       ````

   
      
