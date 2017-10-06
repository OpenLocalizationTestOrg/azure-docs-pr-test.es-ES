---
title: aaaRequire transferencia segura en el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de la característica de \"Requerir una transferencia segura\" hello para el almacenamiento de Azure y cómo tooenable lo."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Requerir transferencia segura

opción de Hola "transferencia segura necesaria" mejora la seguridad de hello de la cuenta de almacenamiento solo tiene que permitir las solicitudes de cuenta de almacenamiento de toohello de conexiones seguras. Por ejemplo, al llamar a las API de REST tooaccess su cuenta de almacenamiento, debe conectarse usando HTTPS. Si "Se requiere transferencia segura" está habilitada, se rechazan todas las solicitudes en que se use HTTP.

Cuando se usa el servicio de archivos de Azure de hello, se produce un error en cualquier conexión sin cifrado cuando "Proteger la transferencia requerida" está habilitada. Esto incluye escenarios con algunos tipos de hello cliente Linux SMB, SMB 2.1 y SMB 3.0 sin cifrado. 

De forma predeterminada, la opción de Hola "transferencia segura necesaria" está deshabilitada.

> [!NOTE]
> Dado que Azure Storage no admite HTTPS para los nombres de dominio personalizados, esta opción no se aplica cuando se utiliza un nombre de dominio personalizado.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Habilitar a "Transferencia segura necesaria" Hola portal de Azure

Puede habilitar Hola "transferencia segura necesario" si se establecen cuando se crea una cuenta de almacenamiento en hello [portal de Azure](https://portal.azure.com)y para las cuentas de almacenamiento existente.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Solicitud de transferencia segura al crear una cuenta de almacenamiento

1. Abra hello **crear cuenta de almacenamiento** hoja Hola portal de Azure.
1. En **Se requiere transferencia segura**, seleccione **Habilitado**.

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Solicitud de transferencia segura en una cuenta de almacenamiento existente

1. Seleccione una cuenta de almacenamiento existente en hello portal de Azure.
1. Seleccione **configuración** en **configuración** en la hoja de menú de cuenta de almacenamiento de Hola.
1. En **Se requiere transferencia segura**, seleccione **Habilitado**.

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Habilitación de "Se requiere transferencia segura" mediante programación

es el nombre de la configuración de Hello _supportsHttpsTrafficOnly_ en Propiedades de la cuenta de almacenamiento. Puede habilitar la configuración "Se requiere transferencia segura" con la API de REST, herramientas o bibliotecas:

* **API de REST** (versión: 2016-12-01): [paquete comercial](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (versión: 4.1.0): [paquete comercial](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (versión: 2.0.11): [paquete comercial](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (versión: 1.1.0): [paquete comercial](https://www.npmjs.com/package/azure-arm-storage/)
* **SDK de .NET** (versión: 6.3.0): [paquete comercial](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **SDK de Python** (versión: 1.1.0): [paquete comercial](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **SDK de Ruby** (versión: 0.11.0): [paquete comercial](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Habilitación de la configuración "Se requiere transferencia segura" con la API de REST

toosimplify pruebas con la API de REST, puede usar [ArmClient](https://github.com/projectkudu/ARMClient) toocall desde la línea de comandos.

 Puede usar por debajo de la opción de línea de comandos toocheck Hola con hello API de REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

En la respuesta de hello, encontrará _supportsHttpsTrafficOnly_ configuración. Sample:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

Puede usar por debajo de la opción de línea de comandos tooenable Hola con hello API de REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Ejemplo de Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Pasos siguientes
Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad, que juntas permiten a los desarrolladores de aplicaciones seguras toobuild. Para obtener más detalles, visite hello [Guía de seguridad de almacenamiento](storage-security-guide.md).
