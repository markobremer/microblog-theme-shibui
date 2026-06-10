# Tema shibui para Micro.blog

Port del tema [shibui](https://github.com/ntk148v/shibui) (el mismo de
`blog.markobremer.com`) como tema personalizado de Micro.blog, para que
`micro.markobremer.com` luzca igual que el blog.

Micro.blog genera los sitios con Hugo y superpone el tema personalizado sobre su
[theme-blank](https://github.com/microdotblog/theme-blank), que aporta feeds
(RSS/JSON), archivo, fotos, robots.txt, etc. Por eso acá solo viven las
plantillas HTML y el CSS; lo demás lo pone Micro.blog.

## Qué incluye

| Archivo | Qué hace |
|---|---|
| `layouts/_default/baseof.html` | Estructura base de shibui (skip-link, header, main, footer) + hooks de Micro.blog (`custom_footer`, `plugins_js`) |
| `layouts/index.html` | Portada: timeline de microposts con contenido completo, paginado |
| `layouts/post/single.html` | Post individual (maneja posts sin título, narración y conversación de Micro.blog) |
| `layouts/_default/list.html` | Categorías y secciones |
| `layouts/_default/single.html` | Páginas estáticas (Sobre, etc.) |
| `layouts/section/replies.html` | Página de respuestas |
| `layouts/partials/` | head (con `microblog_head`), breadcrumb de shibui, footer, paginación |
| `static/css/main.css` | CSS de shibui (main + custom) más estilos para el timeline y conversation.js |

Verificado con Hugo 0.91.2 y 0.117.0 (las dos versiones que usa Micro.blog),
montado sobre `theme-blank` tal como lo hace Micro.blog.

## Cómo instalarlo en Micro.blog

Micro.blog importa temas personalizados desde un repo Git **público** con el
tema en la **raíz**. Como este repo es privado y el tema vive en una subcarpeta,
hay que exportarlo a un repo público propio una vez:

1. Crear un repo público vacío, p. ej. `markobremer/microblog-theme-shibui`
   (sin README inicial).

2. Desde este repo, exportar la carpeta como branch y empujarla:

   ```bash
   git subtree split --prefix=microblog-theme -b microblog-theme-export
   git push https://github.com/markobremer/microblog-theme-shibui.git microblog-theme-export:main
   git branch -D microblog-theme-export
   ```

3. En Micro.blog: **Design → Edit Custom Themes → New Theme**, marcar
   **"Clone from existing Git repository"** y pegar
   `https://github.com/markobremer/microblog-theme-shibui`.

4. De vuelta en **Design**, seleccionar el tema personalizado recién creado como
   tema del blog. En la misma página conviene fijar **Hugo version: 0.117** y
   revisar que el título del sitio sea `Marko Bremer` (para que el breadcrumb
   `/Marko Bremer/...` coincida con el blog).

5. Para futuros cambios: editar acá, repetir el paso 2, y en Micro.blog abrir el
   tema y usar **"Update from Git"** (o borrar y re-importar).

Alternativa sin repo extra: crear un tema en blanco en **Edit Custom Themes** y
copiar/pegar estos ~10 archivos a mano en el editor web de Micro.blog (con la
misma ruta cada uno).

## Notas

- Los microposts no llevan título: el timeline muestra el contenido completo y
  la fecha como enlace al post; el `<title>` y el breadcrumb usan la fecha.
- La numeración automática de encabezados de shibui se reinicia en cada post del
  timeline (si no, los h2 de un post continuarían la cuenta del anterior).
- Si se activa **include_conversation** en Micro.blog, la conversación se
  muestra con el mismo estilo (bordes y avatares redondos monocromos).
- El menú de navegación de la portada sale de **Design → Pages** de Micro.blog
  (ahí se agregan "Sobre", "Archive", etc.).
