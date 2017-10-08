---
title: "recuperación ante desastres de aaaImplement mediante una copia de seguridad y restauración en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse copias de seguridad y restaura tooperform de recuperación ante desastres en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>¿Cómo tooimplement ante desastres recuperación mediante copia de seguridad de servicio y restaurar en la administración de API de Azure
Mediante la elección de toopublish y administrar las API a través de administración de API de Azure se sacar partido de las muchas capacidades de tolerancia y la infraestructura del error que, de lo contrario tendría toodesign, implementar y administrar. Hola plataforma Windows Azure, mitiga una gran parte de los posibles errores en una fracción del costo de Hola.

toorecover de problemas de disponibilidad que afectan a Hola región donde reside el servicio de administración de API hospedadas debe ser tooreconstitute preparado su servicio en una región diferente en cualquier momento. Según los objetivos de disponibilidad y el objetivo de tiempo de recuperación podría desea tooreserve un servicio de copia de seguridad en una o varias regiones e intente toomaintain su configuración y contenido sincronizado con el servicio activo de Hola. copia de seguridad de servicio de Hola y la característica de restauración proporciona Hola bloques de creación necesarios para implementar la estrategia de recuperación ante desastres.

Esta guía le mostrará cómo tooauthenticate Azure Resource Manager solicita y cómo toobackup y restaurar las instancias de servicio de administración de API.

> [!NOTE]
> proceso de Hola para realizar copias de seguridad y restauración de una instancia de servicio de administración de API para la recuperación ante desastres puede utilizarse también para la replicación de instancias de servicio de administración de API para escenarios, como el almacenamiento provisional.
>
> Tenga en cuenta que cada copia de seguridad expira después de 30 días. Si intentas toorestore una copia de seguridad después de que ha expirado el período de expiración de 30 días de hello, se producirá un error de restauración de hello con un `Cannot restore: backup expired` mensaje.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Solicitudes de autenticación del Administrador de recursos de Azure
> [!IMPORTANT]
> Hello API de REST para copia de seguridad y restauración usa Azure Resource Manager y tiene un mecanismo de autenticación distinto de hello las API de REST para administrar las entidades de la administración de API. pasos de Hello en esta sección describe cómo solicita tooauthenticate Azure Resource Manager. Par obtener más información, consulte [Solicitudes de autenticación del Administrador de recursos de Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Todas las tareas de Hola que realice en los recursos con hello Azure Resource Manager deben autenticarse con Azure Active Directory con hello pasos.

* Agregar a un inquilino de Azure Active Directory de toohello de aplicación.
* Establecer permisos para la aplicación hello que agregó.
* Obtener token de Hola para autenticar las solicitudes tooAzure el Administrador de recursos.

Hola primer paso es toocreate una aplicación de Azure Active Directory. Inicie sesión en hello [Portal clásico de Azure](http://manage.windowsazure.com/) usando suscripción Hola que contiene el servicio de administración de API de instancia y navegue toohello **aplicaciones** ficha para su Azure Active Directory de manera predeterminada.

> [!NOTE]
> Si directorio predeterminado de hello Azure Active Directory no es visible tooyour cuenta, Administrador de contacto Hola de Hola Hola de toogrant de suscripción de Azure requiere una cuenta con permisos tooyour.

![Creación de una aplicación de Azure Active Directory][api-management-add-aad-application]

Haga clic en **Agregar**, **Agregar una aplicación que mi organización está desarrollando** y elija **Aplicación de cliente nativo**. Escriba un nombre descriptivo y haga clic en la flecha siguiente Hola. Escriba una dirección URL de marcador de posición como `http://resources` para hello **URI de redireccionamiento**, tal y como es un campo obligatorio, pero no se usa el valor de hello más tarde. Haga clic en la aplicación de hello casilla toosave Hola.

Una vez que se guarda la aplicación hello, haga clic en **configurar**, desplácese hacia abajo toohello **permisos tooother aplicaciones** sección y haga clic en **Agregar aplicación**.

![Adición de permisos][api-management-aad-permissions-add]

Seleccione **Windows** **API de administración de servicios de Azure** y haga clic en la aplicación de hello casilla tooadd Hola.

![Adición de permisos][api-management-aad-permissions]

Haga clic en **permisos delegados** lateral Hola recién agregado **Windows** **API de administración de servicios de Azure** aplicación, casilla Hola para **acceso de Azure Administración de servicios (versión preliminar)**y haga clic en **guardar**.

![Adición de permisos][api-management-aad-delegated-permissions]

Tooinvoking anterior hello las API que generan Hola copia de seguridad y restaurarlo, es necesario tooget un token. Hello en el ejemplo siguiente se usa hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token de Hola de tooretrieve de paquete de nuget.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Reemplace `{tentand id}`, `{application id}`, y `{redirect uri}` Hola siguiendo las instrucciones de uso.

Reemplace `{tenant id}` con el identificador de inquilino de Hola de hello aplicación de Azure Active Directory que acaba de crear. Puede tener acceso a identificador hello haciendo clic en **ver extremos**.

![Puntos de conexión][api-management-aad-default-directory]

![Puntos de conexión][api-management-endpoint]

Reemplace `{application id}` y `{redirect uri}` con hello **Id. de cliente** y Hola dirección URL de hello **URI de redireccionamiento** sección de la aplicación de Azure Active Directory **configurar**  ficha.

![Recursos][api-management-aad-resources]

Una vez que se especifican valores de hello, ejemplo de código de hello debe devolver un token toohello similar siguiente ejemplo.

![SWT][api-management-arm-token]

Antes de llamar a Hola copia de seguridad y restaurar las operaciones que se describe en las secciones siguientes de hello, establezca el encabezado de solicitud de autorización de hello para la llamada de REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"></a>Crear una copia de seguridad del servicio API Management
tooback seguridad un Hola de problema de servicio de administración de API después de la solicitud HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

donde:

* `subscriptionId`-Id. de suscripción de Hola que contiene el servicio de administración de API de hello estás intentando toobackup
* `resourceGroupName`-una cadena con formato hello 'Api - Default: {región del servicio}' donde `service-region` identifica Hola región de Azure donde se hospeda el servicio de administración de API que estamos toobackup Hola, p. ej.`North-Central-US`
* `serviceName`-nombre de Hola de hello servicio de administración de API que se está realizando una copia de seguridad especificado en tiempo de presentación de su creación
* `api-version`: reemplazar por `2014-02-14`

En el cuerpo de saludo de solicitud de hello, especifique el nombre de cuenta de almacenamiento de Azure de destino de hello, clave de acceso, el nombre del contenedor de blob y nombre de la copia de seguridad:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Establecer valor de Hola de hello `Content-Type` encabezado de solicitud demasiado`application/json`.

Copia de seguridad es una operación larga que puede tardar varios toocomplete minutos.  Si se completó la solicitud de Hola y se inició el proceso de copia de seguridad de hello recibirá un `202 Accepted` código de estado de respuesta con un `Location` encabezado.  Asegúrese de 'GET'. las solicitudes URL toohello Hola `Location` toofind encabezado estado Hola de operación de Hola. Mientras se realiza la copia de seguridad de hello continuará tooreceive un código de estado '202 aceptado'. El código de respuesta `200 OK` indicará la finalización correcta de la operación de copia de seguridad de Hola.

Tenga en cuenta las siguientes restricciones cuando se realiza una solicitud de copia de seguridad de Hola.

* **Contenedor** especificado en el cuerpo de la solicitud de hello **debe existir**.
* Mientras se crea la copia de seguridad, **no realice ninguna operación de administración del servicio** (por ejemplo, una actualización o degradación de SKU o un cambio de nombre de dominio).
* Restauración de un **copia de seguridad se garantiza que sólo durante 30 días** desde el momento de Hola de su creación.
* **Datos de uso** utiliza para crear informes de análisis **no se incluye** en copia de seguridad de Hola. Use [API de REST de administración de API de Azure] [ Azure API Management REST API] tooperiodically recuperar informes de análisis por motivos de seguridad.
* frecuencia de Hello con el que realizar copias de seguridad de servicio afectará a su objetivo de punto de recuperación. toominimize, se recomienda implementar copias de seguridad periódicas, así como realizar copias de seguridad a petición después de realizar importante cambia tooyour servicio de administración de API.
* **Cambios** configuración del servicio realizadas toohello (p. ej., API, las directivas de apariencia portal para desarrolladores) durante la operación de copia de seguridad está en curso **no pueden incluirse en la copia de seguridad de hello y, por tanto, se perderán**.

## <a name="step2"></a>Restaurar el servicio Administración de API
toorestore un servicio de administración de API desde una copia de seguridad creado anteriormente que Hola después de la solicitud HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

donde:

* `subscriptionId`-Id. de suscripción de Hola que contiene el servicio de administración de API de hello va a restaurar una copia de seguridad en
* `resourceGroupName`-una cadena con formato hello 'Api - Default: {región del servicio}' donde `service-region` identifica Hola región de Azure donde se hospeda Hola va a restaurar una copia de seguridad en el servicio de administración de API, p. ej.`North-Central-US`
* `serviceName`-nombre de Hola de hello administración de API se restauran en el servicio especificado en tiempo de presentación de su creación
* `api-version`: reemplazar por `2014-02-14`

En el cuerpo de saludo de solicitud de hello, especificar ubicación del archivo de copia de seguridad de hello, es decir, nombre de la cuenta de almacenamiento de Azure, la clave de acceso, el nombre del contenedor de blob y nombre de copia de seguridad:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Establecer valor de Hola de hello `Content-Type` encabezado de solicitud demasiado`application/json`.

Restauración es una operación larga que puede llevar hasta too30 o toocomplete de minutos más.  Si se completó la solicitud de Hola y se inició el proceso de restauración de hello recibirá un `202 Accepted` código de estado de respuesta con un `Location` encabezado.  Asegúrese de 'GET'. las solicitudes URL toohello Hola `Location` toofind encabezado estado Hola de operación de Hola. Mientras se realiza la restauración de hello continuará tooreceive código de estado de "202 Accepted". El código de respuesta `200 OK` indicará la finalización correcta de la operación de restauración de Hola.

> [!IMPORTANT]
> **Hola SKU** del servicio de Hola se restauran en **debe coincidir con** Hola SKU de hello copia de seguridad que se están restaurando el servicio.
>
> **Cambios** toohello realizadas servicio configuración (por ejemplo, API, directivas, apariencia portal para desarrolladores) durante la operación de restauración está en curso **podría sobrescribirse**.
>
>

## <a name="next-steps"></a>Pasos siguientes
Extraer del repositorio Hola después de blogs de Microsoft para los dos tutoriales diferentes del proceso de copia de seguridad/restauración Hola.

* [Replicate Azure API Management Accounts (Réplica de cuentas de Administración de API de Azure)](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Gracias tooGisela para su artículo de toothis contribución.
* [Azure API Management: Backing Up and Restoring Configuration (Administración de API de Azure: copia de seguridad y restauración de la configuración)](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * enfoque de Hello detallado por Stuart no coincide con la orientación oficial de Hola pero es muy interesante.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
