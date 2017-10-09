---
title: "integración de registro de alertas de Azure Security Center aaaIntegrating con Azure | Documentos de Microsoft"
description: "Este artículo lo ayuda a comenzar a integrar las alertas de Security Center con la integración de registro de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Integración de las alertas de Azure Security Center con la integración de registro de Azure
Muchas operaciones de seguridad y los equipos de respuesta a incidentes se basan en una solución de administración de eventos (SIEM) e información de seguridad como punto de partida para clasificación e investigación de alertas de seguridad de Hola. La integración de registros de Azure permite integrar las alertas de Azure Security Center con una solución de SIEM.

En la actualidad, la integración de registros de Azure admite HP ArcSight, Splunk e IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>¿Qué registros se pueden integrar?
Azure genera gran cantidad de registros para cada servicio. Estos registros se categorizan de la siguiente manera:

* **Registros de control/Management** que obtener una visibilidad en hello las operaciones de administrador de recursos de Azure cree, UPDATE y DELETE. Estos eventos de plano de control aparecen en hello registros de actividad de Azure
* **Registros de datos plano** que obtener una visibilidad en los eventos de hello generados cuando se usa un recurso de Azure. Un ejemplo es el registro de eventos de Windows hello, donde puede obtener información sobre eventos de seguridad de canal de seguridad del Visor de eventos de Hola. Los eventos del plano de datos (que los generan una máquina virtual o un servicio de Azure) los exponen los registros de diagnóstico de Azure.

Integración de registros de Azure actualmente admite la integración de Hola de:

* Registros de VM de Azure
* Registros de auditoría de Azure
* Alertas de Azure Security Center

## <a name="install-azure-log-integration"></a>Instalación de la integración de registro de Azure
Descargue la [integración de registro de Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Hola servicio de integración de registros de Azure recopila los datos de telemetría de máquina de hello en el que está instalado.  Los datos de telemetría recopilados son:

* Excepciones que se producen durante la ejecución de la integración de registro de Azure.
* Estadísticas sobre el número de Hola de eventos procesados y consultas
* Estadísticas sobre cuáles son las opciones de la línea de comandos de Azlog.exe que se usan.

> [!NOTE]
> Puede desactivar la recopilación de datos de telemetría si quita la marca de esta opción.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integración de los registros de auditoría de Azure y las alertas de Security Center
1. Hola abrir símbolo del sistema y **cd** en **c:\Program Files\Microsoft Azure registro integración**.
2. Ejecute hello **azlog createazureid** comando toocreate un [entidades de servicio de Azure Active Directory](../active-directory/active-directory-application-objects.md) en hello Azure Active Directory (AD), los inquilinos que hospedan Hola suscripciones de Azure.

    Se le pedirá los datos de inicio de sesión de Azure.

   > [!NOTE]
   > Debe ser propietario de suscripción de Hola o un Coadministrador de suscripción de Hola.
   >
   >

    TooAzure de autenticación se realiza a través de Azure AD.  Crear a una entidad de servicio para la integración de registros de Azure crea la identidad de Azure AD de Hola que tiene acceso tooread de las suscripciones de Azure.
3. Ejecute hello **azlog autorizar <SubscriptionID>**  comando tooassign acceso de lectura en la entidad de servicio toohello Hola suscripción creada en el paso 2. Si no se especifica un **SubscriptionID**, entidad de servicio de hello es Hola asignado lector rol tooall suscripciones toowhich tiene acceso.

   > [!NOTE]
   > Puede ver las advertencias si ejecuta hello **autorizar** comando inmediatamente después de hello **createazureid** comando. Hay alguna latencia entre cuando se crea la cuenta de hello Azure AD y cuando la cuenta de hello está disponible para su uso. Si espera unos 10 segundos después de ejecutar hello **createazureid** comando toorun hello **autorizar** comando, no debe ver estas advertencias.
   >
   >
4. Comprobar existen Hola después tooconfirm de carpetas que Hola archivos JSON de registro de auditoría:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Hola de comprobación siguientes tooconfirm de carpetas que existen las alertas del centro de seguridad de ellos:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Configurar Hola SIEM archivo reenviador conector toohello carpeta adecuado. procedimiento de Hello varían según Hola SIEM que usa.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de los registros de actividad de Azure y definiciones de propiedades, vea:

* [Operaciones de auditoría con Resource Manager](../azure-resource-manager/resource-group-audit.md)

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.
