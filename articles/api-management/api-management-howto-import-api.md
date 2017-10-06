---
title: "aaaImport una API a la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimport una API y sus operaciones en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>¿Cómo tooimport Hola definición de una API con las operaciones de administración de API de Azure
Administración de API, se pueden crear nuevas API y operaciones de hello agregó manualmente o hello API puede importarse junto con operaciones de hello en un solo paso.

Las API y sus operaciones pueden importarse mediante Hola después de formatos.

* WADL
* Swagger

En esta guía se muestra cómo crear una API e importar sus operaciones en un solo paso. Para obtener información sobre cómo crear manualmente una API y las operaciones de adición, vea [cómo toocreate API] [ How toocreate APIs] y [cómo tooadd operaciones tooan API] [ How tooadd operations tooan API].

## <a name="import-api"></a>Importación de una API
Las API se crean y configuran en el portal para desarrolladores de Hola. tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.

![Portal del publicador][api-management-management-console]

Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **importar API**.

![Importar API][api-management-import-apis]

Hola **API de importación** ventana tiene tres pestañas correspondientes de la especificación de toohello tres formas tooprovide Hola API.

* **Desde el Portapapeles** permite toopaste especificación de hello API en el cuadro de texto designado Hola.
* **Desde archivo** permite archivo seleccione Hola de toobrowse tooand que contiene la especificación de hello API.
* **Desde URL** permite la especificación de toohello de dirección URL de toosupply Hola para hello API.

![Import API format][api-management-import-api-clipboard]

Después de proporcionar la especificación de API de hello, utilice los botones de radio de hello en formato de especificación de hello tooindicate derecho Hola. Hola siguientes formatos es compatibles.

* WADL
* Swagger

A continuación, especifique un **Sufijo de dirección URL API web**. Se trata de toohello anexado de dirección URL base para el servicio de administración de API. dirección URL base de Hello es común para todas las API que se hospedan en cada instancia de un servicio de administración de API. Administración de API distingue API mediante su sufijo y, por tanto, el sufijo de hello debe ser único para todas las API en una instancia de servicio de administración de API específica.

Una vez que se escriben todos los valores, haga clic en **guardar** hello y API de hello toocreate asociados operaciones. 

> [!NOTE]
> Para ver un tutorial de la importación de una API de calculadora básica en formato Swagger, consulte [Administración de su primera API en Administración de API de Azure](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Exportación de una API
En suma tooimporting nuevas API, puede exportar las definiciones de saludo de las API de portal para desarrolladores de Hola. toodo por lo tanto, haga clic en **API exportar** de hello **ficha Resumen** de su **API**.

![Export API][api-management-export-api]

Las API se pueden exportar con WADL o Swagger. Seleccione el formato deseado de hello, haga clic en **guardar**y elija la ubicación de hello en qué archivo de hello toosave.

![Export API format][api-management-export-api-format]

## <a name="next-steps"></a>Pasos siguientes
Una vez que se crea una API y operaciones de hello importadas, puede revisar y configurar cualquier configuración adicional, agregue Hola API tooa producto y publicarlo para que esté disponible para los desarrolladores. Para obtener más información, vea Hola siguiendo a las guías.

* [¿Cómo tooconfigure API de configuración][How tooconfigure API settings]
* [¿Cómo toocreate y publicación de productos][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
