---
title: recursos de aaaManage con hello CLI de Azure | Documentos de Microsoft
description: "Usar toomanage de interfaz de línea de comandos (CLI) de Azure de hello Azure recursos y grupos"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Usar hello Azure CLI toomanage Azure y grupos de recursos
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [CLI de Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API DE REST](resource-manager-rest-api.md)
> 
> 

Hola interfaz de línea de comandos de Azure (Azure CLI) es una de las diversas herramientas puede usar toodeploy y administrar recursos con el Administrador de recursos. Este artículo detallan comunes formas toomanage Azure y grupos de recursos mediante el uso de Hola CLI de Azure en el modo de administrador de recursos. Para obtener información sobre el uso de recursos de toodeploy de hello CLI, consulte [implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](resource-group-template-deploy-cli.md). Para obtener información acerca de los recursos de Azure y el Administrador de recursos, visite hello [Azure Resource Manager Overview](resource-group-overview.md).

> [!NOTE]
> toomanage Azure recursos con hello CLI de Azure, que necesita demasiado[instalar hello Azure CLI](../cli-install-nodejs.md), y [sesión tooAzure](../xplat-cli-connect.md) mediante el uso de hello `azure login` comando. Asegúrese de hello seguro CLI está en modo de administrador de recursos (ejecutar `azure config mode arm`). Si lo ha hecho, está listo toogo.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Obtención de recursos y grupos de recursos
### <a name="resource-groups"></a>Grupos de recursos
tooget una lista de todos los grupos de recursos en su suscripción y sus ubicaciones, ejecute este comando.

    azure group list


### <a name="resources"></a>Recursos
 el nombre de todos los recursos de un grupo, por ejemplo, uno con toolist *testRG*, usar hello siguiente comando:

    azure resource list testRG

un recurso individual en el grupo de hello, como una máquina virtual denominada tooview *MyUbuntuVM*, utilizar un comando como Hola siguiente:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Hola aviso **Microsoft.Compute/virtualMachines** parámetro. Este parámetro indica el tipo hello del recurso de Hola que solicita información en.

> [!NOTE]
> Cuando se usa hello **recursos de azure** comandos que no sean de hello **lista** de comandos, debe especificar versión de Hola API de recursos de hello con hello **-o** parámetro. Si no está seguro acerca de la versión de la API de hello, consulte el archivo de plantilla de hello y encontrar el campo de valor apiVersion de hello para el recurso de Hola. Para más información acerca de las versiones de API de Resource Manager, vea [Tipos y proveedores de recursos](resource-manager-supported-services.md).
> 
> 

Al ver los detalles en un recurso, a menudo resulta útil toouse hello `--json` parámetro. Este parámetro hace que los resultados Hola sea más legible, porque algunos de los valores son estructuras anidadas o colecciones. Hello en el ejemplo siguiente se muestra devolver resultados Hola de hello **mostrar** comando como un documento JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Si lo desea, guarde Hola JSON datos toofile mediante el uso de hello &gt; archivo de tooa de salida de caracteres toodirect Hola. Por ejemplo:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Etiquetas
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Administración de recursos
tooadd un recurso como un grupo de recursos tooa de cuenta de almacenamiento, ejecute un comando similar al:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Además toospecifying Hola versión de API de recurso de hello con hello **-o** parámetro, use hello **-p** toopass formato JSON de la cadena de parámetros con cualquier necesario o propiedades adicionales.

toodelete un recurso existente como un recurso de la máquina virtual, use un comando como Hola siguiente:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello **mover recursos de azure** comando. Hola siguiente ejemplo se muestra cómo toomove caché en Redis tooa nuevo grupo de recursos. Hola **-i** parámetro, proporcione una lista separada por comas de toomove del Id. de recurso Hola.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Tooresources de acceso de control
Puede usar hello toocreate de CLI de Azure y administrar directivas toocontrol acceso tooAzure recursos. Para obtener información acerca de las definiciones de directiva y asignar tooresources de directivas, consulte [usar Directiva toomanage recursos y controlar el acceso](resource-manager-policy.md).

Por ejemplo, definir Hola después directiva toodeny todas las solicitudes donde la ubicación no es oeste de Estados Unidos o Ee.uu. Central Norte y guardar policy.json de archivo de definición de directiva de toohello:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

A continuación, ejecute hello **Crear definición de directiva** comando:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Este comando muestra la siguiente toohello similar de salida:

    + Creación de definición de directiva MyPolicy datos:    PolicyName:             MyPolicy datos:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    datos:    PolicyType:             Custom datos:    DisplayName:            undefined datos:    Description:            undefined datos:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 una directiva en el ámbito de Hola que desee, use hello tooassign **PolicyDefinitionId** devueltos por el comando anterior Hola. En el siguiente ejemplo de Hola, este ámbito es suscripción hello, pero puede establecer el ámbito tooresource grupos o recursos individuales:

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

Puede obtener, cambiar o quitar las definiciones de directivas mediante hello **mostrar de la definición de directiva**, **conjunto de definiciones de directiva**, y **eliminar la definición de directiva** comandos.

De forma similar, puede obtener, cambiar o quitar las asignaciones de directivas mediante hello **mostrar de la asignación de directiva**, **conjunto de asignación de directiva**, y **Eliminar asignación de directiva** comandos .

## <a name="export-a-resource-group-as-a-template"></a>Exportación de un grupo de recursos como una plantilla
Para un grupo de recursos existente, puede ver la plantilla de administrador de recursos de Hola Hola para grupo de recursos. Exportar plantilla Hola ofrece dos ventajas:

1. Puede automatizar fácilmente las futuras implementaciones de soluciones de hello porque toda la infraestructura de Hola se define en la plantilla de Hola.
2. Familiarícese con la sintaxis de plantilla examinando Hola JSON que representa la solución.

Con hello CLI de Azure, se puede exportar una plantilla que representa el estado actual de Hola de su grupo de recursos, o descargar plantilla de Hola que se usó para una implementación concreta.

* **Exportar plantilla Hola para un grupo de recursos** -Esto resulta útil cuando realiza cambios tooa grupo de recursos y necesita tooretrieve Hola representación JSON de su estado actual. Sin embargo, plantilla generada hello contiene solo un número mínimo de parámetros y no hay ninguna variable. La mayoría de los valores de hello en plantilla Hola está codificados. Antes de implementar la plantilla de hello generado, es recomendable tooconvert varios de los valores de hello en los parámetros para que pueda personalizar la implementación de Hola para diferentes entornos.
  
    plantilla de hello tooexport para un recurso grupo tooa directorio local, ejecute hello `azure group export` comando tal como se muestra en el siguiente ejemplo de Hola. (Sustituya un directorio local adecuado para su entorno de sistema operativo).
  
        azure group export testRG ~/azure/templates/
* **Descargar plantilla de Hola para una implementación concreta** : Esto es útil cuando necesita tooview Hola real de la plantilla que usa toodeploy recursos. plantilla de Hello incluye todos los parámetros y las variables definidas para la implementación original de Hola. Sin embargo, si alguien de su organización realiza grupo de recursos de toohello de cambios fuera de la definición de hello en plantilla hello, esta plantilla no representa el estado actual de Hola Hola del grupo de recursos.
  
    plantilla de hello toodownload utilizada para un implementación determinada tooa directorio local, ejecute hello `azure group deployment template download` comando. Por ejemplo:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> La exportación de plantillas es una versión preliminar y no todos los tipos de recursos admiten actualmente la exportación de una plantilla. Al intentar tooexport una plantilla, verá un error que indica que algunos recursos no se exportaron. Si es necesario, defina manualmente estos recursos en la plantilla después de descargarla.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* detalles de tooget de las operaciones de implementación y solucionar errores de implementación con hello CLI de Azure, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).
* Si desea toouse Hola CLI tooset una aplicación o recursos de script tooaccess, consulte [toocreate de CLI de Azure Use una entidad de servicio tooaccess recursos](resource-group-authenticate-service-principal-cli.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

