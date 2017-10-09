---
title: "Introducción al administrador de recursos aaaAzure | Documentos de Microsoft"
description: "Describe cómo toouse Azure Resource Manager para la implementación, administración y control de acceso de recursos en Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Información general del Administrador de recursos de Azure
infraestructura de Hola para su aplicación normalmente se compone de muchos componentes, puede ser una máquina virtual, cuenta de almacenamiento y red virtual, o una aplicación web, base de datos, servidor de base de datos y 3 servicios de terceros. Estos componentes no se ven como entidades independientes, sino como partes de una sola entidad relacionadas e interdependientes. Desea toodeploy, administrar y supervisar como un grupo. Administrador de recursos de Azure permite toowork con recursos de hello en la solución como un grupo. Puede implementar, actualizar o eliminar todos los recursos de hello para la solución en una única operación coordinada. Para realizar la implementación se usa una plantilla, que puede funcionar en distintos entornos, como producción, pruebas y ensayo. Administrador de recursos proporciona seguridad, auditoría y etiquetado características toohelp administrar sus recursos después de la implementación. 

## <a name="terminology"></a>Terminología
Si está tooAzure nuevo administrador de recursos, hay algunos de los términos que podría no estar familiarizado con.

* **recurso** : elemento administrable que está disponible a través de Azure. Algunos recursos comunes son una máquina virtual, una cuenta de almacenamiento, una aplicación web, una base de datos y una red virtual, pero hay muchos más.
* **grupo de recursos** : contenedor que almacena los recursos relacionados con una solución de Azure. grupo de recursos de Hello puede incluir todos los recursos de hello para la solución de hello, o sólo aquellos recursos que desea toomanage como un grupo. Decida cómo desea que los recursos de tooallocate tooresource grupos basan en lo que le resulte hello más conveniente para su organización. Consulte [Grupos de recursos](#resource-groups).
* **proveedor de recursos** -un servicio que proporciona recursos de hello puede implementar y administrar mediante el Administrador de recursos. Cada proveedor de recursos proporciona operaciones para trabajar con recursos de Hola que se implementan. Algunos proveedores de recursos comunes son Microsoft.Compute, que proporciona recursos de máquina virtual de hello, almacenamiento de Microsoft, que proporciona recursos de cuenta de almacenamiento de hello, y Microsoft.Web, que proporciona recursos relacionados tooweb aplicaciones. Consulte [Proveedores de recursos](#resource-providers).
* **Plantilla de administrador de recursos** -archivo A JavaScript Object Notation (JSON) que define uno o varios recursos toodeploy tooa grupo de recursos. También define las dependencias de hello entre recursos de hello implementado. plantilla de Hello puede ser usado toodeploy Hola recursos varias veces y de forma coherente. Consulte [Implementación de plantilla](#template-deployment).
* **la sintaxis declarativa** -estado de sintaxis que le permite "aquí es lo que va toocreate" sin necesidad de secuencia de hello toowrite de toocreate de comandos de programación. plantilla de administrador de recursos de Hello es un ejemplo de la sintaxis declarativa. En el archivo hello, definir propiedades Hola Hola infraestructura toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>ventajas de Hola de usar el Administrador de recursos
Administrador de recursos ofrece varias ventajas:

* Puede implementar, administrar y supervisar todos los recursos de hello para la solución como un grupo, en lugar de controlar estos recursos individualmente.
* Repetidamente, puede implementar la solución a lo largo del ciclo de vida de desarrollo de Hola y estar seguro de que los recursos se implementan en un estado coherente.
* Puede administrar la infraestructura mediante plantillas declarativas en lugar de scripts.
* Puede definir las dependencias de hello entre los recursos, por lo que se implementan en el orden correcto de Hola.
* Puede aplicar tooall servicios de control de acceso en el grupo de recursos porque el Control de acceso basado en roles (RBAC) se integra de forma nativa en plataforma de administración de Hola.
* Puede aplicar etiquetas tooresources toologically organizar todos los recursos de hello en su suscripción.
* Puede aclarar la facturación de su organización mediante la visualización de los costos de un grupo de recursos de uso compartido Hola la misma etiqueta.  

Administrador de recursos proporciona un nuevo toodeploy de manera y administrar sus soluciones. Si ha usado Hola modelo de implementación anterior y desea toolearn acerca de los cambios de hello, consulte [Administrador de recursos de la descripción y la implementación clásica](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Capa de administración coherente
El Administrador de recursos proporciona un nivel de administración coherente para tareas de Hola que realizar a través de PowerShell de Azure, CLI de Azure, portal de Azure, API de REST y las herramientas de desarrollo. Todas las herramientas de hello usar un conjunto común de las operaciones. Use herramientas de Hola que funcionan mejor para usted y se pueden utilizar indistintamente sin confusión. 

Hello siguiente imagen muestra cómo interactúan todas las herramientas de Hola Hola misma API del Administrador de recursos de Azure. Hola API pasa las solicitudes de servicio de administrador de recursos de toohello, que autentica y autoriza las solicitudes de Hola. El Administrador de recursos, a continuación, enruta los proveedores de recursos adecuados de toohello de hello las solicitudes.

![Modelo de solicitud de Resource Manager](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Guía
Hello estas sugerencias ayudarle a aprovechar al máximo del Administrador de recursos cuando se trabaja con las soluciones.

1. Definir e implementar la infraestructura a través de la sintaxis declarativa hello en las plantillas de administrador de recursos, en lugar de mediante comandos imperativos.
2. Definir todos los pasos de implementación y configuración de plantilla de Hola. No debería tener ningún paso manual para configurar la solución.
3. Ejecutar comandos imperativo toomanage sus recursos, como toostart o detener una aplicación o la máquina.
4. Organizar los recursos con hello mismo ciclo de vida en un grupo de recursos. Use etiquetas para organizar los demás recursos.

Para más recomendaciones sobre platillas, consulte [Procedimientos recomendados para crear plantillas de Azure Resource Manager](resource-manager-template-best-practices.md).

Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Grupos de recursos
Hay algunos factores importantes tooconsider al definir el grupo de recursos:

1. Todos los recursos de hello en el grupo deben compartir Hola mismo ciclo de vida. Se implementan, actualizan y eliminan de forma conjunta. Si un recurso, como un servidor de base de datos, necesita tooexist en un ciclo de implementación diferentes debe estar en otro grupo de recursos.
2. Cada recurso solo puede existir en un grupo de recursos.
3. Puede agregar o quitar un grupo de recursos de tooa de recursos en cualquier momento.
4. Puede mover un recurso de un grupo de tooanother de grupo de recursos. Para obtener más información, consulte [Mover grupo de recursos de toonew de recursos o suscripción](resource-group-move-resources.md).
5. Un grupo de recursos puede contener recursos que residen en diferentes regiones.
6. Puede ser un grupo de recursos utiliza tooscope el control de acceso para las acciones administrativas.
7. Un recurso puede interactuar con los recursos de otros grupos. Esta interacción suele ocurrir cuando los recursos de hello dos se relacionan pero no comparten Hola mismo ciclo de vida (por ejemplo, aplicaciones web de conexión de base de datos de tooa).

Al crear un grupo de recursos, debe tooprovide una ubicación para ese grupo de recursos. Pero puede preguntarse: "¿Por qué necesita un grupo de recursos una ubicación? Y, si los recursos de hello pueden tener diferentes ubicaciones que el grupo de recursos de hello, ¿por qué es ubicación del grupo de recursos de hello relevante en absoluto?" grupo de recursos de Hello almacena metadatos acerca de los recursos de Hola. Por lo tanto, cuando se especifica una ubicación para el grupo de recursos de hello, está especificando donde se almacenan los metadatos. Por motivos de cumplimiento, puede que necesite tooensure que se almacenan los datos en una región determinada.

## <a name="resource-providers"></a>Proveedores de recursos
Cada proveedor de recursos ofrece un conjunto de recursos y operaciones para trabajar con un servicio de Azure. Por ejemplo, si desea toostore claves y secretos, puede trabajar con hello **Microsoft.KeyVault** proveedor de recursos. Este proveedor de recursos ofrece un tipo de recurso denominado **almacenes** para crear el almacén de claves de Hola. 

nombre de Hola de un tipo de recurso está en formato de hello: **{proveedor de recursos} / {tipo de recurso}**. Por ejemplo, es el tipo de almacén de claves de hello **Microsoft.KeyVault/vaults**.

Antes de comenzar con la implementación de los recursos, debe obtener una descripción de los proveedores de recursos disponibles Hola. Conocer los nombres de hello del recurso de proveedores y los recursos de ayuda a definir los recursos que desee toodeploy tooAzure. Además, deberá ubicaciones válidas de tooknow hello y versiones de API para cada tipo de recurso. Para más información, consulte [Tipos y proveedores de recursos](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Implementación de plantilla
Con el Administrador de recursos, puede crear una plantilla (en formato JSON) que define la infraestructura de Hola y la configuración de la solución de Azure. Mediante una plantilla, puede implementar la solución repetidamente a lo largo del ciclo de vida y tener la seguridad de que los recursos se implementan de forma coherente. Cuando se crea una solución de portal de hello, solución de hello incluye automáticamente una plantilla de implementación. No tiene toocreate la plantilla desde cero ya que puede empezar con la plantilla de hello para la solución y personalizarlo toomeet sus necesidades específicas. Puede recuperar una plantilla para un grupo de recursos existente exportar estado actual de Hola Hola del grupo de recursos, o ver plantilla Hola que se usa para una implementación concreta. Ver hello [Exportar plantilla](resource-manager-export-template.md) es un toolearn de forma útil acerca de la sintaxis de la plantilla de Hola.

toolearn acerca del formato de Hola de plantilla de Hola y cómo se crea, consulte [crear la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md). Hola tooview sintaxis de JSON para los tipos de recursos, consulte [definir los recursos en las plantillas de Azure Resource Manager](/azure/templates/).

El Administrador de recursos procesa plantilla hello como cualquier otra solicitud (vea la imagen de Hola para [capa de administración coherente](#consistent-management-layer)). Analiza la plantilla de Hola y convierte su sintaxis en las operaciones de API de REST para proveedores de recursos adecuados de Hola. Por ejemplo, cuando el Administrador de recursos recibe una plantilla con hello después de la definición de recursos:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Convierte Hola definición toohello después de la operación de API de REST, que se envía el proveedor de recursos de almacenamiento de Microsoft toohello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Cómo definir plantillas y grupos de recursos es completamente hasta tooyou y cómo desea toomanage la solución. Por ejemplo, puede implementar la aplicación de tres niveles mediante una única plantilla tooa único grupo de recursos.

![plantilla de tres niveles](./media/resource-group-overview/3-tier-template.png)

Sin embargo, no tiene toodefine toda la infraestructura de una única plantilla. A menudo, tiene sentido toodivide los requisitos de implementación en un conjunto de plantillas de destino, propósito específico. Estas plantillas se pueden reutilizar fácilmente para distintas soluciones. toodeploy una solución concreta, crear una plantilla maestra que se vincula todas las plantillas de hello necesario. Hello siguiente imagen muestra cómo toodeploy una solución de tres niveles a través de una plantilla primaria que incluye tres anidar plantillas.

![plantilla de niveles anidada](./media/resource-group-overview/nested-tiers-template.png)

Si práctico imaginar los niveles de tener los ciclos de vida independientes, puede implementar los grupos de recursos de tooseparate de tres niveles. Aviso Hola recursos pueden seguir siendo tooresources vinculados en otros grupos de recursos.

![plantilla de niveles](./media/resource-group-overview/tier-templates.png)

Para obtener sugerencias sobre cómo diseñar las plantillas, consulte [Prácticas recomendadas para diseñar plantillas de Azure Resource Manager](best-practices-resource-manager-design-templates.md). Para más información acerca de las plantillas anidadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).

El Administrador de recursos Azure analiza las dependencias de recursos de tooensure se crean en el orden correcto de Hola. Si un recurso se basa en un valor de otro recurso (por ejemplo, una máquina virtual que necesita una cuenta de almacenamiento para los discos), establezca una dependencia. Para obtener más información, consulte [Definición de dependencias en plantillas del Administrador de recursos de Azure](resource-group-define-dependencies.md).

También puede usar Hola plantilla de infraestructura de actualizaciones de toohello. Por ejemplo, puede agregar una solución de tooyour de recursos y agregar reglas de configuración para los recursos de Hola que ya estén implementados. Si la plantilla de hello especifica la creación de un recurso pero ese recurso ya existe, el Administrador de recursos de Azure realiza una actualización en lugar de crear un nuevo recurso. Azure Resource Manager actualizaciones Hola existente asset toohello mismo estado tal y como sería como nuevo.  

El Administrador de recursos proporciona extensiones para escenarios cuando necesite operaciones adicionales como la instalación de software en particular que no se incluye en el programa de instalación de Hola. Si ya utiliza un servicio de administración de configuración, como DSC, Chef o Puppet, puede seguir trabajando con ese servicio mediante las extensiones. Para más información acerca de las extensiones de máquina virtual, consulte [Acerca de las características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Por último, plantilla de Hola se convierte en parte del código fuente de hello para la aplicación. Puede comprobarlo en el repositorio de código fuente tooyour y actualizarla a medida que evolucione su aplicación. Puede editar la plantilla de Hola a través de Visual Studio.

Después de definir la plantilla, está listo toodeploy Hola recursos tooAzure. Hola comandos toodeploy Hola recursos, consulte:

* [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](resource-group-template-deploy.md)
* [Implementación de recursos con plantillas de Resource Manager y la CLI de Azure](resource-group-template-deploy-cli.md)
* [Implementación de recursos con las plantillas de Resource Manager y Azure Portal](resource-group-template-deploy-portal.md)
* [Implementación de recursos con las plantillas de Resource Manager y la API de REST de Resource Manager](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Etiquetas
El Administrador de recursos proporciona una característica de etiquetado que le permite recursos toocategorize según los requisitos de tooyour para administrar o facturación. Utilizar etiquetas cuando tiene un conjunto complejo de grupos de recursos y recursos y necesita toovisualize esos recursos en forma de Hola que le resulte Hola mayoría tooyou de sentido. Por ejemplo, podría etiquetar recursos que no sirven para una función similar en su organización o pertenecen toohello mismo departamento. Sin etiquetas, los usuarios de su organización pueden crear varios recursos que pueden ser difíciles de toolater identifican y administración. Por ejemplo, podría desear toodelete todos los recursos de Hola para un determinado proyecto. Si no se etiquetan esos recursos para el proyecto de hello, deberá toomanually encontrarlos. Etiquetado puede ser un aspecto importante para usted tooreduce costos innecesarios en su suscripción. 

Recursos no es necesario tooreside Hola mismo tooshare de grupo de recursos una etiqueta. Puede crear su propios tooensure de taxonomía de etiqueta que todos los usuarios de su organización usan etiquetas comunes en lugar de los usuarios sin darse cuenta aplicar etiquetas ligeramente diferentes (por ejemplo, "departamento" en lugar de "departamento").

Hola de ejemplo siguiente muestra una máquina virtual de tooa de etiqueta aplicada.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

tooretrieve todos los recursos de hello con un valor de etiqueta, usan Hola siguiente cmdlet de PowerShell:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

O bien, Hola siguiente comando de CLI de Azure 2.0:

```azurecli
az resource list --tag costCenter=Finance
```

También puede ver recursos etiquetados a través de hello portal de Azure.

Hola [informe de uso de](../billing/billing-understand-your-bill.md) para la suscripción incluye nombres de etiquetas y valores, lo que le permite toobreak los costos por etiquetas. Para obtener más información acerca de las etiquetas, vea [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md).

## <a name="access-control"></a>Control de acceso
El Administrador de recursos permite toocontrol quién tiene acceso toospecific acciones para su organización. Forma nativa se integra en el control de acceso basado en roles (RBAC) en la plataforma de administración de Hola y se aplica ese servicios de tooall de control de acceso en el grupo de recursos. 

Hay dos toounderstand conceptos principales cuando se trabaja con control de acceso basado en roles:

* Definiciones de rol: describen un conjunto de permisos y se pueden usar en muchas asignaciones.
* Las asignaciones de roles: asocian una definición con una identidad (usuario o grupo) para un ámbito determinado (suscripción, grupo de recursos o recurso). asignación de Hola se hereda en ámbitos inferiores.

Puede agregar plataforma definida por el toopre de los usuarios y roles específicos de recursos. Por ejemplo, puede aprovechar las ventajas de función predefinido de hello denominada lector que permite que los usuarios tooview recursos, pero no modificarlas. Agregar usuarios de su organización que necesiten este tipo de rol de lector de acceso toohello y aplicar la suscripción de toohello de rol de hello, el grupo de recursos o el recurso.

Azure proporciona Hola siguientes cuatro roles de plataforma:

1. Propietario: puede administrar todo, incluido el acceso.
2. Colaborador: puede administrar todo, excepto el acceso.
3. Lector: puede ver todo, pero no realizar cambios.
4. Administrador de acceso de usuario: puede administrar los recursos de tooAzure de acceso de usuario

Azure también proporciona varios roles específicos de los recursos. Algunos comunes son:

1. Puede administrar máquinas virtuales pero no conceder acceso a toothem y no puede administrar Hola virtual red o almacenamiento cuenta toowhich están conectados colaborador de la máquina virtual:
2. Colaborador de red - puede administrar todos los recursos de red, pero no conceder acceso toothem
3. Colaborador de la cuenta de almacenamiento - puede administrar cuentas de almacenamiento, pero no conceder acceso toothem
4. Colaborador de SQL Server: puede administrar bases de datos y servidores SQL, pero no las directivas relacionadas con la seguridad.
5. Sitio Web colaborador - puede administrar sitios Web, pero no Hola toowhich de planes de web están conectados

Para hello lista completa de los roles y las acciones permitidas, consulte [RBAC: integrada en Roles](../active-directory/role-based-access-built-in-roles.md). Para más información sobre el control de acceso basado en roles, consulte [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md). 

En algunos casos desee toorun código o script que obtiene acceso a recursos, pero no desea toorun en las credenciales del usuario. En su lugar, desea toocreate una identidad que se llama a un servicio principal para la aplicación hello y asignar Hola rol adecuado para la entidad de servicio de Hola. El Administrador de recursos permite toocreate credenciales para la aplicación hello y autenticar mediante programación aplicación hello. toolearn acerca de cómo crear entidades de servicio, consulte uno de los temas siguientes:

* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure](resource-group-authenticate-service-principal.md)
* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure](resource-group-authenticate-service-principal-cli.md)
* [Usar la aplicación de portal toocreate Azure Active Directory y la entidad de servicio que puede tener acceso a recursos](resource-group-create-service-principal-portal.md)

Se pueden bloquear explícitamente los recursos críticos tooprevent los usuarios eliminen o modificarlos. Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Registros de actividad
Resource Manager registra todas las operaciones que crean, modifican o eliminan un recurso. Puede usar toofind de registros de actividad de hello un error para solucionar el problema o toomonitor cómo un usuario de su organización modifica un recurso. seleccionar registros de hello toosee, **registros de actividad** Hola **configuración** hoja para un grupo de recursos. Puede filtrar los registros de Hola por muchos valores diferentes, incluidos qué operación de hello iniciada por el usuario. Para obtener información sobre cómo trabajar con registros de actividad de hello, consulte [toomanage Azure de registros de actividad de la vista recursos](resource-group-audit.md).

## <a name="customized-policies"></a>Directivas personalizadas
El Administrador de recursos permite toocreate personalizado directivas para administrar los recursos. tipos de Hola de directivas que cree pueden incluir diversos escenarios. Puede exigir que los recursos sigan una convención de nomenclatura, limitar los tipos e instancias de recursos que se pueden implementar o limitar las regiones que pueden hospedar un tipo de recurso. Puede requerir un valor de etiqueta sobre la facturación de tooorganize de recursos por departamentos. Crear directivas toohelp reducir los costos y mantener la coherencia de la suscripción. 

Puede definir directivas con JSON y, a continuación, aplicarlas mediante su suscripción o en un grupo de recursos. Las directivas son diferentes de control de acceso basado en roles porque son tipos tooresource aplicada.

Hola de ejemplo siguiente muestra una directiva que garantice la coherencia entre las etiquetas mediante la especificación de que todos los recursos incluyen una etiqueta costCenter.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Hay muchos más tipos de directivas que puede crear. Para obtener más información, consulte [recursos toomanage de directiva de uso y controlar el acceso](resource-manager-policy.md).

## <a name="sdks"></a>SDK
Los SDK de Azure están disponibles para múltiples lenguajes y plataformas. Cada una de estas implementaciones de lenguajes está disponibles a través de su administrador de paquetes del ecosistema y GitHub.

Presentamos los repositorios de SDK de código abierto. Agradecemos todo tipo de comentarios, problemas y solicitudes de extracción.

* [SDK de Azure para .NET](https://github.com/Azure/azure-sdk-for-net)
* [Bibliotecas de administración de Azure para Java](https://github.com/Azure/azure-sdk-for-java)
* [SDK de Azure para Node.js](https://github.com/Azure/azure-sdk-for-node)
* [SDK de Azure para PHP](https://github.com/Azure/azure-sdk-for-php)
* [SDK de Azure para Python](https://github.com/Azure/azure-sdk-for-python)
* [SDK de Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Para obtener información acerca del uso de estos lenguajes sus los recursos, consulte:

* [Azure para desarrolladores de .NET](/dotnet/azure/?view=azure-dotnet)
* [Azure para desarrolladores de Java](/java/azure/)
* [Azure para desarrolladores de Node.js](/nodejs/azure/)
* [Azure para desarrolladores de Python](/python/azure/)

> [!NOTE]
> Si Hola SDK no ofrece funcionalidad de hello necesario, también puede llamar a toohello [API de REST de Azure](https://docs.microsoft.com/rest/api/resources/) directamente.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Para una tooworking introducción sencilla con las plantillas, consulte [exportar una plantilla de Azure Resource Manager de los recursos existentes](resource-manager-export-template.md).
* Para ver un tutorial más detallado sobre la creación de una plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).
* funciones de hello toounderstand se pueden usar en una plantilla, consulte [funciones de plantilla](resource-group-template-functions.md)
* Para más información sobre el uso de Visual Studio con Resource Manager, consulte [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

La siguiente es una demostración de esta introducción.

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
