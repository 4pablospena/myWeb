## HTML - Info Interesante.

### `head`

`dns-prefetch` 

 (Pre-resolución DNS) Esta etiqueta le dice al navegador que resuelva el nombre de dominio a una dirección IP lo antes posible.

> El problema: 
    Cuando tu navegador necesita un archivo de otro servidor, primero debe preguntar a un servidor DNS: 
        "¿Cuál es la dirección IP de este nombre?". 
    Esto puede tardar entre 20ms y 120ms.

>    La solución: 
    Con dns-prefetch, el navegador hace esa pregunta en segundo plano mientras el usuario aún está leyendo el HTML inicial. Cuando llega el momento de descargar la imagen o el script de Twitter, ya sabe a qué IP ir.

>    Cuándo usarlo: 
    Es ideal para dominios que no son críticos para la carga inicial o como "respaldo" para navegadores antiguos

---

`preconnect`

 (Pre-conexión completa) Esta es una versión más potente y moderna que la anterior. No solo resuelve el DNS, sino que también establece la conexión completa con el servidor.
 
 >   Específicamente, realiza tres pasos:  
>  1) DNS Lookup: Encuentra la IP.TCP 
>  2) Handshake: Establece la conexión con el servidor.
>  3) TLS/SSL Negotiation: (Si es HTTPS) Intercambia las llaves de seguridad para cifrar la comunicación.
    
>    La ventaja: Al hacer estos tres pasos por adelantado, ahorras mucho tiempo de espera ("latencia") cuando el navegador finalmente solicita el recurso real.
    
>    Cuándo usarlo: Para dominios externos desde los cuales sabes que vas a descargar archivos importantes de inmediato (fuentes de Google, librerías de scripts o imágenes principales)

---
`<script>` 

Sirve para cargar y ejecutar código JavaScript antes de que el resto de la página (el contenido visible o <body>) termine de procesarse.

Dependiendo de cómo se escriba, puede tener efectos muy distintos en la velocidad de tu web:

1. Scripts de configuración crítica
Se colocan en el head cuando el código debe ejecutarse antes de que el usuario vea nada.

>    Ejemplo: Un script que detecta si el usuario prefiere "Modo Oscuro" o "Modo Claro" para aplicar los colores correctos de inmediato y evitar un destello blanco molesto.

2. Carga de librerías externas
Históricamente, muchas librerías (como las de analíticas o rastreo) pedían ir en el head para asegurar que empezaran a medir la visita desde el primer milisegundo.

>   Ejemplo: Google Tag Manager o servicios de detección de errores.    

El gran problema: El bloqueo del renderizado
Por defecto, cuando el navegador encuentra un `<script>` en el `<head>`, se detiene por completo. Deja de leer el HTML, descarga el JS, lo ejecuta y solo entonces sigue con el resto. Esto puede hacer que el usuario vea una pantalla en blanco durante unos segundos.

Las mejores prácticas actuales
Para evitar que el sitio se sienta lento, hoy en día usamos dos atributos especiales cuando ponemos scripts en el head:

A. Atributo defer (El más recomendado)
El script se descarga mientras el HTML se sigue leyendo, pero solo se ejecuta cuando el HTML ha terminado de cargar por completo.

Uso: <script src="app.js" defer></script>

Ventaja: No bloquea la página y mantiene el orden de ejecución.

B. Atributo async
El script se descarga en segundo plano y, en cuanto termina de descargar, se ejecuta, pausando el análisis del HTML si es necesario.

Uso: <script src="publicidad.js" async></script>

Ventaja: Útil para cosas que no dependen de nada más, como un anuncio o un contador de visitas.

---

La diferencia clave: Inline vs. Block
Para entender el `<span>`, hay que compararlo con el `<div>`:

> `<div>` (Bloque): Crea un salto de línea antes y después. Ocupa todo el ancho disponible.

> `<span>` (En línea): Solo ocupa el espacio necesario para el contenido que tiene dentro y no rompe el flujo del texto.
---