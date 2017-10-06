---
title: ancho de banda de aaaAzure RemoteApp red - directrices generales | Documentos de Microsoft
description: "Entender algunas directrices básicas del ancho de banda de red para sus colecciones y aplicaciones de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Ancho de banda de red de Azure RemoteApp: directrices generales (si no puede probarlo usted mismo)
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Si no tiene Hola de tiempo o la funcionalidad de Hola toorun [pruebas de ancho de banda de red](remoteapp-bandwidthtests.md) de RemoteApp de Azure, estas son algunas directrices bastante genéricas que pueden ayudarle a calcular el ancho de banda por usuario.

Si tiene una combinación de estos escenarios, se desaconseja algo menor que (o igual que) 10 MB/s Hola ancho de banda de red de mínimo de las aplicaciones actuales en un entorno remoto conectado a Internet. (Aunque, como se explicó anteriormente, esto no garantizará una experiencia de usuario superior a la media).

## <a name="complex-powerpoint-simple-powerpoint"></a>PowerPoint de tipo complejo y de tipo simple
Azure RemoteApp funciona mejor con una red LAN de 100 MB. En Hola 10 MB/perfil de red s, vibración por encima de 120 ms una vez más del 5%, usuario Hola verán una experiencia promedio. En Hola de 1 MB/s diferentes es terribles - por ejemplo, en una presentación con diapositivas, Hola el usuario puede no ver transiciones animadas en absoluto porque se omiten los fotogramas.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, PDF mixto, PDF, texto
Perfil de red de 10 MB/s es cerrar tooLAN en casi todos los aspectos. 1 MB/s proporcionará una experiencia de Aceptar, aunque puede haber algunas vibración cuando un usuario se desplaza mientras hay imágenes en la pantalla de bienvenida.

## <a name="flash-video-youtube"></a>Vídeo Flash (YouTube)
LAN de 100 MB/s proporciona mejor experiencia de hello, mientras que 10 MB/s es aceptable (es decir, hacer frente a la velocidad de fotogramas de hello, pero vibración aumenta). A 1 MB/s, la vibración es muy alta y apreciable.

## <a name="word-typing-word-remote-input"></a>Escritura en Word (entrada remota de Word)
Se trata de un escenario de uso de ancho de banda bajo. A 256 KB/s, proporcionamos una experiencia tan buena como la de la red LAN.

## <a name="learn-more"></a>Más información
* [Cálculo aproximado del uso del ancho de banda de red de Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp: ¿cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp: probar su uso de ancho de banda de red con algunos escenarios comunes)](remoteapp-bandwidthtests.md)

