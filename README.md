# WEGS API Dokümantasyonu

Servis entegrasyonu için güncel ve hızlı kullanım rehberi.

## İçindekiler
- [Hızlı Başlangıç](#hızlı-başlangıç)
- [Kimlik Doğrulama](#kimlik-doğrulama)
- [Endpointler](#endpointler)
- [Postman](#postman)
- [Vergi Muafiyet Kodları](#vergi-muafiyet-kodları)

## Hızlı Başlangıç
1. `client_id` ve `api_key` bilgilerinizi alın.
2. İsteklerde header olarak bu iki alanı gönderin.
3. Sipariş/fatura için `POST /V3/fastorder` endpointini kullanın.
4. Oluşan faturanın PDF'ini `GET /V1/sendinvoiceread/.../pdf` ile alın.

Örnek base URL:
- `https://wegs.dev`

## Kimlik Doğrulama
Tüm isteklerde aşağıdaki header'lar kullanılmalıdır:

```http
client_id: YOUR_CLIENT_ID
api_key: YOUR_API_KEY
Content-Type: application/json
```

## Endpointler

### 1) Hızlı Sipariş ve Fatura Oluşturma
```http
POST /V3/fastorder
```

Tam URL:
```http
POST https://wegs.dev/V3/fastorder
```

#### Zorunlu alanlar
`Cari` altında:
- `phone`: Telefon numarası (başında `0` olmadan)
- `mail`
- `tcvkn`
- `customer_title`
- `billing_address`

`Urun[]` altında her ürün için:
- `stock_code`
- `product_name`
- `stock_tracking` (`0` veya `1`)
- `currency_type` (`TRY`, `USD` vb.)
- `tax` (`0`, `1`, `8`, `10`, `20` vb.)
- `price_1` (KDV dahil birim fiyat)
- `unit_type`
- `quantity`

#### İş kuralları
- `stock_tracking = 1` ise `store_id` zorunludur.
- `tax = 0` veya `tax = 1` ise `taxExemption` zorunludur.
- Geçmiş tarihli fatura için:
- `billDate`: `d-m-Y`
- `billTime`: `H:i:s`
- `makeInvoice = 1` ise fatura kesilir.
- `isRefund = 1` ise iade faturası akışı çalışır ve `refundBillId` + `refundBillDate` gerekir.

#### Örnek istek
```json
{
  "Action": {
    "type": "create"
  },
  "Cari": {
    "phone": "5456571256",
    "tag": "",
    "mail": "example@mail.com",
    "customer_title": "Ornek Musteri",
    "cari_code": "",
    "cari_group": "Wegs Musterileri",
    "tcvkn": "11111111111",
    "vd": "",
    "billing_address": "Address",
    "delivery_address": "Address",
    "city": "City",
    "district": "District",
    "country": "TR",
    "note": "",
    "post_code": "20150"
  },
  "Urun": [
    {
      "barcode": "",
      "stock_code": "Custom",
      "product_name": "SIA Custom Metal",
      "stock_tracking": 0,
      "currency_type": "TRY",
      "tax": 10,
      "price_1": 2000,
      "unit_type": "Adet",
      "quantity": 1,
      "store_id": "",
      "product_description": "",
      "specialArea": [
        {
          "item_name": null,
          "item_value": null
        }
      ]
    }
  ],
  "specialArea": [
    {
      "salesChannel": "trendyol"
    }
  ],
  "taxExemption": null,
  "billDate": "05-08-2024",
  "billTime": "10:10:24",
  "testInvoice": 1,
  "makeInvoice": 1,
  "isRefund": 0,
  "refundBillId": "",
  "refundBillDate": ""
}
```

#### Örnek başarılı yanıt
```json
{
  "return": true,
  "sale": {
    "ID": "673daa0686f80188d4089788",
    "returnType": "Sales"
  },
  "invoice": {
    "return": true,
    "invoice_id": "FT02024000000010",
    "invoice_uuid": "40708075-6F6C-4C6B-8AF8-19DC17EAACD7",
    "invoice_env_uuid": "4cac9bbd-7420-4d9d-a02b-4d6002db73f7",
    "invoice_cust_inv_id": "40708075-6F6C-4C6B-8AF8-19DC17EAACD7",
    "count": 1
  }
}
```

### 2) Fatura PDF Alma
```http
GET /V1/sendinvoiceread/{client_id}/{invoice_id}/{invoice_uuid}/pdf
```

Tam URL örneği:
```http
https://wegs.dev/V1/sendinvoiceread/YOUR_CLIENT_ID/YOUR_INVOICE_ID/YOUR_INVOICE_UUID/pdf
```

Parametreler:
- `client_id`: Size ait client kimliği
- `invoice_id`: `fastorder` yanıtındaki `invoice.invoice_id`
- `invoice_uuid`: `fastorder` yanıtındaki `invoice.invoice_uuid`

## Postman
Repo içinde hazır koleksiyon dosyası:
- `postman/WEGS_API.postman_collection.json`

Postman import adımları:
1. Postman > `Import`
2. `postman/WEGS_API.postman_collection.json` dosyasını seçin
3. Collection variables alanına `client_id` ve `api_key` değerlerini girin
4. İstekleri çalıştırın

## Vergi Muafiyet Kodları
Tüm kod listesi aşağıdaki dosyada:
- `docs/tax-exemption-codes.md`

`taxExemption` alanına kodu açıklamasıyla birlikte gönderin.
Örnek:
- `301 - 11/1-a Mal İhracatı`

## cURL Örneği
```bash
curl --location 'https://wegs.dev/V3/fastorder' \
--header 'client_id: YOUR_CLIENT_ID' \
--header 'api_key: YOUR_API_KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
  "Action": { "type": "create" },
  "Cari": {
    "phone": "5456571256",
    "mail": "example@mail.com",
    "tcvkn": "11111111111",
    "customer_title": "Ornek Musteri",
    "billing_address": "Address"
  },
  "Urun": [
    {
      "stock_code": "Custom",
      "product_name": "SIA Custom Metal",
      "stock_tracking": 0,
      "currency_type": "TRY",
      "tax": 10,
      "price_1": 2000,
      "unit_type": "Adet",
      "quantity": 1
    }
  ],
  "makeInvoice": 1
}'
```
