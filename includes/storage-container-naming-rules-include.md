Cada blob del almacenamiento de Azure debe residir en un contenedor. Hola contenedor forma parte del nombre de blob de Hola. Por ejemplo, `mycontainer` es Hola nombre del contenedor de hello en estos URI de blob de ejemplo:

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Un nombre de contenedor debe ser un nombre DNS válido, conforme toohello siguiendo las reglas de nomenclatura:

1. Los nombres de contenedor deben empezar por una letra o un número y pueden contener solo letras, números y caracteres de guión (-) Hola.
2. Todos los caracteres de guión (-) deben estar inmediatamente precedidos y seguidos por una letra o un número; no se permiten guiones consecutivos en nombres de contenedor.
3. Todas las letras del nombre de un contenedor deben aparecer en minúsculas.
4. Los nombres de contenedor deben tener entre 3 y 63 caracteres de longitud.

> [!IMPORTANT]
> Tenga en cuenta que Hola nombre de un contenedor siempre debe estar en minúscula. Si incluye una letra mayúscula en un nombre de contenedor, o en caso contrario, infringe las reglas de nomenclatura de contenedor de hello, recibirá un error 400 (solicitud incorrecta). 
> 
> 

