---
title: "Migración de plataforma de centro de seguridad de aaaAzure | Documentos de Microsoft"
description: Este documento explica alguna manera de toohello cambios datos de Azure Security Center se recopila.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migración de la plataforma de Azure Security Center

A partir de los principios de junio de 2017, centro de seguridad de Azure implementa importante se recopilan y almacenan los datos de seguridad de manera toohello de cambios.  Estos cambios desbloquear nuevas capacidades como datos de seguridad de búsqueda de hello capacidad tooeasily y mejor se adapte a otra administración de Azure y supervisar los servicios.

> [!NOTE]
> migración de la plataforma de Hello no debería afectar a los recursos de producción y no es necesario desde el lado ninguna acción.


## <a name="whats-happening-during-this-platform-migration"></a>¿Qué sucede durante esta migración de la plataforma?

Anteriormente, el centro de seguridad utiliza datos de seguridad toocollect Hola de agente de supervisión de Azure desde las máquinas virtuales. Esto incluye información sobre las configuraciones de seguridad, que son utilizados tooidentify vulnerabilidades, y eventos de seguridad, que son las amenazas de toodetect usado. Estos datos se almacenan en sus cuentas de Storage de Azure.

En el futuro, que el centro de seguridad usa Microsoft Monitoring Agent: hello es hello usa el mismo agente por hello Operations Management Suite y el servicio de análisis de registros. Datos recopilados de este agente se almacenan en cualquier otra *análisis de registros* [área de trabajo](../log-analytics/log-analytics-manage-access.md) asociada a su suscripción de Azure o áreas de trabajo nuevo, teniendo en cuenta Hola geolocation de hello VM .

## <a name="agent"></a>Agente

Como parte de la transición de hello, Hola Microsoft Monitoring Agent (para [Windows](../log-analytics/log-analytics-windows-agents.md) o [Linux](../log-analytics/log-analytics-linux-agents.md)) está instalado en todas las máquinas virtuales de Azure desde la que actualmente está están recopilando datos.  Si Hola que Hola el agente de supervisión de Microsoft instalado, la máquina virtual ya tiene el centro de seguridad utiliza Hola actual había instalado el agente.

Durante un período de tiempo (normalmente unos días), ambos agentes ejecutarán en paralelo tooensure una transición fluida sin pérdida de datos. Esto permitirá que Microsoft toovalidate que Hola nueva canalización de datos está operativa antes de dejar de usar la canalización actual Hola. Hola una vez comprobado, el agente de supervisión de Azure se quitará de las máquinas virtuales. No es necesario que el usuario intervenga de ninguna forma. Cuando todos los clientes se hayan migrado, recibirá una notificación por correo electrónico.
 
No se recomienda desinstalar manualmente Hola agente de supervisión de Azure durante la migración de hello tal y como se pudieron dar lugar a huecos en los datos de seguridad. Si necesita ayuda adicional, consulte [servicio de Soporte técnico y Atención al cliente de Microsoft](https://support.microsoft.com/contactus/). 

Hola supervisión Microsoft agente para Windows requiere que utilizan el puerto TCP 443, leer [Guía de solución de problemas de Azure Security Center](security-center-troubleshooting-guide.md) para obtener más información.


> [!NOTE] 
> Dado Hola Microsoft Monitoring Agent puede utilizarse por otra administración de Azure y supervisar los servicios, Hola agente no se desinstalará automáticamente cuando desactivar la recopilación de datos en el centro de seguridad. Sin embargo, puede desinstalar manualmente el agente de hello si es necesario.

## <a name="workspace"></a>Área de trabajo

Tal y como se ha descrito anteriormente, los datos recopilados de hello Microsoft Monitoring Agent (en nombre del centro de seguridad) se almacenan en un análisis de registro existente áreas de trabajo asociadas a su suscripción de Azure o un nuevo espacios de trabajo, teniendo en Hola de cuenta ubicación geográfica del programa Hola a máquina virtual.

Hola portal de Azure, puede examinar toosee una lista de las áreas de trabajo de análisis de registros, las que se crearon mediante el centro de seguridad incluidas. Se creará un grupo de recursos relacionado para las nuevas áreas de trabajo. Ambas siguen esta convención de nomenclatura:

- Área de trabajo: *DefaultWorkspace-[subscription-ID]-[geo]*
- Grupo de recursos: *DefaultResouceGroup-[geo]* 
 
En el caso de las áreas de trabajo creadas por Security Center, los datos se conservan durante 30 días. Para las áreas de trabajo existentes, retención se basa en área de trabajo de hello nivel de precios.

> [!NOTE]
> Los datos recopilados previamente por Security Center permanecen en sus cuentas de Storage. Una vez completada la migración de hello, puede eliminar estas cuentas de almacenamiento.

### <a name="oms-security-solution"></a>Solución de seguridad de OMS 

Los clientes existentes que no tengan instalada la solución de seguridad de OMS están de suerte. Microsoft la instalará en sus áreas de trabajo, pero irá dirigida únicamente a las máquinas virtuales de Azure. No desinstale esta solución, ya que no existe ninguna solución automática si lo hace desde la consola de administración de OMS.


## <a name="other-updates"></a>Otras actualizaciones

Junto con la migración de la plataforma de hello, estamos efectuando algunas actualizaciones secundarias adicionales:

- Se admitirán otras versiones de sistema operativo. Ver lista de hello [aquí](security-center-faq.md#virtual-machines).
- lista de Hola de vulnerabilidades de sistema operativo que se va a expandir. Ver lista de hello [aquí](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- Los [precios](https://azure.microsoft.com/pricing/details/security-center/) se prorratearán por hora (antes era diariamente), lo que se traducirá en un ahorro de costos para los clientes.
- Recopilación de datos se requiere y se habilita automáticamente para clientes de nivel de precios estándar Hola.
- Azure Security Center comenzará a detectar soluciones antimalware que no se implementaron mediante extensiones de Azure. En primer lugar estará disponible la detección de Symantec Endpoint Protection y Defender para Windows 2016.
- Directivas de prevención y las notificaciones solo son configurables en hello *suscripción* nivel, pero el precio todavía se puede establecer en hello *grupo de recursos* nivel

