---
title: aaaHow toomigrate desde una red virtual de Azure de RemoteApp VNET tooan | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate desde una red virtual de Azure de RemoteApp VNET tooan"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>¿Cómo toomigrate una colección híbrida de una red virtual de Azure de RemoteApp VNET tooan
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

¡Buenas noticias! Hemos habilitado toodeploy colecciones de RemoteApp híbrida directamente en sus existentes redes virtuales de Azure (redes virtuales) en lugar de crear redes virtuales específicos de RemoteApp. Esto le permite aprovechar las ventajas del programa Hola a las características más recientes de red virtual (por ejemplo, ExpressRoute) y proporcionar servicios de Azure a su tooother de acceso híbrido colecciones directa a la red y máquinas virtuales implementadas toothat red virtual.  (Esto le permite disfrutar de un mejor rendimiento y mayor facilidad de configuración con respecto a las instalaciones de red virtual a red virtual).

Supongamos que ya ha creado una colección de RemoteApp híbrida denominada *OriginalCollection* con una red virtual de RemoteApp llamada *RemoteAppVNET*. Presentamos Hola pasos toomigrate tooa nueva red virtual de Azure denominado *AzureVNET*.

1. En hello **redes** ficha hello [portal de administración de](http://manage.windowsazure.com/), crear una red virtual denominada *AzureVNET*con Hola la misma ubicación, la configuración de DNS y el espacio de direcciones (para al menos uno Hola *AzureVNET* subredes) que utilizó para *RemoteAppVNET*.
2. Configurar *AzureVNET* tooeither hospedar o debe tener la implementación de Active Directory de toohello de conectividad de red que *OriginalCollection* está unido a un dominio a.
3. En hello **RemoteApps** ficha, cree una nueva colección de RemoteApp denominada *nueva colección*. (Hola de uso **crear con red virtual** opción, no **creación rápida**.)
4. Configurar *NewCollection* toobe implementado subred tooa en *AzureVNET*.
5. Configurar *NewCollection* toouse Hola misma imagen e información de unión de dominio que utilizó para *OriginalCollection*.
6. Después de unas horas, *NewCollection* aparecerá en la lista de colecciones con un estado activo.

Ahora, si no necesita toomigrate cualquier información de usuario de hello original colección toohello nueva colección, siga estos pasos a continuación:

1. Elimine *OriginalCollection*.
2. Elimine *RemoteAppVNET*.

¡Y ya está!

Como alternativa, si necesita información de usuario de toomigrate de hello original colección toohello nueva colección, siga estos pasos a continuación:

1. Enviar un correo electrónico demasiado[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) con el identificador de suscripción de Azure, Hola nombre de la colección original y el nombre de saludo de la nueva colección de y pídale que toomigrate la información del usuario.
2. Próximos 2 días laborables equipo de RemoteApp Hola moverá lista de acceso de usuario de Hola y todos los documentos de usuario y configuración de usuario de hello original colección toohello nueva colección.
3. Elimine *OriginalCollection*.
4. Elimine *RemoteAppVNET*.

Y ahora, ¡ya ha terminado!

Si tiene alguna pregunta o necesita ayuda especial, envíe un correo electrónico a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

