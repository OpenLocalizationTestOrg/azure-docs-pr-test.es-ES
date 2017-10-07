---
title: "aaaAzure registro de almacén de claves | Documentos de Microsoft"
description: "Use este tutorial toohelp empezar a trabajar con el almacén de claves de Azure registro."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Registro del Almacén de claves de Azure
Almacén de claves de Azure está disponible en la mayoría de las regiones. Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introducción
Después de haber creado uno o varios almacenes de claves, probablemente le interesará toomonitor cómo y cuándo la clave de los almacenes de credenciales son acceder y por quién. Puede hacerlo al habilitar el registro del Almacén de claves, que guarda la información en una cuenta de almacenamiento de Azure proporcionada por el usuario. Un nuevo contenedor llamado **insights-logs-auditevent** se crea automáticamente para su cuenta de almacenamiento especificada, y puede utilizar esta misma cuenta para recopilar registros de varios almacenes de claves.

Puede tener acceso a la información de registro a lo sumo, la operación del almacén de 10 minutos después de la clave de Hola. En la mayoría de los casos, será más rápido que esto.  Es una tooyou toomanage los registros en la cuenta de almacenamiento:

* Utilice toosecure de métodos de control de acceso de Azure estándar los registros mediante la restricción de quién puede tener acceso a ellos.
* Eliminar los registros que ya no desea tookeep en su cuenta de almacenamiento.

Use este tutorial toohelp empezar a trabajar con el almacén de claves de Azure, el registro toocreate su cuenta de almacenamiento, habilitar el registro e interpretar la información de registro de hello recopilada.  

> [!NOTE]
> Este tutorial no incluye instrucciones de cómo toocreate clave almacenes, claves o secretos. Para obtener información, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md). O bien, para obtener instrucciones de la interfaz de la línea de comandos entre plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).
>
> Actualmente, no se puede configurar el almacén de claves de Azure en hello portal de Azure. En su lugar, siga estas instrucciones de Azure PowerShell.
>
>

Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, debe tener Hola siguientes:

* Un Almacén de claves existente que ha utilizado.  
* Azure PowerShell, **versión mínima: 1.0.1**. tooinstall PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Si ya ha instalado Azure PowerShell y no conoce la versión de hello, desde la consola de PowerShell de Azure de hello, escriba `(Get-Module azure -ListAvailable).Version`.  
* Suficiente almacenamiento en Azure para sus registros del Almacén de claves.

## <a id="connect"></a>Conectar tooyour suscripciones
Inicie una sesión de PowerShell de Azure e inicie sesión en tooyour cuenta de Azure con hello siguiente comando:  

    Login-AzureRmAccount

En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña. Azure PowerShell obtendrá todas las suscripciones de Hola que están asociadas a esta cuenta y de forma predeterminada, usa Hola primero.

Si tiene varias suscripciones, es posible que tenga toospecify una en concreto que estaba toocreate usa su almacén de claves de Azure. Escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:

    Get-AzureRmSubscription

A continuación, toospecify Hola suscripción que está asociado con el almacén de claves que iniciará sesión, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Este es un paso importante y especialmente útil si tiene varias suscripciones asociadas a su cuenta. Puede recibir un tooregister de error Microsoft.Insights si se omite este paso.
>   
>

Para obtener más información acerca de cómo configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Creación de una cuenta de almacenamiento nueva para los registros
Aunque puede usar una cuenta de almacenamiento existente para sus registros, vamos a crear una nueva cuenta de almacenamiento que estará dedicado tooKey almacén registros. Por comodidad para cuando se tiene toospecify esto más adelante, se podrá almacenar detalles de hello en una variable denominada **sa**.

Para mayor facilidad de administración, vamos a usar Hola el mismo grupo de recursos como Hola uno que contiene el almacén de claves. De hello [tutorial de introducción](key-vault-get-started.md), este grupo de recursos se denomina **ContosoResourceGroup** y seguiremos ubicación de Asia oriental toouse Hola. Sustituya estos valores para los suyos propios, según corresponda:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Si decide toouse una cuenta de almacenamiento existente, debe usar Hola misma suscripción como el almacén de claves y deben utilizar modelo de implementación del Administrador de recursos de hello, en lugar de modelo de implementación de hello clásico.
>
>

## <a id="identify"></a>Identificar el almacén de claves de Hola para sus registros de
En nuestro Ver tutorial introductorio, era el nombre de almacén de claves **ContosoKeyVault**, por lo que vamos a seguir toouse que asigne un nombre y almacenar los detalles de hello en una variable denominada **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Habilitación del registro
tooenable registro para el almacén de claves, vamos a usar el cmdlet de hello AzureRmDiagnosticSetting conjunto, junto con las variables de hello creado para la nueva cuenta de almacenamiento y el almacén de claves. También programaremos hello **-habilitado** marca demasiado**$true** y establezca Hola categoría tooAuditEvent (Hola única categoría para el registro de almacén de claves),:

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

salida de Hello para esto incluye:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Esto confirma que ahora está habilitado el registro para el almacén de claves, guardar la cuenta de almacenamiento de información tooyour.

Opcionalmente también se puede establecer una directiva de retención para los registros, de forma que los registros más antiguos se eliminen automáticamente. Por ejemplo, establecer la directiva de retención con **- RetentionEnabled** marca demasiado**$true** y establecer **- RetentionInDays** parámetro demasiado**90** para que los registros de más de 90 días se eliminarán automáticamente.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Qué se registra:

* Se registran todas las solicitudes de API de REST autenticadas, incluidas las solicitudes con error debido a permisos de acceso, errores del sistema o solicitudes incorrectas.
* Operaciones de clave de hello del almacén de sí mismo, que incluye la creación, eliminación, directivas de acceso del almacén de claves de configuración, y actualizar los atributos del almacén de claves como etiquetas.
* Operaciones en claves y secretos en el almacén de claves de hello, que incluye crear, modificar o eliminar estas claves o secretos; operaciones como inicio de sesión, compruebe, cifrar, descifrar, ajustar y unwrap claves, obtener secretos, enumeración de claves y secretos y sus versiones.
* Solicitudes no autenticadas que dan como resultado una respuesta 401. Por ejemplo, las solicitudes que no tienen un token de portador, cuyo formato es incorrecto o está caducado o tienen un token no válido.  

## <a id="access"></a>Acceso a los registros
Registros de almacén de claves se almacenan en hello **auditevent de registros de visión** contenedor en la cuenta de almacenamiento de hello proporcionada. toolist todos los blobs de hello en este contenedor, escriba:

En primer lugar, cree una variable de nombre de contenedor de Hola. Esto se usará en resto Hola de hello recorra.

    $container = 'insights-logs-auditevent'

toolist todos los blobs de hello en este contenedor, escriba:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
salida de Hello será toothis algo similar:

**Identificador URI de contenedor: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Name**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Como puede ver este resultado, blobs Hola siguen una convención de nomenclatura: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

los valores de fecha y hora de Hello usan UTC.

Dado que hello misma cuenta de almacenamiento puede ser registros toocollect usado para varios recursos, hello Id. de recurso completo en nombre de blob de hello es tooaccess muy útil o blobs de hello solo descarga que necesita. Pero antes de hacerlo, primero lo veremos cómo toodownload Hola a todos los blobs.

En primer lugar, cree un Hola de toodownload carpeta blobs. Por ejemplo:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

A continuación, obtenga una lista de todos los blobs:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Canalice esta lista a través de blobs de hello toodownload 'Get-AzureStorageBlobContent' en la carpeta de destino:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Al ejecutar este comando segundo, Hola ** / ** delimitador en nombres de blob de hello creará una estructura de carpeta completa en la carpeta de destino de hello, y esta estructura de blobs de hello toodownload y almacén usados como archivos.

tooselectively descargar blobs, usar caracteres comodín. Por ejemplo:

* Si tiene varios almacenes de claves y desea que los registros de toodownload para un solo almacén de claves, denominado CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Si tiene varios grupos de recursos y desea registros toodownload para un solo grupo de recursos, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Si desea toodownload todos los registros de hello mes de Hola de enero de 2016, use `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Está ahora listo toostart examinando Novedades en hello registra. Pero antes de pasar al que, dos más parámetros de Get-AzureRmDiagnosticSetting, que puede ser necesario tooknow:

* estado de hello tooquery de configuración de diagnóstico para el recurso de almacén de claves:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* registro de toodisable para el recurso de almacén de claves:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpretación de los registros de Key Vault
Los blobs individuales se almacenan como texto, con formato de blob JSON. A continuación se muestra una entrada del registro de ejemplo cuando se ejecuta `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Hello tabla siguiente enumeran los nombres de campo de Hola y descripciones.

| Nombre del campo | Description |
| --- | --- |
| Twitter en tiempo |Fecha y hora (UTC). |
| resourceId |Identificador de recursos del Administrador de recursos de Azure Para los registros de almacén de claves, siempre es identificador de recurso de almacén de claves de Hola. |
| operationName |Nombre de operación de hello, tal como se describe en la tabla siguiente Hola. |
| operationVersion |Se trata de una versión de API de REST de hello solicitada por el cliente de Hola. |
| categoría |Para los registros de almacén de claves, AuditEvent es valor único, que está disponible de Hola. |
| resultType |Resultado de la solicitud de API de REST. |
| resultSignature |Estado de HTTP |
| resultDescription |Descripción adicional sobre el resultado de hello, cuando esté disponible. |
| durationMs |Duración de la solicitud de API de REST de tooservice hello, en milisegundos. Esto no incluye latencia de red de hello, para tiempo Hola que medir en el lado del cliente de hello podría no coincidir con este momento. |
| callerIpAddress |Dirección IP del cliente de Hola que realizó la solicitud de saludo. |
| correlationId |Un GUID opcional que Hola cliente puede pasar toocorrelate registros de cliente con los registros del lado del servicio (el almacén de claves). |
| identidad |Identidad del token de Hola que se presenta al realizar la solicitud de API de REST de Hola. Suele ser un "usuario", una "entidad de servicio" o una combinación de "usuario + appId" como en el caso de una solicitud procedente de un cmdlet de Azure PowerShell. |
| propiedades |Este campo contendrá información diferente en función de operación de hello (operationName). En la mayoría de los casos, contiene información del cliente (Hola useragent cadena pasado por cliente hello), Hola exacta URI de solicitud de API de REST y código de estado HTTP. Además, cuando un objeto se devuelve como resultado de una solicitud (por ejemplo, KeyCreate o VaultGet) también contendrá Hola URI de clave (como "id"), el URI de almacén o el URI de secreto. |

Hola **operationName** valores de campo están en formato de ObjectVerb. Por ejemplo:

* Todas las operaciones de almacén de claves tienen hello ' almacén`<action>`' dar formato, como `VaultGet` y `VaultCreate`.
* Todas las operaciones de clave tienen hello ' clave`<action>`' dar formato, como `KeySign` y `KeyList`.
* Todas las operaciones de secreto tener hello ' secreto`<action>`' dar formato, como `SecretGet` y `SecretListVersions`.

Hello en la tabla siguiente enumera operationName Hola y el comando de API de REST correspondiente.

| operationName | Comando de API de REST |
| --- | --- |
| Autenticación |Mediante un punto de conexión de Azure Active Directory |
| VaultGet |[Obtener información acerca de un almacén de claves](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Crear o actualizar un almacén de claves](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Eliminar un almacén de claves](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Crear o actualizar un almacén de claves](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Lista de todos los almacenes de claves en un grupo de recursos](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Crear una clave](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Obtener información sobre una clave](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importar una clave a un almacén](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Realizar una copia de seguridad de una clave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Eliminar una clave](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Restaurar una clave](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Firmar con una clave](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Comprobar con una clave](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Encapsular una clave](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Desencapsular una clave](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Cifrar con una clave](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Descifrar con una clave](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Actualizar una clave](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Enumeración de claves de hello en un almacén.](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Lista de versiones de Hola de una clave](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Crear un secreto](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Obtener un secreto](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Actualizar un secreto](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Eliminar un secreto](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Enumerar secretos en un almacén](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Enumerar versiones de un secreto](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Uso de Log Analytics

Puede usar soluciones de almacén de claves de Azure de hello en tooreview de análisis de registros que registra AuditEvent de almacén de claves de Azure. Para obtener más información, incluido cómo tooset este proceso, consulte [solución de almacén de claves de Azure en análisis de registros](../log-analytics/log-analytics-azure-key-vault.md). En este artículo también contiene instrucciones si necesita toomigrate desde la antigua solución de almacén de claves de Hola que se proporcionó durante la vista previa del análisis de registros de hello, donde los enrutan su tooan registros cuenta de almacenamiento de Azure en primer lugar y se configura tooread de análisis de registros a partir de ahí.

## <a id="next"></a>Pasos siguientes
Para ver un tutorial que use Azure Key Vault en una aplicación web, consulte [Uso de Azure Key Vault desde una aplicación web](key-vault-use-from-web-application.md).

Para las referencias de programación, vea [Hola Guía del desarrollador de almacén de claves de Azure](key-vault-developers-guide.md).

Para obtener una lista de los cmdlets de Azure PowerShell 1.0 para Azure Key Vault, consulte [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault)(Cmdlets de Azure Key Vault).

Para obtener un tutorial sobre la rotación de clave y el registro de auditoría al almacén de claves de Azure, consulte [cómo toosetup el almacén de claves con tooend final clave rotación y auditoría](key-vault-key-rotation-log-monitoring.md).
