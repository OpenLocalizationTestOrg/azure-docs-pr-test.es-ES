---
title: "aaaBest prácticas para servicio de aplicaciones de Azure"
description: "Información acerca de los procedimientos recomendados y la solución de problemas del Servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Procedimientos recomendados para el Servicio de aplicaciones de Azure
En este artículo se resumen los procedimientos recomendados para usar el [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Ubicación compartida
Al redactar una solución como una aplicación web y una base de datos de recursos de Azure se encuentran en los efectos de diferentes regiones Hola puede incluir siguiente de hello:

* Mayor latencia en la comunicación entre recursos
* Monetarios cargos para los datos salientes transferir entre regiones como se indicó en hello [Azure página de precios](https://azure.microsoft.com/pricing/details/data-transfers).

La colocación en hello misma región es más adecuado para crear una solución como una aplicación web de recursos de Azure y utiliza una cuenta de base de datos o almacenamiento toohold contenido o los datos. Cuando la creación de recursos debe asegurarse de que están en Hola misma región de Azure a menos que tenga específicos del negocio o diseña motivo para ellos no toobe. Puede mover una toohello de aplicación de servicio de aplicaciones misma región que la base de datos mediante el aprovechamiento de hello [servicio de aplicaciones de característica clonación](app-service-web-app-cloning-portal.md) actualmente disponibles para las aplicaciones de Plan de servicio de aplicaciones Premium.   

## <a name="memoryresources"></a>Cuando las aplicaciones consumen más memoria de lo esperado
Cuando observe una aplicación consume más memoria de lo esperado tal como se indica a través de supervisión o considere la posibilidad de un servicio de recomendaciones hello [característica de recuperación automática del servicio de aplicación](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Una de las opciones de hello para la característica de recuperación automática de hello está tardando acciones personalizadas en función de un umbral de memoria. Acciones abarcan espectro de Hola de tooinvestigation de notificaciones de correo electrónico a través de la mitigación de tooon puntual de volcado de memoria mediante el reciclado de procesos de trabajo de Hola. Recuperación automática puede configurarse a través del archivo web.config y a través de una interfaz de usuario descriptivo como se describe en esta entrada de blog para hello [extensión del sitio de soporte técnico de servicio de aplicación](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Cuando las aplicaciones consumen más CPU de lo esperado
Cuando se observe que una aplicación consume más CPU que se esperaba o experimenta repite picos de CPU como se indica a través de supervisión o recomendaciones de servicio considere la posibilidad de escalar verticalmente o escalar horizontalmente Hola plan de servicio de aplicaciones. Si la aplicación es el estado, el escalado es única opción hello, mientras que si la aplicación sin estado, escalado horizontal, tendrá más flexibilidad y mayor potencial de escala. 

Para obtener más información sobre las aplicaciones "con estado" y "sin estado", puede ver este vídeo: [Planning a Scalable End-to-End Multi-Tier Application on Microsoft Azure Web App](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid)(Planeamiento de una aplicación completa de niveles múltiples en una aplicación web de Microsoft Azure). Para obtener más información sobre las opciones de escalado y escalado automático del Servicio de aplicaciones, consulte [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md).  

## <a name="socketresources"></a>Cuando se agotan los recursos del socket
Una razón común para las conexiones TCP salientes agotando es Hola uso de bibliotecas de cliente que no son las conexiones TCP de implementada tooreuse o, en caso de hello de un protocolo de nivel superior como HTTP - no se aprovecha Keep-Alive. Revise la documentación de Hola para cada una de las bibliotecas de Hola Hola aplicaciones en su tooensure Plan de servicio de aplicaciones que se configuran o acceso en el código para una reutilización eficiente de las conexiones salientes al que hace referencia. También siga las instrucciones de documentación de biblioteca de hello para la creación correcta y versión o limpieza tooavoid pérdida de conexiones. Mientras tales investigaciones de bibliotecas de cliente están en el impacto de progreso puede mitigar mediante el escalado horizontal toomultiple instancias.  

## <a name="appbackup"></a>Cuando la copia de seguridad de la aplicación comienza a fallar
Hola dos razones más comunes, ¿por qué genera un error de aplicación copia de seguridad: base de datos no válidos y la configuración de almacenamiento no es válida. Estos errores se producen normalmente cuando hay cambios toostorage o recursos de base de datos o cambios de cómo tooaccess estos recursos (por ejemplo, credenciales se actualizó con la base de datos de hello seleccionada en la configuración de copia de seguridad de hello). Las copias de seguridad normalmente ejecutan según una programación y requieren acceso toostorage (de salida para hello copiado de seguridad de archivos) y las bases de datos (para copiar y leer toobe contenido incluido en la copia de seguridad de hello). Hola resultado de un error tooaccess cualquiera de estos recursos sería error de copia de seguridad coherente. 

Cuando se producen errores de copia de seguridad, revise más reciente toounderstand resultados sucede qué tipo de error. En caso de hello de errores de acceso de almacenamiento, revisar y actualizar la configuración de almacenamiento de hello utilizado en la configuración de copia de seguridad de Hola. En caso de hello de errores de acceso de la base de datos, revise y actualice las cadenas de conexiones como parte de la configuración de la aplicación; a continuación, continuar tooupdate su tooproperly de configuración de copia de seguridad incluyen bases de datos de hello necesario. Para obtener más información sobre la copia de seguridad de aplicaciones, consulte hello [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md) documentación.

## <a name="nodejs"></a>Cuando nuevas aplicaciones Node.js están implementado tooAzure servicio de aplicaciones
Azure configuración predeterminada de servicio de aplicaciones para las aplicaciones de Node.js es toobest previsto que se adapte a las necesidades de Hola de las aplicaciones más comunes. Si la configuración de la aplicación Node.js podría beneficiarse de optimización del rendimiento tooimprove personalizadas u optimizar el uso de recursos para los recursos de red, CPU o memoria, puede revisar nuestras prácticas recomendadas y pasos para solucionar problemas. Este artículo de documentación describen configuraciones de iisnode de Hola que puede necesitar tooconfigure para la aplicación Node.js, describe Hola diversos escenarios o los problemas que pueda sufrir su aplicación y se muestra cómo tooaddress estos problemas: [las prácticas recomendadas y Guía de solución de problemas para las aplicaciones del nodo en el servicio de aplicaciones de Azure](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

