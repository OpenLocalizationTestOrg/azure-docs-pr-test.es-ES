---
title: aaaCannot eliminar una red virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot Hola problema en el que no se puede eliminar una red virtual en Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Solución de problemas: No se pudo toodelete una red virtual en Azure

Puede recibir errores cuando intente toodelete una red virtual en Microsoft Azure. Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Guía de solución de problemas 

1. [Compruebe si una puerta de enlace de red virtual se ejecuta en la red virtual de hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Compruebe si una puerta de enlace de la aplicación se ejecuta en la red virtual de hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Comprobar si el servicio del dominio de Active Directory de Azure está habilitada en la red virtual de hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Comprobar si la red virtual de Hola se tooother conectado recursos](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Comprobar si una máquina virtual todavía se está ejecutando en la red virtual de hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Compruebe si la red virtual de hello está atascada en migración](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Compruebe si una puerta de enlace de red virtual se ejecuta en la red virtual de Hola

red virtual de tooremove hello, primero debe quitar la puerta de enlace de red virtual de Hola.

Para las redes virtuales clásicas, visite toohello **Introducción** página de red virtual clásica de Hola Hola portal de Azure. Hola **conexiones VPN** sección, si se ejecuta la puerta de enlace de hello en red virtual de hello, verá Hola IP dirección de puerta de enlace de Hola. 

![Compruebe si la puerta de enlace se está ejecutando](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Para las redes virtuales, consulte toohello **Introducción** página de red virtual de Hola. Comprobar **dispositivos conectados** para puerta de enlace de red virtual de Hola.

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Antes de poder quitar la puerta de enlace de hello, quite primero cualquier **conexión** objetos de puerta de enlace de Hola. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Compruebe si una puerta de enlace de la aplicación se ejecuta en la red virtual de Hola

Vaya toohello **Introducción** página de red virtual de Hola. Comprobar hello **dispositivos conectados** para puerta de enlace de aplicación Hola.

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Si hay una puerta de enlace de la aplicación, debe quitarlo antes de poder eliminar la red virtual de Hola.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Comprobar si el servicio del dominio de Active Directory de Azure está habilitada en la red virtual de Hola

Si Hola servicios de dominio de Active Directory está habilitado y conectado toohello red virtual, no se puede eliminar esta red virtual. 

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable Hola servicio, siga estos pasos:

1. Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel izquierdo de hello, seleccione **Active Directory**.
3. Seleccione el directorio de Azure Active Directory (Azure AD) de Hola que tiene el servicio de dominio de Active Directory habilitado.
4. Seleccione hello **configurar** ficha.
5. En **los servicios de dominio**, cambiar hello **habilitar los servicios de dominio para este directorio** opción demasiado**No**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Comprobar si la red virtual de Hola se recursos tooother conectado

Busque vínculos de circuito, conexiones y emparejamientos de red virtual. Cualquiera de ellos puede producir un toofail de eliminación de la red virtual. 

Hello orden de eliminación recomendada es la siguiente:

1. Conexiones de puerta de enlace
2. Puertas de enlace
3. Direcciones IP
4. Emparejamientos de red virtual
5. App Service Environment (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Comprobar si una máquina virtual todavía se está ejecutando en la red virtual de Hola

Asegúrese de que ninguna máquina virtual está en red virtual de Hola.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Compruebe si la red virtual de hello está atascada en migración

Si la red virtual de Hola se quede en un estado de migración, no se puede eliminar. Ejecute hello después de la migración de hello tooabort de comando y, a continuación, eliminar la red virtual de Hola.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Pasos siguientes

- [Red virtual de Azure](virtual-networks-overview.md)
- [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)