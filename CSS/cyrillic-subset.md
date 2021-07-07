## Cyrillic Subset
U+0400-045F - Русский алфавит из Кириллицы
U+0490-0491 - Кириллическая заглавная буква г с подъемом (Ґ) и Кириллическая строчная буква г с подъемом (ґ)
U+04B0-04B1 Кириллическая заглавная буква «прямое у» с чертой (Ұ) и Кириллическая строчная буква «прямое у» с чертой (ұ)
U+2116 - Знак номера (№)
U+20BD - Знак рубля (₽) по каким-то причинам не входит в Cyrillic Subset. Google, почему?

## Cyrillic Extended Subset
U+0460-052F - Часть Кириллицы без русского алфавита + Дополнительные символы кириллицы
U+1C80-1C88 - Расширенная кириллица C
U+20B4 - Знак гривны (₴)
U+2DE0-2DFF - Расширенная кириллица A
U+A640-A69F - Расширенная кириллица-B
U+FE2E-FE2F - Combining Cyrillic Titlo Left Half (︮) и Combining Cyrillic Titlo Right Half (︯). Являются частью Комбинируемых половинок символов


```
/* cyrillic */
@font-face {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 400;
  src: local('Noto Sans'), local('NotoSans'), url(https://fonts.gstatic.com/s/notosans/v7/o-0IIpQlx3QUlC5A4PNr4TRAW_0.woff2) format('woff2');
  unicode-range: U+0400-045F, U+0490-0491, U+04B0-04B1, U+2116;
}

/* cyrillic-ext */
@font-face {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 400;
  src: local('Noto Sans'), local('NotoSans'), url(https://fonts.gstatic.com/s/notosans/v7/o-0IIpQlx3QUlC5A4PNr6DRAW_0.woff2) format('woff2');
  unicode-range: U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;
}
```


## Латиница

Latin					U+0000-00FF
Latin-extended-a		U+0100-017F
Latin-extended-b		U+0180-024F
Rest middle				U+0259-03C0
Latin-extended-additional	U+1E00-1EFF
Rest						U+2000-FB02

```
@font-face {
  font-family: 'Source Sans Pro';
  src: url('/fonts/SourceSansPro.woff2') format('woff2');
  unicode-range: U+0020-007F; /* The bare minimum for the English Language */
}
```
