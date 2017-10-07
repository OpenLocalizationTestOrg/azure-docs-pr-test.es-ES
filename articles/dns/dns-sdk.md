---
title: las zonas DNS de aaaCreate y conjuntos de registros de DNS de Azure utilizando Hola .NET SDK | Documentos de Microsoft
description: "¿Cómo toocreate zonas DNS y un registro establece en DNS de Azure mediante Hola .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Crear las zonas DNS y los conjuntos de registros mediante Hola SDK para .NET

Puede automatizar operaciones toocreate, eliminación o actualización de zonas de DNS, conjuntos de registros y los registros mediante DNS SDK con la biblioteca de administración de DNS. NET. Un proyecto completo de Visual Studio se encuentra disponible [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).

## <a name="create-a-service-principal-account"></a>Creación de una cuenta de entidad de servicio

Normalmente, se concede recursos tooAzure de acceso mediante programación a través de una cuenta dedicada en lugar de sus propias credenciales de usuario. Estas cuentas dedicadas se denominan cuentas de 'entidad de servicio'. proyecto de ejemplo de Hola toouse Azure SDK de DNS, primero necesita una cuenta de entidad de servicio toocreate y asignar los permisos correctos de Hola.

1. Siga [estas instrucciones](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate una cuenta de entidad de servicio (proyecto de ejemplo de SDK de DNS de Azure de hello supone autenticación basada en contraseña).
2. Cree un grupo de recursos ([aquí se explica cómo](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Use RBAC de Azure toogrant Hola servicio cuenta de entidad 'Colaborador de zona DNS' permisos toohello grupo de recursos ([mostramos cómo](../active-directory/role-based-access-control-configure.md).)
4. Si utiliza el proyecto de ejemplo de SDK de DNS de Azure de hello, edite hello 'program.cs' como se indica a continuación:

   * Insertar valores correctos de Hola hello tenantId, clientId (también conocido como Id. de cuenta), secreto (contraseña de cuenta de entidad de servicio) y Id. de suscripción como se utiliza en el paso 1.
   * Escriba el nombre del grupo de recursos de hello elegido en el paso 2.
   * Escriba un nombre de zona DNS de su elección.

## <a name="nuget-packages-and-namespace-declarations"></a>Paquetes NuGet y declaraciones de espacio de nombres

toouse Hola DNS de Azure .NET SDK, deberá hello tooinstall **biblioteca de administración de DNS de Azure** paquete de NuGet y otro necesario paquetes de Azure.

1. En **Visual Studio**, abra un proyecto o cree uno nuevo.
2. Vaya demasiado**herramientas**  **>**  **Administrador de paquetes de NuGet**  **>**  **administrar paquetes de NuGet para Solución...** .
3. Haga clic en **examinar**, habilitar hello **versión preliminar de inclusión** casilla de verificación y el tipo de **Microsoft.Azure.Management.Dns** en el cuadro de búsqueda de Hola.
4. Seleccione el paquete de Hola y haga clic en **instalar** tooadd, proyecto de Visual Studio tooyour.
5. Repetir proceso Hola anteriormente tooalso instalación Hola siguientes paquetes: **Microsoft.Rest.ClientRuntime.Azure.Authentication** y **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Incorporación de declaraciones de espacio de nombres

Agregar Hola siguientes declaraciones de espacio de nombres

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Inicializar el cliente de administración de DNS de Hola

Hola *DnsManagementClient* contiene métodos de Hola y propiedades necesarios para administrar zonas DNS y los conjuntos de registros.  Hola código siguiente registra en la cuenta de entidad de servicio toohello y crea un objeto DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Creación o actualización de una zona DNS

toocreate una zona DNS, en primer lugar "de zona" se crea un objeto los parámetros de zona DNS de toocontain Hola. Dado que las zonas DNS no son región específica tooa vinculado, ubicación de Hola se establece too'global'. En este ejemplo, un [Azure Resource Manager 'etiqueta'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) también se agrega la zona toohello.

tooactually crear o actualizar la zona de DNS de Azure, objeto de la zona de Hola que contiene los parámetros de la zona de Hola Hola se pasa toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.

> [!NOTE]
> DnsManagementClient admite tres modos de funcionamiento: sincrónica ('CreateOrUpdate'), asincrónica ('CreateOrUpdateAsync'), o asincrónico con la respuesta de acceso toohello HTTP ('CreateOrUpdateWithHttpMessagesAsync').  Puede elegir cualquiera de estos modos, dependiendo de sus necesidades de aplicación.

DNS de Azure admite la simultaneidad optimista denominada [Etags](dns-getstarted-create-dnszone.md). En este ejemplo, especifica "*" para el encabezado de hello 'If-None-Match' indica toocreate DNS de Azure una zona DNS si no existe.  se produce un error en la llamada de Hello si ya existe una zona con el nombre especificado de Hola Hola dado el grupo de recursos.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>Creación de registros y conjuntos de registros de DNS

Los registros DNS se administran como un conjunto de registros. Un conjunto de registros es un conjunto de registros con hello mismo nombre y grabar tipo dentro de una zona.  nombre de conjunto de registros de Hello es el nombre de la zona de toohello relativa, no Hola nombre DNS completo.

toocreate o actualización de un conjunto de registros, se crea un objeto de parámetros de "Conjunto de registros" y se pasan demasiado*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Como con las zonas DNS, hay tres modos de operación: sincrónica ('CreateOrUpdate'), asincrónica ('CreateOrUpdateAsync'), o asincrónico con la respuesta de acceso toohello HTTP ('CreateOrUpdateWithHttpMessagesAsync').

Al igual que con las zonas DNS, las operaciones en los conjuntos de registros incluyen compatibilidad con la simultaneidad optimista.  En este ejemplo, puesto que se especifica 'If-Match' ni 'If-None-Match', conjunto de registros de hello siempre se crea.  Esta llamada sobrescribe cualquier registro existente establecido con hello mismo nombre y registre el tipo de esta zona DNS.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>Obtención de zonas y conjuntos de registros

Hola *DnsManagementClient.Zones.Get* y *DnsManagementClient.RecordSets.Get* métodos recuperan zonas individuales y conjuntos de registros, respectivamente. Conjuntos de registros se identifican por su tipo, el nombre y el grupo de recursos y la zona de hello existen en. Las zonas se identifican por su grupo de recursos de hello y el nombre que se encuentran en.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Actualización de un conjunto de registros existente

conjunto de tooupdate un registro DNS existente, recuperar primero el conjunto de registros de hello, a continuación, actualizar registro de hello el contenido del conjunto, a continuación, envíe el cambio de Hola.  En este ejemplo, especificamos Hola "Etag" de hello recupera el conjunto de registros de parámetro de 'If-Match' hello. se produce un error en la llamada de Hello si una operación simultánea modificó Hola conjunto de registros de hello mientras tanto.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Enumeración de zonas y conjuntos de registros

zonas de toolist, usar hello *DnsManagementClient.Zones.List...*  utilizan métodos, que admiten enumerar a todas las zonas de un determinado grupo de recursos o todas las zonas de conjuntos de registros de una toolist determinada suscripción de Azure (a través de grupos de recursos.), *DnsManagementClient.RecordSets.List...*  métodos, que son compatibles con enumerar todos los conjuntos de registros en una zona determinada o solo los conjuntos de registros de un tipo específico.

Al mostrar zonas y conjuntos de registros, tenga en cuenta que los resultados pueden estar paginados.  Hola siguiente ejemplo se muestra cómo tooiterate a través de páginas de Hola de resultados. (Un tamaño de página artificialmente pequeño de '2' es tooforce usado paginación; en la práctica este parámetro, se debe omitir y Hola tamaño de página predeterminado utilizado).

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>Pasos siguientes

Descargar hello [proyecto de ejemplo de SDK de .NET de DNS de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que incluyen más ejemplos de cómo toouse Hola SDK de .NET de DNS de Azure, incluidos ejemplos para otros tipos de registro de DNS.
