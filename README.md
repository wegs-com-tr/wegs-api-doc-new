# api-doc-new


# WEGS API DOC

![Logo](https://app.wegs.com.tr/images/logo/logo-light-crop.png)

    
## API Dokümantasyonu

<a href="https://wegs.com.tr">Muhasebe Programı</a>

## - Ücretsiz Kayıt Olmak İçin Tıkla 

- Wegs' Ücretsiz Tıkla Kaydol (https://app.wegs.com.tr/)

## - Cari Bilgilerini Gönderme

## Açıklama
Bu API, müşteri (cari) bilgilerini sisteme göndermek için kullanılır.
- client_id: Panelde Solda Client id mevcut.
- api_key: Ayarlar -> lisanslar bölümünde.

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

Endpoint:
```http
POST https://wegs.dev/V2/customers
```

####  Request Body:
####  Cari Bilgileri:
- phone (string): Carinin telefon numarası. (Sıfır olmadan) ZORUNLU ***
- mail (string): Carinin e-mail adresi. ZORUNLU ***
- tcvkn (string): Müşterinin TCsi yada vkn si.ZORUNLU ***
- customer_title (string): Cari unvanı. ZORUNLU ***
- tag (string, nullable): Carinin kısa ismi.
- cari_group (string, nullable): Cari grubu.
- cari_code (string, nullable): Cari kodu.
- vd (string, nullable): Vergi Dairesi.
- billing_address (string): Fatura adresi. ZORUNLU ***
- delivery_address (string, nullable): Teslimat adresi.
- city (string): Şehir.
- district (string): İlçe.
- country (string): Ülke kodu. Ülke kodları kısaltılmış formatta olmalı. Örneğin TR, US, DE, AU gibi. Aksi halde fatura oluştururken hata alabilirsiniz.
- state (string): Eyalet/Bölge.
- post_code (string): Posta kodu.
- note (string): Not.

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Cari": {
    "phone": "5064723443",
    "mail": "example@mail.com",
    "customer_title": "Ornek Musteri",
    "tag": "Ornek",
    "cari_group": null,
    "cari_code": null,
    "tcvkn": null,
    "vd": null,
    "billing_address": "12.CAD.30.SOK.34/6 DEMETEVLER",
    "delivery_address": null,
    "city": "Ankara",
    "district": "Yenimahalle",
    "country": "TR",
    "state": null,
    "post_code": "6000",
    "note": ""
  }
}
```

## - Cari Bilgilerini Listeleme
Endpoint:
```http
POST https://wegs.dev/V2/customers
```
####  Örnek post JSON

```json
{
  "Action": {
    "type": "list"
  }
}

```

## - Ürün Bilgilerini Gönderme
Endpoint:
```http
POST https://wegs.dev/V2/products
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Request Body:
####  Urun Bilgileri:
- barcode (string): Ürün barkod numarası.
- stock_code (string): Stok kodu.
- product_name (string): Ürün adı. ZORUNLU ***
- stock_tracking (int): Stok takibi yapılıp yapılmayacağı. (1: Yapılacak, 0: Yapılmayacak)
- currency_type (string): Para birimi türü. ZORUNLU ***
- tax (int): Vergi yüzdesi. ZORUNLU ***
- price_1 (float): Ürün parekende fiyatı.
- price_2 (float): Ürün alış fiyatı. (null olabilir)
- price_3,price_4,price_5,price_6,price_7,price_8 (float): Sizin belirleyeceğiniz fiyatlar. (null olabilir)
- unit_type (string): Ürün birim türü. (Örneğin: Adet, Kg, Litre) ZORUNLU ***
- quantity (int): Fatura kalemindeki adet.
- product_description : Ürün açıklaması. max 2000 karakter sınırlaması vardır.
- specialArea: Ürüne ait varyantlar, detaylı ürün bilgileri (Örneğin: Beden, renk, boy)

##### Lütfen stok kodu yazıyorsanız gerçek olsun sonradan gelen istekler stok koduna göre işlem yapacak. yoksa sadece isim göndermeniz yeterli.

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Urun": {
      "barcode": "",
      "stock_code": "stokkodu",
      "stock_group_code": "stokgrupkodu",
      "product_name": "API Ozel Alan",
      "stock_tracking": 1,
      "currency_type": "TRY",
      "tax": 0,
      "price_1": 20,
      "price_2": 10,
      "price_3": null,
      "price_4": null,
      "price_5": null,
      "price_6": null,
      "price_7": null,
      "price_8": null,
      "unit_type": "Adet",
      "quantity": 0,
      "product_description": "Ürün bilgileri",
      "specialArea": [
        {
          "item_name": "Renk",
          "item_value": "Kırmızı"
        },
        {
          "item_name": "Beden",
          "item_value": "M"
        },
        {
          "item_name": "Boy",
          "item_value": "150"
        }
      ]
    }
}


```
## - Ürün Bilgilerini Listeleme
Endpoint:
```http
POST https://wegs.dev/V2/products
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Örnek post JSON

```json
{
  "Action": {
    "type": "list"
  }
}
```


## - Tüm Ürün Kategori Bilgilerini Listeleme
Endpoint:
```http
POST https://wegs.dev/V2/categories
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key
- 
####  Request Body:
- category_type : Listeleme için 'category_type' alanının 'category' olarak kalması gerekmektedir.
  
####  Örnek post JSON

```json
{
  "Action": {
    "type": "list",
    "category_type": "category"
  }
}
```


## - İlgili Kategori Bilgilerini Görüntüleme
Endpoint:
```http
POST https://wegs.dev/V2/categories
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key
- 
####  Request Body:
- category_type : Listeleme için 'category_type' alanının 'category' olarak kalması gerekmektedir.
- category_id : İlgili kategorinin oid'i. Ürünün category_id'si ile bu kategorinin bilgisine ulaşılabilir.
  
####  Örnek post JSON

```json
{
  "Action": {
    "type": "read",
    "category_type": "category",
    "category_id" : "65576ce69b50ce288e01e484"
  }
}
```

## - Satış Bilgilerini Gönderme
Endpoint:
```http
POST https://wegs.dev/V2/sales
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Request Body:
####  Satış Bilgileri:
- title (string): Satış başlığı.
- invoiceNumber (string): Satış numarası (ZORUNLU ***)
- invoiceTo_id(string) : Cari oid  (ZORUNLU ***)
- invoiceDate (string): Satış Tarihi. (ZORUNLU ***)
- invoiceExchange(string): Para birimi türü (ZORUNLU ***) 
- invoiceExchangeRate (float) : Para Birimi kuru(TL Kur:1, Diğer döviz cinsleri günlük kur değeri) (ZORUNLU ***)
- specialArea (array): Satış Kanalı (ZORUNLU ***)
- employee_id (string) : Çalışan oid
- notesStatus (string): true veya false (ZORUNLU ***) 
- note (string): Satış notu 
- subTotal (float): Vergisiz toplam (ZORUNLU ***) 
- taxTotal (float): Vergiler toplamı (ZORUNLU ***) 
- discountTotal (float): İndirimler toplamı (ZORUNLU ***) 
- total (float): Satışın toplam değeri (ZORUNLU ***) 
- product_id (string): Ürün oid. (ZORUNLU ***) 
- invoice_stocktracking (int): Stok takibi yapılıp yapılmayacağı. ('true': Yapılacak, 'false': Yapılmayacak) (ZORUNLU ***) 
- invoice_unit (string): Ürün birim türü. (Örneğin: Adet, Kg, Litre) (ZORUNLU ***) 
- invoice_amount (int): Fatura kalemindeki adet. (ZORUNLU ***) 
- invoice_unit_price (float): Ürün birim fiyatı. (ZORUNLU ***) 
- invoice_unit_currency (string): Para birimi türü (Satış para birimi ile aynı olmak zorunda). (ZORUNLU ***) 
- invoice_tax (int): Vergi yüzdesi. (%10, %20) (ZORUNLU ***) 
- invoice_discount_amount (float): Fatura kalemindeki indirim tutarı.
- invoice_discount (float): Fatura kalemindeki indirim tutarı. (invoice_discount_amount ile eşit değer, invoice_discount_amount varsa zorunlu)
- invoice_discount_type (string): Fatura kalemindeki indirim tipi. ('0'->Fiyat bazında indirim. Örneğin; 100 TL. '1'->Yüzdelik indirim. Örneğin; %10) (ZORUNLU ***) 
- invoice_tax_not_included (float): Fatura kalemindeki vergisiz toplam tutar. (ZORUNLU ***) 
- invoice_tax_amount (float): Fatura kalemindeki vergilerin toplam tutarı. (ZORUNLU ***) 
- invoice_total (float): Fatura kalemindeki toplam tutar. (ZORUNLU ***)
- specialArea : Satış kanal bilgisi, max 2000 karakter sınırlaması vardır

##### Lütfen stok kodu yazıyorsanız gerçek olsun sonradan gelen istekler stok koduna göre işlem yapacak. yoksa sadece isim göndermeniz yeterli.

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Satis": {
        "title": "ApiSatis22",
        "invoiceTo_id": "654a592872edb6c3d60ca95e",
        "invoiceDate": "21-08-2023",
        "invoiceExchange": "TRY",
        "invoiceExchangeRate": 1,
        "employee_id": null,
        "notesStatus": "true",
        "note": "Siz ve ekibinizle çalışmak bir zevkti. Teşekkür ederiz!",
        "subTotal": 791.67,
        "taxTotal": 116.73,
        "discountTotal": 208,
        "total": 700.4,
        "specialArea": [
            {
               "salesChannel": "trendyol,hepsiburada"
            }
        ],
        "invoiceForm": [
            {
                "product_id": "64d38f643e5e78eeb8072026",
                "invoice_stocktracking": "false",
                "invoice_unit": "Adet",
                "invoice_amount": 1,
                "invoice_unit_price": 791666,
                "invoice_unit_currency": "TRY",
                "invoice_store": null,
                "invoice_tax": 20,
                "invoice_discount_amount": 208,
                "invoice_discount": 208,
                "invoice_discount_type": "0",
                "invoice_tax_not_included": 583.67,
                "invoice_tax_amount": 116.73,
                "invoice_total": 700.4
            }
          ]
        }
    }

```
## - Satış Bilgilerini Listeleme 
Endpoint:
```http
POST https://wegs.dev/V2/sales
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Örnek post JSON

```json
{
  "Action": {
    "type": "list"
  }
}
```

```
## - Gelen Faturaların Listelenmesi
Endpoint:
```http
POST https://wegs.dev/V2/incominginvoice
```

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Örnek post JSON

```json
{
  "Action": {
    "type": "list"
  }
}
```

## - Hızlı Sipariş ve Parametreye Bağlı Fatura Oluşturma 
Endpoint:
```http
POST https://wegs.dev/V2/fastorder
```
####  Request Body:
####  Cari Bilgileri:
- phone (string): Carinin telefon numarası. (Sıfır olmadan) ZORUNLU ***
- mail (string): Carinin e-mail adresi. ZORUNLU ***
- tcvkn (string): Müşterinin TCsi yada vkn si. ZORUNLU ***
- customer_title (string): Cari unvanı. ZORUNLU ***
- tag (string, nullable): Carinin kısa ismi.
- cari_group (string, nullable): Cari grubu.
- cari_code (string, nullable): Cari kodu.
- vd (string, nullable): Vergi Dairesi.
- billing_address (string): Fatura adresi. ZORUNLU ***
- delivery_address (string, nullable): Teslimat adresi.
- city (string): Şehir.
- district (string): İlçe.
- country (string): Ülke kodu. Ülke kodları kısaltılmış formatta olmalı. Örneğin TR, US, DE, AU gibi. Aksi halde fatura oluştururken hata alabilirsiniz.
- state (string): Eyalet/Bölge.
- post_code (string): Posta kodu.
- note (string): Not.


####  Fatura Bilgileri:
- store_id (string): stock_tracking === 1 ise depo id zorunlu bir alandır.
- Urun[specialArea] : Urun array'in de bulunan specialArea, ürünün detaylı bilgisi içindir.
- specialArea : Satış kanal bilgisi, max 2000 karakter sınırlaması vardır,
- taxExemption(string||null) : KDV oranı 0 veya 1 olduğu zaman KDV istisnası göndermek zorunludur. 8, 10, 20 gibi oranlarda null gönderilebilir. 
- makeInvoice(int) : Oluşturulan siparişin faturasını kesebilmek için belirlenen type. Sadece "(int) 1" gönderilmesi durumunda fatura oluşturulur. Aksi takdirde sadece satış bilgileri kaydedilir.   

####  Örnek post JSON

```json
{
    "Action":
    {
        "type":"create"
    },
    "Cari":
    {
        "phone":"5456571256",
        "mail":"example@mail.com",
        "customer_title":"Ornek Musteri",
        "cari_code":"",
        "tcvkn":"11111111111",
        "vd":"",
        "billing_address":"Address",
        "delivery_address":"Address",
        "city":"City",
        "district":"district",
        "country":"TR",
        "post_code":"20150"
    },
    "Urun":
    [
        {
            "barcode":"",
            "stock_code":"Custom",
            "product_name":"SIA Custom Metal",
            "stock_tracking":0,
            "currency_type":"TRY",
            "tax":10,
            "price_1": 2000,
            "unit_type":"Adet",
            "quantity": 1,
            "store_id":"",
            "product_description":"",
            "specialArea": [
                {
                  "item_name": null,
                  "item_value": null
                }
            ]
        },
        {
          "barcode": "",
          "stock_code": "stokkodu",
          "stock_group_code": "stokgrupkodu",
          "product_name": "Filtre Kahve",
          "stock_tracking": 1,
          "currency_type": "TRY",
          "tax": 20,
          "price_1": 54,
          "unit_type": "Adet",
          "quantity": 3,
          "store_id": "64d0b02543b455171501b8c9",
          "product_description": "Ürün bilgileri",
          "specialArea": [
            {
              "item_name": "Boy",
              "item_value": "917 ml"
            }
          ]
        }
    ],
    "specialArea":[{"salesChannel":"perakende"}],
    "taxExemption": "301 - 11/1-a Mal İhracatı",
    "makeInvoice":1
}

```


## - Fatura Oluşturma
Endpoint:
```http
POST https://wegs.dev/V2/invoice
```

####  Request Body:
####  Fatura Bilgileri:
- salesId (string): Faturasını oluşturmak istediğiniz satışın oid.

### Headers

- `Content-Type`: application/json
- `client_id`: Your client ID
- `api_key`: Your API key

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Fatura": {
        "salesId": "658e9c37197f4145d40e1b34"
        }
}
```

## Vergi Muafiyet Sebebi (Baştaki Kodları İle Beraber Gönderilmelidir. Orn; 101 - İhracat İstisnası)
```json
101 - İhracat İstisnası
102 - Diplomatik İstisna
103 - Askeri Amaçlı İstisna
104 - Petrol Arama Faaliyetlerinde Bulunanlara Yapılan Teslimler
105 - Uluslararası Anlaşmadan Doğan İstisna
106 - Diğer İstisnalar
107 - 7/a Maddesi Kapsamında Yapılan Teslimler
108 - Geçici 5. Madde Kapsamında Yapılan Teslimler
201 - 17/1 Kültür ve Eğitim Amacı Taşıyan İşlemler
202 - 17/2-a Sağlık, Çevre Ve Sosyal Yardım Amaçlı İşlemler
204 - 17/2-c Yabancı Diplomatik Organ Ve Hayır Kurumlarının Yapacakları Bağışlarla İlgili Mal Ve Hizmet Alışları
205 - 17/2-d Taşınmaz Kültür Varlıklarına İlişkin Teslimler ve Mimarlık Hizmetleri
206 - 17/2-e Mesleki Kuruluşların İşlemleri
207 - 17/3 Askeri Fabrika, Tersane ve Atölyelerin İşlemleri
208 - 17/4-c Birleşme, Devir, Dönüşüm ve Bölünme İşlemleri
209 - 17/4-e Banka ve Sigorta Muameleleri Vergisi Kapsamına Giren İşlemler
211 - 17/4-h Zirai Amaçlı Su Teslimleri İle Köy Tüzel Kişiliklerince Yapılan İçme Suyu teslimleri
212 - 17/4-ı Serbest Bölgelerde Verilen Hizmetler
213 - 17/4-j Boru Hattı İle Yapılan Petrol Ve Gaz Taşımacılığı
214 - 17/4-k Organize Sanayi Bölgelerindeki Arsa ve İşyeri Teslimleri İle Konut Yapı Kooperatiflerinin Üyelerine Konut Teslimleri
215 - 17/4-l Varlık Yönetim Şirketlerinin İşlemleri
216 - 17/4-m Tasarruf Mevduatı Sigorta Fonunun İşlemleri
217 - 17/4-n Basın-Yayın ve Enformasyon Genel Müdürlüğüne Verilen Haber Hizmetleri
218 - 17/4-o Gümrük Antrepoları, Geçici Depolama Yerleri, Gümrüklü Sahalar ve Vergisiz Satış Yapılan Mağazalarla İlgili Hizmetler
219 - 17/4-p Hazine ve Arsa Ofisi Genel Müdürlüğünün işlemleri
220 - 17/4-r İki Tam Yıl Süreyle Sahip Olunan Taşınmaz ve İştirak Hisseleri Satışları
221 - Geçici 15 Konut Yapı Kooperatifleri, Belediyeler ve Sosyal Güvenlik Kuruluşlarına Verilen İnşaat Taahhüt Hizmeti
223 - Geçici 20/1 Teknoloji Geliştirme Bölgelerinde Yapılan İşlemler
225 - Geçici 23 Milli Eğitim Bakanlığına Yapılan Bilgisayar Bağışları İle İlgili Teslimler
226 - 17/2-b Özel Okulları, Üniversite ve Yüksekokullar Tarafından Verilen Bedelsiz Eğitim Ve Öğretim Hizmetleri
227 - 17/2-b Kanunların Gösterdiği Gerek Üzerine Bedelsiz Olarak Yapılan Teslim ve Hizmetler
228 - 17/2-b Kanunun (17/1) Maddesinde Sayılan Kurum ve Kuruluşlara Bedelsiz Olarak Yapılan Teslimler
229 - 17/2-b Gıda Bankacılığı Faaliyetinde Bulunan Dernek ve Vakıflara Bağışlanan Gıda, Temizlik, Giyecek ve Yakacak Maddeleri
230 - 17/4-g Külçe Altın, Külçe Gümüş Ve Kiymetli Taşlarin Teslimi
231 - 17/4-g Metal Plastik, Lastik, Kauçuk, Kağit, Cam Hurda Ve Atıkların Teslimi
232 - 17/4-g Döviz, Para, Damga Pulu, Değerli Kağıtlar, Hisse Senedi ve Tahvil Teslimleri
234 - 17/4-ş Konut Finansmanı Amacıyla Teminat Gösterilen ve İpotek Konulan Konutların Teslimi
235 - 16/1-c Transit ve Gümrük Antrepo Rejimleri İle Geçici Depolama ve Serbest Bölge Hükümlerinin Uygulandığı Malların Teslimi
236 - 19/2 Usulüne Göre Yürürlüğe Girmiş Uluslararası Anlaşmalar Kapsamındaki İstisnalar (İade Hakkı Tanınmayan)
237 - 17/4-t 5300 Sayılı Kanuna Göre Düzenlenen Ürün Senetlerinin İhtisas/Ticaret Borsaları Aracılığıyla İlk Teslimlerinden Sonraki Teslim
238 - 17/4-u Varlıkların Varlık Kiralama Şirketlerine Devri İle Bu Varlıkların Varlık Kiralama Şirketlerince Kiralanması ve Devralınan Kuruma Devri
239 - 17/4-y Taşınmazların Finansal Kiralama Şirketlerine Devri, Finansal Kiralama Şirketi Tarafından Devredene Kiralanması ve Devri
240 - 17/4-z Patentli Veya Faydalı Model Belgeli Buluşa İlişkin Gayri Maddi Hakların Kiralanması, Devri ve Satışı
241 - Türk Akım Gaz Boru Harrı Projesine İlişkin Anlaşmanın (9/b) Maddesinde Yer Alan Hizmetler
242 - KDV 17/4-ö md. Gümrük Antrepoları, Geçici Depolama Yerleri ile Gümrüklü Sahalarda, İthalat ve İhracat İşlemlerine konu mallar ile transit rejim
250 - Diğerleri
301 - 11/1-a Mal İhracatı
302 - 11/1-a Hizmet İhracatı
303 - 11/1-a Roaming Hizmetleri
304 - 13/a Deniz Hava ve Demiryolu Taşıma Araçlarının Teslimi İle İnşa, Tadil, Bakım ve Onarımları
305 - 13/b Deniz ve Hava Taşıma Araçları İçin Liman Ve Hava Meydanlarında Yapılan Hizmetler
306 - 13/c Petrol Aramaları ve Petrol Boru Hatlarının İnşa ve Modernizasyonuna İlişkin Yapılan Teslim ve Hizmetler
307 - 13/c Maden Arama, Altın, Gümüş, ve Platin Madenleri İçin İşletme, Zenginleştirme Ve Rafinaj Faaliyetlerine İlişkin Teslim Ve Hizmetler
308 - 13/d Teşvikli Yatırım Mallarının Teslimi
309 - 13/e Liman Ve Hava Meydanlarının İnşası, Yenilenmesi Ve Genişletilmesi
310 - 13/f Ulusal Güvenlik Amaçlı Teslim ve Hizmetler
311 - 14/1 Uluslararası Taşımacılık
312 - 15/a Diplomatik Organ Ve Misyonlara Yapılan Teslim ve Hizmetler
313 - 15/b Uluslararası Kuruluşlara Yapılan Teslim ve Hizmetler
314 - 19/2 Usulüne Göre Yürürlüğe Girmiş Uluslar Arası Anlaşmalar Kapsamındaki İstisnalar
315 - 14/3 İhraç Konusu Eşyayı Taşıyan Kamyon, Çekici ve Yarı Romorklara Yapılan Motorin Teslimleri
316 - 11/1-a Serbest Bölgelerdeki Müşteriler İçin Yapılan Fason Hizmetler
317 - 17/4-s Engellilerin Eğitimleri, Meslekleri ve Günlük Yaşamlarına İlişkin Araç-Gereç ve Bilgisayar Programları
318 - Geçici 29 3996 Sayılı Kanuna Göre Yap-İşlet-Devret Modeli Çerçevesinde Gerçekleştirilecek Projeler, 3359 Sayılı Kanuna Göre Kiralama Karşılığı Yaptırılan Sağlık Tesislerine İlişkin Projeler ve 652 Sayılı Kanun Hükmünde Kararnameye Göre Kiralama Karşılığı Yaptırılan Eğitim Öğretim Tesislerine İlişkin Projelere İlişkin Teslim ve Hizmetler
319 - 13/g Başbakanlık Merkez Teşkilatına Yapılan Araç Teslimleri
320 - Geçici 16 (6111 sayılı K.) İSMEP Kapsamında İstanbul İl Özel İdaresi'ne Bağlı Olarak Faaliyet Gösteren "İstanbul Proje Koordinasyon Birimi"ne Yapılacak Teslim ve Hizmetler
321 - Geçici 26 Birleşmiş Milletler (BM) ile Kuzey Atlantik Antlaşması Teşkilatı (NATO) Temsilcilikleri ve Bu Teşkilatlara Bağlı Program, Fon ve Özel İhtisas Kuruluşları ile İktisadi İşbirliği ve Kalkınma Teşkilatına (OECD) Resmi Kullanımları İçin Yapılacak Mal Teslimi ve Hizmet İfaları, Bunların Sosyal ve Ekonomik Yardım Amacıyla Bedelsiz Olarak Yapacakları Mal Teslimi ve Hizmet İfaları İle İlgili Bunlara Yapılan Mal Teslimi ve Hizmet İfaları
322 - 11/1-a Türkiye'de İkamet Etmeyenlere Özel Fatura ile Yapılan Teslimler (Bavul Ticareti)
323 - 13/ğ 5300 Sayılı Kanuna Göre Düzenlenen Ürün Senetlerinin İhtisas/Ticaret Borsaları Aracılığıyla İlk Teslimi
324 - 13/h Türkiye Kızılay Derneğine Yapılan Teslim ve Hizmetler ile Türkiye Kızılay Derneğinin Teslim ve Hizmetleri
325 - 13/ı Yem Teslimleri
326 - 13/ı Gıda, Tarım ve Hayvancılık Bakanlığı Tarafından Tescil Edilmiş Gübrelerin Teslimi
327 - 13/ı Gıda, Tarım ve Hayvancılık Bakanlığı Tarafından Tescil Edilmiş Gübrelerin İçeriğinde Bulunan Hammaddelerin Gübre Üreticilerine Teslimi
328 - 13/i Konut veya İşyeri Teslimleri
330 - KDV 13/j md. Organize Sanayi Bölgeleri ile Küçük Sanayi Sitelerinin İnşasına İlişkin Teslim ve Hizmetler
331 - KDV 13/m md. Ar-Ge, Yenilik ve Tasarım Faaliyetlerinde Kullanılmak Üzere Yapılan Yeni Makina ve Teçhizat Teslimlerinde İstisna
332 - KDV Geçici 39. Md. İmalat Sanayiinde Kullanılmak Üzere Yapılan Yeni Makina ve Teçhizat Teslimlerinde İstisna
333 - KDV 13/k md. Kapsamında Genel ve Özel Bütçeli Kamu İdarelerine, İl Özel İdarelerine, Belediyelere ve Köylere bağışlanan Tesislerin İnşasına İlişkin İstisna
334 - KDV 13/l md. Kapsamında Yabancılara Verilen Sağlık Hizmetlerinde İstisna
335 - KDV 13/n Basılı Kitap ve Süreli Yayınların Teslimleri
336 - Geçici 40 UEFA Müsabakaları Kapsamında Yapılacak Teslim ve Hizmetler
337 - Türk Akım Gaz Boru Hattı Projesine İlişkin Anlaşmanın (9/h) Maddesi Kapsamındaki Gaz Taşıma Hizmetleri
338 - İmalatçıların Mal İhracatları
339 - İmalat Sanayii ile Turizme Yönelik Yatırım Teşvik Belgesi Kapsamındaki İnşaat İşlerine İlişkin Teslim ve Hizmetler
340 - Elektrik Motorlu Taşıt Araçlarının Geliştirilmesine Yönelik Mühendislik Hizmetleri
350 - Diğerleri
351* - KDV - İstisna Olmayan Diğer
```

## API Kullanım Örneği

Aşağıda, API'ye istek göndermek için kullanabileceğiniz bir PHP örneği bulabilirsiniz:

```php
function sendRequest($url, $method = 'GET', $client_id, $api_key, $data = []) {
    $ch = curl_init($url);

    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'client_id: ' . $client_id,
        'api_key: ' . $api_key,
        'Content-Type: application/json'
    ]);

    if ($method === 'POST') {
        curl_setopt($ch, CURLOPT_POST, 1);
        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
    } elseif ($method !== 'GET') {
        curl_setopt($ch, CURLOPT_CUSTOMREQUEST, $method);
        if (!empty($data)) {
            curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        }
    }

    $response = curl_exec($ch);
    curl_close($ch);

    return json_decode($response, true);
}

// Örnek kullanımlar
// GET örneği
$dataGet = sendRequest("https://yourapiurl.com/list", 'GET', "YOUR_CLIENT_ID", "YOUR_API_KEY");
print_r($dataGet);

// POST örneği
$insertData = [
  "Action": {
    "type": "create"
  },
  .......
  .......
];
$dataPost = sendRequest("https://yourapiurl.com/manage", 'POST', "YOUR_CLIENT_ID", "YOUR_API_KEY", $insertData);
print_r($dataPost);
```

Bu örneği kullanarak, kendi API'nize istekler gönderebilir ve yanıtları işleyebilirsiniz.
