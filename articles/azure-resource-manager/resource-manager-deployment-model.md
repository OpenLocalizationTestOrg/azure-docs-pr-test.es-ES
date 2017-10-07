---
title: "aaaResource administrador e implementación clásico | Documentos de Microsoft"
description: "Describe el modelo de implementación de hello las diferencias entre el modelo de implementación del Administrador de recursos de Hola y Hola clásico (o administración de servicios)."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Administrador de recursos de Azure frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos
En este tema, aprenderá sobre el Administrador de recursos de Azure y los modelos de implementación clásica, estado de saludo de los recursos, y por qué se implementaron los recursos con uno u Hola otro. Hola, Administrador de recursos y los modelos de implementación clásica representan dos maneras de implementar y administrar sus soluciones de Azure. Trabajar con ellos a través de dos conjuntos de API diferentes y los recursos de hello implementado pueden contener diferencias importantes. Hola dos modelos no son totalmente compatibles entre sí. En este tema se describen esas diferencias.

implementación de hello toosimplify y administración de recursos, Microsoft recomienda que use el Administrador de recursos para todos los recursos nuevo. Si es posible, Microsoft recomienda que vuelva a implementar los recursos existentes a través de Resource Manager.

Si es nuevo tooResource administrador, puede que desee terminología de Hola de revisión toofirst definida en hello [Introducción a Azure Resource Manager](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Historial de modelos de implementación de Hola
Solo el modelo de implementación clásica Hola originalmente había proporcionado por Azure. En este modelo, cada recurso existía independientemente; no había forma de toogroup relacionados con recursos juntos. En su lugar, se tenía toomanually realizar un seguimiento de los recursos que se compone de la solución o aplicación y recuerde toomanage ellas en un planteamiento coordinado. toodeploy una solución, había tooeither crear cada recurso individualmente a través del portal clásico de Hola o crear una secuencia de comandos que implementan todos los recursos de hello en el orden correcto de Hola. toodelete una solución, había toodelete cada recurso individualmente. No se podía aplicar ni actualizar fácilmente las directivas de control de acceso para los recursos relacionados. Por último, no pudo aplicar etiquetas tooresources toolabel con los términos que le ayudarán a supervisar los recursos y administración la facturación.

En 2014, Azure introdujo al administrador de recursos que agrega el concepto de Hola de un grupo de recursos. Un grupo de recursos es un contenedor para los recursos que comparten un ciclo de vida común. modelo de implementación del Administrador de recursos de Hello ofrece varias ventajas:

* Puede implementar, administrar y supervisar todos los servicios de hello para la solución como un grupo, en lugar de controlar estos servicios individualmente.
* Puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente.
* Puede aplicar tooall de control de acceso a recursos en el grupo de recursos y las directivas se aplican automáticamente cuando los recursos nuevos se agregan toohello grupo de recursos.
* Puede aplicar etiquetas tooresources toologically organizar todos los recursos de hello en su suscripción.
* Puede usar la infraestructura de hello toodefine de JavaScript Object Notation (JSON) para su solución. archivo de Hello JSON se conoce como una plantilla de administrador de recursos.
* Puede definir las dependencias de hello entre los recursos, por lo que se implementan en el orden correcto de Hola.

Cuando se agrega el Administrador de recursos, todos los recursos que se agregaron con carácter retroactivo toodefault grupos de recursos. Si crea un recurso a través de la implementación clásica ahora, se crean automáticamente recursos Hola dentro de un grupo de recursos predeterminado para ese servicio, aunque no se especificó ese grupo de recursos en la implementación. Sin embargo, solo existente dentro de un grupo de recursos significa que los recursos de Hola ha sido modelo del Administrador de recursos de toohello convertido. Analizaremos cómo cada servicio controla dos modelos de implementación hello en la sección siguiente Hola. 

## <a name="understand-support-for-hello-models"></a>Entender la compatibilidad para los modelos de Hola
La hora de decidir qué toouse de modelo de implementación para los recursos, hay tres toobe escenarios tenga en cuenta:

1. servicio de Hello es compatible con el Administrador de recursos y proporciona únicamente un solo tipo.
2. Hello servicio admite el Administrador de recursos, pero proporciona dos tipos: uno para el Administrador de recursos y otro para clásico. Este escenario aplica solo toovirtual máquinas, las cuentas de almacenamiento y redes virtuales.
3. servicio de Hello no es compatible con el Administrador de recursos.

toodiscover si un servicio admite el Administrador de recursos, consulte [proveedores de recursos y los tipos](resource-manager-supported-services.md).

Si el servicio de hello desea toouse no es compatible con el Administrador de recursos, debe seguir usando la implementación clásica.

Si el servicio de hello es compatible con el Administrador de recursos y **no es** una máquina virtual, la cuenta de almacenamiento o la red virtual, puede usar el Administrador de recursos sin complicaciones.

Para máquinas virtuales, las cuentas de almacenamiento y redes virtuales, si se creó el recurso de Hola a través de la implementación clásica, debe seguir toooperate en él a través de operaciones clásicas. Si la máquina virtual de hello, cuenta de almacenamiento o red virtual se creó a través de la implementación del Administrador de recursos, debe seguir utilizando las operaciones del Administrador de recursos. Esta distinción puede resultar confusa cuando la suscripción contiene una combinación de los recursos creados mediante Resource Manager y la implementación clásica. Esta combinación de recursos puede crear resultados inesperados porque no admite recursos Hola Hola las mismas operaciones.

En algunos casos, un comando del Administrador de recursos puede recuperar información sobre un recurso que se creó mediante la implementación clásica o puede realizar una tarea administrativa, como mover un grupo de recursos de tooanother recurso clásico. Sin embargo, estos casos no deben proporcionar la impresión de Hola que tipo hello es compatible con las operaciones del Administrador de recursos. Por ejemplo, supongamos que tiene un grupo de recursos que contiene una máquina virtual creada con la implementación clásica. Si ejecuta Hola siguiente comando del Administrador de recursos PowerShell:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Devuelve la máquina virtual de hello:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

Sin embargo, Hola cmdlet del Administrador de recursos **AzureRmVM Get** solo devuelve las máquinas virtuales implementadas a través del Administrador de recursos. Hello siguiente comando no devolver Hola máquina virtual que se creó mediante la implementación clásica.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Solo los recursos creados a través del Administrador de recursos son compatibles con las etiquetas. No se puede aplicar etiquetas tooclassic recursos.

## <a name="resource-manager-characteristics"></a>Características del Administrador de recursos
toohelp comprender Hola dos modelos, revisemos las características de Hola de tipos de administrador de recursos:

* Se creó mediante hello [portal de Azure](https://portal.azure.com/).
  
     ![Azure Portal](./media/resource-manager-deployment-model/portal.png)
  
     Para el cálculo, almacenamiento y recursos de red, tendrá posibilidad de Hola de usando la implementación en el Administrador de recursos o estándar. Select **Administrador de recursos**.
  
     ![Implementación de Resource Manager](./media/resource-manager-deployment-model/select-resource-manager.png)
* Se creó con la versión del Administrador de recursos de Hola de hello cmdlets de PowerShell de Azure. Estos comandos tienen formato hello *AzureRmNoun verbo*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Se creó mediante hello [API de REST de Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) para operaciones REST.
* Se creó mediante comandos de CLI de Azure que se ejecutan en hello **arm** modo.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* no incluye el tipo de recurso de Hello **(clásica)** en nombre de Hola. Hello siguiente imagen muestra tipo hello como **cuenta de almacenamiento**.
  
    ![aplicación web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Características de implementación clásica
También puede saber el modelo de implementación clásica de hello como modelo de administración de servicios de Hola.

Recursos creados en Hola Hola del recurso compartido del modelo de implementación clásica siguientes características:

* Se creó mediante hello [portal clásico](https://manage.windowsazure.com)
  
     ![Portal de Azure](./media/resource-manager-deployment-model/classic-portal.png)
  
     O bien, Hola portal de Azure y especificar **clásico** implementación (por proceso, almacenamiento y redes).
  
     ![Implementación clásica](./media/resource-manager-deployment-model/select-classic.png)
* Se creó mediante la versión de administración de servicios de Hola de hello cmdlets de PowerShell de Azure. Estos nombres de comando tienen formato de hello *AzureNoun verbo*.

  ```powershell
  New-AzureVM
  ```

* Se creó mediante hello [API de REST de administración de servicios](https://msdn.microsoft.com/library/azure/ee460799.aspx) para operaciones REST.
* Creado mediante los comandos de la CLI de Azure ejecutados en modo **asm** .

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* tipo de recurso de Hello incluye **(clásica)** en nombre de Hola. Hello siguiente imagen muestra tipo hello como **cuenta de almacenamiento (clásica)**.
  
    ![tipo clásico](./media/resource-manager-deployment-model/classic-type.png)

Puede usar los recursos de Azure toomanage portal Hola que se crearon a través de la implementación clásica.

## <a name="changes-for-compute-network-and-storage"></a>Cambios de proceso, red y almacenamiento
Hello siguiente diagrama muestra los recursos de proceso, red y almacenamiento implementados a través del Administrador de recursos.

![Arquitectura de Resource Manager](./media/resource-manager-deployment-model/arm_arch3.png)

Tenga en cuenta Hola siguiendo las relaciones entre los recursos de hello:

* Todos los recursos de hello existen dentro de un grupo de recursos.
* máquina virtual de Hello depende de una cuenta de almacenamiento específicos definida en toostore de proveedor de recursos de almacenamiento de hello (obligatorio) de almacenamiento de blobs de los discos en.
* máquina virtual de Hello hace referencia a una NIC específica definida en el proveedor de recursos de red de hello (obligatorio) y un conjunto definido en el proveedor de recursos de proceso de hello (opcional) de disponibilidad.
* Hola NIC referencias hello de la máquina virtual asignada (obligatorio), la dirección de la IP subred Hola de red virtual de hello para la máquina virtual de hello (obligatorio) y tooa el grupo de seguridad de red (opcional).
* subred de Hello en una red virtual hace referencia a un grupo de seguridad de red (opcional).
* instancia de equilibrador de carga de Hello hace referencia a grupo de back-end de Hola de direcciones IP que incluyen hello formación de una máquina virtual (opcional) y una dirección equilibrador de carga pública o privada IP (opcional).

Estos son componentes de Hola y sus relaciones de implementación clásica:

![arquitectura clásica](./media/resource-manager-deployment-model/arm_arch1.png)

Hola clásico solución para hospedar una máquina virtual incluye:

* Un servicio de nube requerido que actúa como contenedor para hospedar máquinas virtuales (cálculo). Las máquinas virtuales se proporcionan automáticamente con una tarjeta de interfaz de red (NIC) y una dirección IP asignada por Azure. Además, el servicio de nube de hello contiene una instancia de equilibrador de carga externo, una dirección IP pública y los puntos de conexión tooallow remoto remoto y escritorio PowerShell tráfico predeterminada para máquinas virtuales basadas en Windows y tráfico de Shell seguro (SSH) para basados en Linux máquinas virtuales.
* Una cuenta de almacenamiento correspondiente que almacenes Hola discos duros virtuales para una máquina virtual, incluido el sistema operativo de hello, discos de datos temporal y adicionales (almacenamiento).
* Una red virtual opcional que actúa como un contenedor adicional, en el que se puede crear una estructura de subredes y designar subred hello en qué Hola se encuentra la máquina virtual (red).

Hello en la tabla siguiente describe los cambios en cómo interactúan los proveedores de recursos de proceso, red y almacenamiento:

| Elemento | Clásico | Resource Manager |
| --- | --- | --- |
| Servicio en la nube para máquinas virtuales |Servicio de nube era un contenedor para almacenar máquinas virtuales de Hola que requieren la disponibilidad de la plataforma de Hola y equilibrio de carga. |Servicio de nube ya no es un objeto que es necesario para crear una máquina Virtual con el nuevo modelo de Hola. |
| Redes virtuales |Una red virtual es opcional para la máquina virtual de Hola. Si se incluye, red virtual de hello no se puede implementar con el Administrador de recursos. |La máquina virtual requiere una red virtual que se ha implementado con Resource Manager. |
| Cuentas de almacenamiento |máquina virtual de Hello requiere una cuenta de almacenamiento que almacena los discos duros virtuales de Hola para sistema operativo de hello, discos de datos temporal y adicionales. |máquina virtual de Hello requiere un toostore de cuenta de almacenamiento sus discos de almacenamiento de blobs. |
| Conjuntos de disponibilidad |Plataforma de toohello de disponibilidad se indica mediante la configuración de Hola mismo "AvailabilitySetName" en hello máquinas virtuales. recuento máximo de Hola de dominios de error es 2. |Un conjunto de disponibilidad es un recurso expuesto por el proveedor de Microsoft.Compute. Máquinas virtuales que requieren alta disponibilidad deben incluirse en el conjunto de disponibilidad de Hola. recuento máximo de Hola de dominios de error ahora es 3. |
| Grupos de afinidad |Los grupos de afinidad eran necesarios para crear redes virtuales. Sin embargo, con la introducción de Hola de redes virtuales regionales, que no fue necesario ya. |toosimplify, el concepto de grupos de afinidad de hello no existe en hello API expuestas a través del Administrador de recursos de Azure. |
| Equilibrio de carga |Creación de un servicio de nube proporciona un equilibrador de carga implícita para hello máquinas virtuales implementadas. |Hola equilibrador de carga es un recurso expuesto por el proveedor de Microsoft.Network Hola. interfaz de red principal de Hola de hello máquinas virtuales que necesita con equilibrio de carga de toobe debe hacer referencia a equilibrador de carga de Hola. Los equilibradores de carga pueden ser internos o externos. Una instancia de equilibrador de carga hace referencia a grupo de back-end de Hola de direcciones IP que incluyen hello formación de una máquina virtual (opcional) y una dirección equilibrador de carga pública o privada IP (opcional). [Más información.](../virtual-network/resource-groups-networking.md) |
| Dirección IP virtual |Servicios en la nube obtienen a una VIP predeterminada (dirección IP Virtual) cuando una máquina virtual se agrega el servicio en la nube tooa. Hola dirección IP Virtual es dirección Hola asociado con el equilibrador de carga implícita de Hola. |Dirección IP pública es un recurso expuesto por el proveedor de Microsoft.Network Hola. La dirección IP pública puede ser estática (reservada) o dinámica. Dinámica de direcciones IP públicas pueden asignarse tooa equilibrador de carga. Las direcciones IP públicas se pueden proteger mediante grupos de seguridad. |
| Dirección IP reservada |Puede reservar una dirección IP en Azure y asociar con un tooensure de servicio en la nube que Hola dirección IP es permanente. |Dirección IP pública pueden crearse en modo "Estático" y ofertas Hola misma capacidad como un "dirección IP reservada". Direcciones IP públicas estáticas sólo puede asignarse equilibrador de carga de tooa ahora mismo. |
| Dirección IP pública (PIP) por máquina virtual |Las direcciones IP públicas también puede ser asociado tooa VM directamente. |Dirección IP pública es un recurso expuesto por el proveedor de Microsoft.Network Hola. La dirección IP pública puede ser estática (reservada) o dinámica. Sin embargo, solamente IP públicas dinámicas pueden tooget de interfaz de red asignadas tooa una IP pública por máquina virtual ahora mismo. |
| Puntos de conexión |Extremos de entrada necesario toobe configurado en una máquina Virtual toobe, abra la conectividad para determinados puertos. Uno de los modos comunes de Hola de conectar los equipos de toovirtual realizando mediante la configuración de los extremos de entrada. |Reglas NAT de entrada se pueden configurar en los equilibradores de carga tooachieve Hola misma capacidad de habilitar los puntos de conexión en puertos específicos para conectar máquinas virtuales toohello. |
| Nombre DNS |Un servicio en la nube obtendría un nombre de DNS único global implícito. Por ejemplo: `mycoffeeshop.cloudapp.net`. |Los nombres DNS son parámetros opcionales que se pueden especificar en un recurso de dirección IP pública. Hola FQDN es siguiente Hola formato - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfaces de red |La interfaz de red principal y secundaria y sus propiedades se definieron como configuración de red de una máquina virtual. |La interfaz de red es un recurso expuesto por el proveedor de Microsoft.Network. ciclo de vida de Hola de hello que interfaz de red no está enlazado tooa Máquina Virtual. Hace referencia a dirección IP asignada la máquina virtual Hola (obligatorio), subred Hola de red virtual de hello para la máquina virtual de hello (obligatorio) y tooa el grupo de seguridad de red (opcional). |

toolearn acerca de cómo conectar redes virtuales de diferentes modelos de implementación, consulte [conectar redes virtuales de diferentes modelos de implementación en el portal de hello](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Migrar desde clásico tooResource Manager
Si estás listo toomigrate los recursos de implementación clásica tooResource deployment Manager, consulte:

1. [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Migración de plataforma admitida de los recursos de IaaS de clásico tooAzure el Administrador de recursos](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante el uso de PowerShell de Azure](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante la CLI de Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Preguntas frecuentes
**¿Puedo crear una máquina virtual mediante Azure Resource Manager toodeploy en una red virtual que creó mediante la implementación clásica?**

ya que no es compatible. No puede usar el Administrador de recursos de Azure toodeploy una máquina virtual en una red virtual que se creó mediante la implementación clásica.

**¿Puedo crear una máquina virtual mediante hello Azure Resource Manager desde una imagen de usuario que se creó mediante la API de administración de servicios de Azure Hola?**

ya que no es compatible. Sin embargo, puede copiar archivos VHD de Hola desde una cuenta de almacenamiento que se creó mediante Hola API de administración de servicios y agregarlos tooa nueva cuenta creada mediante el Administrador de recursos de Azure.

**¿Cuál es el impacto de hello en una cuota de Hola para mi suscripción?**

las cuotas de Hola de hello las máquinas virtuales, redes virtuales y las cuentas de almacenamiento se creó mediante hello Azure Resource Manager son distintos de otras cuotas. Cada suscripción Obtiene las cuotas toocreate Hola recursos usando Hola nuevas API. Puede leer más acerca de las cuotas adicionales de hello [aquí](../azure-subscription-service-limits.md).

**¿Puedo seguir toouse mis scripts automatizados para el aprovisionamiento de máquinas virtuales, redes virtuales y las cuentas de almacenamiento a través de la API del Administrador de recursos de hello?**

Todos los automatización hello y scripts que ha compilado continúan toowork máquinas virtuales existentes hello, redes virtuales creadas en el modo de administración de servicios de Azure Hola. Sin embargo, las secuencias de comandos de hello tienen esquema nuevo Hola de toobe toouse actualizada para la creación de hello mismos recursos a través del modo de administrador de recursos de Hola.

**¿Dónde puedo encontrar ejemplos de plantillas del Administrador de recursos de Azure?**

Puede encontrar un conjunto completo de plantillas de inicio en [Plantillas de inicio rápido de Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Pasos siguientes
* toowalk por la creación de hello de plantilla que define una máquina virtual, su cuenta de almacenamiento y red virtual, vea [tutorial de la plantilla de administrador de recursos](resource-manager-template-walkthrough.md).
* comandos de hello toosee para la implementación de una plantilla, consulte [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

