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

