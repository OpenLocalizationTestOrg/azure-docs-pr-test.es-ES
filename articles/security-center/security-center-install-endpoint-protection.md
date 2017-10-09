---
title: aaaInstall Endpoint Protection en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** instalar Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Instalación de Endpoint Protection en Azure Security Center
Azure Security Center recomienda instalar Endpoint Protection en las máquinas virtuales de Azure si aún no se ha habilitado esta solución. Esta recomendación aplica tooWindows máquinas virtuales.

> [!NOTE]
> En esta implementación de ejemplo se utiliza Microsoft Antimalware. Consulte [Integración de asociados en Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) para ver una lista de asociados integrados con Security Center.  
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  Este documento no es una guía paso a paso.
>
>

1. Hola **recomendaciones** hoja, seleccione **instalar Endpoint Protection**.
   ![Selección de instalar Endpoint Protection][1]
2. Hola **instalar Endpoint Protection** hoja abrirá mostrando una lista de las máquinas virtuales sin protección de extremo. Seleccione uno de Hola Hola de lista máquinas virtuales que desea que tooinstall endpoint protection en y haga clic en **instalar en máquinas virtuales**.
   ![Seleccione las máquinas virtuales tooinstall Endpoint Protection en][2]
3. Hola **seleccione Endpoint Protection** hoja abre tooallow se tooselect Hola extremo solución de protección que desee toouse. En este ejemplo, vamos a seleccionar **Microsoft Antimalware**.
   ![Select Endpoint Protection][3]
4. Se muestra información adicional sobre solución de protección de extremo de Hola. Seleccione **Crear**.
   ![Creación de solución antimalware][4]
5. Escriba valores de configuración de hello necesario en hello **Agregar extensión** hoja y, a continuación, seleccione **Aceptar**. toolearn más información acerca de los valores de configuración de hello, consulte [predeterminadas y configuración de Antimalware personalizada](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) está activo en hello selecciona las máquinas virtuales.

## <a name="see-also"></a>Otras referencias
En este artículo se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Instalar Endpoint Protection". toolearn más acerca de cómo habilitar Microsoft Antimalware en Azure, vea Hola siguiente documento:

* [Microsoft Antimalware para servicios en la nube y máquinas virtuales](../security/azure-security-antimalware.md) : Obtenga información acerca de cómo toodeploy Microsoft Antimalware.

toolearn más información acerca del centro de seguridad, vea Hola siguientes documentos:

* [Configuración de directivas de seguridad en el centro de seguridad de Azure](security-center-policies.md) : Obtenga información acerca de cómo las directivas de seguridad de tooconfigure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
