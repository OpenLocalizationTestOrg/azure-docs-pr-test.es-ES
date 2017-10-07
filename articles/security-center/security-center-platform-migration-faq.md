---
title: "Preguntas más frecuentes de la migración de plataformas aaaSecurity Center | Documentos de Microsoft"
description: "Preguntas sobre la migración de la plataforma de centro de seguridad de Azure Hola responden a estas preguntas más frecuentes."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Preguntas frecuentes sobre la migración de la plataforma de Security Center
En principios de junio de 2017, centro de seguridad de Azure comenzó con hello Microsoft Monitoring Agent toocollect y el almacén de datos. más información, consulte toolearn [migración de la plataforma de Azure Security Center](security-center-platform-migration.md). Preguntas sobre la migración de la plataforma de hello responden a estas preguntas más frecuentes.

## <a name="data-collection-agents-and-workspaces"></a>Recopilación de datos, agentes y áreas de trabajo

### <a name="how-is-data-collected"></a>¿Cómo se recopilan los datos?
Centro de seguridad utiliza datos de seguridad de hello Microsoft Monitoring Agent toocollect de las máquinas virtuales. datos de seguridad de saludo incluyen información sobre las configuraciones de seguridad, que son utilizados tooidentify vulnerabilidades, y eventos de seguridad, que son las amenazas de toodetect usado. Datos recopilados por el agente de Hola se almacenan en un toohello conectado del área de trabajo de análisis de registros existente máquina virtual o una nueva área de trabajo creados por el centro de seguridad. Cuando el centro de seguridad se crea una nueva área de trabajo, ubicación geográfica de Hola de hello VM se tiene en cuenta.

> [!NOTE]
> Hola Microsoft Monitoring Agent es hello usa el mismo agente Hola Operations Management Suite (OMS), servicio de análisis de registros y System Center Operations Manager (SCOM).
>
>

Cuando se habilita la recopilación de datos para hello primera vez o cuando se migran las suscripciones, el centro de seguridad comprueba toosee si Hola Microsoft Monitoring Agent ya está instalado como una extensión de Azure en cada una de las máquinas virtuales. Si no está instalado Microsoft Monitoring Agent hello, a continuación, el centro de seguridad hará lo siguiente:

- instalar a agente de Microsoft Monitoring de hello en hello VM
   - Si un área de trabajo creado por el centro de seguridad ya existe en la misma ubicación geográfica Hola VM, Hola de Hola agente es el área de trabajo de toothis conectado
   - Si no existe un área de trabajo, centro de seguridad crea un nuevo grupo de recursos predeterminado de área de trabajo en esa ubicación geográfica y conectar el área de trabajo de hello agente toothat. convención de nomenclatura de Hello para el grupo de recursos y el área de trabajo de hello son:

       Área de trabajo: DefaultWorkspace-[subscription-ID]-[geo]

       Grupo de recursos: DefaultResouceGroup-[geo]
- instalar una solución de centro de seguridad en el área de trabajo de Hola

ubicación de Hello del área de trabajo de Hola se basa en ubicación Hola de hello VM. más información, consulte toolearn [seguridad de los datos](security-center-data-security.md).

> [!NOTE]
> Migración de tooplatform anterior, el centro de seguridad recopiló datos de seguridad de las máquinas virtuales con hello agente de supervisión de Azure y datos se almacenan en la cuenta de almacenamiento. Después de la migración de la plataforma de hello, centro de seguridad utiliza Hola Microsoft Monitoring Agent y almacén y área de trabajo toocollect Hola mismos datos. cuenta de almacenamiento de Hello puede quitarse después de la migración de Hola.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>¿Se factura para análisis de registros o OMS en áreas de trabajo de hello creadas por el centro de seguridad?
No. Las áreas de trabajo creadas por Security Center, mientras estén configuradas para OMS por facturación de nodo, no incurren en gastos de OMS. Facturación del centro de seguridad siempre se basa en las soluciones hello y directiva de seguridad Centro de seguridad instaladas en un área de trabajo:

- **Nivel gratis** : Centro de seguridad instala la solución de 'SecurityCenterFree' de hello en el área de trabajo de hello predeterminada. No se le facturará de nivel gratuito Hola.
- **Nivel estándar** : Centro de seguridad instala hello 'SecurityCenterFree' y soluciones de 'Seguridad' en Hola área de trabajo predeterminada.

Para más información, vea [Precios de Security Center ](https://azure.microsoft.com/pricing/details/security-center/). Hola precios direcciones de página cambia toosecurity el almacenamiento de datos y prorrateados facturación a partir de junio de 2017.

> [!NOTE]
> nivel de precios de OMS Hola de áreas de trabajo creadas por el centro de seguridad no afecta a la facturación de centro de seguridad.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>¿Se pueden eliminar áreas de trabajo de hello predeterminado creados por el centro de seguridad?
**No se recomienda eliminar el área de trabajo de hello predeterminada.** Centro de seguridad utiliza datos de seguridad de saludo predeterminado áreas de trabajo toostore de las máquinas virtuales.  Si elimina un área de trabajo, el centro de seguridad es no se puede toocollect estos datos y algunas recomendaciones de seguridad y las alertas no están disponibles

toorecover, Hola quitar Microsoft Monitoring Agent en el área de trabajo de hello las máquinas virtuales conectadas toohello eliminado. Centro de seguridad se vuelve a instalar al agente de Hola y crea nuevas áreas de trabajo de forma predeterminada.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>¿Qué ocurre si Hola Microsoft Monitoring Agent ya se ha instalado como una extensión en hello VM?
Centro de seguridad no reemplaza a áreas de trabajo de toouser las conexiones existentes. Centro de seguridad almacena los datos de seguridad de máquina virtual en el área de trabajo de Hola Hola ya conectado.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>¿Qué ocurre si tuviera un agente de supervisión de Microsoft instalado en el equipo de hello, pero no como una extensión?
Si Hola Microsoft Monitoring Agent se instala directamente en hello VM (no como una extensión de Azure), el centro de seguridad no se instalará Microsoft Monitoring Agent de Hola y supervisión de seguridad estará limitado.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>¿Cuál es el impacto de saludo de la eliminación de estas extensiones?
Si quita Hola extensión de supervisión de Microsoft, el centro de seguridad no son datos de seguridad de toocollect capaz de hello VM y algunas recomendaciones de seguridad y las alertas no están disponibles. Dentro de 24 horas, centro de seguridad determina que Hola VM no tiene extensión hello y vuelve a instalar Hola extensión.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>¿Cómo detener la instalación de agente automática de Hola y la creación de área de trabajo?
Puede desactivar la recopilación de datos de las suscripciones en la directiva de seguridad de hello pero no se recomienda hacerlo. La desactivación de la recopilación de datos limita las recomendaciones y las alertas de Security Center. Recopilación de datos es necesaria para las suscripciones en el nivel de precios estándar Hola. recopilación de datos de toodisable:

1. Si su suscripción está configurado para el nivel estándar de hello, abrir Directiva de seguridad de Hola para esa suscripción y seleccione hello **libre** capa.

   ![Plan de tarifa ][1]

2. A continuación, desactivar la recopilación de datos seleccionando **desactivar** en hello **directiva de seguridad: recopilación de datos** hoja.

   ![Colección de datos][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>¿Cómo quito extensiones OMS instaladas por Security Center?
También puede quitar manualmente Hola Microsoft Monitoring Agent. Sin embargo, no es recomendable porque limita las recomendaciones y las alertas de Security Center.

> [!NOTE]
> Si está habilitada la recopilación de datos, el centro de seguridad se volverá a instalar al agente de hello después de quitarla.  Debe toodisable de recopilación de datos antes de quitar manualmente el agente de Hola. Vea [¿cómo detener la creación de área de trabajo y de instalación de agente automática Hola?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) para obtener instrucciones acerca de cómo deshabilitar la recopilación de datos.
>
>

toomanually Quitar agente hello:

1.  En el portal de hello, abra **análisis de registros**.
2.  En la hoja de análisis de registros de hello, seleccione un área de trabajo:
3.  Seleccione cada máquina virtual que no desee toomonitor y seleccione **desconexión**.

   ![Quitar a agente Hola][3]

> [!NOTE]
> Si una VM Linux ya tiene un agente OMS no es una extensión, quitar extensión hello quita también el agente de Hola y cliente de hello tiene tooreinstall lo.
>
>

## <a name="existing-oms-customers"></a>Clientes de OMS existentes

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>¿Invalida Security Center las conexiones existentes entre VM y áreas de trabajo?
Si una máquina virtual ya tiene Hola Microsoft Monitoring Agent que se instala como una extensión de Azure, centro de seguridad no reemplaza la conexión de área de trabajo existente de Hola. En su lugar, el centro de seguridad usa el área de trabajo existente de Hola.

Una solución de centro de seguridad está instalado en el área de trabajo de hello si no están ya presentes y solución de hello es aplicado toohello solo máquinas virtuales relevantes. Cuando se agrega una solución, se implementa automáticamente por tooall Windows y Linux agentes conectados tooyour análisis de registros área de trabajo predeterminada. [Destinatarios de la solución](../operations-management-suite/operations-management-suite-solution-targeting.md), que es una característica OMS, permite tooapply un ámbito tooyour soluciones.

Si Hola Microsoft Monitoring Agent está instalado directamente en hello VM (no como una extensión de Azure), el centro de seguridad no se instalará Microsoft Monitoring Agent de Hola y supervisión de la seguridad está limitado.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>¿Qué debo hacer si sospecha que la migración de plataformas de datos de Hola interrumpió la conexión Hola entre uno de Mis máquinas virtuales y mi área de trabajo?
Esto no debería ocurrir. Si producen, a continuación, [crear una solicitud de soporte técnico de Azure](../azure-supportability/how-to-create-azure-support-request.md) e incluyen hello detalles siguientes:

- Id. de recurso de Azure de Hola de hello afectado VM
- Id. de recurso de Azure de Hello del área de trabajo de hello configurado en extensión de hello antes de que se interrumpió la conexión de Hola
- agente de Hola y la versión que se instaló previamente

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>¿Instala Security Center soluciones en mis áreas de trabajo OMS existentes? ¿Qué implicaciones de facturación de hello?
Cuando el centro de seguridad identifica si una máquina virtual ya está conectado tooa área de trabajo que creó, centro de seguridad permite a las soluciones en esta área de trabajo según el nivel de precios de tooyour. Hola soluciones está aplicado toohello solo máquinas virtuales de Azure pertinentes, a través de [solución destinatarios](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), por lo que sigue siendo de facturación de Hola Hola igual.

- **Nivel gratis** : Centro de seguridad instala la solución de 'SecurityCenterFree' de hello en el área de trabajo de Hola. No se le facturará de nivel gratuito Hola.
- **Nivel estándar** : Centro de seguridad instala hello 'SecurityCenterFree' y las soluciones de 'Seguridad' en Hola área de trabajo.

   ![Soluciones del área de trabajo predeterminada][4]

> [!NOTE]
> Hola solución 'Seguridad' en el análisis de registros es Hola seguridad y solución de auditoría de OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Ya tiene áreas de trabajo en mi entorno, ¿puedo usarlas toocollect datos de seguridad?
Si una máquina virtual ya tiene Hola Microsoft Monitoring Agent que se instala como una extensión de Azure, el centro de seguridad utiliza área de trabajo conectada Hola existente. Una solución de centro de seguridad está instalado en el área de trabajo de hello si no están ya presentes y solución Hola es aplicado toohello solo relevantes máquinas virtuales a través de [como destino de la solución](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Cuando el centro de seguridad instala Hola Microsoft Monitoring Agent en máquinas virtuales, usa Hola de espacios de trabajo predeterminado creado por el centro de seguridad. Pronto clientes será capaz de tooconfigure se utilizan los espacios de trabajo.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Ya tengo una solución de seguridad en mis áreas de trabajo. ¿Qué implicaciones de facturación de hello?
Hola solución seguridad y auditoría es tooenable usa características del nivel estándar de centro de seguridad de máquinas virtuales de Azure. Si la solución de seguridad y auditoría de Hola ya está instalada en un área de trabajo, el centro de seguridad utiliza solución existente de Hola. No hay ningún cambio en la facturación.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la migración de la plataforma de centro de seguridad de hello, vea

- [Migración de la plataforma de Azure Security Center](security-center-platform-migration.md)
- [Guía de solución de problemas de Azure Security Center](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
