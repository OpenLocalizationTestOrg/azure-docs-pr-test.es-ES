---
title: "problemas de implementación de servicio de nube aaaTroubleshoot | Documentos de Microsoft"
description: "Hay algunos problemas comunes que pueden surgir al implementar un tooAzure de servicio de nube. Este artículo proporciona soluciones toosome de ellos."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Solución de problemas de implementación de servicios en la nube
Cuando se implementa un tooAzure de paquete de aplicación de servicio de nube, puede obtener información acerca de la implementación de Hola de hello **propiedades** panel Hola portal de Azure. Puede utilizar los detalles de hello en este panel toohelp solucionar los problemas con el servicio de nube de Hola y puede proporcionar esta compatibilidad de información tooAzure al abrir una nueva solicitud de soporte técnico.

Puede encontrar Hola **propiedades** panel como se indica a continuación:

* Hola portal de Azure, haga clic en implementación de Hola de servicio en la nube, haga clic en **toda la configuración de**y, a continuación, haga clic en **propiedades**.
* Hola portal de Azure clásico, haga clic en implementación de Hola de servicio en la nube, haga clic en **panel**, que se encuentra en la esquina inferior derecha de Hola de página hello (bajo **vista rápida**). Tenga en cuenta que en este panel no hay ninguna etiqueta "Propiedades".

> [!NOTE]
> Puede copiar contenido de Hola de hello **propiedades** Portapapeles de toohello panel haciendo clic en el icono de hello en la esquina superior derecha de hello del panel de Hola.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problema: no puedo acceder a mi sitio web, pero la implementación se ha iniciado y todas las instancias de rol están listas
vínculo de dirección URL del sitio Web Hola que se muestra en el portal de hello no incluye el puerto de Hola. puerto predeterminado de Hola para los sitios Web es 80. Si la aplicación está configurada toorun en un puerto diferente, debe agregar URL de toohello de número de puerto correcto de hello al acceder al sitio Web de Hola.

1. Hola portal de Azure, haga clic en implementación de Hola de servicio en la nube.
2. Hola **propiedades** panel de hello portal de Azure, compruebe los puertos de Hola Hola para instancias de rol (en **extremos de entrada**).
3. Si el puerto de hello no es 80, agregar dirección URL toohello de valor de puerto correcto de hello cuando tiene acceso a la aplicación hello. toospecify un puerto no predeterminado, escriba la dirección URL de hello, seguido de dos puntos (:), seguido por número de puerto de hello, sin espacios en blanco.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problema: mis instancias de rol se reciclan automáticamente
La recuperación del servicio se produce automáticamente cuando Azure detecta nodos del problema y, por tanto, mueve a nodos de toonew de instancias de rol. Cuando esto ocurre, puede que vea que las instancias de rol se reciclan automáticamente. toofind out si la recuperación se produjo del servicio:

1. Hola portal de Azure, haga clic en implementación de Hola de servicio en la nube.
2. Hola **propiedades** panel de hello portal de Azure, revise la información de Hola y determinar si la recuperación del servicio ha producido durante el tiempo de Hola que observa el reciclaje de roles de Hola.

Los roles también se reciclarán aproximadamente una vez al mes durante las actualizaciones del sistema operativo del host y del sistema operativo invitado.  
Para obtener más información, consulte el blog de hello [actualizaciones de instancia de rol se reinicia debido tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problema: No puedo realizar un intercambio de VIP y recibo un error
No se permite un intercambio de VIP si una actualización de implementación está en curso. Las actualizaciones de implementación pueden ocurrir automáticamente cuando:

* Hay un nuevo sistema operativo invitado y ha configurado actualizaciones automáticas
* Se produce una recuperación de servicio.

toofind espera si actualiza una automática le impide realizar un intercambio de VIP:

1. Hola portal de Azure, haga clic en implementación de Hola de servicio en la nube.
2. Hola **propiedades** panel de hello portal de Azure, busque valor Hola de **estado**. Si es **listo**, a continuación, busque **en la última operación** toosee si produjo recientemente una que podría impedir que el intercambio de hello VIP.
3. Repita los pasos 1 y 2 para la implementación de producción de hello.
4. Si una actualización automática está en curso, espere toofinish antes de tratar de intercambio de VIP de hello toodo.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problema: Una instancia de rol entra en un bucle entre Iniciado, Inicializando, Ocupado y Detenido
Esta condición puede indicar un problema con el código de la aplicación, el paquete o el archivo de configuración. En ese caso, debe ser capaz de toosee estado de hello cambia cada pocos minutos y hello portal de Azure puede aparecer algo como **reciclaje**, **ocupado**, o **Initializing**. Esto indica que hay algún error en la aplicación hello que se mantiene la instancia de rol de Hola de ejecución.

Para obtener más información acerca de cómo tootroubleshoot para este problema, consulte la entrada de blog hello [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) y [problemas comunes que toorecycle de roles causa](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problema: Mi aplicación dejó de funcionar
1. Hola portal de Azure, haga clic en instancia de rol de Hola.
2. Hola **propiedades** panel de hello portal de Azure, considere la posibilidad de hello siguientes condiciones tooresolve el problema:
   * Si recientemente ha detenido la instancia de rol de hello (se puede comprobar el valor de Hola de **recuento de anulados**), podría estar actualizando la implementación de Hola. Espere toosee si reanuda el funcionamiento en su propia instancia de rol de Hola.
   * Si es la instancia de rol de hello **ocupado**, compruebe su toosee de código de aplicación si hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) evento está controlado. Tal vez necesite tooadd o corregir el código que controla este evento.
   * Vaya a través de los datos de diagnóstico de Hola y deba resolver un problema en la entrada de blog de hello [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Si se recicla el servicio en la nube, se restablecen las propiedades de hello para la implementación de hello, se borra eficazmente información de hello problema original Hola.
>
>

## <a name="next-steps"></a>Pasos siguientes
Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.

toolearn cómo emite tootroubleshoot rol de servicio de nube mediante el uso de datos de diagnóstico del equipo de PaaS de Azure, consulte [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
