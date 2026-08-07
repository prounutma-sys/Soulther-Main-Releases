# Soulther Mod (Minecraft Forge 1.20.1)

Bu proje, istediğin özellikleri içeren bir **Minecraft Forge modunun kaynak kodudur**:

- **Yeni boyut: Soulther** — kendi gökyüzü/atmosfer efektleri, biyomu ve mob spawn'larıyla
- **Warden Kalbi ile açılan özel portal** — Warden'ı öldürünce düşen "Warden Kalbi" eşyasını,
  Warden Kalbi Bloklarından yapılmış bir çerçeveye sağ tıklayarak portalı açıyorsun
- **Yeni cevher & materyal**: Soulther Cevheri → Soulther Külçesi
- **Yeni zırh seti**: Soulther Miğfer/Göğüslük/Pantolon/Bot (netherite'dan güçlü)
- **Yeni aletler**: kılıç, kazma, balta, kürek, çapa
- **Yeni moblar**: Soul Wraith (uçan), Voidling (koşan sürü canavarı)
- **Yeni boss ejderha**: Soulther Dragon (boss bar'lı, uçan, güçlü boss)
- **Yeni bloklar**: Soulther Taşı, Çimi, Kütüğü, Yaprağı, Bloğu
- **Yeni sıvı**: Liquid Soul (Ruh Sıvısı)

## ÖNEMLİ — Bunu neden derleyemedim

Bu ortamda internet erişimi olmadığı için Forge/Gradle bağımlılıklarını indirip
`.jar` dosyası üretemedim. Bu yüzden sana **kaynak kod projesini** veriyorum;
kendi bilgisayarında (internet bağlantısı olan) birkaç adımda derleyebilirsin.

## Nasıl derlenir

1. [Java 17 (JDK)](https://adoptium.net/) kurulu olmalı.
2. Bu klasörü aç, terminalde proje köküne git.
3. Şunu çalıştır:
   - Windows: `gradlew.bat build`
   - macOS/Linux: `./gradlew build`
4. İlk çalıştırmada Gradle otomatik olarak Forge 1.20.1-47.3.0'ı indirecek (internet gerekir).
5. Derleme bitince `.jar` dosyası `build/libs/soulther-1.0.0.jar` içinde olacak.
6. Bu `.jar`'ı Forge 1.20.1 kurulu `mods` klasörüne koy.

> Not: `gradlew` / `gradlew.bat` betikleri ve `gradle-wrapper.jar` bu pakette
> eksik olabilir (indirilemedi). Eğer eksikse, herhangi bir Forge MDK (Mod
> Development Kit) klasöründeki `gradlew`, `gradlew.bat`, `gradle/wrapper/gradle-wrapper.jar`
> dosyalarını bu projenin köküne kopyalaman yeterli — kaynak kodun geri kalanı zaten hazır.
> Ya da IntelliJ IDEA ile projeyi açıp "Import Gradle Project" dersen Gradle wrapper'ı kendisi kurar.

## Bilinen sınırlamalar / geliştirilebilecek yerler

- **Dokular (texture)**: Şu an tüm bloklar/eşyalar basit düz renkli placeholder
  16x16 PNG kullanıyor. Gerçek pixel-art dokuları `src/main/resources/assets/soulther/textures/`
  altına kendi PNG'lerinle değiştirebilirsin.
- **Portal çerçeve algılama**: `SoultherPortalShape` sınıfı basitleştirilmiş bir
  algoritma kullanıyor; tam nether-portal-benzeri sağlam köşe tespiti için
  geliştirilmesi gerekebilir. Şu an en güvenilir kullanım: dikdörtgen çerçevenin
  **alt sırasına** (herhangi bir kenar bloğuna) sağ tıklamak.
- **Soulther Dragon**: Ender Dragon'daki gibi çoklu faz (kristal kırma, halka
  uçuşu vb.) yok; genişletilebilir basit bir boss temeli.
- **Entity teleport mantığı**: `SoultherPortalBlock` içindeki geçiş kodu
  basitleştirilmiş; Forge/Minecraft sürüm mapping'ine göre küçük ayarlamalar
  gerekebilir (derleme hatası çıkarsa ilgili metod imzalarını IDE'nin önerdiği
  şekilde güncelle).
- Ejderha, Soul Wraith ve Voidling için özel 3D model/animasyon (renderer) yok;
  şu an vanilla temel render sistemine dayanıyorlar — istersen ekleyebiliriz.

## Klasör yapısı özeti

```
src/main/java/com/soulther/
  SoultherMod.java          -> ana mod sınıfı
  init/                     -> tüm kayıtlar (blok, eşya, mob, sıvı, yaratıcı sekme)
  item/                     -> zırh materyali, alet tier'ı, Warden Kalbi eşyası
  portal/                   -> portal bloğu ve çerçeve tespiti
  entity/                   -> Soul Wraith, Voidling, Soulther Dragon
  fluid/                    -> Liquid Soul render tipi

src/main/resources/
  data/soulther/            -> boyut, boyut tipi, biyom, tarifler, loot table'lar
  data/minecraft/           -> Warden'ın loot table override'ı (Warden Kalbi düşürür)
  assets/soulther/          -> lang, blockstate, model, placeholder texture'lar
```

İyi oyunlar! 🐉
