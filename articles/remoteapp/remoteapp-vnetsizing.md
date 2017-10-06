---
title: "información de aaaSizing para una red virtual en Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de los requisitos de dirección IP de Hola para ejecutar con una red virtual de Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Información de tamaño para una red virtual de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Cuando usas Azure RemoteApp con una red virtual (VNET), RemoteApp usa direcciones IP dentro de la subred de Hola. En función de la escala de Hola de su servicio de RemoteApp, debe tooensure que la subred tiene suficientes direcciones IP disponibles para las máquinas virtuales de RemoteApp. Aunque esta guía sobre tamaños no es perfecta dado el modo en que RemoteApp aumenta y disminuye dinámicamente la capacidad de las máquinas virtuales dentro de una colección, le permitirá calcular el intervalo de subredes. Esto es especialmente importante que, una vez que un servicio de RemoteApp se coloca en una red virtual, no se puede aumentar el tamaño de la subred de hello sin quitar RemoteApp.

Para cada colección de RemoteApp que quiere que toorun en su capacidad máxima, debe tener 100 direcciones IP disponibles. Por ejemplo, si tiene una colección de RemoteApp en plan estándar de Hola y desea toohave Hola máximo 500 usuarios, debe tener 100 direcciones IP para esa colección. De igual forma, necesita 100 direcciones IP para una colección de RemoteApp de plan básico Hola con 800 usuarios. Si tiene previsto toohave menos usuarios (menor que Hola máximo), puede reducir las direcciones IP Hola necesarios por la colección. requisito de tamaño de Hello subred mínimo es 30 direcciones IP (/ 27).

Hola sigue toomake de información que la red virtual está configurada y funciona correctamente, consulte:

* [Migrar desde una tooan de red virtual personal red virtual de Azure](remoteapp-migratevnet.md)
* [Validar hello toouse de red virtual de Azure con Azure RemoteApp](remoteapp-vnet.md)

