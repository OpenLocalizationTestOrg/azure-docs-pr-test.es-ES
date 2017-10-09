---
title: "aaaDelete un Azure clúster y sus recursos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo eliminar toocompletely un tejido de servicio de clúster ya sea eliminando grupo de recursos de Hola que contiene el clúster de Hola o eliminando recursos de forma selectiva."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Eliminar un clúster de Service Fabric en los recursos de Azure y hello usa
Además propio recurso de clúster toohello, un clúster de Service Fabric se compone de muchos otros recursos de Azure. Por lo que toocompletely eliminar un clúster de Service Fabric debe toodelete que todos Hola recursos que está formada.
Tienes dos opciones: los grupos de recursos de Hola delete que Hola clúster está en (que elimina los recursos de clúster de Hola y otros recursos en el grupo de recursos de hello) o eliminar específicamente el recurso de clúster de Hola y tiene asociados recursos (pero no para otras recursos de grupo de recursos de hello).

> [!NOTE]
> Eliminar el recurso de clúster de hello **no** delete todos Hola otros recursos que está formado por el clúster de Service Fabric.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Eliminar grupo de recursos completo de hello (RG) que Hola a tejido de servicio de clúster se encuentra en
Se trata de tooensure Hola de manera más fácil que elimine todos los recursos de hello asociados al clúster, incluido el grupo de recursos de Hola. Puede eliminar grupo de recursos de hello con PowerShell o a través de hello portal de Azure. Si el grupo de recursos tiene recursos que no son tooService relacionados tejido clústeres, puede eliminar recursos específicos.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Eliminar grupo de recursos de hello mediante PowerShell de Azure
También puede eliminar el grupo de recursos de hello ejecutando Hola siguientes cmdlets de PowerShell de Azure. Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior. Si no ha hecho esto antes, siga los pasos de hello descritos en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)

Abra una ventana de PowerShell y ejecute hello siguientes cmdlets de PS:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Obtendrá una eliminación de hello tooconfirm preguntar si no usas hello *-Force* opción. En la confirmación Hola RG y se eliminan todos los recursos de hello contiene.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Eliminar un grupo de recursos en hello portal de Azure
1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Navegar por clúster de Service Fabric toohello desea toodelete.
3. Haga clic en hello nombre del grupo de recursos en página de hello clúster essentials.
4. Se abrirá hello **Essentials de grupo de recursos** página.
5. Hacer clic en **Eliminar**.
6. Siga las instrucciones de hello en dicha eliminación de página toocomplete Hola Hola del grupo de recursos.

![Eliminación de un grupo de recursos][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Eliminar el recurso de clúster de Hola y recursos de Hola que utiliza, pero no otros recursos en el grupo de recursos de Hola
Si el grupo de recursos tiene únicamente los recursos que están en clúster de Service Fabric toohello relacionados que desee toodelete, resulta más fácil toodelete Hola todo grupo de recursos. Si desea recursos Hola de delete tooselectively uno por uno, en el grupo de recursos que, a continuación, siga estos pasos.

Si implementa el clúster mediante el portal de Hola o utilizando uno de plantillas de servicio Administrador de recursos de tejido de Hola desde la Galería de plantillas de hello, todos los recursos de Hola Hola de clúster utiliza se etiquetan con hello siguiendo dos etiquetas. Puede usar toodecide qué recursos desea toodelete.

***Etiqueta n.º 1:*** clave = clusterName, valor = 'nombre de clúster de hello'

***Etiqueta 2:*** Clave = resourceName, valor = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Eliminar recursos específicos de hello portal de Azure
1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Navegar por clúster de Service Fabric toohello desea toodelete.
3. Vaya demasiado**toda la configuración de** en la hoja de essentials Hola.
4. Haga clic en **etiquetas** en **administración de recursos** en la hoja de configuración de Hola.
5. Haga clic en uno de hello **etiquetas** en hello etiquetas hoja tooget una lista de todos los recursos de Hola que contienen esa etiqueta.
   
    ![Etiquetas del recurso][ResourceTags]
6. Una vez que tenga la lista de Hola de recursos etiquetados, haga clic en cada uno de los recursos de Hola y eliminarlos.
   
    ![Recursos etiquetados][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Eliminar recursos de hello usando Azure PowerShell
Puede eliminar recursos Hola uno por uno, ejecute hello siguientes cmdlets de PowerShell de Azure. Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior. Si no ha hecho esto antes, siga los pasos de hello descritos en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)

Abra una ventana de PowerShell y ejecute hello siguientes cmdlets de PS:

```powershell
Login-AzureRmAccount
```
Para cada uno de los recursos de hello desea toodelete, ejecute hello siguiente:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

recurso de clúster en hello toodelete, ejecute hello siguiente:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Pasos siguientes
Hola de lectura sigue tooalso Aprenda a actualizar a un clúster y servicios de creación de particiones:

* [Obtener información sobre actualizaciones de clúster](service-fabric-cluster-upgrade.md)
* [Obtener información sobre los servicios con estado de creación de particiones para una escala máxima](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
