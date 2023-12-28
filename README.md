# api-doc-new


# WEGS API DOC

![Logo](https://app.wegs.com.tr/images/logo/logo-light-crop.png)

    
## API Dokümantasyonu

## - Ücretsiz Kayıt Olmak İçin Tıkla 

- Wegs' Ücretsiz Tıkla Kaydol (https://app.wegs.com.tr/)

## - Cari Bilgilerini Gönderme API'si

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
- phone (string): Carinin telefon numarası. (Sıfır olmadan)
- mail (string, nullable): Carinin e-mail adresi.
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
  },
}
```

## - Cari Bilgilerini Listeleme API'si
Endpoint:
```http
GET https://wegs.dev/V2/customers
```
####  Örnek post JSON

```json
{
  "Action": {
    "type": "list"
  }
}

```

## - Ürün Bilgilerini Gönderme API'si
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
- product_name (string): Ürün adı.
- stock_tracking (int): Stok takibi yapılıp yapılmayacağı. (1: Yapılacak, 0: Yapılmayacak)
- currency_type (string): Para birimi türü.
- tax (int): Vergi yüzdesi. (Zorunlu)
- price_1 (float): Ürün fiyatı.
- unit_type (string): Ürün birim türü. (Örneğin: Adet, Kg, Litre)
- quantity (int): Fatura kalemindeki adet.

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
      "product_name": "Kahve",
      "stock_tracking": 1,
      "currency_type": "TRY",
      "tax": 0,
      "price_1": 0,
      "unit_type": "Adet",
      "quantity": 0
    }
}


```
## - Ürün Bilgilerini Listeleme API'si
Endpoint:
```http
GET https://wegs.dev/V2/products
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
  },
}
```

## - Satış Bilgilerini Gönderme API'si
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

##### Lütfen stok kodu yazıyorsanız gerçek olsun sonradan gelen istekler stok koduna göre işlem yapacak. yoksa sadece isim göndermeniz yeterli.

####  Örnek post JSON

```json
{
  "Action": {
    "type": "create"
  },
  "Satis": {
        "title": null,
        "invoiceNumber": "2023081528",
        "invoiceTo_id": "654a592872edb6c3d60ca95e",
        "invoiceDate": "21-08-2023",
        "invoiceExchange": "TRY",
        "invoiceExchangeRate": 1,
        "salesChannel": "trendyol",
        "employee_id": null,
        "notesStatus": "true",
        "note": "Siz ve ekibinizle çalışmak bir zevkti. Teşekkür ederiz!",
        "subTotal": 791.67,
        "taxTotal": 116.73,
        "discountTotal": 208,
        "total": 700.4,
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
          "specialArea": [
            {
                "salesChannel": {
                    "trendyol",
                    "hepsiburada"
                }
            }
          ]
        }
    }


```
## - Satış Bilgilerini Listeleme API'si
Endpoint:
```http
GET https://wegs.dev/V2/sales
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
  },
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
