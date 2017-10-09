---
title: aaaAdd un servidor de aplicaciones web en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** agregar un servidor de seguridad de aplicación web ** y ** finalizar la protección de aplicación **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Adición de un firewall de aplicaciones web en el Centro de seguridad de Azure
Centro de seguridad de Azure puede recomienda agregar un servidor de aplicaciones web (WAFS) desde un toosecure de partner de Microsoft las aplicaciones web. Este documento le guía a través de un ejemplo de cómo tooapply esta recomendación.

Se muestra una recomendación WAFS para cualquier IP pública (dirección IP de nivel de instancia o con equilibrio de carga) que tiene un grupo de seguridad de red asociado con puertos abiertos web entrantes (80 y 443).

Centro de seguridad, se recomienda que aprovisionar un toohelp WAFS defenderse contra los ataques que se dirige a las aplicaciones web en máquinas virtuales y en el entorno del servicio de aplicaciones. Un entorno de App Service es una opción de plan de servicio [Premium](https://azure.microsoft.com/pricing/details/app-service/) de Azure App Service que proporciona un entorno plenamente aislado y dedicado para ejecutar de forma segura las aplicaciones de Azure App Service. toolearn más información acerca de ASE, vea hello [documentación del entorno de servicio de aplicación](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  Este documento no es una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **proteger la aplicación web con el servidor de aplicaciones web**.
   ![Aplicación web segura][1]
2. Hola **proteger las aplicaciones web utilizando el servidor de aplicaciones web** hoja, seleccione una aplicación web. Hola **agregar un servidor de seguridad de la aplicación Web** abre la hoja.
   ![Add a web application firewall][2]
3. Puede elegir a toouse un servidor de aplicaciones web existentes si está disponible o puede crear uno nuevo. En este ejemplo no hay ningún WAF existente, por lo que vamos a crear uno.
4. toocreate un WAFS, seleccione una solución de lista de Hola de socios integrados. En ese ejemplo, seleccionaremos **Firewall de aplicaciones web de Barracuda**.
5. Hola **Firewall de aplicación Web de Barracuda** hoja abre, proporciona información sobre solución de socios de Hola. Seleccione **crear** en la hoja de información de Hola.

   ![Hoja de información del firewall][3]

6. Hola **nuevo Firewall de aplicación Web** se abre la hoja, donde puede realizar **configuración de máquina virtual** pasos y proporcionar **WAFS información**. Seleccione **Configuración de VM**.
7. Hola **configuración de máquina virtual** hoja, especifique información toospin requiere una máquina virtual de Hola que ejecuta Hola WAFS.
   ![VM configuration][4]
8. Devolver toohello **nuevo Firewall de aplicación Web** hoja y seleccione **WAFS información**. Hola **WAFS información** hoja, configurar WAFS Hola propio. Paso 7 le permite tooconfigure Hola virtual machine en qué Hola WAFS se ejecuta y el paso 8 permite tooprovision Hola WAFS propio.

## <a name="finalize-application-protection"></a>Finalización de la protección de la aplicación
1. Devolver toohello **recomendaciones** hoja. Se genera una nueva entrada después de crear WAFS hello, denominado **finalizar la protección de la aplicación**. Esta entrada le permite saber que necesita el proceso de hello toocomplete de transmitiendo realmente Hola WAFS dentro de hello red Virtual de Azure para que puedan proteger la aplicación hello.

   ![Finalización de la protección de la aplicación][5]

2. Seleccione **Finalize application protection**(Finalizar la protección de la aplicación). Se abre una nueva hoja. Puede ver que hay una aplicación web que necesita toohave su tráfico vuelve a enrutar.
3. Seleccione la aplicación web de hello. Una hoja que se incluyen los pasos para finalizar la instalación de servidor de seguridad de aplicación web de hello abre. Complete los pasos de hello y, a continuación, seleccione **restringir el tráfico**. Centro de seguridad, a continuación, Hola cableado telefónico para usted.

   ![Restringir tráfico][6]

> [!NOTE]
> Puede proteger varias aplicaciones web en el centro de seguridad mediante la adición de estas implementaciones de WAFS aplicaciones tooyour existentes.
>
>

registros de Hola desde ese WAFS ahora están totalmente integrados. Centro de seguridad puede iniciar automáticamente recopilar y analizar los registros de Hola para que puede aparecer tooyou de alertas de seguridad importante.

## <a name="next-steps"></a>Pasos siguientes
Este documento se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Agregar una aplicación web". toolearn más información acerca de cómo configurar un firewall de aplicación web, vea Hola recursos siguientes:

* [Configuración de un firewall de aplicaciones web (WAF) para entornos del Servicio de aplicaciones](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
