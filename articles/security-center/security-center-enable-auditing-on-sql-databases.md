---
title: "bases de datos de detección de auditoría y de las amenazas de aaaEnable en SQL en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** habilitar la detección de auditoría y de las amenazas en las bases de datos SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Habilitación de la auditoría y la detección de amenazas en bases de datos SQL en Azure Security Center
Azure Security Center recomienda activar la auditoría y la detección de amenazas en todas las bases de datos SQL, en caso de que no se hayan habilitado aún las auditorías. La auditoría y la detección de amenazas pueden ayudarle a mantener el cumplimiento de normativas, conocer la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o violaciones de la seguridad sospechosas.

Una vez has activado la auditoría, puede configurar alertas de seguridad de tooreceive de correos electrónicos y configuración de detección de amenazas. La detección de amenazas detecta actividades anómalas de la base de datos que indica la base de datos toohello amenazas de seguridad potenciales. Esto le permite toodetect y responder toopotential amenazas cuando se producen.

Esta recomendación aplica toohello solo; el servicio de SQL Azure no se incluye con las máquinas virtuales SQL.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **habilitar auditoría y amenaza para la detección en las bases de datos SQL**.  Se abrirá hello **habilitar auditoría y amenaza para la detección en las bases de datos SQL** hoja.

   ![Habilitación de la auditoría en bases de datos SQL][1]
2. Seleccione una auditoría de tooenable de base de datos SQL en. Se abrirá hello **auditoría y la detección de amenazas** hoja.

3. En hello **auditoría y la detección de amenazas** hoja, seleccione **ON** en **auditoría**.

   ![Activación de la detección de amenazas y auditoría][2]
4. Siga los pasos de hello en [detección de amenazas de base de datos de SQL en el portal de Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn en y configurar la detección de amenazas y lista de hello tooconfigure de mensajes de correo electrónico que recibirán las alertas de seguridad tras la detección de actividades anómalas.

## <a name="see-also"></a>Otras referencias
En este artículo se ha mostrado cómo tooimplement Hola centro de seguridad recomendación "Habilitar auditoría & amenaza para la detección en las bases de datos SQL". toolearn más acerca de cómo proteger la base de datos SQL, vea Hola recursos siguientes:

* [Protección de bases de datos SQL](../sql-database/sql-database-security-overview.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
