İstediğin gibi bir `README.md` dosyasını aşağıdaki şekilde düzenledim:

```md
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
```

Bu dosya, istediğin URL örneklerine dayalı olarak kullanıcılara açıklayıcı bir şekilde bilgi verecektir.
