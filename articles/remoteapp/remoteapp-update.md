---
title: "aaaUpdate su colección de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupdate su colección de RemoteApp de Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Actualización de una colección en Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Aparecerá un tiempo, inevitablemente, cuando necesite tooupdate Hola aplicaciones o imagen en la colección de RemoteApp de Azure. Si está utilizando una de las imágenes de hello incluidas con su suscripción de RemoteApp de Azure, en la colección de una nube o híbridas, una o todas las actualizaciones se controlan RemoteApp de Azure, por lo que puede colocar la forma más fácil.

Sin embargo, si está utilizando una imagen personalizada (que crea a partir de cero o que creó mediante la modificación de una de nuestras imágenes), se va a encargar de mantenimiento de aplicaciones y la imagen de Hola. Si necesita tooupdate la imagen o cualquiera de las aplicaciones de hello dentro de él, debe toocreate una versión nueva y actualizada de hello imagen y, a continuación, reemplazar Hola existente imagen en la colección con esta nueva imagen actualizada.

Por lo tanto, ¿cómo tiene que proceder para actualizar la colección? Es bastante sencillo:

1. Imagen de Hola de actualización que utiliza en la colección. Aplique las revisiones o actualizaciones necesarias y guárdela con un otro nombre.
2. [Cargar](remoteapp-uploadimage.md) o [importar](remoteapp-image-on-azurevm.md) tooRemoteApp de esa imagen.
3. Ahora, haga clic en la página de la colección de hello, **actualización**.
4. Elegir nueva imagen de Hola Hola **imagen de plantilla** lista.
5. Aquí es parte complicada hello - necesita toodecide cómo toodeal con cualquier usuario que usa actualmente una aplicación en la colección de Hola. Tener Hola siguientes opciones:
   
   * **Proporcionar a los usuarios 60 minutos después de la actualización de hello**. Tan pronto como finaliza la actualización de hello, Azure RemoteApp mostrará un mensaje tooany active los usuarios informándoles toosave el trabajo y su registro desactivado y volver a iniciar sesión. Transcurridos los 60 minutos, se cerrará automáticamente la sesión de todos los usuarios activos que no la cerraron. Los usuarios pueden volver a iniciar sesión inmediatamente.
   * **Cerrar inmediatamente la sesión de los usuarios**. Tan pronto como finaliza la actualización de hello, cerrar todos los usuarios automáticamente sin previo aviso. Si elige esta opción, los usuarios pueden perder datos. Sin embargo, puede volver a conectar toohello aplicación inmediatamente.
6. Haga clic en actualización de hello marca de verificación toostart Hola.

