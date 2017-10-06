---
title: aaaPoint un nombre de dominio de empresa Internet dominio tooa Traffic Manager | Documentos de Microsoft
description: "Este artículo le ayudará a dirigir su nombre de dominio de empresa dominio nombre tooa Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Seleccione un dominio de Azure Traffic Manager empresa tooan de dominio de Internet

Cuando se crea un perfil de Traffic Manager, Azure asigna automáticamente un nombre DNS para ese perfil. toouse un nombre de la zona DNS, cree un registro CNAME DNS que asigna el nombre de dominio toohello de su perfil de Traffic Manager. Puede encontrar el nombre de dominio de Traffic Manager de Hola Hola **General** sección en la página de configuración de Hola de hello perfil de Traffic Manager.

Por ejemplo, www.contoso.com toohello contoso.trafficmanager.net de nombre de DNS de Traffic Manager de toopoint nombre, crearía Hola siguiendo el registro de recursos DNS:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Todo el tráfico de solicitudes demasiado*www.contoso.com* dirigidos demasiado*contoso.trafficmanager.net*.

> [!IMPORTANT]
> No puede apuntar a un dominio de segundo nivel, como *contoso.com*, dominio de Traffic Manager toohello. Los estándares de protocolo DNS no permiten registros CNAME para nombres de dominio de segundo nivel.

## <a name="next-steps"></a>Pasos siguientes

* [Métodos de enrutamiento del Administrador de tráfico](traffic-manager-routing-methods.md)
* [Administrador de tráfico: deshabilitación, habilitación o eliminación de un perfil](disable-enable-or-delete-a-profile.md)
* [Administrador de tráfico: deshabilitación o habilitación de un extremo](disable-or-enable-an-endpoint.md)
