# Пример полного тега picture
```
<picture class="">
  <!-- десктопы больше чем  1369px -->
  <source
    media="(min-width: 1369px)"
    srcset="
      https://server_img_path/1050_16x9-hash.webp,
      https://server_img_path/1050_16x9-hash.webp 2x
    "
    sizes="1050px"
    type="image/webp" />
  <source
    media="(min-width: 1369px)"
    srcset="
      https://server_img_path/1050_16x9-hash.jpeg,
      https://server_img_path/1050_16x9-hash.jpeg 2x
    "
    sizes="1050px"
    type="image/jpeg" />

  <!-- десктопы/планшеты от 1281px и до 1368px -->
  <source
    media="(min-width: 1281px and max-width: 1368px)"
    srcset="
      https://server_img_path/992_16x9-hash.webp,
      https://server_img_path/1050_16x9-hash.webp 2x
    "
    sizes="992px"
    type="image/webp" />
  <source
    media="(min-width: 1281px and max-width: 1368px)"
    srcset="
      https://server_img_path/992_16x9-hash.jpeg,
      https://server_img_path/1050_16x9-hash.jpeg 2x
    "
    sizes="992px"
    type="image/jpeg" />

  <!-- планшеты от 769px до 1280px -->
  <source
    media="(min-width: 769px and max-width: 1280px)"
    srcset="
      https://server_img_path/768_16x9-hash.webp,
      https://server_img_path/992_16x9-hash.webp 2x
    "
    sizes="768px"
    type="image/webp" />
  <source
    media="(min-width: 769px and max-width: 1280px)"
    srcset="
      https://server_img_path/768_16x9-hash.jpeg,
      https://server_img_path/992_16x9-hash.jpeg 2x
    "
    sizes="768px"
    type="image/jpeg" />

  <!-- планшеты/телефоны от 363 до 768px -->
  <source
    media="(min-width: 364px and max-width: 768px)"
    srcset="
      https://server_img_path/720_16x9-hash.webp,
      https://server_img_path/768_16x9-hash.webp 2x
    "
    sizes="720px"
    type="image/webp" />
  <source
    media="(min-width: 364px and max-width: 768px)"
    srcset="
      https://server_img_path/720_16x9-hash.jpeg,
      https://server_img_path/768_16x9-hash.jpeg 2x
    "
    sizes="720px"
    type="image/jpeg" />

  <!-- для мобилок 363px и меньше  -->
  <source
    media="(max-width: 363px)"
    srcset="
      https://server_img_path/415_16x9-hash.webp,
      https://server_img_path/720_16x9-hash.webp 2x
    "
    sizes="415px"
    type="image/webp" />
  <source
    media="(max-width: 363px)"
    srcset="
      https://server_img_path/415_16x9-hash.jpeg,
      https://server_img_path/720_16x9-hash.jpeg 2x
    "
    sizes="415px"
    type="image/jpeg" />

  <img
    src="https://server_img_path/415_16x9-hash.jpeg"
    class=""
    alt="описание_картинки"
/></picture>
<picture class="">
  <!-- десктопы больше чем  1369px -->
  <source
    media="(min-width: 1369px)"
    srcset="
      https://server_img_path/1050_16x9-hash.webp,
      https://server_img_path/1050_16x9-hash.webp 2x
    "
    sizes="1050px"
    type="image/webp" />
  <source
    media="(min-width: 1369px)"
    srcset="
      https://server_img_path/1050_16x9-hash.jpeg,
      https://server_img_path/1050_16x9-hash.jpeg 2x
    "
    sizes="1050px"
    type="image/jpeg" />

  <!-- десктопы/планшеты от 1281px и до 1368px -->
  <source
    media="(min-width: 1281px and max-width: 1368px)"
    srcset="
      https://server_img_path/992_16x9-hash.webp,
      https://server_img_path/1050_16x9-hash.webp 2x
    "
    sizes="992px"
    type="image/webp" />
  <source
    media="(min-width: 1281px and max-width: 1368px)"
    srcset="
      https://server_img_path/992_16x9-hash.jpeg,
      https://server_img_path/1050_16x9-hash.jpeg 2x
    "
    sizes="992px"
    type="image/jpeg" />

  <!-- планшеты от 769px до 1280px -->
  <source
    media="(min-width: 769px and max-width: 1280px)"
    srcset="
      https://server_img_path/768_16x9-hash.webp,
      https://server_img_path/992_16x9-hash.webp 2x
    "
    sizes="768px"
    type="image/webp" />
  <source
    media="(min-width: 769px and max-width: 1280px)"
    srcset="
      https://server_img_path/768_16x9-hash.jpeg,
      https://server_img_path/992_16x9-hash.jpeg 2x
    "
    sizes="768px"
    type="image/jpeg" />

  <!-- планшеты/телефоны от 363 до 768px -->
  <source
    media="(min-width: 364px and max-width: 768px)"
    srcset="
      https://server_img_path/720_16x9-hash.webp,
      https://server_img_path/768_16x9-hash.webp 2x
    "
    sizes="720px"
    type="image/webp" />
  <source
    media="(min-width: 364px and max-width: 768px)"
    srcset="
      https://server_img_path/720_16x9-hash.jpeg,
      https://server_img_path/768_16x9-hash.jpeg 2x
    "
    sizes="720px"
    type="image/jpeg" />

  <!-- для мобилок 363px и меньше  -->
  <source
    media="(max-width: 363px)"
    srcset="
      https://server_img_path/415_16x9-hash.webp,
      https://server_img_path/720_16x9-hash.webp 2x
    "
    sizes="415px"
    type="image/webp" />
  <source
    media="(max-width: 363px)"
    srcset="
      https://server_img_path/415_16x9-hash.jpeg,
      https://server_img_path/720_16x9-hash.jpeg 2x
    "
    sizes="415px"
    type="image/jpeg" />

  <img
    src="https://server_img_path/415_16x9-hash.jpeg"
    class=""
    alt="описание_картинки"
/></picture>
```
