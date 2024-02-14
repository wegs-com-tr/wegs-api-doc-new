# api-doc-new


# WEGS API DOC

![Logo](https://app.wegs.com.tr/images/logo/logo-light-crop.png)

    
## API Dokümantasyonu

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
- mail (string, nullable): Carinin e-mail adresi. ZORUNLU ***
- tcvkn (string, nullable): Müşterinin TCsi yada vkn si.ZORUNLU ***
- customer_title (string, nullable): Cari unvanı. ZORUNLU ***
- tag (string, nullable): Carinin kısa ismi.
- cari_group (string, nullable): Cari grubu.
- cari_code (string, nullable): Cari kodu.
- vd (string, nullable): Vergi Dairesi.
- billing_address (string): Fatura adresi. ZORUNLU ***
- delivery_address (string, nullable): Teslimat adresi.
- city (string): Şehir.
- district (string): İlçe.
- country (string): Ülke kodu.
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
    "mail": null,
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

## - Hızlı Sipariş Oluşturma
Endpoint:
```http
POST https://wegs.dev/V2/fastorder
```
####  Request Body:
####  Cari Bilgileri:
- phone (string): Carinin telefon numarası. (Sıfır olmadan) ZORUNLU ***
- mail (string, nullable): Carinin e-mail adresi. ZORUNLU ***
- tcvkn (string, nullable): Müşterinin TCsi yada vkn si.ZORUNLU ***
- customer_title (string, nullable): Cari unvanı. ZORUNLU ***
- tag (string, nullable): Carinin kısa ismi.
- cari_group (string, nullable): Cari grubu.
- cari_code (string, nullable): Cari kodu.
- vd (string, nullable): Vergi Dairesi.
- billing_address (string): Fatura adresi. ZORUNLU ***
- delivery_address (string, nullable): Teslimat adresi.
- city (string): Şehir.
- district (string): İlçe.
- country (string): Ülke kodu.
- state (string): Eyalet/Bölge.
- post_code (string): Posta kodu.
- note (string): Not.

####  Fatura Bilgileri:
- store_id (string): stock_tracking === 1 depo id zorunlu bir alandır.
- Urun[specialArea] : Urun array'in de bulunan specialArea ürünün detaylı bilgisi içindir.
- specialArea : Satış kanal bilgisi, max 2000 karakter sınırlaması vardır

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Cari": {
    "phone": "5064723443",
    "mail": null,
    "customer_title": "Ornek API Musteri",
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
  },
  "Urun": [
    {
      "barcode": "",
      "stock_code": "stokkodu",
      "stock_group_code": "stokgrupkodu",
      "product_name": "Latte",
      "stock_tracking": 0,
      "currency_type": "TRY",
      "tax": 10,
      "price_1": 85,
      "unit_type": "Adet",
      "quantity": 1,
      "store_id": null,
      "product_description": "Ürün bilgileri",
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
  "specialArea": [
    {
       "salesChannel": "hepsiburada, trendyol"
    }
 ]
}
```


## - Fatura Oluşturma
Endpoint:
```http
POST https://wegs.dev/V2/invoice
```

####  Request Body:
####  Fatura Bilgileri:
- salesId (string): Faturasını oluşturmak istediğiniz oid.

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
