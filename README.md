# api-doc-new


# WEGS API DOC

![Logo](https://app.wegs.com.tr/images/logo/logo-light-crop.png)

    
## API Dokümantasyonu


## - Cari Bilgilerini Gönderme API'si

## Açıklama
Bu API, müşteri (cari) ve ürün bilgilerini sisteme göndermek için kullanılır.
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
- tcvkn (string, nullable): Müşterinin TCsi yada vkn si.
- customer_title (string, nullable): Cari unvanı. ZORUNLU ***
- tag (string, nullable): Carinin kısa ismi.
- cari_group (string, nullable): Cari grubu.
- cari_code (string, nullable): Cari kodu.
- vd (string, nullable): Vergi Dairesi.
- billing_address (string): Fatura adresi.
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
    "state": "Ankara",
    "post_code": "6000",
    "note": ""
  },
}
```
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
  "Urun": [
    {
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
  ]
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
