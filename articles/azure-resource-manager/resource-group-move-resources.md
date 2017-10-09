---
title: "aaaMove toonew suscripción o recurso de grupo de recursos de Azure | Documentos de Microsoft"
description: "Use el Administrador de recursos de Azure toomove recursos tooa nuevo grupo de recursos o suscripción."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Mover grupo de recursos de toonew de recursos o suscripción
Este tema muestra cómo toomove recursos tooeither una nueva suscripción o en un nuevo recurso de grupo en hello misma suscripción. Puede usar el portal de hello, PowerShell, CLI de Azure u Hola recursos toomove de API de REST. las operaciones de movimiento de Hello en este tema están disponible tooyou sin ayuda de soporte técnico de Azure.

Al mover los recursos, los grupos de código fuente de Hola y Hola destino se bloquean durante la operación de Hola. Escribir y eliminar operaciones están bloqueados en grupos de recursos de hello hasta que se completa el movimiento de Hola. Este bloqueo significa que no se puede agregar, actualizar o eliminar los recursos en grupos de recursos de hello, pero no significa que se inmovilizan recursos Hola. Por ejemplo, si mueve un servidor SQL Server y su grupo de recursos de base de datos tooa nuevo, una aplicación que utiliza la base de datos de hello no experimenta ningún tiempo de inactividad. Todavía puede leer y escribir toohello base de datos.

No se puede cambiar la ubicación de hello del recurso de Hola. Mover un recurso solo mueve tooa nuevo grupo de recursos. nuevo grupo de recursos de Hello puede tener una ubicación diferente, pero no cambiar la ubicación de hello del recurso de Hola.

> [!NOTE]
> Este artículo describe cómo cuenta oferta toomove recursos dentro de un Azure existente. Si realmente desea toochange su cuenta de Azure de la oferta (por ejemplo, la actualización de pago por uso toopre-pay) mientras continúa toowork con los recursos existentes, consulte [cambiar su oferta de suscripción de Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Lista de comprobación antes de mover recursos
Hay algunos tooperform pasos importantes antes de mover un recurso. Puede evitar errores mediante la comprobación de estas condiciones.

1. Hello las suscripciones de origen y de destino deben existir en hello mismo [inquilino de Azure Active Directory](../active-directory/active-directory-howto-tenant.md). toocheck que ambas suscripciones han Hola mismo identificador de inquilino, usar Azure PowerShell o CLI de Azure.

  Para Azure PowerShell, use:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Para la CLI de Azure 2.0, use:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Si Hola inquilino identificadores para las suscripciones de origen y destino de hello no son Hola mismo, puede tratar de directorio de hello toochange para la suscripción de Hola. Sin embargo, esta opción está solo disponible tooService los administradores que han iniciado sesión con una cuenta de Microsoft (no una cuenta profesional). tooattempt cambiando el directorio de hello, inicio de sesión toohello [portal clásico](https://manage.windowsazure.com/)y seleccione **configuración**y seleccione la suscripción de Hola. Si hello **editar directorio** icono está disponible, seleccione toochange Hola asociados Azure Active Directory.

  ![editar directorio](./media/resource-group-move-resources/edit-directory.png)

  Si este icono no está disponible, debe ponerse en contacto con el soporte técnico toomove Hola recursos tooa nuevo inquilino.

2. servicio de Hello debe habilitar recursos de hello capacidad toomove. Este tema enumeran los servicios que permiten mover recursos y los servicios que no permiten el traslado de recursos.
3. suscripción de destino de Hello debe estar registrada para el proveedor de recursos de Hola de recurso de Hola que se va a mover. Si no es así, recibirá un error que indica que hello **suscripción no está registrada para un tipo de recurso**. Podría encontrar este problema al mover una nueva suscripción de recursos tooa, pero esa suscripción nunca se ha utilizado con ese tipo de recurso. toolearn cómo toocheck Hola estado de registro y registrar proveedores de recursos, consulte [proveedores de recursos y los tipos](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>¿Cuándo admitirá toocall
Puede mover la mayoría de los recursos a través de operaciones de autoservicio de Hola que se muestra en este tema. Usar operaciones de autoservicio de Hola para:

* Trasladar recursos de Resource Manager.
* Mover los recursos clásicos según toohello [limitaciones de implementación clásica](#classic-deployment-limitations).

Llame a soporte técnico cuando necesite:

* Mueva la cuenta de Azure nuevo recursos tooa (y los inquilinos de Azure Active Directory).
* Mover los recursos clásicos pero están teniendo problemas con las limitaciones de Hola.

## <a name="services-that-enable-move"></a>Servicios que permiten el traslado
Por ahora, servicios de Hola que habilite móvil tooboth un nuevo grupo de recursos y la suscripción son:

* API Management
* App Service apps (Web Apps) - consulte las [limitaciones de App Service](#app-service-limitations)
* Application Insights
* Automation
* Batch
* Mapas de Bing
* CDN
* Cloud Services (consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)
* Cognitive Services
* Content Moderator
* Data Catalog
* Data Factory
* Data Lake Analytics
* Almacén de Data Lake
* DNS
* Azure Cosmos DB
* Event Hubs
* Clústeres de HDInsight: consulte [Limitaciones de HDInsight](#hdinsight-limitations).
* IoT Hubs
* Key Vault
* Equilibradores de carga
* Logic Apps
* Machine Learning
* Media Services
* Mobile Engagement
* Notification Hubs
* Operational Insights
* Operations Management
* Power BI
* Redis Cache
* Scheduler
* Search
* Servidor de administración
* Service Bus
* Service Fabric
* Storage
* Storage (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)
* Stream Analytics: los trabajos de Stream Analytics no se pueden mover si se encuentran en estado de ejecución.
* Servidor de base de datos SQL: hello base de datos y el servidor deben residir en hello mismo grupo de recursos. Cuando se mueve un servidor SQL Server, se mueven también todas sus bases de datos.
* Administrador de tráfico
* Máquinas virtuales
* Máquinas virtuales con certificado almacenado en el almacén de claves - mover el grupo de recursos de toonew en la misma suscripción está habilitada, pero no está habilitado el movimiento de suscripción cruzado.
* Virtual Machines (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)
* Conjuntos de escalado de máquina virtual
* Virtual Networks: por el momento, no se puede mover una red virtual emparejada hasta que el emparejamiento de la red virtual se haya inhabilitado. Una vez deshabilitado, Hola red Virtual se podrá mover correctamente y se puede habilitar el intercambio de tráfico de red virtual de Hola. Además, una red Virtual no puede ser movida tooa otra suscripción si Hola red Virtual contiene ninguna subred con vínculos de navegación de recursos. Por ejemplo, una subred de red virtual tiene un vínculo de navegación de recursos cuando se implementa un recurso de redis Microsoft.Cache en esta subred.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Servicios que no permiten el traslado
Servicios de Hola que actualmente no se permiten mover un recurso son:

* Servicios de dominio de AD
* Servicio de mantenimiento híbrido de AD
* Application Gateway
* Conjuntos de disponibilidad con Virtual Machines con discos administrados
* Servicios de BizTalk
* Container Service
* ExpressRoute
* Laboratorios de desarrollo y pruebas - mover el grupo de recursos de toonew en la misma suscripción está habilitado, pero entre el movimiento de suscripción no está habilitado.
* Dynamics LCS
* Imágenes creadas a partir de discos administrados
* Managed Disks
* Aplicaciones administradas
* Almacén de servicios de recuperación: también ¿Hola no movimiento Hola proceso, red y almacenamiento de recursos asociados con los servicios de recuperación del almacén, vea [limitaciones de servicios de recuperación](#recovery-services-limitations).
* Seguridad
* Instantáneas creadas a partir de discos administrados
* Administrador de dispositivos de StorSimple
* Virtual Machines con discos administrados
* Virtual Networks (clásico); consulte las [limitaciones de la implementación clásica](#classic-deployment-limitations)
* Virtual Machines creadas a partir de recursos de Marketplace (no se pueden mover entre suscripciones). Recurso necesita toobe canceló el aprovisionamiento en la suscripción actual de Hola y volver a implementarse en nueva suscripción de Hola

## <a name="app-service-limitations"></a>Limitaciones de App Service
Si se trabaja con aplicaciones de App Service, no se puede mover solo un plan de App Service. aplicaciones de servicio de aplicaciones de toomove, las opciones son:

* Mover hello plan de servicio de aplicaciones y todos los demás recursos de servicio de aplicaciones en dicho recurso grupo tooa nuevo grupo de recursos que ya no tiene los recursos del servicio de aplicación. Este requisito significa que se debe mover incluso Hola recursos de servicio de aplicaciones que no están asociados con hello plan de servicio de aplicaciones.
* Mover grupo de recursos distinto de hello aplicaciones tooa, pero tenga todos los planes de servicio de aplicaciones en el grupo de recursos de hello original.

Hello plan no es necesario tooreside en el servicio de aplicaciones Hola mismo grupo de recursos como aplicación hello para hello aplicación toofunction correctamente.

Por ejemplo, si el grupo de recursos contiene:

* **web-a** asociada a **plan-a**
* **web-b** asociada a **plan-b**

Tendrá las siguientes opciones:

* Trasladar **web-a**, **plan-a**, **web-b** y **plan-b**
* Trasladar **web-a** y **web-b**
* Mover **web-a**
* Mover **web-b**

Todas las demás combinaciones implican dejar un tipo de recurso que debe trasladarse al mover un plan de App Service (cualquier tipo de recurso de App Service).

Si la aplicación web se encuentra en un grupo de recursos diferente que su plan de servicio de aplicaciones, pero desea toomove ambos tooa nuevo grupo de recursos, debe realizar el movimiento de hello en dos pasos. Por ejemplo:

* **web-a** reside en **web-group**.
* **plan-a** reside en **plan-group**.
* Desea **web-a** y **un plan** tooreside en **grupo combinado**

tooaccomplish Esto mueve, realizar dos operaciones de movimiento independientes en hello sigue secuencia:

1. Mover hello **web-a** demasiado**grupo de plan**
2. Mover **web-a** y **un plan** demasiado**grupo combinado**.

Puede mover un nuevo grupo de recursos de certificado de servicio de aplicación tooa o suscripción sin ningún problema. Sin embargo, si la aplicación web incluye un certificado SSL que adquirió externamente y toohello aplicación ha cargado, debe eliminar certificado de hello antes de la aplicación móvil de web de hello. Por ejemplo, puede realizar Hola pasos:

1. Eliminar certificado de hello cargado desde la aplicación web de hello
2. Mueva la aplicación web de hello
3. Cargar la aplicación web de hello certificado toohello

## <a name="recovery-services-limitations"></a>Limitaciones de Recovery Services
Movimiento no está habilitada para el almacenamiento, red, o los recursos de proceso usan tooset la recuperación ante desastres con Azure Site Recovery.

Por ejemplo, suponga que ha configurado la replicación de la cuenta de almacenamiento de tooa de máquinas locales (Storage1) y desee Hola protegido máquina toocome seguridad después de la conmutación por error tooAzure como una máquina virtual (VM1) había conectado a la red virtual de tooa (Network1). No se puede mover cualquiera de estos recursos de Azure - Storage1, VM1, y Network1 - a través de recursos grupos dentro de hello misma suscripción o a través de suscripciones.

## <a name="hdinsight-limitations"></a>Limitaciones de HDInsight

Puede mover HDInsight clústeres tooa nueva suscripción o grupo de recursos. Sin embargo, no se puede mover a través de hello suscripciones redes de clúster de HDInsight toohello vinculado de recursos (por ejemplo, la red virtual de hello, NIC o equilibrador de carga). Además, no se puede mover el grupo de recursos nuevo tooa una NIC que está adjunto tooa virtual machine para clúster Hola.

Al mover una suscripción nuevo de tooa de clúster de HDInsight, mueva primero otros recursos (como cuenta de almacenamiento de hello). A continuación, mover el clúster de HDInsight de Hola por sí mismo.

## <a name="classic-deployment-limitations"></a>limitaciones de la implementación clásica
Hello opciones para mover recursos implementados a través del modelo clásico Hola varían en función de si va a mover recursos Hola dentro de una suscripción o tooa nuevo.

### <a name="same-subscription"></a>Misma suscripción
Al mover los recursos del grupo de recursos tooanother un recurso de grupo dentro de la misma suscripción, Hola siguientes restricciones se aplican de Hola:

* No se pueden mover redes virtuales (clásico).
* Máquinas virtuales (clásicas) se deben mover con el servicio de nube de Hola.
* Servicio de nube solo puede aplicarse al movimiento de hello incluye todas sus máquinas virtuales.
* Solo se puede mover un servicio en la nube cada vez.
* Solo se puede mover una cuenta de almacenamiento (clásico) cada vez.
* No se puede mover la cuenta de almacenamiento (clásica) en hello misma operación con una máquina virtual o un servicio de nube.

toomove recursos clásicos tooa nuevo grupo de recursos en Hola misma suscripción, utilice las operaciones de movimiento estándar de Hola a través de hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), o [API de REST](#use-rest-api). Usa Hola mismas operaciones que use para mover recursos del Administrador de recursos.

### <a name="new-subscription"></a>Suscripción nueva
Al mover tooa nueva suscripción de recursos, se aplica Hola siguientes restricciones:

* Se deben mover todos los recursos clásicos de suscripción de Hola Hola misma operación.
* suscripción de destino de Hello no debe contener ningún otro recurso clásico.
* Hola movimiento solo se puede solicitar a través de una API de REST independiente para movimientos clásicos. comandos de movimiento de administrador de recursos estándar de Hello no funcionan al mover la nueva suscripción de recursos clásicos tooa.

toomove recursos clásicos tooa nueva suscripción, operaciones de REST de Hola de uso son recursos tooclassic específicos. toouse REST, lleve a cabo Hola pasos:

1. Compruebe si la suscripción de origen Hola puede participar en una suscripción entre mover. Usar hello después de operación:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     En el cuerpo de la solicitud de hello, incluya:

  ```json
  {
    "role": "source"
  }
  ```

     respuesta de Hello para la operación de validación de hello es Hola siguiendo el formato:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Compruebe si la suscripción de destino de hello puede participar en una suscripción entre mover. Usar hello después de operación:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     En el cuerpo de la solicitud de hello, incluya:

  ```json
  {
    "role": "target"
  }
  ```

     respuesta de Hello es en el mismo formato que la validación de suscripción del origen de Hola de Hola.
3. Si ambas suscripciones pasan la validación, mover todos los recursos clásicos de suscripción de tooanother de una suscripción con hello después de operación:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    En el cuerpo de la solicitud de hello, incluya:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

operación de Hello puede llevar varios minutos.

## <a name="use-portal"></a>Mediante el portal
toomove recursos, seleccione grupo de recursos de Hola que contiene esos recursos y, a continuación, seleccione hello **mover** botón.

![Mover recursos](./media/resource-group-move-resources/select-move.png)

Seleccione si va a mover Hola recursos tooa nuevo grupo de recursos o una nueva suscripción.

Seleccione toomove de recursos de Hola y el grupo de recursos de destino de Hola. Confirmar que necesite tooupdate scripts para estos recursos y seleccione **Aceptar**. Si ha seleccionado el icono de suscripción de edición de hello en el paso anterior de hello, también debe seleccionar la suscripción de destino de Hola.

![seleccionar destino](./media/resource-group-move-resources/select-destination.png)

En **notificaciones**, verá que Hola mover la operación se ejecuta.

![mostrar el estado del traslado](./media/resource-group-move-resources/show-status.png)

Cuando se ha completado, se le notificará de resultado de hello.

![mostrar el resultado del traslado](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Uso de PowerShell
existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `Move-AzureRmResource` comando.

Hola el primer ejemplo se muestra cómo toomove un recurso tooa nuevo grupo de recursos.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Hola segundo ejemplo se muestra cómo toomove varios recursos tooa nuevo grupo de recursos.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nueva suscripción, especifique un valor para hello `DestinationSubscriptionId` parámetro.

Se le pide tooconfirm que desea toomove Hola de los recursos especificados.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Uso de la CLI de Azure 2.0
existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `az resource move` comando. Proporcionar Hola identificadores de recursos de hello recursos toomove. Puede obtener Id. de recurso con hello siguiente comando:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Hola de ejemplo siguiente muestra cómo toomove un almacenamiento cuenta tooa nuevo grupo de recursos. Hola `--ids` parámetro, proporcionan una lista separada por espacios de toomove de identificadores de recursos de Hola.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nueva suscripción, proporcione hello `--destination-subscription-id` parámetro.

## <a name="use-azure-cli-10"></a>Uso de CLI de Azure 1.0
existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello `azure resource move` comando. Proporcionar Hola identificadores de recursos de hello recursos toomove. Puede obtener Id. de recurso con hello siguiente comando:

```azurecli
azure resource list -g sourceGroup --json
```

Que devuelve Hola siguiendo el formato:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Hola de ejemplo siguiente muestra cómo toomove un almacenamiento cuenta tooa nuevo grupo de recursos. Hola `-i` parámetro, proporcione una lista separada por comas de toomove de identificadores de recursos de Hola.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Se le pide tooconfirm que desea toomove Hola el recurso especificado.

## <a name="use-rest-api"></a>Use la API de REST
grupo de recursos de recursos existente de toomove tooanother o suscripción, ejecute:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

En el cuerpo de la solicitud de hello, especifique el grupo de recursos de destino de Hola y Hola recursos toomove. Para obtener más información acerca de la operación de REST de movimiento de hello, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de los cmdlets de PowerShell para administrar su suscripción, vea [con Azure PowerShell con el Administrador de recursos](powershell-azure-resource-manager.md).
* toolearn acerca de los comandos de CLI de Azure para administrar su suscripción, vea [Using Hola CLI de Azure con el Administrador de recursos](xplat-cli-azure-resource-manager.md).
* toolearn acerca de características del portal para administrar su suscripción, vea [uso de recursos de Azure toomanage portal hello](resource-group-portal.md).
* toolearn acerca de cómo aplicar un recurso de tooyour organización lógica, consulte [mediante etiquetas tooorganize los recursos de](resource-group-using-tags.md).
