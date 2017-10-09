---
title: "el almacén de claves con SQL Server en máquinas virtuales de Windows Azure (clásica) aaaIntegrate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooautomate Hola configuración de cifrado de SQL Server para su uso con el almacén de claves de Azure. Este tema explica cómo se crean toouse integración del almacén de claves de Azure con máquinas virtuales de SQL Server en el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configurar la integración de Azure Key Vault para SQL Server en máquinas virtuales de Azure (implementación clásica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Clásico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Información general
SQL Server tiene varias características de cifrado, como el [cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), el [cifrado de nivel de columna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) y el [cifrado de copia de seguridad](https://msdn.microsoft.com/library/dn449489.aspx). Estas formas de cifrado requieren toomanage y almacenan las claves criptográficas de Hola que utilice para el cifrado. Hola servicio de almacén de claves de Azure (claves) está diseñado tooimprove Hola seguridad y la administración de estas claves en una ubicación segura y altamente disponible. Hola [conector de SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite a SQL Server toouse estas claves del almacén de claves de Azure.

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Si está ejecutando SQL Server con equipos locales, hay [pasos que puede seguir tooaccess el almacén de claves de Azure desde el equipo de SQL Server local](https://msdn.microsoft.com/library/dn198405.aspx). Pero para SQL Server en máquinas virtuales de Azure, puede ahorrar tiempo mediante el uso de hello *integración del almacén de claves de Azure* característica. Con unos tooenable de cmdlets de PowerShell de Azure esta característica, puede automatizar Hola configuración necesaria para una VM de SQL tooaccess el almacén de claves.

Cuando esta característica está habilitada, Hola conector de SQL Server se instala, configura Hola EKM proveedor tooaccess el almacén de claves de Azure y automáticamente crea Hola credencial tooallow se tooaccess el almacén. Si busca en pasos de Hola Hola se ha mencionado previamente documentación local, puede ver que esta característica automatiza los pasos 2 y 3. lo único que Hola todavía necesitaría toodo manualmente es claves y el almacén de claves de hello toocreate. Desde allí, se automatiza la instalación completa de hello de la VM de SQL. Una vez completada la instalación, esta característica puede ejecutar toobegin de instrucciones de T-SQL cifrar sus bases de datos o las copias de seguridad, tal y como lo haría normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configuración de la integración de AKV
Usar PowerShell tooconfigure integración del almacén de claves de Azure. Hello las secciones siguientes proporciona una introducción de los parámetros de hello necesario y, a continuación, un script de PowerShell de ejemplo.

### <a name="install-hello-sql-server-iaas-extension"></a>Instalar Hola extensión de IaaS de SQL Server
En primer lugar, [instalar Hola extensión de IaaS de SQL Server](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Comprender los parámetros de entrada de Hola
Hello siguiente tabla listas Hola requieren parámetros toorun script de PowerShell de hello en la sección siguiente Hola.

| Parámetro | Description | Ejemplo |
| --- | --- | --- |
| **$akvURL** |**dirección URL del almacén de claves de Hola** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Nombre de entidad de servicio** |"fde2b411-33d5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Secreto de entidad de servicio** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=" |
| **$credName** |**Nombre de la credencial**: integración de claves crea una credencial de SQL Server, lo que permite Hola VM toohave acceso toohello el almacén de claves. Elija un nombre para esta credencial. |"mycred1" |
| **$vmName** |**Nombre de máquina virtual**: nombre de Hola de una VM de SQL creado anteriormente. |"myvmname" |
| **$serviceName** |**Nombre del servicio**: nombre de servicio en la nube de Hola que está asociado con hello VM de SQL. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>Habilitación de la integración de AKV con PowerShell
Hola **AzureVMSqlServerKeyVaultCredentialConfig New** crea un objeto de configuración para la característica de integración del almacén de claves de Azure de Hola. Hola **conjunto AzureVMSqlServerExtension** configura esta integración con hello **KeyVaultCredentialSettings** parámetro. Hola siguientes pasos muestran cómo toouse estos comandos.

1. En PowerShell de Azure, en primer lugar configurar parámetros de entrada de hello con los valores específicos como se describe en secciones anteriores de Hola de este tema. Hola siguiente secuencia de comandos es un ejemplo.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. A continuación, usar a continuación Hola script tooconfigure y habilitar la integración de claves.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Hola extensión del agente de IaaS de SQL actualizará Hola VM de SQL con esta nueva configuración.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

