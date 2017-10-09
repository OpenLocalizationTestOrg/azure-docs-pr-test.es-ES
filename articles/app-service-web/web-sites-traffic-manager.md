---
title: "aaaControlling tráfico de aplicación web de Azure con Azure Traffic Manager"
description: "Este artículo proporciona información de resumen para el Administrador de tráfico de Azure en lo referente a las aplicaciones web tooAzure."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Control del tráfico de aplicaciones web de Azure con el Administrador de tráfico de Azure
> [!NOTE]
> Este artículo proporciona información resumida de Microsoft Azure Traffic Manager en lo referente a las aplicaciones tooAzure aplicación de servicio Web. Puede encontrar más información acerca de Azure Traffic Manager propio visitando Hola vínculos que aparecen al final de Hola de este artículo.
> 
> 

## <a name="introduction"></a>Introducción
Puede usar Azure toocontrol Traffic Manager cómo las solicitudes de los clientes web son aplicaciones distribuidas tooweb en el servicio de aplicación de Azure. Cuando los extremos de la aplicación web se agregan tooa perfil de Traffic Manager de Azure, Azure Traffic Manager realiza un seguimiento de estado de Hola de las aplicaciones web (en ejecución, detenido o eliminadas) por lo que puede decidir cuáles de esos puntos de conexión deben recibir el tráfico.

## <a name="load-balancing-methods"></a>Métodos de equilibrio de carga
El Administrador de tráfico de Azure utiliza tres métodos de equilibrio de carga distintos. Se describen en hello conforme a la lista que pertenecen a las aplicaciones web tooAzure.

* **Conmutación por error**: si tiene clones de aplicación web en diferentes regiones, puede usar este tooservice de aplicación de un sitio web de método tooconfigure todo el tráfico de cliente web y configurar otra aplicación web en un tooservice de otra región de tráfico en mayúsculas Hola primera aplicación de web deja de estar disponible.
* **Operación por turnos**: Si tienes clones de aplicación web en diferentes regiones, puede usar este tráfico de toodistribute método igualmente a través de las aplicaciones web hello en regiones diferentes.
* **Rendimiento**: Hola método rendimiento distribuye el tráfico en función de hello tooclients de tiempo de ida y vuelta más corta. Hola método rendimiento puede utilizarse para las aplicaciones web dentro de hello misma región o en regiones diferentes.

## <a name="web-apps-and-traffic-manager-profiles"></a>Aplicaciones web y perfiles del Administrador de tráfico
control de hello tooconfigure de tráfico de aplicación web, crear un perfil en el administrador del tráfico de Azure que utiliza uno de los métodos descritos anteriormente de equilibrio de carga de hello tres y, a continuación, agregar los extremos de hello (en este caso, las aplicaciones web) que se desea toocontrol tráfico toohello perfil. El estado de las aplicaciones web (en ejecución, detenido o eliminado) se toohello con regularidad comunicado del perfil para que Azure Traffic Manager puede dirigir el tráfico en consecuencia.

Al usar el Administrador de tráfico de Azure con Azure, tenga en Hola de cuenta siguientes puntos:

* Para implementaciones solo de aplicación web dentro de hello misma región, las aplicaciones Web ya proporciona la funcionalidad de conmutación por error y round-robin sin modo de aplicación de tooweb de tener en cuenta.
* Para las implementaciones en Hola misma región que usan las aplicaciones Web junto con otro servicio de nube de Azure, puede combinar ambos tipos de escenarios híbridos de tooenable de puntos de conexión.
* Solo puede especificar un extremo de aplicación web por región en un perfil. Cuando se selecciona una aplicación web como un extremo para una región, Hola restantes aplicaciones web en esa región dejan de estar disponibles para la selección de ese perfil.
* Hola web extremos de la aplicación que se especifican en un perfil de Traffic Manager de Azure aparecerá en hello **nombres de dominio** sección en la página de configuración de hello para la aplicación web de hello en el perfil de hello, pero no se podrán configurar no existe.
* Después de agregar un perfil de tooa de aplicación web, Hola **dirección URL del sitio** en el panel de web Hola Hola página del portal de la aplicación mostrará Hola dominio personalizado dirección URL de aplicación web de hello si ha configurado uno. En caso contrario, se mostrará Hola dirección URL del perfil de Traffic Manager (por ejemplo, `contoso.trafficmgr.com`). Ambos Hola nombre de dominio directo de aplicación web de Hola y Hola dirección URL del Administrador de tráfico estará visible en la página de configuración de la aplicación web hello en hello **nombres de dominio** sección.
* Los nombres de dominio personalizado funcionará según lo previsto, pero en suma tooadding les tooyour las aplicaciones web, también debe configurar su toohello de toopoint de asignación DNS dirección URL del Administrador de tráfico. Para obtener información acerca de cómo tooset un dominio personalizado para una aplicación web de Azure, consulte [configurar un nombre de dominio personalizado para un sitio web de Azure](app-service-web-tutorial-custom-domain.md).
* Solo puede agregar las aplicaciones web que se encuentran en el modo estándar o premium tooa perfil de Traffic Manager de Azure.

## <a name="next-steps"></a>Pasos siguientes
Si desea obtener información general de carácter técnico y conceptual del Administrador de tráfico de Azure, consulte [Información general sobre el Administrador de tráfico](../traffic-manager/traffic-manager-overview.md).

Para obtener más información acerca del uso de Traffic Manager con las aplicaciones Web, vea las entradas de blog hello [utilizando Azure Traffic Manager con sitios Web Azure](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) y [Azure Traffic Manager ahora puede integrar con los sitios Web](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

