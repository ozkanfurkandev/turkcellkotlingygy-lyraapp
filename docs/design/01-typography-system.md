# LyraApp - Tipografi Sistemi

> Bu dosya LyraApp isimli uygulamanın tipografi tanımları için
> **tek doğruluk kaynağıdır** (single source of truth) ve
> doğrudan bir **Android Jetpack Compose** projesinde kullanılmak
> üzere düzenlenmiştir.

---

## 1. Temel Kural

> Hiçbir `@Composable` içinde ham `TextStyle(...)` veya `fontSize = 14.sp` yazılmaz.
> Metin stilleri daima `MaterialTheme.typography.<slot>` üzerinden okunmak zorundadır.

Ham `TextStyle` tanımı yalnızca `Type.kt` içinde, `LyraTypography` sabiti oluşturulurken kullanılır.

---

## 2. Font Ailesi

| Özellik | Değer |
|---------|-------|
| Font | **Roboto** |
| Kaynak | Google Fonts (Downloadable Fonts API) |
| Kotlin sabiti | `RobotoFontFamily` |
| Dosya | `app/src/main/java/com/turkcell/lyraapp/ui/theme/Type.kt` |

Roboto, Material Design 3 tipografi ölçeğinin resmi font ailesidir. Tüm ağırlıklar (Regular 400, Medium 500, Bold 700) Google Fonts üzerinden yüklenir.

---

## 3. Material 3 Tipografi Slotları

Aşağıdaki tablo M3 varsayılan ölçeğine uyar; tüm slotlarda `fontFamily = RobotoFontFamily` kullanılır.

| Slot | fontSize | lineHeight | fontWeight | letterSpacing |
|------|----------|------------|------------|---------------|
| displayLarge | 57sp | 64sp | Normal (400) | -0.25sp |
| displayMedium | 45sp | 52sp | Normal (400) | 0sp |
| displaySmall | 36sp | 44sp | Normal (400) | 0sp |
| headlineLarge | 32sp | 40sp | Normal (400) | 0sp |
| headlineMedium | 28sp | 36sp | Normal (400) | 0sp |
| headlineSmall | 24sp | 32sp | Normal (400) | 0sp |
| titleLarge | 22sp | 28sp | Normal (400) | 0sp |
| titleMedium | 16sp | 24sp | Medium (500) | 0.15sp |
| titleSmall | 14sp | 20sp | Medium (500) | 0.1sp |
| bodyLarge | 16sp | 24sp | Normal (400) | 0.5sp |
| bodyMedium | 14sp | 20sp | Normal (400) | 0.25sp |
| bodySmall | 12sp | 16sp | Normal (400) | 0.4sp |
| labelLarge | 14sp | 20sp | Medium (500) | 0.1sp |
| labelMedium | 12sp | 16sp | Medium (500) | 0.5sp |
| labelSmall | 11sp | 16sp | Medium (500) | 0.5sp |

---

## 4. `Type.kt` — Kotlin Implementasyonu

```kotlin
package com.turkcell.lyraapp.ui.theme

import androidx.compose.material3.Typography
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.googlefonts.Font
import androidx.compose.ui.text.googlefonts.GoogleFont
import androidx.compose.ui.unit.sp
import com.turkcell.lyraapp.R

private val Roboto = GoogleFont("Roboto")

val RobotoFontFamily = FontFamily(
    Font(googleFont = Roboto, fontProvider = googleFontProvider, weight = FontWeight.Normal),
    Font(googleFont = Roboto, fontProvider = googleFontProvider, weight = FontWeight.Medium),
    Font(googleFont = Roboto, fontProvider = googleFontProvider, weight = FontWeight.Bold),
)

val LyraTypography = Typography(
    displayLarge = TextStyle(
        fontFamily = RobotoFontFamily,
        fontWeight = FontWeight.Normal,
        fontSize = 57.sp,
        lineHeight = 64.sp,
        letterSpacing = (-0.25).sp,
    ),
    // ... tüm slotlar aynı kalıpla
)
```

---

## 5. `Theme.kt` — Tema Entegrasyonu

```kotlin
MaterialTheme(
    colorScheme = colorScheme,
    typography = LyraTypography,
    content = content,
)
```

---

## 6. Kullanım Örnekleri

```kotlin
// Doğru
Text(
    text = "Şarkı Adı",
    style = MaterialTheme.typography.titleLarge,
)

// Yanlış — ham TextStyle kullanımı yasak
Text(
    text = "Şarkı Adı",
    fontSize = 22.sp,
)
```

---

## 7. Bağımlılıklar

| Kütüphane | Amaç |
|-----------|------|
| `androidx.compose.ui:ui-text-google-fonts` | Roboto indirilebilir font desteği |

Sertifika dosyası: `app/src/main/res/values/font_certs.xml`
