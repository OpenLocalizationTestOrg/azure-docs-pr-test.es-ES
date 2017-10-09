---
title: "una aplicación en Azure RemoteApp aaaPublish | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish las aplicaciones y recursos de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>¿Cómo toopublish una aplicación de RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Después de crear la colección de RemoteApp, necesitará toopublish Hola aplicaciones o recursos que desee toomake disponible para los usuarios. Hello imágenes de plantilla proporcionadas con la suscripción solo tienen unas pocas aplicaciones publicadas de forma predeterminada, tooshare Hola otras aplicaciones, necesita toopublish ellos.

> [!NOTE]
> ¿Necesita tooupdate una aplicación? Necesitará demasiado[actualización Hola imagen](remoteapp-update.md) primero.
> 
> 

En hello **publicación** , haga clic en el portal de hello **publicar**. Puede agregar una aplicación de la imagen de plantilla **iniciar** menú o proporcionar aplicación Hola de hello ruta de acceso toowhere está instalado en la imagen de plantilla de Hola. Si elige tooadd de hello **iniciar** menú, elija hello toopublish de aplicación de lista de Hola. Si elige tooprovide Hola ruta de acceso toohello aplicación, escriba un nombre para la aplicación hello y aplicación de toohello de ruta de acceso de hello. Usar variables en la ruta de acceso de hello - por ejemplo, "% systemdrive %" en lugar de "c:\".

> [!NOTE]
> Si desea que tooadd la aplicación de hello **iniciar** menú, necesita toohave *agrega esa aplicación toohello **iniciar** menú en la imagen de plantilla.* En caso contrario, RemoteApp solo verá qué *es* en hello **iniciar** menú y se confundirse. 
> 
> toomake seguro de que la aplicación está en hello **iniciar** menú, coloque un archivo de acceso directo - **.lnk** : dentro de la carpeta de hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.
> 
> Si ha olvidado tooadd Hola aplicación toohello **iniciar** menú cuando se creó la plantilla de hello, elija aplicación toohello de tooadd hello ruta de acceso. (O volver a crear la imagen de plantilla, pero supone algo más de trabajo).
> 
> 

