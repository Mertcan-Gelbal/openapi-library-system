# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Mertcan Gelbal
- **Öğrenci Numarası**: 171421012

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyası projenin GitHub reposuna yüklenmiştir.
- Swagger Editor ile test edilmiş ve hatasız çalışmaktadır.

### 🔗 GitHub Repo Linki
https://github.com/Mertcan-Gelbal/openapi-library-system

---

## 📝 API Açıklaması

### 🏗️ Varlıklar (Entities)

Tasarlanan API'de üç ana varlık bulunmaktadır:

#### 📚 **books** (Kitaplar)
- `id`: UUID formatında benzersiz tanımlayıcı
- `title`: Kitap başlığı (string, zorunlu)
- `author`: Yazar adı (string, zorunlu)
- `isbn`: ISBN-13 formatında kitap kodu
- `publisher`: Yayınevi (string, zorunlu)
- `pageCount`: Sayfa sayısı (integer, pozitif)
- `stock`: Stok miktarı (integer, negatif olmayan)

#### 👤 **students** (Öğrenciler)
- `id`: UUID formatında benzersiz tanımlayıcı
- `name`: Öğrenci adı (string, zorunlu)
- `studentNumber`: Öğrenci numarası (string, benzersiz)
- `email`: E-posta adresi (email formatı, benzersiz)
- `isActive`: Aktiflik durumu (boolean, varsayılan: true)

#### 🔄 **loans** (Ödünç Alma)
- `id`: UUID formatında benzersiz tanımlayıcı
- `studentId`: Öğrenci referansı (UUID)
- `bookId`: Kitap referansı (UUID)
- `loanDate`: Ödünç alma tarihi (ISO 8601 date)
- `returnDate`: İade tarihi (ISO 8601 date, nullable)
- `status`: Durum (enum: ongoing, returned, late)

### 🛠️ CRUD İşlemleri ve Endpoint'ler

#### 📘 Books Resource
- `GET /books` → Tüm kitapları listele (sayfalama: page, size)
- `GET /books/{id}` → Tek kitap detayı
- `POST /books` → Yeni kitap ekleme
- `PUT /books/{id}` → Kitap güncelleme
- `DELETE /books/{id}` → Kitap silme

#### 👤 Students Resource
- `GET /students` → Tüm öğrencileri listele
- `GET /students/{id}` → Tek öğrenci detayı
- `POST /students` → Yeni öğrenci kaydı
- `PUT /students/{id}` → Öğrenci güncelleme
- `DELETE /students/{id}` → Öğrenci silme

#### 🔄 Loans Resource
- `GET /loans` → Tüm ödünç alma kayıtları
- `GET /loans/{id}` → Tek ödünç alma detayı
- `POST /loans` → Yeni ödünç alma
- `PATCH /loans/{id}/return` → Kitap iade etme

### 🧩 OpenAPI Bileşenleri Kullanımı

#### **components/schemas**
- **Book, Student, Loan**: Ana varlık şemaları
- **BookCreate, StudentCreate, LoanCreate**: POST işlemleri için şemalar (id hariç)
- **Pagination**: Sayfalama metadata şeması
- **ErrorResponse**: Standart hata yanıt şeması
- **ValidationError**: Validasyon hata detay şeması

#### **parameters**
- **Path Parameters**: `{id}` parametresi (UUID formatı)
- **Query Parameters**: `page`, `size` (sayfalama), `status` (filtreleme)
- **Header Parameters**: `X-Request-ID` (istek takip ID'si)

#### **responses**
- **200 OK**: Başarılı GET işlemleri
- **201 Created**: Başarılı POST işlemleri
- **400 Bad Request**: Validasyon hataları
- **404 Not Found**: Kaynak bulunamadı
- **500 Internal Server Error**: Sunucu hataları

### 📄 Sayfalama ve Hata Durumları

#### **Sayfalama (GET /books)**
- `page`: Sayfa numarası (varsayılan: 1, minimum: 1)
- `size`: Sayfa boyutu (varsayılan: 10, minimum: 1, maksimum: 100)
- Response'da `pagination` objesi ile metadata döndürülür

#### **Hata Yönetimi**
- **Validasyon Hataları**: ISBN-13, email, UUID format kontrolleri
- **İş Kuralı Hataları**: Stok kontrolü, aktif öğrenci kontrolü
- **Sistem Hataları**: 500 Internal Server Error için standart format

---

## 🧪 Test Notları

Swagger Editor üzerinden test edilen örnek senaryolar:

### **GET /books** Çağrısı
```json
{
  "data": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "title": "Clean Code",
      "author": "Robert C. Martin",
      "isbn": "978-0132350884",
      "publisher": "Prentice Hall",
      "pageCount": 464,
      "stock": 5
    }
  ],
  "pagination": {
    "page": 1,
    "size": 10,
    "total": 150,
    "totalPages": 15
  }
}
```

### **POST /students** RequestBody Örneği
```json
{
  "name": "Ahmet Yılmaz",
  "studentNumber": "2021001234",
  "email": "ahmet.yilmaz@marun.edu.tr",
  "isActive": true
}
```

### **400 Bad Request** Hata Örneği
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Input validation failed",
    "details": [
      {
        "field": "isbn",
        "message": "ISBN must be in ISBN-13 format"
      }
    ]
  }
}
```

---

## 📌 Ek Açıklamalar

### ✅ Ödev Gereksinimlerinin Karşılanması

| Gereksinim | Durum | Açıklama |
|------------|-------|----------|
| OpenAPI 3.0/3.1 | ✅ | 3.0.3 versiyonu kullanıldı |
| Zorunlu varlıklar | ✅ | books, students, loans tam olarak tanımlandı |
| CRUD endpoint'leri | ✅ | 13 endpoint, birebir ödev gereksinimlerine uygun |
| components/schemas | ✅ | 9 şema tanımlandı |
| parameters çeşitliliği | ✅ | path, query, header parametreleri |
| requestBody | ✅ | required, enum, format kullanıldı |
| responses | ✅ | 200, 201, 400, 404, 500 örnekleri |
| example kullanımı | ✅ | Tüm endpoint'lerde örnekler |
| Sayfalama | ✅ | GET /books'ta uygulandı |
| description & tags | ✅ | Açıklayıcı dokümantasyon |

### 🎯 Öne Çıkan Özellikler
- **UUID v4 formatı** tüm ID'lerde kullanıldı
- **ISBN-13 validasyonu** kitaplar için uygulandı
- **Email format kontrolü** öğrenciler için eklendi
- **Enum değerleri** loan status için tanımlandı
- **Comprehensive error handling** tüm endpoint'lerde
- **Consistent naming convention** camelCase kullanıldı

### 🔍 Swagger Editor Test Sonucu
- ✅ YAML syntax doğrulaması geçti
- ✅ OpenAPI 3.0.3 şema validasyonu başarılı
- ✅ Tüm endpoint'ler test edildi
- ✅ Request/Response örnekleri çalışıyor
- ✅ Parametre validasyonları doğru

Bu proje, verilen tüm ödev gereksinimlerini karşılamakta ve OpenAPI 3.0.3 standardına tam uyum sağlamaktadır.
