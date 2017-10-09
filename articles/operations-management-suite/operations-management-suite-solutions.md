---
title: aaaSolutions en Operations Management Suite (OMS) | Documentos de Microsoft
description: "Soluciones de amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar área de trabajo OMS tootheir.  En este artículo se proporciona información sobre cómo los clientes y asociados pueden crear soluciones personalizadas."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Uso de soluciones de administración en Operations Management Suite (OMS) (versión preliminar)
> [!NOTE]
> La versión de la documentación de las soluciones de administración de OMS está actualmente en fase preliminar.    
> 
> 

Soluciones de administración de amplían la funcionalidad de Hola de Operations Management Suite (OMS) proporcionando escenarios de administración empaquetada que los clientes pueden agregar entorno de tootheir.  Además demasiado[soluciones proporcionadas por Microsoft](../log-analytics/log-analytics-add-solutions.md), socios y clientes pueden crear toobe de soluciones de administración usa en su propio entorno o estará toocustomers disponible a través de la Comunidad de Hola.

## <a name="finding-and-installing-management-solutions"></a>Búsqueda e instalación de soluciones de administración
Existen varios métodos para buscar e instalar soluciones de administración como se describe en las secciones siguientes de Hola.

### <a name="azure-marketplace"></a>Azure Marketplace
Soluciones de administración proporcionan por Microsoft y asociados de confianza pueden instalarse desde hello Azure Marketplace en hello portal de Azure.

1. Inicie sesión en toohello portal de Azure.
2. En el panel izquierdo de hello, seleccione **más servicios**.
3. Ya sea descienda demasiado**soluciones** o tipo *soluciones* en hello **filtro** cuadro de diálogo.
4. Haga clic en hello **+ agregar** botón.
5. Buscar soluciones que le interesa ya sea mediante la exploración, haga clic en hello **filtro** botón o escribiendo en hello **búsqueda todo** cuadro.
6. Haga clic en un tooview de elemento de marketplace su información detallada.
7. Haga clic en **crear** tooopen hello **Agregar solución** panel.
8. Podrá toorequired solicitadas información como hello [OMS área de trabajo y la cuenta de automatización](#oms-workspace-and-automation-account) además toovalues en cualquier parámetro Hola solución.
9. Haga clic en **crear** solución de hello tooinstall.

### <a name="oms-portal"></a>Portal de OMS
Soluciones de administración de Microsoft pueden instalarse desde Hola Galería de soluciones en el portal de OMS Hola.

1. Inicie sesión en toohello portal de OMS.
2. Haga clic en hello **Galería de soluciones** icono.
3. En la página de la Galería de soluciones de OMS de hello, obtenga información acerca de cada solución disponible. Haga clic en el nombre de Hola de solución de Hola que desea tooadd tooOMS.
4. En la página hello para la solución de Hola que eligió, se muestra información detallada sobre solución de Hola. Haga clic en **Agregar**.
5. Un icono nuevo para la solución de Hola que ha agregado aparece en Hola página información general de OMS y puede empezar a usarlo una vez el servicio OMS Hola procese los datos.

### <a name="azure-quickstart-templates"></a>Plantillas de inicio rápido de Azure
Los miembros de la Comunidad de hello pueden enviar tooAzure de soluciones de administración plantillas de inicio rápido.  Puede descargar estas plantillas para la instalación más adelante o inspeccionarlos toolearn cómo demasiado[crear sus propias soluciones](#creating-a-solution).

1. Siga el proceso de hello descrito en [OMS área de trabajo y la cuenta de automatización](#oms-workspace-and-automation-account) toolink un área de trabajo y la cuenta.
2. Vaya demasiado[plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).  
3. Busque una solución que le interese.
4. Seleccione solución Hola de hello resultados tooview sus detalles.
5. Haga clic en hello **implementar tooAzure** botón.
6. Es posible que información tooprovide solicitadas como grupo de recursos de Hola y la ubicación en toovalues de suma para los parámetros de solución de Hola.
7. Haga clic en **compra** solución de hello tooinstall.

### <a name="deploy-azure-resource-manager-template"></a>Implementación de plantilla de Azure Resource Manager
Soluciones que se obtiene de la Comunidad de Hola o que se [crear usted mismo](#creating-a-solution) se implementan como una plantilla de administrador de recursos, y puede utilizar cualquiera de los métodos estándar para hello [implementar una plantilla de](../azure-resource-manager/resource-group-template-deploy-portal.md).  Tenga en cuenta que antes de instalar la solución de hello, debe crear y vincular hello [OMS área de trabajo y la cuenta de automatización](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>Área de trabajo de OMS y cuenta de Automation
La mayoría de soluciones de administración requiere un [área de trabajo OMS](../log-analytics/log-analytics-manage-access.md) toocontain vistas y un [cuenta de automatización](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks y recursos relacionados. área de trabajo de Hola y cuenta debe cumplir Hola según los requisitos.

* Una solución solo puede utilizar un área de trabajo de OMS y una cuenta de Automation.  
* Hello área de trabajo OMS y cuenta de automatización que se usa una solución deben estar vinculado tooone otro. Un área de trabajo OMS solo puede ser vinculado tooone cuenta de automatización y una cuenta de automatización solo puede ser el área de trabajo OMS tooone vinculado.
* toobe vinculado, Hola área de trabajo OMS y automatización de la cuenta debe estar en Hola mismo grupo de recursos y la región.  excepción de Hello es un área de trabajo OMS en la región Este de EE. y y cuenta de automatización de la zona horaria del Pacífico oriental 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Creación de un vínculo entre un área de trabajo de OMS y una cuenta de Automation
Cómo especificar el área de trabajo OMS de Hola y cuenta de automatización depende del método de instalación de hello para la solución.

* Al instalar una solución de Microsoft a través del portal de OMS hello, está instalado en el área de trabajo OMS actual hello y no hay ninguna cuenta de automatización es necesaria.
* Al instalar una solución a través de hello Azure Marketplace, se le pedirá una cuenta de automatización y el área de trabajo OMS y vínculo Hola entre ellos se crea automáticamente.  
* Para las soluciones fuera de hello Azure Marketplace, debe vincular el área de trabajo OMS de Hola y cuenta de automatización antes de instalar la solución de Hola.  Para ello, puede seleccionar cualquier solución de hello Azure Marketplace y seleccionar área de trabajo OMS de Hola y cuenta de automatización.  No es necesario tooactually instalar soluciones de hello porque el vínculo de Hola se creará en cuanto se seleccionan el área de trabajo OMS de Hola y cuenta de automatización.  Una vez que se crea el vínculo de hello, puede usar esa área de trabajo OMS y la cuenta de automatización para cualquier solución. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Comprobar Hola vínculo entre un área de trabajo OMS y la cuenta de automatización
Puede comprobar Hola vínculo entre un área de trabajo OMS y una cuenta de automatización mediante Hola siguiendo el procedimiento.

1. Seleccione la cuenta de automatización de Hola Hola portal de Azure.
2. Desplazar hacia abajo de toohello de hello **configuración** panel.
3. Si hay una sección denominada **recursos de OMS** en hello **configuración** panel y, a continuación, esta cuenta es el área de trabajo OMS de tooan adjunto.
4. Seleccione **área de trabajo** detalles de hello tooview del área de trabajo OMS Hola vinculado toothis cuenta de automatización.

## <a name="listing-management-solutions"></a>Visualización de soluciones de administración
Usar hello después de soluciones de administración de procedimiento tootooview hello en hello áreas de trabajo vinculado tooyour suscripción de Azure.

1. Inicie sesión en toohello portal de Azure.
2. En el panel izquierdo de hello, seleccione **más servicios**.
3. Ya sea descienda demasiado**soluciones** o tipo *soluciones* en hello **filtro** cuadro de diálogo.
4. Se mostrarán las soluciones instaladas en todas las áreas de trabajo.

Tenga en cuenta que puede ver solo las soluciones de Microsoft hello instaladas en hello área de trabajo actual mediante el portal de OMS Hola.

## <a name="removing-a-management-solution"></a>Eliminación de una solución de administración
Cuando se quita una solución de administración, también se quitan todos los recursos de solución de Hola.  

1. Localizar soluciones de hello en hello Azure portal mediante el procedimiento de hello en [enumerar soluciones](#listing-solutions).
2. Seleccione Hola solución tooremove.
3. Haga clic en hello **eliminar** botón.

## <a name="creating-a-management-solution"></a>Creación de una solución de administración
Hay disponible una guía completa sobre cómo crear soluciones de administración en el artículo sobre [creación de soluciones de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Pasos siguientes
* Búsqueda de [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates) para obtener ejemplos de diferentes plantillas de Resource Manager.
* Cree sus propias [soluciones de administración](operations-management-suite-solutions-creating.md).

