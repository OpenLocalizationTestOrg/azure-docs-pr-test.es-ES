---
title: aaaUsing Outlook en Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure y usar Outlook en Azure RemoteApp | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Uso de Microsoft Outlook en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Azure RemoteApp admite Microsoft Outlook O365. Obtenga más información sobre la manera en que [Office funciona en Azure RemoteApp](remoteapp-officesubscription.md). Hay algunas opciones de configuración recomendadas para Outlook cuando se usa en Azure RemoteApp.

## <a name="cached-mode"></a>Modo de almacenamiento en caché
El modo de almacenamiento en caché es una configuración recomendada al usar Outlook en Azure RemoteApp. Cuando se configura un toouse de cuenta de Outlook 2013 funciona el modo de intercambio en caché, Outlook 2013 desde una copia local del buzón de correo del usuario de Hola de Microsoft Exchange que se almacena en un archivo de datos sin conexión (archivo OST) en el equipo del usuario de hello, junto con hello libreta de direcciones sin conexión (OAB). buzón en la caché de Hola y OAB se actualizan periódicamente de hello servicio de Office 365. Obtenga más información sobre [Hola diferencias entre el modo en línea y en caché](https://technet.microsoft.com/library/jj683103.aspx).

Puede seleccionar usuario Hello **el modo de intercambio en caché** o **modo en línea** durante la instalación de la cuenta o cambiando la configuración de la cuenta de hello. También puede implementar un modo o hello otro mediante Hola herramienta de personalización de Office (OCT) o directiva de grupo.  

Lectura las [instrucciones detalladas sobre cómo habilitar el modo en caché](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Search
En Azure RemoteApp, el uso de la búsqueda dentro de Outlook tiene limitaciones. RemoteApp de Azure utiliza las sesiones de usuario de tooaccommodate máquinas virtuales agrupadas. Indización de búsqueda depende de Id. de máquina de hello, que es diferente para diferentes máquinas virtuales. Es posible que cada vez que un usuario inicia sesión en Azure RemoteApp, son tooa dirigido nueva máquina virtual. Se significaría que, si se habilita la búsqueda local, indizador Hola se ejecutará cada vez que cambia de Id. de máquina de hello (si es usuario de hello en una máquina virtual diferente). Según el tamaño de Hola Hola. Archivo OST, indizador Hola podría tardar un toocomplete mucho tiempo y utilizar los recursos necesarios para otras aplicaciones. La búsqueda no solo sería lenta, sino que quizás tampoco daría resultados. Con un perfil de cuenta de modo en línea podría solucionar este problema, pero se vería afectado el rendimiento general debido a falta de toohello de una memoria caché local (vea Hola por encima de vínculos para obtener más información acerca de la diferencia de hello entre el modo en línea y en caché). Lamentablemente, no se puede deshabilitar la búsqueda local o indexada y no se puede habilitar la búsqueda en línea de forma predeterminada en Outlook 2013.

