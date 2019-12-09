# Declaración de intenciones

Este repositorio tiene como objetivo principal, la traducción al idioma español de los tutoriales publicados por DO. [Nuestro sitio web](https://www.ks7000.net.ve/), al momento de escribir estas líneas, está alojado en máquinas virtuales llamadas _droplets_ por dicha empresa, y pagamos religiosamente por nuestra publicación en línea. Es así que nuestro único interés es la difusión del conocimiento y del software libre (objetivo de nuestro blog) y facilitar así la asimilación de nuevas tecnologías para nuestro país, Venezuela.

Con nuestro trabajo acortamos la labor, eliminamos así la barrera del idioma, teniendo en cuenta las diversas variantes que tiene el castellano, tanto en Europa como en América. Como tuvo su origen en el Viejo Mundo hacemos y/o revisamos cada traducción primero en español (España), y luego en español (Venezuela).

Cada artículo en este repositorio se rige por su licencia original:

https://creativecommons.org/licenses/by-nc-sa/4.0/

Ustedes pueden leer la misma licencia en español (España) en el siguiente enlace:

https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es_ES

**¡Pero esperen todavía hay más!** Traducir de por sí es un trabajo, nosotros damos valor agregado al revisar las instrucciones y el código en cada tutorial. Es sumamente raro que hallemos error alguno, pero nos consta que, cuando ha sucedido, los autores y editores han sido muy solícitos y amables en reconocer su error y lo ha corregido sin problema alguno. También han aceptado propuestas de mejoras de igual manera; hacemos un reconocimiento especial a [Erika Heidi](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-laravel-with-lemp-on-ubuntu-18-04?comment=81516), [Kamal Nasser](https://www.digitalocean.com/community/tutorials/how-to-use-a-remote-docker-server-to-speed-up-your-workflow?comment=82401) y [Brian Boucheron](https://www.digitalocean.com/community/tutorials/how-to-set-up-time-synchronization-on-debian-10?comment=81504), por nombrar solamente tres casos puntuales.

## Consideraciones adicionales

El idioma castellano es, a diferencia del idioma inglés, extenso, amplio en conjugaciones verbales y sumamente sensible a las redundancias (de hecho se ofrecen disculpas cuando las pronunciamos, a lo que de manera jocosa nuestros oyentes replican con «perdonen la **rebuznancia**» -¿qué culpa tienen esos pobres animales de rebuznar siempre de la misma forma, manera y consecutivo? -). Preferimos percibirlo como un idioma inclinado más hacia la poesía que hacia la prosa y choca de frente con el lenguaje técnico, por ello nuestro esfuerzo en realizar este trabajo.

Si eso no es suficiente razón, agregamos otra: la redundancia en las traducciones no ofrecen un asidero nemotécnico, lo que dificulta recordar los párrafos. Mejor es recorrerlos y asociarlos con diferentes sinóminos y verbos, aunque expresen las mismas órdenes.

## Método de trabajo

Hay muchas maneras de trabajar en entornos distribuidos con Git, tal como explica [Scott Chacon en su libro «Pro Git 2»](https://git-scm.com/book/es/v2/Git-en-entornos-distribuidos-Flujos-de-trabajo-distribuidos). Nosotros hemos escogido simplemente tener una rama principal (llamada _main_) con los archivos necesarios de presentación, licencia y código para automatizar la labor, únicamente eso :sparkles: .

Para cada tutorial (también lo denominamos **artículo** o **publicación**) abrimos una rama cuyo nombre es la [URL semántica](https://es.wikipedia.org/wiki/URL_sem%C3%A1ntica) (_slug_) de la publicación original. El lenguaje Python es el seleccionado para:

* Descargar el contenido del artículo y guardar con dicha URL semántica pero en [formato MarkDown, versión GitHub](https://guides.github.com/features/mastering-markdown/) :octocat: y realizar una acometida (_commit_).
* Si la publicación ya tiene traducción al español, copiar el anterior archivo **con la URL semántica en español como nombre** y realizar acometida (_commit_).
* Descargar la traducción oficial y guardarla en el fichero del paso anterior (sobreescribir) y realizar acometida (_commit_).
* Copiar la traducción oficial agregando a la URL semántica el sufijo "-ve" para significar castellano de Venezuela.
* Realizar sobre este último archivo los cambios necesarios para la mejor comprensión en nuestro país del tutorial en cuestión.

Dichas ramas, que como dijimos cada una es un artículo, **no son ni serán fusionadas en la principal** y solamente publicamos las instrucciones y el código necesario para realizar una bifurcación _fork_,fusionarlas y convertirlas en HTML a fin de publicarlas sin necesidad de tener una base de datos como manejador de contenido (así, de hecho, este repositorio **es** el manejador de contenido).

### Estructura de proyecto

Seguimos las [recomendaciones del sr. Kenneth Reitz](https://docs.python-guide.org/writing/structure/) acerca de los componentes y prácticas necesarias para el lenguaje Python.
