---
title: "aaaLog características de análisis de proveedores de servicios | Documentos de Microsoft"
description: Log Analytics puede ayudar a proveedores de servicios administrados (MSP), grandes empresas, proveedores de software independientes (ISV) y proveedores de servicios de hospedaje a administrar y supervisar servidores en infraestructuras locales en la nube del cliente.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Características de Log Analytics para proveedores de servicios
Log Analytics puede ayudar a proveedores de servicios administrados (MSP), grandes empresas, proveedores de software independientes (ISV) y proveedores de servicios de hospedaje a administrar y supervisar servidores en infraestructuras locales en la nube del cliente. 

Las grandes empresas comparten muchas similitudes con los proveedores de servicios, especialmente cuando hay un equipo de TI centralizado que es responsable de la administración de TI de muchas unidades de negocio diferentes. Para simplificar, este documento usa el término hello *proveedor de servicios* pero hello misma funcionalidad también está disponible para las empresas y otros clientes.

## <a name="cloud-solution-provider"></a>Proveedor de soluciones en la nube
Para los socios y proveedores de servicios que forman parte del programa Hola a [proveedor de soluciones de nube (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) programa, análisis de registros es uno de hello Azure servicios disponibles en una suscripción de CSP. 

Análisis de registros, Hola siguiendo las capacidades está habilitado en *Cloud Solution Provider* suscripciones.

Los *proveedores de soluciones en la nube* pueden realizar las siguientes tareas:

* Crear áreas de trabajo de Log Analytics en una suscripción de inquilino (cliente).
* Acceder a las áreas de trabajo que creen los inquilinos. 
* Agregar y quitar usuario acceso toohello área de trabajo mediante administración de usuarios de Azure. Cuando en el área de trabajo de un inquilino Hola OMS no está disponible la página de administración de usuario de portal hello en la configuración
  * Análisis de registros no admiten acceso basado en roles aún - conceder a un usuario `reader` permiso Hola portal de Azure les permite toomake cambios de configuración en el portal de OMS Hola

toolog suscripción de inquilino tooa, deberá identificador del inquilino toospecify Hola. identificador del inquilino de Hello es a menudo esa última parte de hello toosign de dirección usada por correo electrónico en.

* En el portal de OMS de hello, agregue `?tenant=contoso.com` en dirección URL de hello para el portal de Hola. Por ejemplo: `mms.microsoft.com/?tenant=contoso.com`
* En PowerShell, use hello `-Tenant contoso.com` parámetro al usar `Add-AzureRmAccount` cmdlet
* identificador del inquilino Hola se agrega automáticamente al usar hello `OMS portal` vínculo de hello tooopen portal Azure e inicie sesión toohello portal de OMS para el área de trabajo de hello seleccionado

Los *clientes* de un proveedor de soluciones en la nube, puede realizar las siguientes tareas:

* Crear áreas de trabajo de Log Analytics en una suscripción de CSP.
* Áreas de trabajo de acceso creadas por hello CSP
  * Hola de uso `OMS portal` vínculo de hello tooopen portal Azure e inicie sesión toohello portal de OMS para el área de trabajo de hello seleccionado
* Ver y usar la página de administración del usuario hello en la configuración en el portal de OMS Hola

> [!NOTE]
> Hola incluye la copia de seguridad y soluciones de Site Recovery para análisis de registros no pueda tooconnect tooa el almacén de servicios de recuperación y no se puede configurar en una suscripción de CSP. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Administrar a varios clientes mediante Log Analytics.
Se recomienda crear un área de trabajo de Log Analytics para cada cliente que administre. Un área de trabajo de Log Analytics proporciona lo siguiente:

* Una ubicación geográfica para toobe datos almacenado. 
* Granularidad para la facturación 
* Aislamiento de datos 
* Configuración única

Mediante la creación de un área de trabajo por cliente, son tookeep capaz de los datos de cada cliente independientes y también un seguimiento del uso de Hola de cada cliente.

Obtener más detalles sobre cuándo y por qué toocreate varias áreas de trabajo se describe en [administrar acceso toolog análisis](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Creación y configuración de áreas de trabajo de cliente se pueden automatizar mediante [PowerShell](log-analytics-powershell-workspace-configuration.md), [plantillas del Administrador de recursos](log-analytics-template-workspace-configuration.md), o mediante hello [API de REST](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

uso de Hola de plantillas de administrador de recursos para la configuración de área de trabajo le permite toohave una configuración maestra que puede ser usado toocreate y configurar áreas de trabajo. Puede estar seguro de que tal y como áreas de trabajo se crean para los clientes que estén automáticamente configurada tooyour requisitos. Al actualizar sus requisitos, plantilla de Hola se actualiza y, a continuación, vuelve a aplicar áreas de trabajo existentes de Hola. Este proceso garantiza que incluso los espacios de trabajo existentes cumplan los nuevos estándares.    

Al administrar varias áreas de trabajo de análisis de registros, se recomienda la integración de cada área de trabajo con el sistema de vales existente / hello utilizando la consola del operador [alertas](log-analytics-alerts.md) funcionalidad. Mediante la integración con los sistemas existentes, personal de soporte técnico puede continuar toofollow sus procesos familiarizados. Análisis de registros con regularidad comprueba cada área de trabajo con criterios de alerta de hello que especifica y genera una alerta cuando es necesario hacer nada.

Para obtener vistas personalizadas de datos, use hello [panel](../azure-portal/azure-portal-dashboards.md) capacidad Hola portal de Azure.  

Nivel ejecutivo de informes que resuman los datos a través de áreas de trabajo que se puede usar Hola integración entre el análisis de registros y [PowerBI](log-analytics-powerbi.md). Si necesita toointegrate con otro sistema de informes, puede usar hello API de búsqueda (a través de PowerShell o [REST](log-analytics-log-search-api.md)) toorun consultas y exportar los resultados de búsqueda.

## <a name="next-steps"></a>Pasos siguientes
* Automatice la creación y configuración de áreas de trabajo con [plantillas de Resource Manager](log-analytics-template-workspace-configuration.md).
* Automatice la creación de áreas de trabajo con [PowerShell](log-analytics-powershell-workspace-configuration.md). 
* Use [alertas](log-analytics-alerts.md) toointegrate con los sistemas existentes
* Genere informes de resumen con [PowerBI](log-analytics-powerbi.md).

