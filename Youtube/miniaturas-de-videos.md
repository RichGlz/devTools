
# Cómo obtener la miniatura (thumbnail) de algún enlace de Youtube

## Opción 1

<!-- ``` nginx -->
``` smalltalk
Ejemplo:

  https://www.youtube.com/watch?v=BrnDlRmW5hs
```

> El ID del video de arriba es: **BrnDlRmW5hs**

**Miniatura de NORMAL calidad (st)**

``` xml
https://img.youtube.com/vi/<ID_del_YTBvideo_AQUÍ>/sddefault.jpg
```

**Miniatura de MEDIANA calidad (mq)**

``` xml
https://img.youtube.com/vi/<ID_del_YTBvideo_AQUÍ>/mqdefault.jpg
```

**Miniatura de ALTA calidad (hq)**

``` xml
https://img.youtube.com/vi/<ID_del_YTBvideo_AQUÍ>/hqdefault.jpg
```

**Miniatura de MÁXIMA calidad (maxres)**

``` xml
https://img.youtube.com/vi/<ID_del_YTBvideo_AQUÍ>/maxresdefault.jpg
```

## Opción 2

### Acceder al valor `"thumbnail_url"` en el objeto JSON de un enlace

<!-- ``` nginx -->
``` smalltalk
Ejemplo:

  http://youtube.com/oembed?url=http://www.youtube.com/watch?v=BrnDlRmW5hs&format=json
```

> El ID del video de arriba es: **BrnDlRmW5hs**

Te devolverá:

``` json
{
  "thumbnail_height": 360,
  "provider_name": "YouTube",
  "html": "<iframe width=\"480\" height=\"270\" src=\"https://www.youtube.com/embed/BrnDlRmW5hs?feature=oembed\" frameborder=\"0\" allow=\"accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture\" allowfullscreen></iframe>",
  "title": "old songs but it's lofi remix",
  "thumbnail_width": 480,
  "provider_url": "https://www.youtube.com/",
  "type": "video",
  "author_url": "https://www.youtube.com/channel/UCaziV_mlABegRYAK1RGNfEQ",
  "width": 480,
  "height": 270,
  "version": "1.0",
  "author_name": "Lo-fi Music",
  "thumbnail_url": "https://i.ytimg.com/vi/BrnDlRmW5hs/hqdefault.jpg"
}
```

###### Información obtenida al día: 27/10/2020.

### Fuente de Stackoverflow: [Embed youtube videos using oembed](https://stackoverflow.com/questions/2068344/how-do-i-get-a-youtube-video-thumbnail-from-the-youtube-api#:~:text=In%20YouTube%20Data%20API%20v3,its%20width%2C%20height%20and%20URL.)