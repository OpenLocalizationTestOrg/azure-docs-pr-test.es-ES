---
title: aaaCreate granjas de servidores de SharePoint en Azure | Documentos de Microsoft
description: "Cree rápidamente una nueva granja de SharePoint 2013 o SharePoint 2016 en Azure con hello Azure marketplace portal."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Crear conjuntos de servidores de SharePoint mediante hello Azure marketplace de portal

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Granjas de servidores de SharePoint 2013
Con el marketplace de portal de Microsoft Azure hello, puede crear rápidamente las granjas de servidores de SharePoint Server 2013 preconfiguradas. Esto puede suponer un importante ahorro de tiempo si necesita una granja de SharePoint básica o de alta disponibilidad para un entorno de desarrollo y pruebas, o si va a evaluar SharePoint Server 2013 como solución de colaboración para su organización.

> [!NOTE]
> Hola **granja de servidores de SharePoint** se ha quitado el elemento de hello Azure Marketplace de hello portal de Azure. Se ha reemplazado con hello **no - HA de granja de SharePoint 2013** y **granja de servidores de SharePoint 2013 HA** elementos.
>
>

granja de SharePoint básica de Hello consta de tres máquinas virtuales de esta configuración.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Utilice esta configuración de granja simplificada para el desarrollo de aplicaciones de SharePoint en su primera evaluación de SharePoint 2013.

granja de SharePoint de (tres servidores) básica de toocreate hello:

1. Haga clic [aquí](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Haga clic en **Implementar**.
3. En hello **no - HA de granja de SharePoint 2013** panel, haga clic en **crear**.
4. Especificar la configuración en los pasos de Hola de hello **crear no - HA de granja de SharePoint 2013** panel y, a continuación, haga clic en **crear**.

granja de SharePoint de alta disponibilidad de Hello consta de nueve máquinas virtuales en esta configuración.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Puede usar esta granja configuración tootest superior cargas máximas del cliente, alta disponibilidad Hola externo del sitio de SharePoint y los grupos de disponibilidad AlwaysOn de SQL Server para una granja de servidores de SharePoint. También puede usar esta configuración para el desarrollo de aplicaciones de SharePoint en un entorno de alta disponibilidad.

granja de SharePoint de toocreate Hola alta disponibilidad (servidor de nueve):

1. Haga clic [aquí](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Haga clic en **Implementar**.
3. En hello **granja de servidores de SharePoint 2013 HA** panel, haga clic en **crear**.
4. Especificar la configuración en los pasos de hello siete de hello **crear HA de granja de SharePoint 2013** panel y, a continuación, haga clic en **crear**.

> [!NOTE]
> No se puede crear hello **no - HA de granja de SharePoint 2013** o **granja de servidores de SharePoint 2013 HA** con una prueba gratuita de Azure.
>
>

Hola portal de Azure crea dos de estos conjuntos de servidores en una red virtual solo en la nube con una presencia en web a través de Internet. No hay ningún sitio a sitio VPN o ExpressRoute conexión back-tooyour red la organización.

> [!NOTE]
> Cuando se crea hello básico o granjas de SharePoint de alta disponibilidad mediante Hola portal de Azure, no se puede especificar un grupo de recursos existente. toowork solucionar esta limitación, cree estas granjas de servidores con Azure PowerShell. Para más información, vea [Crear granjas de servidores de desarrollo y pruebas de SharePoint 2013 con Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Granjas de servidores de SharePoint 2016
Vea [este artículo](https://technet.microsoft.com/library/mt723354.aspx) para Hola Hola de toobuild instrucciones siguientes solo servidor SharePoint Server 2016 de la granja.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Administración de granjas de servidores de SharePoint de Hola
Puede administrar servidores de Hola de estos conjuntos de servidores a través de conexiones de escritorio remoto. Para obtener más información, consulte [inicie sesión en la máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).

De sitio de SharePoint de Administración Central de hello, puede configurar Mis sitios, aplicaciones de SharePoint y otras funciones. Para obtener más información, consulte [Configuración de SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Pasos siguientes
* Descubra más configuraciones de [SharePoint](https://technet.microsoft.com/library/dn635309.aspx) en los servicios de infraestructura de Azure.
