---
title: aaaReference para navegar por hello portal de Azure
description: "Obtenga información acerca de hello experiencias de usuario diferentes para la aplicación de servicio Web entre el portal de administración de Hola y Hola Portal de Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Referencia para navegar por hello portal de Azure
Sitios web de Azure ahora se llama [Aplicaciones web del Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714). Estamos actualizando todos nuestro tooreflect documentación este nombre cambio y tooprovide las instrucciones de hello Portal de Azure. Hasta que se realiza este proceso, puede usar este documento como guía para trabajar con aplicaciones Web de hello portal de Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>Hola futuro de hello Portal clásico de Azure
Mientras que observará Hola cambios en el Portal de Azure clásico Hola de marca, ese portal está en proceso de Hola de que será reemplazada por hello Portal de Azure. Tal y como está desapareciendo portal clásico de hello, foco de hello para el nuevo desarrollo está cambiando toohello Portal de Azure. Todas las próximas características nuevas para las aplicaciones Web aparecerá en hello Portal de Azure. Empezar a usar hello Azure Portal tootake aprovechar Hola mayor que las aplicaciones Web tienen toooffer y más reciente.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Diferencias de diseño entre Hola Portal clásico de Azure y el Portal de Azure
En el portal clásico de hello, todos hello Azure services se muestran en hello del lado izquierdo. La navegación en el portal clásico de hello sigue una estructura de árbol, donde inicio del servicio de Hola y navegue a cada elemento. Esta estructura funciona bien para administrar componentes independientes. Si embargo, las aplicaciones integradas en Azure constituyen una colección de servicios interconectados y la estructura de árbol no es la ideal para trabajar con este tipo de colecciones. 

Hola portal de Azure hace fácil toobuild aplicaciones-to-end con componentes de varios servicios. portal de Hola se organiza como *viajes*. A *viaje* es una serie de *hojas*, que son contenedores de hello diferentes componentes. Por ejemplo, establecer el escalado automático para una aplicación web es un *viaje* que toma varias hojas de tal y como se muestra en el siguiente ejemplo de Hola: Hola **sitio web** hoja (que título de hoja no se ha recibido toouse actualizada Hola terminología nueva), hello **configuración** hello y hoja **escalar horizontalmente** hoja. En el ejemplo de Hola, escalado automático se va a configurar toodepend en el uso de CPU, por lo que es también un **porcentaje de CPU** hoja. Hola componentes dentro de hello *hojas* se denominan *elementos*, que el aspecto iconos. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Ejemplo de navegación: crear una aplicación web
La creación de aplicaciones web sigue siendo muy fácil. Hola siguiente imagen muestra hello clásico hello y portal portal side-by-side toodemonstrate que no ha cambiado mucho en número de Hola de pasos necesarios tooget una aplicación web de seguridad y en ejecución. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

En el portal de hello puede elegir entre tipos más comunes de Hola de las aplicaciones web, incluidas las aplicaciones de la Galería populares como WordPress. Para obtener una lista completa de las aplicaciones disponibles, visite hello [Azure Marketplace].

Cuando se crea una aplicación web, especificar la dirección URL, el plan de servicio de aplicaciones y ubicación en el portal de hello igual que lo haría en el portal clásico de Hola. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Además, la opción Hola portal le permite definir otras opciones de configuración comunes. Por ejemplo, [grupos de recursos](../azure-resource-manager/resource-group-overview.md) hacerla toosee simple y administrar recursos relacionados con Azure. 

## <a name="navigation-example-settings-and-features"></a>Ejemplo de navegación: configuración y características
Todos los valores de Hola y características ahora se agrupan lógicamente en una sola hoja, desde la que puede navegar.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Por ejemplo, puede crear dominios personalizados haciendo clic en **los dominios personalizados y SSL** en hello **configuración** hoja.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset una alerta de supervisión, haga clic en **solicitudes y errores** y, a continuación, **Agregar alerta**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Diagnósticos de tooenable, haga clic en **registros de diagnóstico** en hello **configuración** hoja.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Haga clic en configuración de la aplicación de tooconfigure **configuración de la aplicación** en hello **configuración** hoja. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Que no sea el nombre de la marca de hello, se han cambiado de nombre o agrupan de forma diferente algunas cosas en el portal de Hola toomake se toofind más fácil de ellos. Por ejemplo, a continuación se muestra una captura de pantalla de página correspondiente de hello para la configuración de la aplicación (**configurar**) en el portal clásico de Hola.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Más recursos
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

