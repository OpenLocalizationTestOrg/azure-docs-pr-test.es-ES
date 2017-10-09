---
title: "aaaMicrosoft Azure Storage Explorer 0.8.7 (versión preliminar) | Documentos de Microsoft"
description: "Notas de la versión del Explorador de Microsoft Azure Storage 0.8.7 (versión preliminar)"
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Explorador de Microsoft Azure Storage 0.8.7 (versión preliminar)
## <a name="overview"></a>Información general
Este artículo contiene notas de la versión de hello para la versión de vista previa de Azure Storage Explorer 0.8.7.

[Explorador de almacenamiento de Microsoft Azure (vista previa)](./vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux.

## <a name="azure-storage-explorer-087-preview"></a>Explorador de Azure Storage 0.8.7 (versión preliminar)
### <a name="download-azure-storage-explorer-087-preview"></a>Descarga del Explorador de Azure Storage 0.8.7 (versión preliminar)
- [Explorador de Azure Storage 0.8.7 - versión preliminar para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Explorador de Azure Storage 0.8.7 - versión preliminar para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Explorador de Azure Storage 0.8.7 - versión preliminar para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Nuevas actualizaciones
* Puede elegir cómo tooresolve conflictos al principio de Hola de una actualización, descargar o copiar sesión Hola **actividades** ventana.
* Mantenga el mouse sobre una ficha toosee Hola ruta de acceso completa del recurso de almacenamiento de Hola.
* Al hacer clic en una pestaña, sincroniza con su ubicación en el panel de navegación del lado izquierdo de Hola.

### <a name="fixes"></a>Correcciones
* Problema corregido: El Explorador de Storage es ahora una aplicación de confianza en macOS.
* Problema corregido: Ubuntu 14.04 se admite de nuevo.
* Problema corregido: En ocasiones hello agregar interfaz de usuario de cuenta parpadea al cargar las suscripciones.
* Problema corregido: En ocasiones, no todos los recursos de almacenamiento estaban incluidos en el panel de navegación del lado izquierdo de Hola.
* Problema corregido: panel de acciones de Hola a veces muestra acciones vacías.
* Problema corregido: tamaño de la ventana de sesión de hello cerró por última vez Hola ahora se conserva.
* Se ha corregido: Se pueden abrir varias pestañas para hello mismo recurso mediante el menú contextual de Hola.

### <a name="known-issues"></a>Problemas conocidos
* Acceso rápido solo funciona con elementos basados en la suscripción. En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.
* Puede tardar unos segundos toonavigate toohello recurso de destino, según la cantidad de recursos que tiene un acceso rápido.
* Tener más de tres grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores.
* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.
* Para hello primera vez con hello Explorador de almacenamiento en macOS, puede que vea varios mensajes piden cadenas de claves del usuario permiso tooaccess Hola. Se recomienda que seleccione **permitir siempre** para no volver a mostrar el mensaje de Hola

## <a name="previous-releases"></a>Versiones anteriores
### <a name="features"></a>Características
#### <a name="main-features"></a>Características principales
* Versiones de macOS, Linux y Windows
* Inicie sesión en tooview sus cuentas de almacenamiento agrupados por suscripción:
    * Use la cuenta de organización, cuenta Microsoft, 2FA, etc.
    * Configure y administre la configuración de proxy.
    * Quite cuentas cerrando la sesión.
* Conectar cuentas tooStorage mediante:
    * Nombre y clave de la cuenta
    * Puntos de conexión personalizados (incluido Azure China)
    * URI de SAS para cuentas de almacenamiento
* Compatibilidad de Azure Resource Manager y almacenamiento clásico
* Genere claves de SAS para blobs, contenedores de blobs, colas, tablas o recursos compartidos de archivos.
* Conectar contenedores tooblob, colas, tablas o recursos compartidos de archivos con la clave de firmas de acceso compartido (SAS)
* Administre directivas de acceso almacenadas para contenedores de blobs, colas, tablas o recursos compartidos de archivos.
* Almacenamiento de desarrollo local con el emulador de almacenamiento (solo Windows)
* Cree y elimine contenedores de blobs, colas o tablas.
* Vea contenedores de blobs $logs y tablas $metrics.
* Busque blobs, colas, tablas o recursos compartidos de archivos específicos.
* Cuentas de toostorage vínculos directos o contenedores, colas, tablas o archivo de recursos compartidos para compartir y acceder fácilmente a los recursos
* Cambie el nombre de contenedores de blobs, tablas y recursos compartidos de archivos.
* Capacidad toomanage y configurar las reglas de CORS
* Copie fácilmente las claves principal y secundaria para las cuentas de almacenamiento.
* Comprobaciones de MD5 de la integridad de datos y la coherencia al cargar y descargar
* Busque los contenedores de blobs, tablas, colas, recursos compartidos de archivos o las cuentas de almacenamiento desde el cuadro de búsqueda de Hola
* Puede ahora pin usa con mayor frecuencia servicios toohello acceso rápido para facilitar la navegación
* Ya puede abrir varios editores en diferentes pestañas. Un solo clic tooopen una pestaña temporal; Haga doble clic en tooopen una pestaña permanente. También puede hacer clic en hello pestaña temporal toomake una pestaña permanente
* Notables mejoras de rendimiento y estabilidad para cargas y descargas, especialmente para archivos de gran tamaño en máquinas rápidas
* Le estamos Introducción a la búsqueda mejorada con ámbito de Hola y el concepto de hello agregada de ámbito. Escriba nodo tooa de hello ruta de acceso a través del icono de hello al mantener el mouse, contextual -> "Búsqueda desde aquí", o manualmente tooscope ese nodo. Una vez que el ámbito, puede agregar un extremo de toohello del término de búsqueda de búsqueda de toodeep de ruta de acceso de Hola a partir de ese nodo
* Hemos agregado varios temas: claro (valor predeterminado), oscuro, negro en alto contraste y blanco en alto contraste.
* Vaya tooEdit -> temas toochange sus preferencias de temas
* En Linux, ahora es necesario utilizar un sistema operativo de 64 bits.
* ¡Hemos actualizado nuestro logotipo!
#### <a name="blobs"></a>Blobs
* Vea blobs y navegue por los directorios.
* Cargue, descargue, elimine y copie blobs y carpetas.
* Abrir y ver los blobs de texto e imagen de contenido de Hola
* Vea y edite propiedades y metadatos de blob.
* Busque blobs por prefijo.
* Cree e interrumpa concesiones de blobs y contenedores de blobs.
* Arrastrar y colocar tooupload de archivos
* Cambie el nombre de blobs y carpetas.
* Las carpetas vacías "virtuales" ya se pueden crear en contenedores de blobs.
* Puede modificar las propiedades del Blob y archivo Hola
#### <a name="tables"></a>Tablas
* Ver y consultar las entidades con ODATA o utilizar consultas complejas de toocreate de generador de consultas
* Agregue, edite y elimine entidades.
* Importe y exporte el contenido de tablas en formato CSV (incluidos los resultados de la consulta de exportación).
* Personalice el orden de las columnas.
* Consultas de toosave de capacidad
#### <a name="queues"></a>Colas
* Ojee los 32 mensajes más recientes.
* Agregue, quite de la cola y vea mensajes.
* Borre mensajes de la cola.
* Se hacía posible que se toodecide si desea tooencode y descodificar los mensajes en cola
#### <a name="file-shares"></a>Recursos compartidos de archivos
* Vea archivos y navegue por los directorios.
* Cargue, descargue, elimine y copie archivos y directorios.
* Vea las propiedades del archivo.
* Cambie el nombre archivos y directorios.

### <a name="bug-fixes"></a>Corrección de errores
* Problema corregido: Problemas de inmovilización de pantalla
* Problema corregido: Mayor seguridad

### <a name="known-issues"></a>Problemas conocidos
* Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado, las instalaciones de macOS pueden requerir permisos elevados.
* Puede mostrar el panel de configuración de la cuenta que necesita credenciales toofilter suscripciones a tooreenter
* Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas. Todas las otras propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.
* Pila de Azure no admite actualmente los archivos, por lo que intentar tooexpand hello **archivos** nodo produce un error
* Linux 14.04 instala la versión de gcc actualizada o ampliada. Hello siguientes pasos muestran cómo tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Versiones anteriores
#### <a name="october-2016-release-version-085"></a>Versión de octubre de 2016 (versión 0.8.5)
* [Descargar para Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Descargar para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Descargar para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
