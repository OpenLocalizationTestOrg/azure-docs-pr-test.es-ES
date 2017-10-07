---
title: aaaGet a trabajar con plantillas privadas | Documentos de Microsoft
description: Agregar, administrar y compartir sus plantillas privadas con hello portal de Azure, hello Azure CLI o PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Empezar a trabajar con plantillas privadas en hello Portal de Azure
Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) plantilla es una plantilla declarativa usa toodefine la implementación. Puede definir hello toodeploy de recursos para una solución y especificar los parámetros y variables que le permiten tooinput valores para diferentes entornos. Hello plantilla consta de JSON y expresiones que se pueden utilizar valores de tooconstruct para su implementación.

Puede usar nueva hello **plantillas** capacidad en hello [Portal de Azure](https://portal.azure.com) junto con hello **Microsoft.Gallery** proveedor de recursos como una extensión de hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate de los usuarios, administrar e implementar plantillas privadas desde una biblioteca personal.

Este documento le guía a través de agregar, administrar y compartir una privada **plantilla** utilizando Hola Portal de Azure.

## <a name="guidance"></a>Guía
Hello las sugerencias siguientes le ayudará a sacar el máximo de **plantillas** cuando se trabaja con las soluciones:

* Una **plantilla** en un recurso de encapsulamiento que contiene una plantilla de Resource Manager y otros metadatos. Se comporta de forma muy similar tooan elemento Hola Marketplace. diferencia clave Hello es que es un elemento privado como elementos de Marketplace de toohello lugar públicos.
* Hola **plantillas** biblioteca funciona bien para los usuarios que necesitan toocustomize sus implementaciones.
* **plantillas** son apropiadas para los usuarios que necesitan disponer de un repositorio sencillo dentro de Azure.
* Para empezar, utilice una plantilla de Resource Manager existente. Para buscar plantillas, utilice [github](https://github.com/Azure/azure-quickstart-templates) o [Exportar plantilla](../azure-resource-manager/resource-manager-export-template.md) desde un grupo de recursos existente.
* **Plantillas de** toohello relacionados para usuarios que publica. nombre del publicador Hello es tooeveryone visible que tiene acceso de lectura tooit.
* **plantillas** son recursos de Resource Manager y, una vez publicadas, su nombre no se puede modificar.

## <a name="add-a-template-resource"></a>Adición de un recurso de plantilla
Hay dos toocreate formas un **plantilla** recursos Hola portal de Azure.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Método 1: Creación de un nuevo recurso de plantilla a partir de un grupo de recursos en funcionamiento
1. Navegar por grupo de recursos existente tooan en hello Portal de Azure. En **Configuración**, seleccione **Exportar plantilla**.
2. Una vez que se exporta la plantilla de administrador de recursos de hello, usar hello **Guardar plantilla** toosave de botón toohello **plantillas** repositorio. Para más detalles sobre la exportación de plantillas, haga clic [aquí](../azure-resource-manager/resource-manager-export-template.md).
   <br /><br />
   ![Exportación de grupo de recursos](media/rg-export-portal1.PNG)  <br />
3. Seleccione hello **guardar tooTemplate** botón de comando.
   <br /><br />
4. Escriba Hola siguiente información:
   
   * Nombre: nombre del objeto de plantilla de hello (Nota: se trata de un nombre según el Administrador de recursos de Azure. por lo que se aplicarán todas las restricciones de nomenclatura, y no se puede cambiar una vez creado).
   * Descripción: resumen rápido acerca de la plantilla de Hola.
     
     ![Guardar plantilla](media/save-template-portal1.PNG)  <br />
5. Haga clic en **Guardar**.
   
   > [!NOTE]
   > Hello hoja de plantilla de exportación muestra notificaciones cuando hello plantilla exportada del Administrador de recursos tiene errores, pero se seguirá toosave capaz de este toohello de plantilla plantillas de administrador de recursos. Asegúrese de comprobar y corregir problemas de las plantillas de cualquier administrador de recursos antes de volver a implementar Hola exporta plantilla del Administrador de recursos.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Método 2 : Agregar un nuevo recurso de plantilla desde Examinar
También puede agregar un nuevo **plantilla** desde cero mediante Hola + Agregar botón de comando en **examinar > plantillas**. Deberá tooprovide un nombre, descripción y Hola plantilla JSON del Administrador de recursos.

![Agregar plantilla](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery es un proveedor de recursos de Azure basado en un inquilino. Hello recurso de plantilla es usuario toohello relacionados que lo creó. No es tooany relacionados de suscripción específica. Una suscripción debe toobe elegido solo cuando se implementa una plantilla.
> 
> 

## <a name="view-template-resources"></a>Consulta de los recursos de plantilla
Todos los **plantillas** tooyou disponible puede verse en **examinar > plantillas**. Aquí encontrará las **plantillas** que ha creado, así como las plantillas que han compartido con usted y que tienen distintos niveles de permisos. Para obtener más detalles en hello [el control de acceso](#access-control-for-a-tenant-resource-provider) sección más adelante.

![Ver plantilla](media/view-template-portal1.PNG)  <br />

Puede ver detalles de Hola de un **plantilla** haciendo clic en un elemento de lista de Hola.

![Ver plantilla](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Edición de un recurso de plantilla
Puede iniciar flujo de edición de Hola para un **plantilla** haga clic en el elemento de hello en la lista de examinación de Hola o eligiendo el botón de comando de edición de Hola.

![Editar plantilla](media/edit-template-portal1a.PNG)  <br />

Puede editar la descripción de Hola o texto de la plantilla de administrador de recursos. No se puede editar el nombre de hello ya que es un nombre de recursos del Administrador de recursos. Al editar plantilla de administrador de recursos de hello JSON se validará tooensure que es un valor JSON válido. Elija **Aceptar** y, a continuación, **guardar** toosave la plantilla actualizada.

![Editar plantilla](media/edit-template-portal2a.PNG)  <br />

Una vez Hola **plantilla** se guarda, verá una notificación de confirmación.

![Editar plantilla](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Implementación de un recurso de plantilla
Puede implementar cualquier **plantilla** en la que tenga permisos de **lectura**. flujo de implementación de Hello inicia la hoja de implementación de plantilla de Azure estándar Hola. Rellene los valores de hello para tooproceed de parámetros de plantilla de hello Administrador de recursos con la implementación de Hola.

![Implementar plantilla](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Uso compartido de un recurso de plantilla
Puede compartir con sus compañeros los recursos de **plantilla** . Uso compartido se comporta del mismo modo demasiado[asignación de roles para cualquier recurso de Azure](../active-directory/role-based-access-control-configure.md). Hola **plantilla** propietario proporciona permisos a los usuarios de tooother que pueden interactuar con un recurso de plantilla. Hola persona o grupo de personas compartir hello **plantilla** con será plantilla de administrador de recursos de toosee capaz de Hola y sus propiedades de la galería.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Control de acceso para los recursos de hello Microsoft.Gallery
| Rol | Permisos |
| --- | --- |
| Propietario |Permite el control total en el recurso de plantilla de hello incluidos los recursos compartidos |
| Lector |Permite leer y Execute(Deploy) en hello recurso de plantilla |
| Colaborador |Permite editar y eliminar permiso en hello recurso de plantilla. Usuario no puede compartir Hola plantilla con otros usuarios |

Seleccione **recurso compartido** en elemento de exploración de hello haciendo clic o en la hoja de la vista de Hola de un elemento específico. De este modo, se iniciará un proceso que le permitirá compartir el recurso de plantilla.

![Compartir plantilla](media/share-template-portal1a.png)  <br />

 Ahora puede elegir un rol y un tooa de acceso de tooprovide usuario o grupo determinado **plantilla**. roles disponibles Hola son lector, Colaborador y propietario. Para obtener más detalles en hello [el control de acceso](#access-control-for-a-tenant-resource-provider) sección anterior.

![Compartir plantilla](media/share-template-portal2b.png)  <br />

![Compartir plantilla](media/share-template-portal3b.png)  <br />

Haga clic en **Seleccionar** y en **Aceptar**. Ahora puede ver Hola usuarios o grupos que agregó toohello recursos.

![Compartir plantilla](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Una plantilla solo puede compartirse con usuarios y grupos en hello mismo inquilino de Azure Active Directory. Si comparte una plantilla con una dirección de correo electrónico que no está en su inquilino, se enviará una invitación pidiendo a inquilino de Hola Hola usuario toojoin como invitado.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [creación de plantillas](../azure-resource-manager/resource-group-authoring-templates.md)
* funciones de hello toounderstand se pueden usar en una plantilla de administrador de recursos, consulte [funciones de plantilla](../azure-resource-manager/resource-group-template-functions.md)
* Para obtener instrucciones sobre cómo diseñar las plantillas, consulte [Prácticas recomendadas para diseñar plantillas del Administrador de recursos de Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

