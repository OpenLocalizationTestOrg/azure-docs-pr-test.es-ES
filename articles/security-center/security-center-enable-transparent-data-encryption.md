---
title: aaaEnable cifrado de datos transparente en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** habilitar transparente datos cifrado **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Habilitación del Cifrado de datos transparente en Azure Security Center
Azure Security Center recomienda que habilite el Cifrado de datos transparente (TDE) en bases de datos SQL si aún no lo ha hecho. TDE protege los datos y le ayuda a cumplir los requisitos de cumplimiento mediante el cifrado de la base de datos, copias de seguridad asociadas y archivos de registro de transacciones en reposo, sin necesidad de cambios tooyour aplicación. toolearn más vea [cifrado de datos transparente con base de datos de SQL Azure](https://msdn.microsoft.com/library/dn948096).

Esta recomendación aplica toohello solo; el servicio de SQL Azure no incluye SQL que se ejecutan en las máquinas virtuales.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **Habilitar cifrado de datos transparente**.
   ![Habilitar el cifrado de datos transparente][1]
2. Se abrirá hello **Habilitar cifrado de datos transparente en las bases de datos SQL** hoja. Seleccione un tooenable de base de datos SQL TDE en.
   ![Seleccionar base de datos SQL tooenable TDE en][2]
3. En hello **cifrado de datos transparente** hoja, seleccione **ON** en cifrado de datos y seleccione **guardar** en la cinta de opciones superior Hola de hoja de Hola.
   ![Activación de TDE][3]

   Una vez que TDE está habilitado en hello seleccionado base de datos SQL, hello **estado de cifrado** cambiará demasiado**Encrypted**.    

   ![Estado de cifrado][4]

## <a name="see-also"></a>Otras referencias
En este artículo se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Habilitar la cifrado de datos transparente". toolearn más información acerca de SQL TDE, vea Hola recursos siguientes:

* [Cifrado de datos transparente con Base de datos SQL de Azure](https://msdn.microsoft.com/library/dn948096)
* [Introducción al cifrado de datos transparente (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
