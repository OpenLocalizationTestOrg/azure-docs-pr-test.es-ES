---
title: "comandos aaaAzure PowerShell basada en el Administrador de recursos para la aplicación Web de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola toomanage de comandos de PowerShell basada en el Administrador de recursos de Azure nuevo las aplicaciones Web de Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Uso de aplicaciones de Web de Azure PowerShell Azure Resource Manager-Based tooManage
> [!div class="op_single_selector"]
> * [CLI de Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Con Microsoft Azure PowerShell versión 1.0.0 se han agregado nuevos comandos, que le proporcionan Hola usuario Hola capacidad toouse basado en el Administrador de recursos de Azure PowerShell comandos toomanage aplicaciones Web.

toolearn acerca de cómo administrar grupos de recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md). 

toolearn acerca de la lista completa de Hola de parámetros y las opciones de hello cmdlets de PowerShell, vea hello [completo referencia de Cmdlet basado en el Administrador de recursos de Azure de aplicación Web de Cmdlets de PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Administración de planes del Servicio de aplicaciones
### <a name="create-an-app-service-plan"></a>Creación de un plan del Servicio de aplicaciones
toocreate un plan de servicio de aplicaciones, usar hello **AzureRmAppServicePlan New** cmdlet.

Siguientes son las descripciones de parámetros diferentes hello:

* **Nombre**: nombre del plan de servicio de aplicación Hola.
* **Location**: ubicación del plan del servicio.
* **ResourceGroupName**: grupo de recursos que incluye el plan de servicio de aplicación Hola recién creado.
* **Nivel**: Hola deseado tarifa (valor predeterminado es gratuito, otras opciones son compartidos, Basic, Standard y Premium).
* **WorkerSize**: Hola tamaño de trabajadores (el valor predeterminado es pequeña si se especificó el parámetro de nivel de hello como Basic, Standard o Premium. Otras opciones son Mediano y Grande.)
* **NumberofWorkers**: Hola el número de trabajos en el plan de servicio de aplicación Hola (el valor predeterminado es 1). 

En el ejemplo se toouse este cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Creación de un plan del Servicio de aplicaciones en un entorno del Servicio de aplicaciones
toocreate planear de un servicio de aplicaciones en un entorno de servicio de aplicaciones, use Hola mismo comando **AzureRmAppServicePlan New** comando con el nombre de hello toospecify de parámetros adicionales del ASE y el nombre del grupo de recursos de ASE.

En el ejemplo se toouse este cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

más información acerca del entorno de servicio de aplicaciones, verificación toolearn [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Enumeración de planes del Servicio de aplicaciones existentes
usar planes de servicio de aplicación existente de toolist hello, **AzureRmAppServicePlan Get** cmdlet.

toolist todos los planes de servicio de aplicación en su suscripción, use: 

    Get-AzureRmAppServicePlan

toolist todos los planes de servicio de aplicaciones en un grupo de recursos específico, use:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget un plan de servicio de aplicación específica, use:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configuración de un plan del Servicio de aplicaciones existente
toochange Hola de un plan de servicio de aplicación existente, utilice hello **AzureRmAppServicePlan conjunto** cmdlet. Puede cambiar el nivel de hello, el tamaño de trabajo y el número de Hola de trabajadores 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Escalado de un plan del Servicio de aplicaciones
tooscale una existente aplicación Plan del servicio, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Cambiar el tamaño de trabajador de Hola de un Plan de servicio de aplicaciones
tamaño de hello toochange de trabajadores de una existente aplicación servicio previsto, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Hola Cambiar nivel de un Plan de servicio de aplicaciones
nivel de hello toochange una existente aplicación de servicio del Plan de, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Eliminación de un plan del Servicio de aplicaciones
toodelete un plan de servicio de aplicación existente, todas asignadas toobe de necesidad de aplicaciones web movido o eliminado en primer lugar. A continuación, usar hello **Remove-AzureRmAppServicePlan** cmdlet puede eliminar el plan de servicio de aplicaciones de Hola.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Administración de aplicaciones web del Servicio de aplicaciones
### <a name="create-a-web-app"></a>Creación de una aplicación web
toocreate una aplicación web, utilice hello **AzureRmWebApp New** cmdlet.

Siguientes son las descripciones de parámetros diferentes hello:

* **Nombre**: nombre de la aplicación web de Hola.
* **AppServicePlan**: nombre para el plan de servicio Hola utiliza toohost hello web app.
* **ResourceGroupName**: grupo de recursos que hospeda el plan de servicio de aplicación Hola.
* **Ubicación**: Hola ubicación de la aplicación web.

En el ejemplo se toouse este cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Creación de una aplicación web en App Service Environment
toocreate una aplicación web en un entorno de servicio de aplicación (ASE). Use Hola mismo **AzureRmWebApp New** comando con nombre de hello ASE toospecify de parámetros adicionales y el nombre de grupo de recursos de Hola Hola ASE pertenece a.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

más información acerca del entorno de servicio de aplicaciones, verificación toolearn [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Eliminación de una aplicación web existente
una aplicación web existente que se puede usar hello toodelete **Remove-AzureRmWebApp** cmdlet, necesita nombre de hello toospecify de aplicación web de hello y nombre de grupo de recursos de Hola.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Lista de aplicaciones web existentes
aplicaciones web existentes a toolist hello, usar hello **AzureRmWebApp Get** cmdlet.

toolist todas las aplicaciones web en su suscripción, use:

    Get-AzureRmWebApp

toolist todas las aplicaciones web en un grupo de recursos específico, use:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget una aplicación web específica, use:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configuración de una aplicación web existente
configuraciones de hello toochange y para una aplicación web existente, use hello **AzureRmWebApp conjunto** cmdlet. Para obtener una lista completa de parámetros, compruebe hello [vínculo de referencia de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)

Ejemplo (1): use este cmdlet toochange las cadenas de conexión

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Ejemplo (2): Adición o cambio de la configuración de una aplicación

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Ejemplo (3): establecer toorun de aplicación web de hello en modo de 64 bits

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Cambio de estado de Hola de una aplicación Web existente
#### <a name="restart-a-web-app"></a>Reinicio de una aplicación web
toorestart una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Detención de una aplicación web
toostop una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Inicio de una aplicación web
toostart una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Administración de perfiles de publicación de aplicaciones web
Cada aplicación web tiene un perfil de publicación que puede ser utilizado toopublish las aplicaciones, se pueden ejecutar varias operaciones en perfiles de publicación.

#### <a name="get-publishing-profile"></a>Obtención de un perfil de publicación
tooget Hola de perfil para una aplicación web, el uso de publicación:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Este comando eco hello publicación de línea de comandos de toohello de perfil también Hola archivo de texto tooa de perfil de publicación de salida.

#### <a name="reset-publishing-profile"></a>Restablecimiento de un perfil de publicación
tooreset ambos Hola contraseña de publicación de FTP y web deploy para una aplicación web, use:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Administración de certificados de aplicaciones web
toolearn acerca de cómo toomanage web certificados de aplicación, consulte [enlace de certificados SSL con PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Pasos siguientes
* toolearn sobre la compatibilidad con el Administrador de recursos de Azure PowerShell, consulte [con Azure PowerShell con el Administrador de recursos de Azure.](../powershell-azure-resource-manager.md)
* toolearn sobre los entornos de servicio de aplicación, consulte [Introducción tooApp entorno del servicio.](app-service-app-service-environment-intro.md)
* toolearn acerca de cómo administrar certificados SSL de servicio de aplicación mediante PowerShell, consulte [enlace de certificados SSL mediante PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn acerca de la lista completa de Hola de cmdlets de PowerShell basada en el Administrador de recursos de Azure para las aplicaciones Web de Azure, consulte [referencia de cmdlets de Azure de Cmdlets de PowerShell del Administrador de recursos de Web aplicaciones de Azure.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn acerca de cómo administrar el servicio de aplicaciones mediante CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para la aplicación Web de Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

