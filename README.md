# Nginx Image Filter ile Dinamik Resim İşleme

Bu dökümantasyon, Nginx'in dinamik resim işleme özelliklerini kullanarak resimleri nasıl boyutlandırabileceğinizi, kırpabileceğinizi, döndürebileceğinizi ve kalitelerini ayarlayabileceğinizi anlatmaktadır.

### Örnek Resim

Test için kullanacağımız örnek resim:
```
https://icdn.adveyer.com/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

### Kullanılabilir URL Yolları

#### 1. **Boyutlandırma (Resize)**
Resmi belirli bir genişliğe boyutlandırmak için:

```
/resize/{width}-{quality}/{image-path}
```

**Örnek:**
```
https://icdn.adveyer.com/resize/300-80/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

Bu URL, resmi 300px genişliğinde ve %80 kalite ile boyutlandıracaktır.

#### 2. **Boyutlandırma ve Döndürme (Resize & Rotate)**
Resmi belirli bir genişliğe boyutlandırıp, belirli bir derece döndürmek için:

```
/resize-rotate/{width}-{quality}-{rotate}/{image-path}
```

**Örnek:**
```
https://icdn.adveyer.com/resize-rotate/300-80-90/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

Bu URL, resmi 300px genişliğinde, %80 kaliteyle boyutlandırır ve 90 derece döndürür.

#### 3. **Kırpma (Crop)**
Resmi belirli bir genişlik ve yükseklikte kırpmak için:

```
/crop/{width}x{height}-{quality}/{image-path}
```

**Örnek:**
```
https://icdn.adveyer.com/crop/100x100-70/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

Bu URL, resmi 100x100 boyutlarında kırpar ve %70 kaliteyle sunar.

### Notlar
- `{width}`: Resmin genişliğini belirler.
- `{height}`: Resmin yüksekliğini belirler (sadece kırpma için).
- `{quality}`: Resim kalitesini belirler (%0-100 arasında bir değer).
- `{rotate}`: Resmi kaç derece döndüreceğinizi belirler.

-------

# Dinamik Resim İşleme (Gstream, Resize, Crop)

Bu dökümantasyon, dinamik olarak resim işleme işlevlerini nasıl kullanabileceğinizi anlatmaktadır. İşlevler arasında resim boyutlandırma, kırpma ve bazı opsiyonel ayarları içerir.

### Örnek Resim

Test için kullanacağımız örnek resim:
```
https://icdn.adveyer.com/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

### Kullanılabilir URL Yolları

#### 1. **Boyutlandırma (Resize)**
Resmi belirli bir genişlik ve yükseklikte boyutlandırmak için:

```
/gsresize/{cmd}-{width}x{height}-{option}/{image-path}
```

- `{cmd}`: Komut adı (örneğin `resize`).
- `{width}`: Resmin genişliği.
- `{height}`: Resmin yüksekliği.
- `{option}`: Ek seçenekler (örneğin kalite, mod vb.).
- `{image-path}`: Resim dosyasının yolu.

**Örnek:**
```
https://icdn.adveyer.com/gsresize/resize-300x200-high/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```
Bu URL, resmi 300x200 piksel boyutlarında ve "high" kalite seçeneğiyle işleme sokacaktır.

#### 2. **Kırpma (Crop)**
Resmi belirli bir genişlik ve yükseklikte kırpmak için:

```
/gscrop/{cmd}-{width}x{height}-{option}/{image-path}
```

**Örnek:**
```
https://icdn.adveyer.com/gscrop/crop-100x100-center/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```
Bu URL, resmi 100x100 piksel boyutlarında kırpar ve "center" opsiyonu ile merkezden kırpma işlemi uygular.

#### 3. **Opsiyonlar (Options)**
- `{cmd}`: İşlemi belirten komut (örneğin `resize`, `crop` vb.).
- `{width}x{height}`: Resmin boyutlarını belirler.
- `{option}`: İsteğe bağlı olarak kalite, mod gibi ek seçenekler içerir.

### Proxy ve Cache İşlemleri

- Resimlerin işlenme sürecinde cache (önbellek) kullanılmaktadır.
- Önbellek anahtarı olarak istek URI’si (`$request_uri`) kullanılmaktadır.
- Resim işleme isteği içeriği aşağıdaki parametrelerle backend'e iletilir:
  - `cmd`: İşlem tipi (örneğin, `resize`).
  - `w`: Genişlik.
  - `h`: Yükseklik.
  - `o`: Seçenekler.
  - `url`: Orijinal resim URL’si.

### Örnek İstek Yapısı

```
https://icdn.adveyer.com/gsresize/resize-300x200-high/wp-content/uploads/2023/03/pexels-karolina-grabowska-4195409-1-scaled.jpg
```

Bu örnek, resmi 300x200 boyutlarında ve yüksek kalite ile sunacaktır. İstek arka planda gerekli proxy işlemleriyle cache’e alınır ve belirtilen sürede geçerli olur.

### Notlar
- `{width}` ve `{height}` boyutları belirtilmezse, orijinal boyut korunur.
- `{option}` parametresi kalite ayarları veya modlar için kullanılır.

