---
title: "metadatos de API del servicio de aplicaciones de aaaApp para la generación de código y de detección de API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las aplicaciones de API de servicio de aplicaciones de Azure usar Swagger toofacilitate API de detección y código de generación de metadatos."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Metadatos de aplicaciones de API del Servicio de aplicaciones para la detección de API y la generación de código
La compatibilidad con los metadatos de la API de [Swagger 2.0](http://swagger.io/) está integrada en las aplicaciones de API del Servicio de aplicaciones. No tienes toouse Swagger, pero si lo use, puede aprovechar las ventajas de las características de aplicaciones de API que facilitan la detección y el consumo.   

## <a name="swagger-endpoint"></a>Punto de conexión de Swagger
Puede especificar un punto de conexión que proporciona metadatos de Swagger 2.0 JSON para una aplicación de API en una propiedad de la aplicación de API de hello. Hola extremo puede ser relativa toohello dirección URL base de la aplicación de API de Hola o una dirección URL absoluta. Las direcciones URL absolutas pueden apuntar fuera de la aplicación de API de hello. 

Muchos clientes de nivel inferiores (por ejemplo, generación de código de Visual Studio y PowerApps "Agregar API" flujo), dirección URL de hello debe ser accesible públicamente (que no esté protegido por el usuario o la autenticación de servicio). Esto significa que si utiliza la autenticación de servicio de aplicaciones y desea definición de la API tooexpose Hola desde dentro de su propia aplicación, necesita toouse opción de autenticación que permite el tráfico anónimo tooreach su API. Para más información, consulte [Autenticación y autorización para Aplicaciones de API en el Servicio de aplicaciones](app-service-api-authentication.md).

### <a name="portal-blade"></a>Hoja del portal
Hola [portal de Azure](https://portal.azure.com/) Hola de punto de conexión de dirección URL puede ser vista y cambiar en hello **definición de la API** hoja.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Propiedad del Administrador de recursos de Azure
También puede configurar dirección URL de la definición de hello API para una aplicación de API mediante [Resource Explorer](https://resources.azure.com/) o [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) en herramientas de línea de comandos como [Azure PowerShell](/powershell/azureps-cmdlets-docs)hello y [CLI de Azure](../cli-install-nodejs.md). 

En **Resource Explorer**, vaya demasiado**suscripciones > {su suscripción} > resourceGroups > {el grupo de recursos} > Proveedores > Microsoft.Web > sitios > {su sitio} > Configuración > web**, y verá hello `apiDefinition` propiedad:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Para obtener un ejemplo de una plantilla de Azure Resource Manager que establece hello `apiDefinition` propiedad, abra hello [azuredeploy.json archivo en la aplicación de ejemplo de lista de tareas pendientes de hello](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Busque la sección de Hola de plantilla de hello similar al ejemplo de Hola JSON mostrado anteriormente.

### <a name="default-value"></a>Valor predeterminado
Cuando se usa Visual Studio toocreate una aplicación de API, el punto de conexión de hello API definición se establece automáticamente toohello dirección URL base de aplicación de API de hello más `/swagger/docs/v1`. Se trata de dirección URL predeterminada de Hola que hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) paquete NuGet utiliza metadatos de Swagger tooserve generada dinámicamente para un proyecto de ASP.NET Web API. 

## <a name="code-generation"></a>Generación de código
Una de las ventajas de saludo de la integración de Swagger en aplicaciones de API de Azure es la generación automática de código. Clases de cliente generado resultará más fácil código toowrite que llama a una aplicación de API.

Puede generar código de cliente para una aplicación de API con Visual Studio o desde la línea de comandos de Hola. Para obtener información acerca de cómo las clases cliente toogenerate en Visual Studio para un proyecto de ASP.NET Web API, consulte [empezar a trabajar con aplicaciones de API y ASP.NET](app-service-api-dotnet-get-started.md#codegen). Para obtener información acerca de cómo toodo del comando hello línea para todos los idiomas admitidos, vea el archivo Léame de Hola de hello [Azure/autorest](https://github.com/azure/autorest) repositorio en GitHub.com.

## <a name="next-steps"></a>Pasos siguientes
Para obtener un tutorial detallado que le guíe en el proceso de creación, implementación y consumo de una aplicación de API, consulte [Introducción a Aplicaciones de API y ASP.NET en el Servicio de aplicaciones de Azure](app-service-api-dotnet-get-started.md).

Si usa administración de API de Azure con aplicaciones de API, puede usar la API tooimport de metadatos de Swagger en la API de administración. Para obtener más información, consulte [cómo tooimport Hola definición de una API con las operaciones de administración de API de Azure](../api-management/api-management-howto-import-api.md). 

