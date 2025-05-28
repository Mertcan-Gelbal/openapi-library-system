# Marmara Üniversitesi Kütüphane Sistemi - OpenAPI Spesifikasyonu

## 📚 Proje Açıklaması

Bu proje, **Marmara Üniversitesi Açık Kaynak Kodlu Yazılımlar** dersi kapsamında hazırlanan **OpenAPI 3.0 spesifikasyonu ödevi**dir.

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Mertcan Gelbal
- **Öğrenci Numarası**: 171421012
- **Üniversite**: Marmara Üniversitesi

## 🎯 Proje Kapsamı

Bir üniversite kütüphanesi için RESTful API tasarımını OpenAPI 3.0.3 standardında tanımlamaktadır.

### Varlıklar
- **books**: Kütüphane kitapları
- **students**: Üniversite öğrencileri  
- **loans**: Ödünç alma işlemleri

### API Endpoint'leri

#### 📘 Books
- `GET /books` - Kitap listesi (sayfalama desteği)
- `GET /books/{id}` - Tek kitap detayı
- `POST /books` - Yeni kitap ekle
- `PUT /books/{id}` - Kitap güncelle
- `DELETE /books/{id}` - Kitap sil

#### 👤 Students
- `GET /students` - Öğrenci listesi
- `GET /students/{id}` - Tek öğrenci detayı
- `POST /students` - Yeni öğrenci ekle
- `PUT /students/{id}` - Öğrenci güncelle
- `DELETE /students/{id}` - Öğrenci sil

#### 🔄 Loans
- `GET /loans` - Ödünç alma kayıtları
- `GET /loans/{id}` - Tek ödünç alma detayı
- `POST /loans` - Yeni ödünç alma
- `PATCH /loans/{id}/return` - Kitap iade et

## 📁 Dosya Yapısı

```
/
├── openapi.yaml        # OpenAPI 3.0.3 spesifikasyonu
├── README.md           # Proje açıklaması
└── DELIVERY.md         # Ödev teslim raporu
```

## 🔗 Swagger Editor

OpenAPI spesifikasyonunu görüntülemek için:
1. https://editor.swagger.io adresine gidin
2. `openapi.yaml` dosyasının içeriğini kopyalayın
3. Swagger Editor'a yapıştırın

## 📝 Ödev Teslimi

Bu proje **DELIVERY.md** dosyası Google Classroom'a yüklenerek teslim edilecektir.

---

**Not**: Bu proje sadece OpenAPI spesifikasyonu içermektedir. Kod implementasyonu bulunmamaktadır.
