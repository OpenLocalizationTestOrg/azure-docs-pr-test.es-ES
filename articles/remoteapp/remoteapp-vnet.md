---
title: toouse de red virtual de Azure de hello aaaValidate con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomake seguro de que la red virtual de Azure está lista toouse con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Validar hello toouse de red virtual de Azure con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Antes de usar una red virtual de Azure con Azure RemoteApp, conviene toovalidate Hola red virtual. Esto ayuda a evitar problemas con la conectividad.

toovalidate su red virtual de Azure, Hola siguientes:

1. Crear una máquina virtual dentro de la subred Hola de hello red virtual de Azure que desee toouse con Azure RemoteApp.
2. Conectar toothat VM mediante el uso de hello **conectar** opción en el portal de administración de Hola.
3. Unir toohello de máquina virtual de hello mismo dominio que desea que toouse con Azure RemoteApp. Si va a crear una colección híbrida que se conecta la red local de tooyour, unirse al dominio local de tooyour de máquina virtual de Hola.

Si esto se realiza correctamente, Hola red virtual de Azure es toouse listo con RemoteApp.

Para obtener más información acerca de flujo de trabajo de recopilación de hello híbrida to-end, vea Hola siguientes artículos:

* [¿Cómo tooplan la red virtual de Azure RemoteApp](remoteapp-planvnet.md)
* [Creación de una colección híbrida](remoteapp-create-hybrid-deployment.md)
* [Implementar Azure RemoteApp colección tooyour red Virtual de Azure (con compatibilidad para ExpressRoute)](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

