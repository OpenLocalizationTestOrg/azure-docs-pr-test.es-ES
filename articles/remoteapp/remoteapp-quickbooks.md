---
title: aaaDeploy QuickBooks en Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooshare QuickBooks con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>¿Cómo se implementa QuickBooks en Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Usar hello después información tooshare QuickBooks como una aplicación en Azure RemoteApp.

Puede compartir QuickBooks 2015 Enterprise con Azure RemoteApp en una colección híbrida o en la nube. archivo de empresa de Hello debe residir en una máquina virtual que está ejecutando el servidor de base de datos de QuickBooks que es independiente de los servidores de hello Azure RemoteApp. Archivo de empresa de hello en la imagen de Azure RemoteApp no almacene nunca: pérdida de datos se espera que si lo hace. Sólo QuickBooks Enterprise es compatible con hospedaje archivo QuickBooks de hello en un recurso compartido externo con el servidor de base de datos de QuickBooks accesible a través de redes de Windows estándar.   

> [!IMPORTANT]
> Hello servidor de base de datos de QuickBooks que hospeda el archivo de empresa de hello debe residir en una máquina virtual independiente dentro de hello misma red virtual como Hola colección RemoteApp de Azure.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Pasos toodeploy QuickBooks
1. Crear una máquina virtual de Azure, instale QuickBooks, servidor de base de datos de QuickBooks y coloque el archivo de empresa de hello en una máquina virtual de Azure.  Asegúrese de que tooproperly configurar reglas de firewall.
2. Instalar QuickBooks en un [imagen personalizada](remoteapp-imageoptions.md) y crear un [colección de Azure RemoteApp](remoteapp-collections.md), en la nube o híbridas, dentro de hello exactamente la misma red virtual donde hospedaje de máquinas virtuales de Hola Hola servidor de base de datos de QuickBooks con archivos de la compañía se encuentra. 
3. [Publicar](remoteapp-publish.md) toousers de aplicación de QuickBooks
4. Iniciar a cliente QuickBooks hospedados en Azure RemoteApp de hello, navegar con el servidor de base de datos de toohello VM hospedaje Hola QuickBooks de red de Windows estándar y abra el archivo de empresa de hello. 

## <a name="documentation-references"></a>Referencias de documentación
* [Configuraciones admitidas](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* [Opciones de implementación](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

También puede desproteger la presentación de Ignite [conceptos básicos de Microsoft Azure RemoteApp administración y administración](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -avancemos too1:02:45 tooget toohello QuickBooks parte.

## <a name="deployment-architecture"></a>Arquitectura de implementación
![Implementación de QuickBooks y RemoteApp de Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

