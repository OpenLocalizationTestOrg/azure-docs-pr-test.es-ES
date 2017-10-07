---
title: "información general de caché Local del servicio de aplicación aaaAzure | Documentos de Microsoft"
description: "Este artículo describe cómo tooenable, cambio de tamaño y consulta Hola estado de la característica de caché Local del servicio de aplicación de Azure Hola"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Información general de caché local del Servicio de aplicaciones de Azure
El contenido de una aplicación web de Azure se almacena en Almacenamiento de Azure y surge de manera duradera como un recurso compartido de contenido. Este diseño es previsto toowork con una variedad de aplicaciones y tiene los siguientes atributos de hello:  

* contenido de Hola se comparte entre varias instancias de máquina virtual (VM) de la aplicación web de hello.
* contenido de Hello es duradera y puede modificarse mediante la ejecución de aplicaciones web.
* Archivos de registro y archivos de datos de diagnóstico están disponibles en hello mismas compartida carpeta de contenido.
* Publicar contenido nuevo directamente actualizaciones Hola carpeta de contenido. También puede inmediatamente Hola de vista mismo contenido a través del sitio Web SCM de Hola y Hola aplicación web en ejecución (normalmente algunas tecnologías, como ASP.NET iniciar un reinicio de la aplicación web en algún contenido más reciente del archivo cambios tooget Hola).

Si bien muchas aplicaciones web usan una o la totalidad de estas características, algunas aplicaciones web solo necesitan un almacén de contenido de solo lectura de gran rendimiento desde donde se puedan ejecutar con alta disponibilidad. Estas aplicaciones se pueden beneficiar de una instancia de VM de una caché local específica.

característica de caché Local del servicio de aplicación de Azure de Hello proporciona una vista de rol web de su contenido. Este contenido es una caché de escritura temporal del contenido de almacenamiento que se crea de forma asincrónica durante el inicio del sitio. Cuando caché Hola está listo, sitio de hello es toorun conmutada con contenido de hello en caché. Las aplicaciones Web que se ejecutan en memoria caché Local tienen Hola siguientes ventajas:

* Únicamente son toolatencies inmune a los que se producen cuando tienen acceso a contenido del almacenamiento de Azure.
* Son inmunes a toohello planeada actualizaciones o tiempos de inactividad no planificados y otras interrupciones con almacenamiento de Azure que se produzcan en servidores que sirven de recurso compartido de contenido de Hola.
* Tienen menos reinicios de aplicación debido a cambios de recurso compartido de toostorage.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>La memoria caché Local cambia el comportamiento del Hola de servicio de aplicaciones
* memoria caché local de Hello es una copia de carpetas de hello /site y /siteextensions de hello web app. Se crea en la instancia de máquina virtual local de hello en el inicio de la aplicación web. Hello tamaño de memoria caché local de Hola por la aplicación web está limitado too300 MB de forma predeterminada, pero puede aumentar la too2 GB.
* caché local de Hello es lectura / escritura. Sin embargo, las modificaciones se descartará cuando hello web aplicación mueve máquinas virtuales u obtiene reinicia. No debe usar almacenamiento en caché Local para las aplicaciones que almacenan datos de misión crítica en el almacén de contenido de Hola.
* Las aplicaciones Web pueden seguir toowrite los archivos de registro y datos de diagnóstico como lo hacen actualmente. Archivos de registro y datos, sin embargo, se almacenan localmente en hello máquina virtual. A continuación, se copian a través periódicamente toohello almacén de contenido compartido. almacén de contenido compartido de copia toohello Hello es un mejor esfuerzo: realiza una copia de escritura, podría perderse debido tooa bloqueo repentina de una instancia de la máquina virtual.
* Hay un cambio en la estructura de carpetas de Hola de hello LogFiles y carpetas de datos para las aplicaciones web que utilizan la memoria caché Local. Ahora hay subcarpetas en hello archivos de registro y datos de carpetas de almacenamiento que siguen el patrón de nomenclatura de Hola de "identificador" + marca de tiempo. Cada una de las subcarpetas de hello corresponde tooa de instancia de máquina virtual donde la aplicación web de hello está ejecutando o se ha ejecutado.  
* Publicar aplicación de cambios toohello web a través de cualquiera de los mecanismos de publicación de hello publicará toohello almacén de contenido compartido. Esto es así por diseño porque deseamos Hola publica contenido toobe duradero. toorefresh Hola memoria caché local de la aplicación web de hello, debe toobe reiniciar. ¿Esto parece como un paso excesivo? ciclo de vida de Hola a toomake sin problemas, vea la información de hello más adelante en este artículo.
* D:\Home señalará toohello de caché local. D:\Local seguirán señalando almacenamiento específico de toohello temporal de máquina virtual.
* vista de contenido de Hello predeterminada del sitio SCM Hola continuará toobe que de hello almacén de contenido compartido.

## <a name="enable-local-cache-in-app-service"></a>Habilitación de la caché local en Servicio de aplicaciones
Para configurar la caché local, se usa una combinación de configuraciones de aplicación reservadas. Puede configurar esta configuración de aplicaciones mediante el uso de hello siguientes métodos:

* [Portal de Azure](#Configure-Local-Cache-Portal)
* [Administrador de recursos de Azure](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Configurar la memoria caché Local mediante Hola portal de Azure
<a name="Configure-Local-Cache-Portal"></a>

Use esta configuración de aplicación para habilitar la caché local en función de la aplicación web: `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Configuración de aplicación del Portal de Azure: Caché local](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Configuración de la caché local mediante Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Cambiar configuración de tamaño de hello en memoria caché Local
De forma predeterminada, es el tamaño de la memoria caché local de hello **300 MB**. Esto incluye /site hello y /siteextensions carpetas que se copian de Hola contenido almacén, así como de cualquier localmente crea carpetas de datos y de registro. tooincrease este límite, use la configuración de la aplicación hello `WEBSITE_LOCAL_CACHE_SIZEINMB`. Puede aumentar el tamaño de hello una copia de seguridad demasiado**2 GB** (2000 MB) por cada aplicación web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Prácticas recomendadas para usar la caché local del Servicio de aplicaciones
Se recomienda usar caché Local junto con hello [entornos de ensayo](../app-service-web/web-sites-staged-publishing.md) característica.

* Agregar hello *rápidas* configuración de la aplicación `WEBSITE_LOCAL_CACHE_OPTION` con el valor de hello `Always` tooyour **producción** ranura. Si usa `WEBSITE_LOCAL_CACHE_SIZEINMB`, también se agrega como una zona de producción de tooyour de configuración rápida.
* Crear un **ensayo** ranura y publicar tooyour zona de ensayo. Normalmente no establece Hola ranura toouse caché Local tooenable un ciclo de vida de compilación-implementación-prueba sin problemas de ensayo si se obtienen ventajas de hello de la memoria caché Local para ranura de producción de hello de almacenamiento provisional.
* Pruebe el sitio en la ranura de ensayo.  
* Una vez que esté preparado, emita una [operación de intercambio](../app-service-web/web-sites-staged-publishing.md#Swap) entre las ranuras de ensayo y producción.  
* Configuración rápida incluye nombre y la ranura de tooa rápidas. Por tanto, cuando la zona de ensayo de hello obtiene pasado a producción, heredará configuración de la aplicación hello memoria caché Local. Hola recién intercambia producción ranura se ejecutará en memoria caché local de hello después de unos minutos y se activa como parte de la preparación de la ranura después del intercambio. Por lo que una vez completada intercambio de ranura de hello, la ranura de producción se ejecutará en memoria caché local de Hola.

## <a name="frequently-asked-questions-faq"></a>Preguntas más frecuentes
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>¿Cómo se puede saber si la memoria caché Local aplica toomy web aplicación?
Si la aplicación web necesita un almacén de contenido de alto rendimiento, confiable, no utiliza datos críticos de toowrite de almacén de contenido de hello en tiempo de ejecución y es inferior a 2 GB en tamaño total, respuesta de hello, es "Sí". tamaño total de Hola de tooget de las carpetas /site y /siteextensions, puede usar extensión de sitio de Hola "Uso del disco de las aplicaciones de Azure Web".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>¿Cómo puedo saber si mi sitio ha cambiado toousing caché Local?
Si usa características de la memoria caché Local de hello con entornos de almacenamiento provisional, operación de intercambio de hello no se completará hasta que la memoria caché Local está activa. toocheck si el sitio se ejecuta en la memoria caché Local, puede comprobar la variable de entorno de proceso de trabajo hello `WEBSITE_LOCALCACHE_READY`. Utilice instrucciones de hello en hello [variable de entorno del proceso de trabajo](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) página tooaccess Hola variable de entorno de proceso de trabajo en varias instancias.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Acaba de publicar nuevos cambios, pero no parece que mi aplicación web toohave ellos. ¿Por qué?
Si la aplicación web usa la memoria caché Local, a continuación, deberá toorestart los cambios más recientes de sitio tooget Hola. ¿No desea el sitio de producción de toopublish cambios tooa? Consulte Opciones de la ranura de hello en sección de prácticas recomendada anterior Hola.

### <a name="where-are-my-logs"></a>¿Dónde están mis registros?
Con la caché local, los registros y las carpetas de datos tienen un aspecto diferente. Sin embargo, hello estructura de su subcarpetas permanece Hola igual, salvo que las subcarpetas de Hola se anida en una subcarpeta con hello formato "identificador único de VM" + marca de tiempo.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Tengo habilitada la caché local, pero mi aplicación web todavía se reinicia. ¿Por qué ocurre esto? Pensé que la memoria caché local que iba a ayudar con los reinicios de aplicación frecuentes.
La caché local ayuda a evitar que la aplicación web relacionada con el almacenamiento se reinicie. Sin embargo, la aplicación web todavía podría realizarse reinicios durante las actualizaciones de infraestructura planeada de hello VM. Hello general reinicios de aplicación que experimenta con caché Local habilitada deben ser menos.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>¿Caché Local excluya las directorios desde los que se va a copian toohello con mayor rapidez la unidad local?
Como parte del paso de Hola que copia el contenido del almacenamiento de Hola se excluirá cualquier carpeta que se denomina repositorio. Esto ayuda a con escenarios donde el contenido del sitio puede contener un repositorio de control de código fuente que no puedan ser necesarios en la operación de tooday de día de la aplicación web de hello. 
