---
title: "aaaManaging datos de automatización de Azure | Documentos de Microsoft"
description: "Este artículo contiene varios temas para administrar un entorno de Automatización de Azure.  Actualmente incluye la retención de datos y la realización de copias de seguridad de la recuperación ante desastres en Automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Administración de datos de Automatización de Azure
Este artículo contiene varios temas para administrar un entorno de Automatización de Azure.

## <a name="data-retention"></a>Retención de datos
Cuando elimina un recurso en Automatización de Azure, se conserva durante 90 días para fines de auditoría antes de quitarlo de manera permanente.  No se puede ver o usar recursos de Hola durante este tiempo.  Esta directiva también aplica tooresources que pertenecen tooan cuenta de automatización que se elimina.

Automatización de Azure elimina automáticamente y quita de manera permanente los trabajos que tengan más de 90 días.

Hello en la tabla siguiente resume la directiva de retención de Hola para los distintos recursos.

| Datos | Directiva |
|:--- |:--- |
| Cuentas |Quita de forma permanente 90 días después de que un usuario elimine cuenta Hola. |
| Recursos |Quita de forma permanente 90 días después de activos de Hola se eliminan un usuario o 90 días después de hello cuenta que contiene el recurso de Hola se elimina un usuario. |
| Módulos |Quita de forma permanente 90 días después de que un usuario elimine el módulo de Hola o 90 días después de hello cuenta que contiene el módulo de Hola se elimina un usuario. |
| Runbooks |Quita de forma permanente 90 días después de que un usuario elimine el recurso de Hola o 90 días después de hello cuenta que incluye recursos de Hola se elimina un usuario. |
| Trabajos |Se eliminan y quitan de manera permanente 90 días después de la última modificación. Esto podría ser después trabajo Hola completa, se detiene o se suspende. |
| Configuraciones de nodo y archivos MOF |La configuración de nodo anterior se quita de forma permanente 90 días después de que se genere una nueva configuración. |
| Nodos de DSC |Quita de forma permanente 90 días después de que el nodo de Hola se anula el registro de cuenta de automatización mediante el portal de Azure o hello [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) cmdlet de Windows PowerShell. Los nodos se quitan permanentemente 90 días después de la cuenta de hello que contiene el nodo de Hola se elimina un usuario. |
| Informes de nodo |Se quitan de forma permanente 90 días después de que se genere un nuevo informe para ese nodo. |

Directiva de retención de Hola aplica a los usuarios de tooall y actualmente no se puede personalizar.

Sin embargo, si necesita tooretain datos durante un período más largo de tiempo, puede reenviar tooLog de registros de trabajo de runbook análisis.  Para obtener más información, consulte [reenviar tooOMS de datos de trabajo de automatización de Azure Log Analytics](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Copia de seguridad de Automatización de Azure
Cuando se elimina una cuenta de automatización de Microsoft Azure, se eliminan todos los objetos de cuenta de hello incluidos runbooks, módulos, configuraciones, configuración, trabajos y activos. no se puede recuperar objetos de Hello cuando se elimina la cuenta de hello.  Puede usar Hola después el contenido de hello toobackup de información de su cuenta de automatización antes de eliminarlo. 

### <a name="runbooks"></a>Runbooks
Puede exportar los archivos de tooscript de runbooks mediante el Portal de administración de Azure de Hola o hello [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) cmdlet de Windows PowerShell.  Es posible importar estos archivos de script a otra cuenta de automatización, tal como se describe en [Creación o importación de un runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Módulos de integración
No es posible exportar módulos de integración desde Automatización de Azure.  Debe asegurarse de que están disponibles fuera de la cuenta de automatización de Hola.

### <a name="assets"></a>Recursos
No es posible exportar [recursos](https://msdn.microsoft.com/library/dn939988.aspx) desde Automatización de Azure.  Con hello Portal de administración de Azure, debe observar detalles de Hola de variables, las credenciales, certificados, conexiones y programaciones.  Luego debe crear manualmente todos los recursos utilizados por los runbooks que importa a otra automatización.

Puede usar [cmdlets de Azure](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve detalles del activos sin cifrar y guardan para futuras hacer referencia o crear activos equivalente en otra cuenta de automatización.

No se puede recuperar el valor de Hola para las variables cifradas o campo de contraseña de Hola de credenciales mediante cmdlets.  Si no conoce estos valores, se puede recuperar desde un runbook con hello [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) y [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) actividades.

No es posible exportar certificados desde Automatización de Azure.  Debe asegurarse de que todos los certificados estén disponibles fuera de Azure.

### <a name="dsc-configurations"></a>Configuraciones DSC
Puede exportar los archivos de tooscript de las configuraciones con hello Portal de administración de Azure o hello [AzureRmAutomationDscConfiguration de exportación](https://msdn.microsoft.com/library/mt603485.aspx) cmdlet de Windows PowerShell. Estas configuraciones se pueden importar y usar en otra cuenta de automatización.

## <a name="geo-replication-in-azure-automation"></a>Replicación geográfica en Automatización de Azure
Replicación geográfica, estándar en cuentas de automatización de Azure, copia cuenta datos tooa región geográfica diferente para redundancia. Puede elegir una región principal al configurar la cuenta y, a continuación, una región secundaria se asigna tooit automáticamente. los datos secundarios Hello, copiados de la región principal de hello, se actualizan continuamente en el caso de pérdida de datos.  

Hello en la tabla siguiente muestra hello emparejamientos de región principal y secundaria disponible.

| Principal | Secundario |
| --- | --- |
| Centro-Sur de EE. UU |Centro-Norte de EE. UU |
| Este de EE. UU. - 2 |Central EE. UU.: |
| Europa occidental |Europa del Norte |
| Sudeste de Asia |Asia oriental |
| Este de Japón |Oeste de Japón |

En el caso poco probable de Hola que se pierdan datos de una región principal, Microsoft intenta toorecover lo. Si no se puede recuperar datos principal de hello, a continuación, se realiza la conmutación por error geográfica y hello clientes afectados le notificará sobre esto a través de su suscripción.

