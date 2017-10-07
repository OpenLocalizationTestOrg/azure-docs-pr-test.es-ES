---
title: "notas de la versión de aaaMicrosoft Explorador de almacenamiento de Azure (versión preliminar) | Documentos de Microsoft"
description: "Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar)

Este artículo contiene la versión de Hola notas para Azure Storage Explorer 0.8.16 (vista previa) de la versión, así como notas de la versión para las versiones anteriores.

[Explorador de almacenamiento de Microsoft Azure (vista previa)](./vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux.

## <a name="version-0816-preview"></a>Versión 0.8.16 (versión preliminar)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Descarga del Explorador de Azure Storage 0.8.16 (versión preliminar)
- [Explorador de Azure Storage 0.8.16 (versión preliminar) para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Explorador de Azure Storage 0.8.16 (versión preliminar) para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Explorador de Azure Storage 0.8.16 (versión preliminar) para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Nuevo
* Al abrir un blob, el Explorador de almacenamiento le solicitará que tooupload Hola Descargar archivo si se detecta un cambio
* Experiencia mejorada de inicio de sesión de Azure Stack
* Rendimiento mejorado Hola de carga/descarga de muchos pequeños archivos de hello mismo tiempo


### <a name="fixes"></a>Correcciones
* En algunos tipos de blob, elegir "reemplazar" demasiado durante un conflicto de carga a veces produciría carga Hola se reinicia. 
* En la versión 0.8.15, las cargas se detendrían a veces en un 99 %.
* Al cargar el recurso compartido de archivos de tooa de archivos, si ha elegido el directorio de tooa tooupload que aún no existe, se producirá un error en la carga.
* El Explorador de Storage estaba generando marcas de tiempo de forma incorrecta para las firmas de acceso compartido y las consultas de tabla.


Problemas conocidos
* El uso de un nombre y una cadena de conexión de clave no funciona actualmente. Se corregirá en la siguiente versión de Hola. Hasta ese momento, puede usar la asociación con el nombre y la clave.
* Si intentas tooopen un archivo con un nombre de archivo no válido de Windows, descarga de Hola dará como resultado un archivo de error no encontrado.
* Después de hacer clic en "Cancelar" en una tarea, puede tardar unos instantes para que toocancel de tarea. Se trata de una limitación de la biblioteca de nodo de almacenamiento de Azure Hola.
* Después de completar una carga de blobs, se actualiza la pestaña de Hola que inició la carga de Hola. Esto es un cambio de comportamiento anterior y también hará que toobe dirigirá toohello raíz se encuentra en el contenedor de Hola de nuevo.
* Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, a continuación, deberá toorestart en orden toohave Explorador de almacenamiento olvida esa decisión.
* puede mostrar el panel de configuración de cuenta de Hello que necesita credenciales toofilter suscripciones a tooreenter.
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.
* Para los usuarios de Ubuntu 14.04, necesitará tooensure GCC está activo toodate: Esto puede hacerse mediante la ejecución de hello sigue comandos y, a continuación, reiniciar el equipo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Para los usuarios de Ubuntu 17.04, necesitará tooinstall GConf: Esto puede hacerse ejecutando Hola sigue comandos y, a continuación, reiniciar el equipo:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Versión 0.8.14 (versión preliminar)
22/06/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar)
* [Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Nuevo

* Too1.7.2 de versión actualizada de electrones en orden tootake aprovechar las varias actualizaciones de seguridad críticas
* Se puede ahora acceder rápidamente a la Guía de solución de problemas en pantalla de Hola desde el menú de Ayuda de Hola
* [Guía][2] de solución de problemas del Explorador de Storage
* [Instrucciones] [ 3] sobre la conexión de suscripción de Azure pila tooan

### <a name="known-issues"></a>Problemas conocidos

* Botones del cuadro de diálogo de confirmación de carpeta de hello delete no se registran con clics del mouse de hello en Linux. Solución alternativa es la tecla ENTRAR de toouse Hola
* Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, deberá toorestart en orden toohave Explorador de almacenamiento olvida decisión Hola
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de
* panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada. 
* Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Versiones anteriores

* [Versión 0.8.13](#version-0813)
* [Versión 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Versión 0.8.9 / 0.8.8](#version-089--088)
* [Versión 0.8.7](#version-087)
* [Versión 0.8.6](#version-086)
* [Versión 0.8.5](#version-085)
* [Versión 0.8.4](#version-084)
* [Versión 0.8.3](#version-083)
* [Versión 0.8.2](#version-082)
* [Versión 0.8.0](#version-080)
* [Versión 0.7.20160509.0](#version-07201605090)
* [Versión 0.7.20160325.0](#version-07201603250)
* [Versión 0.7.20160129.1](#version-07201601291)
* [Versión 0.7.20160105.0](#version-07201601050)
* [Versión 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Versión 0.8.13
05/12/2017

#### <a name="new"></a>Nuevo

* [Guía][2] de solución de problemas del Explorador de Storage
* [Instrucciones] [ 3] sobre la conexión de suscripción de Azure pila tooan

#### <a name="fixes"></a>Correcciones

* Problema corregido: Había una alta probabilidad de que, al cargar un archivo, se produjese un error de memoria agotada.
* Problema corregido: Ahora puede iniciar sesión con una tarjeta inteligente o un PIN.
* Problema corregido: Abrir en Portal ahora funciona con Azure China, Azure Germany, Azure US Government y Azure Stack.
* Problema corregido: Al cargar un contenedor de blobs de tooa de carpeta, "Operación no válida" produciría un error a veces
* Problema corregido: Seleccionar todo se deshabilita durante la administración de instantáneas.
* Problema corregido: Hola metadatos del blob base Hola podrían se sobrescriban después de ver las propiedades de Hola de sus instantáneas

#### <a name="known-issues"></a>Problemas conocidos

* Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, deberá toorestart en orden toohave Explorador de almacenamiento olvida decisión Hola
* Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de
* panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada. 
* Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Versión 0.8.12 / 0.8.11 / 0.8.10
07/04/2017

#### <a name="new"></a>Nuevo

* Explorador de almacenamiento ahora se cerrará automáticamente cuando se instala una actualización de notificación de actualización de Hola
* El acceso rápido local proporciona una experiencia mejorada a la hora de trabajar con los recursos a los que accede con más frecuencia.
* En el editor de contenedor de blobs de hello, ahora puede ver qué máquina virtual al que pertenece un blob en concesión
* Ahora se puede contraer el panel del lado izquierdo de Hola
* Detección ahora se ejecuta en hello mismo tiempo como descarga
* Usar las estadísticas en hello contenedor de blobs, recurso compartido de archivos y tabla editores toosee Hola el tamaño de los recursos o la selección
* Ahora puede tooAzure inicio de sesión en Active Directory (AAD) según las cuentas de la pila de Azure. 
* Ahora el archivo de carga de archivos de cuentas de almacenamiento de más de 32 MB tooPremium puede
* Compatibilidad de accesibilidad mejorada.
* Ahora puede agregar confianza Base64 codificado certificados X.509 SSL por va tooEdit -&gt; certificados de SSL:&gt; importar certificados

#### <a name="fixes"></a>Correcciones

* Problema corregido: después de actualizar las credenciales de una cuenta, vista de árbol de hello haría a veces no actualizar automáticamente
* Problema corregido: Al generar un SAS para tablas y colas de emulador, se producía una URL no válida.
* Problema corregido: Las cuentas de almacenamiento premium ahora se pueden ampliar mientras haya un proxy habilitado.
* Se ha corregido: Hola botón Aplicar en las cuentas de hello página de administración no funcionaría si hubiera 1 ó 0 cuentas seleccionadas
* Problema corregido: Se puede producir un error al cargar blobs que requieran resoluciones de conflictos. Esto se ha corregido en la versión 0.8.11. 
* Problema corregido: No se podían enviar comentarios en la versión 0.8.11. Corregido en la versión 0.8.12. 

#### <a name="known-issues"></a>Problemas conocidos

* Después de actualizar too0.8.10, necesitará toorefresh todos sus credenciales.
* Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello.
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores.
* panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden.
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada. 
* Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Versión 0.8.9 / 0.8.8
23/02/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nuevo

* 0.8.9 del explorador de almacenamiento descargará automáticamente la versión más reciente de Hola para las actualizaciones.
* Revisión: mediante el portal genera tooattach de URI de SAS que una cuenta de almacenamiento produciría un error.
* Ahora puede crear, administrar y promover instantáneas de blobs.
* Ahora puede iniciar sesión en cuentas tooAzure de China, Azure en Alemania y gobierno de EE.
* Ahora puede cambiar el nivel de zoom de Hola. Utilizar opciones de Hola Hola vista menú tooZoom en Alejar y restablecer Zoom.
* Ahora se admiten caracteres Unicode en los metadatos de usuarios para blobs y archivos.
* Mejoras de accesibilidad.
* notas de la versión de la versión siguiente de Hello pueden verse de notificación de actualización de Hola. También puede ver Hola actual notas de la versión desde el menú de Ayuda de Hola.

#### <a name="fixes"></a>Correcciones

* Problema corregido: número de versión de Hola correctamente aparece ahora en el Panel de Control en Windows
* Problema corregido: búsqueda ya no es too50 limitado, 000 nodos
* Problema corregido: recurso compartido de archivos de tooa de carga creadas para siempre si el directorio de destino de hello no existía todavía
* Problema corregido: Estabilidad mejorada para cargas y descargas largas.

#### <a name="known-issues"></a>Problemas conocidos

* Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello.
* Acceso rápido solo funciona con elementos basados en la suscripción. En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.
* Puede tardar unos segundos toonavigate toohello recurso de destino, según la cantidad de recursos que tiene un acceso rápido.
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores.

16/12/2016
### <a name="version-087"></a>Versión 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuevo

* Puede elegir cómo tooresolve conflictos al principio de Hola de una actualización, descargar o copiar la sesión en la ventana de actividades de hello
* Mantenga el mouse sobre una ficha toosee Hola ruta de acceso completa del recurso de almacenamiento de Hola
* Al hacer clic en una pestaña, se sincroniza con su ubicación en el panel de navegación del lado izquierdo de Hola

#### <a name="fixes"></a>Correcciones

* Problema corregido: El Explorador de Storage es ahora una aplicación de confianza en Mac.
* Problema corregido: Ubuntu 14.04 se admite de nuevo.
* Problema corregido: A veces Hola Agregar cuenta UI parpadea al cargar las suscripciones
* Problema corregido: En ocasiones, no todos los recursos de almacenamiento figuraban en el panel de navegación del lado izquierdo de Hola
* Problema corregido: panel de acciones de Hola a veces muestra acciones vacías
* Fijo: ahora se conserva tamaño de la ventana de Hola de sesión de hello cerró por última vez
* Se ha corregido: Se pueden abrir varias pestañas para hello mismo recurso mediante el menú contextual de Hola

#### <a name="known-issues"></a>Problemas conocidos

* Acceso rápido solo funciona con elementos basados en la suscripción. En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.
* Puede tardar unos segundos toonavigate toohello recurso de destino, dependiendo de cuántos recursos tendrá acceso rápido
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de
* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.
* Para hello primera vez con hello Explorador de almacenamiento en macOS, puede que vea varios mensajes piden llaveros de tooaccess de permiso del usuario. Se recomienda que seleccione Permitir siempre por lo que el mensaje Hola no vuelva a mostrarse

18/11/2016
### <a name="version-086"></a>Versión 0.8.6

#### <a name="new"></a>Nuevo

* Puede ahora pin usa con mayor frecuencia servicios toohello acceso rápido para facilitar la navegación
* Ya puede abrir varios editores en diferentes pestañas. Un solo clic tooopen una pestaña temporal; Haga doble clic en tooopen una pestaña permanente. También puede hacer clic en hello pestaña temporal toomake, una pestaña permanente
* Hemos realizado mejoras notables de rendimiento y estabilidad para cargas y descargas, especialmente para archivos de gran tamaño en máquinas rápidas
* Las carpetas vacías "virtuales" ya se pueden crear en contenedores de blobs.
* Hemos vuelto a incorporar la búsqueda en ámbito con la nueva y mejorada búsqueda de subcadenas, por lo que ahora tiene dos opciones para realizar búsquedas: 
    * Global búsqueda - tan sólo debe escribir un término de búsqueda en el cuadro de texto de búsqueda de Hola
    * Búsqueda de ámbito - haga clic en hello lupa icono siguiente tooa nodo, a continuación, agregar un extremo de toohello del término de búsqueda de ruta de acceso de hello, o haga clic en y seleccione "Búsqueda desde aquí"
* Hemos agregado varios temas: claro (valor predeterminado), oscuro, negro en alto contraste y blanco en alto contraste. Vaya tooEdit -&gt; toochange temas sus preferencias de temas
* Puede modificar las propiedades de blobs y archivos.
* Ahora se admiten mensajes de cola cifrados (Base64) y sin cifrar.
* En Linux, ahora es necesario usar un sistema operativo de 64 bits. En esta versión solo se admite Ubuntu 16.04.1 LTS de 64 bits.
* ¡Hemos actualizado nuestro logotipo!

#### <a name="fixes"></a>Correcciones

* Problema corregido: Problemas de inmovilización de pantalla
* Problema corregido: Mayor seguridad
* Problema corregido: A veces, podrían aparecer cuentas conectadas duplicadas.
* Problema corregido: Un blob con un tipo de contenido sin definir podría generar una excepción.
* Problema corregido: Hola de abrir el Panel de consulta en una tabla vacía no era posible
* Problema corregido: Varios errores en la búsqueda.
* Fijo: Mayor número de Hola de recursos cargados desde too100 50 al hacer clic en "Más carga"
* Problema corregido: En la primera ejecución, si ha iniciado sesión con una cuenta, ahora se seleccionan todas las suscripciones para esa cuenta de manera predeterminada. 

#### <a name="known-issues"></a>Problemas conocidos

* Esta versión de Hola Explorador de almacenamiento no se ejecuta en Ubuntu 14.04
* tooopen varias pestañas para hello mismo recurso, realice continuamente no haga clic en Hola mismo recurso. Haga clic en otro recurso y, a continuación, volver atrás y, a continuación, vuelva a hacer clic en hello original recursos tooopen en otra ficha 
* Acceso rápido solo funciona con elementos basados en la suscripción. En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.
* Puede tardar unos segundos toonavigate toohello recurso de destino, dependiendo de cuántos recursos tendrá acceso rápido
* Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de
* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.

03/10/2016
### <a name="version-085"></a>Versión 0.8.5

#### <a name="new"></a>Nuevo

* Puede ahora tooattach tooStorage de claves de uso SAS generado por el Portal de cuentas y recursos

#### <a name="fixes"></a>Correcciones

* Corregido: condición de carrera durante la búsqueda a veces debe toobecome de nodos no se pueden expandir
* Problema corregido: "Usar HTTP" no funciona cuando se conecta tooStorage cuentas con clave y el nombre de cuenta
* Problema corregido: Las claves SAS (especialmente las generadas en el Portal) devuelven un error de “barra oblicua final”.
* Problema corregido: Problemas al importar tablas.
    * A veces se revertían la clave de fila y la clave de partición
    * No se puede tooread "null" claves de partición

#### <a name="known-issues"></a>Problemas conocidos

* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.
* Pila de Azure no admite actualmente los archivos, para intentar tooexpand archivos mostrará un error

12/09/2016
### <a name="version-084"></a>Versión 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuevo

* Generar cuentas toostorage de vínculos directos, contenedores, las colas, las tablas o recursos compartidos de archivos para compartir y fácil de obtener acceso a recursos de tooyour - Windows y Mac OS admiten
* Busque los contenedores de blobs, tablas, colas, recursos compartidos de archivos o las cuentas de almacenamiento desde el cuadro de búsqueda de Hola
* Ahora puede agrupar las cláusulas en Generador de consultas de tabla de Hola
* Cambie el nombre y copie y pegue contenedores de blobs, recursos compartidos de archivos, tablas, blobs, carpetas de blobs, archivos y directorios desde cuentas conectadas mediante SAS y contenedores.
* Al cambiar el nombre y copiar contenedores de blobs y recursos compartidos de archivos, ahora se conservan las propiedades y los metadatos.

#### <a name="fixes"></a>Correcciones

* Problema corregido: No se pueden editar las entidades de tablas si contienen propiedades binarias o booleanas.

#### <a name="known-issues"></a>Problemas conocidos

* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.

03/08/2016
### <a name="version-083"></a>Versión 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuevo

* Cambie el nombre de contenedores, tablas y recursos compartidos de archivos.
* Experiencia mejorada con el generador de consultas.
* Consultas de toosave y carga de capacidad
* Dirigir toostorage cuentas o contenedores, las colas, tablas de vínculos o recursos compartidos para compartir y acceder fácilmente a los recursos de archivos (sólo Windows - macOS admiten próximamente!)
* Capacidad toomanage y configurar las reglas de CORS

#### <a name="fixes"></a>Correcciones

* Problema corregido: Las cuentas de Microsoft requieren que vuelva a autenticarse en períodos de 8 a 12 horas.

#### <a name="known-issues"></a>Problemas conocidos

* A veces hello interfaz de usuario podría parezca detenida: lo que maximiza la ventana hello ayuda a resolver este problema
* Puede que la instalación en macOS requiera permisos elevados.
* Puede mostrar el panel de configuración de la cuenta que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden
* Cambio de nombre de recursos compartidos de archivos, contenedores de blobs y tablas no conserva los metadatos u otras propiedades en el contenedor de hello, como la cuota del recurso compartido de archivos, nivel de acceso público o las directivas de acceso
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las otras propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* No se puede copiar o cambiar de nombre recursos en cuentas conectadas mediante SAS.

07/07/2016
### <a name="version-082"></a>Versión 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuevo

* Las cuentas de almacenamiento se agrupan por suscripciones; el almacenamiento de desarrollo y los recursos conectados mediante clave o SAS se muestran en el nodo (Local y Adjuntos).
* Cierre la sesión de las cuentas en el panel “Configuración de la cuenta de Azure”.
* Configurar tooenable de configuración de proxy y administrar inicio de sesión
* Cree y rompa concesiones de blobs.
* Abra contenedores de blobs, colas, tablas y archivos con un solo clic.

#### <a name="fixes"></a>Correcciones

* Problema corregido: Los mensajes de cola insertados con bibliotecas de Java o .NET no se descodifican correctamente desde Base64.
* Problema corregido: Las tablas de $metrics no se muestran en las cuentas de Blob Storage.
* Problema corregido: El nodo de tablas no funciona para el almacenamiento local (desarrollo).

#### <a name="known-issues"></a>Problemas conocidos

* Puede que la instalación en macOS requiera permisos elevados.

15/06/2016
### <a name="version-080"></a>Versión 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuevo

* Compatibilidad con recursos compartidos de archivos: visualización, carga, descarga, copia de archivos y directorios, URI de SAS (creación y conexión).
* Mejor experiencia del usuario para la conexión tooStorage con URI de SAS o claves de cuenta
* Exportación de resultados de consulta de tabla.
* Reordenación y personalización de columnas de tabla.
* Consulta de contenedores de blob $logs y tablas de $metrics para cuentas de almacenamiento con las métricas habilitadas.
* Comportamiento de importación y exportación mejorado. Ahora incluye el tipo de valor de propiedad.

#### <a name="fixes"></a>Correcciones

* Problema corregido: Al cargar o descargar blobs grandes, se puede producir una carga o descarga incompleta.
* Problema corregido: edición, la adición o la importación de una entidad con un valor de cadena numérica ("1") lo convertirá toodouble
* Problema corregido: Nodo de tabla de hello tooexpand no se puede en el entorno de desarrollo local Hola

#### <a name="known-issues"></a>Problemas conocidos

* Las tablas de $metrics no son visibles para cuentas de Blob Storage.
* Cola de mensajes agregado mediante programación no se muestren correctamente si los mensajes de saludo se codifican utilizando la codificación Base64

17/05/2016
### <a name="version-07201605090"></a>Versión 0.7.20160509.0

#### <a name="new"></a>Nuevo

* Mejor control de errores para bloqueos de la aplicación.

#### <a name="fixes"></a>Correcciones

* Se ha corregido un error en el que los mensajes de la barra de información a veces no se mostraban cuando se requerían credenciales de inicio de sesión.

#### <a name="known-issues"></a>Problemas conocidos

* Tablas: Agregar, editar, o importar una entidad que tiene una propiedad con un valor numérico de forma ambigua, como "1" o "1.0", y Hola toosend de intentos de usuario como un `Edm.String`, valor de hello volverá a través de API como un Edm.Double de cliente hello

31/03/2016

### <a name="version-07201603250"></a>Versión 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nuevo

* Compatibilidad con tablas: visualización, realización de consultas, exportación, importación y operaciones CRUD para entidades.
* Compatibilidad con colas: visualización, adición y eliminación de mensajes de la cola.
* Generación de URI de SAS para cuentas de almacenamiento.
* Cuentas de conexión tooStorage con URI de SAS
* Notificaciones de actualización para las actualizaciones futuras tooStorage Explorer
* Apariencia actualizada.

#### <a name="fixes"></a>Correcciones

* Mejoras de rendimiento y confiabilidad.

### <a name="known-issues-amp-mitigations"></a>Problemas conocidos y mitigaciones

* La descarga de archivos de blob grandes no funciona correctamente. Le recomendamos que use AzCopy mientras no se soluciona este problema. 
* Las credenciales de cuenta no pueden recuperar ni almacenado en memoria caché si la carpeta particular de hello no se encuentra o no puede escribirse en
* Si nos estamos agregar, editar o importar una entidad que tiene una propiedad con un valor numérico de forma ambigua, como "1" o "1.0", y trata de usuario de hello toosend como un `Edm.String`, valor de hello volverá a través de API como un Edm.Double de cliente hello
* Al importar archivos CSV con los registros de varias líneas, datos de hello pueden obtener reducidos o codificadas

03/02/2016

### <a name="version-07201601291"></a>Versión 0.7.20160129.1

#### <a name="fixes"></a>Correcciones

* Rendimiento general mejorado al cargar, descargar y copiar blobs.

14/01/2016

### <a name="version-07201601050"></a>Versión 0.7.20160105.0

#### <a name="new"></a>Nuevo

* Compatibilidad con Linux (tooOSX de características de paridad)
* Agregue contenedores de blobs con clave de Firmas de acceso compartido (SAS).
* Agregue cuentas de almacenamiento para Azure China.
* Agregue cuentas de almacenamiento con puntos de conexión personalizados.
* Abrir y ver los blobs de texto e imagen de contenido de Hola
* Vea y edite propiedades y metadatos de blob.

#### <a name="fixes"></a>Correcciones

* Se ha corregido: carga o descarga un gran número de blobs (500 +) a veces podrían Hola aplicación toohave una pantalla en blanco 
* Problema corregido: al establecer el nivel de acceso público de contenedor de blob, Hola nuevo valor no se actualiza hasta que se vuelva a establecer el foco de hello en el contenedor de Hola. Además, el cuadro de diálogo de hello siempre tiene como valor predeterminado demasiado "de acceso No público" y no Hola actual valor real.
* Mejor accesibilidad de teclado general y compatibilidad con IU.
* El historial de enlaces se ajusta cuando es demasiado largo con espacios en blanco.
* El cuadro de diálogo de SAS admite la validación de entradas.
* Almacenamiento local continúa toobe disponible incluso si las credenciales de usuario han caducado
* Cuando se elimina un contenedor de blobs abierto, se cierra el Explorador de blob Hola Hola derecha

#### <a name="known-issues"></a>Problemas conocidos

* Necesidades de instalación de Linux versión gcc había actualizado o ampliado – tooupgrade pasos son los siguientes: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

18/11/2015
### <a name="version-07201511160"></a>Versión 0.7.20151116.0

#### <a name="new"></a>Nuevo

* Versiones de Windows y macOS.
* Inicie sesión en tooview sus cuentas de almacenamiento: use la cuenta de organización, Microsoft Account, 2FA, etcetera.
* Almacenamiento de desarrollo local (use un emulador de almacenamiento, solo para Windows).
* Compatibilidad de Azure Resource Manager y recursos clásicos.
* Cree y elimine blobs, colas o tablas.
* Busque blobs, colas o tablas específicos.
* Explorar el contenido de Hola de contenedores de blob
* Vea y navegue por directorios.
* Cargue, descargue y elimine blobs y carpetas.
* Vea y edite propiedades y metadatos de blob.
* Genere claves SAS.
* Administre y cree directivas de acceso a almacenamiento (SAP).
* Busque blobs por prefijo.
* Arrastrar y colocar tooupload de archivos o descarga

#### <a name="known-issues"></a>Problemas conocidos

* Al establecer el nivel de acceso público de contenedor de blob, valor nuevo de hello no se actualiza hasta que se vuelva a establecer el foco de hello en el contenedor de Hola
* Cuando se abre el nivel de acceso público de hello diálogo tooset hello, siempre no muestra "acceso público" como hello, valor predeterminado y no Hola real actual
* No se puede cambiar el nombre de los blobs descargados.
* Entradas del registro de actividad en ocasiones quedar "bloqueado" en una en curso de estado cuando se produce un error y no se muestra el error de Hola
* A veces se bloquea o pone completamente en blanco al intentar tooupload o descarga un gran número de blobs
* A veces no se puede cancelar una operación de copia.
* Durante la creación de un contenedor (blob o cola o tabla), si un nombre no válido de entrada y continuar toocreate otra nueva en un tipo de contenedor diferentes no puede establecer foco en el nuevo tipo de Hola
* No se puede crear una carpeta nueva ni cambiarle el nombre.




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md