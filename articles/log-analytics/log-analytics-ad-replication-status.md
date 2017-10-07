---
title: "estado de replicación de Active Directory con Azure Log Analytics aaaMonitor | Documentos de Microsoft"
description: "Hola paquete de solución de estado de replicación de Active Directory con regularidad supervisa el entorno de Active Directory para cualquier error de replicación y notifica los resultados de hello en el panel OMS."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Supervisión del estado de replicación de Active Directory con Azure Log Analytics

![Símbolo de AD Replication Status](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory es un componente clave de un entorno de TI empresarial. tooensure alta disponibilidad y alto rendimiento, cada controlador de dominio tiene su propia copia de base de datos de Active Directory de Hola. Controladores de dominio se replican entre sí en toopropagate ordenar los cambios a través de la empresa de Hola. Errores en este proceso de replicación pueden provocar una variedad de problemas en enterprise Hola.

Hola paquete de solución de estado de replicación de AD con regularidad supervisa el entorno de Active Directory para cualquier error de replicación y notifica los resultados de hello en el panel OMS.

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

* Debe instalar a agentes en los controladores de dominio que son miembros de hello dominio toobe evaluada. O bien, debe instalar los agentes en servidores miembro y configurar tooOMS de datos de replicación de hello agentes toosend AD. toounderstand tooconnect tooOMS de equipos de Windows, vea [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md). Si el controlador de dominio ya forma parte de un entorno de System Center Operations Manager existente que desea tooconnect tooOMS, consulte [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md).
* Agregar tooyour solución Hola estado de replicación de Active Directory que se describe el área de trabajo OMS mediante el proceso de hello en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).  No es necesario realizar ninguna configuración más.

## <a name="ad-replication-status-data-collection-details"></a>Detalles de recopilación de datos de Estado de replicación de AD
Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de estado de replicación de AD.

| plataforma | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |cada cinco días |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Opcionalmente, puede habilitar un tooOMS de datos de controlador de dominio no toosend AD
Si no desea tooconnect de cualquiera de los controladores de dominio directamente tooOMS, puede usar cualquier otro equipo conectado a OMS en su toocollect dominio datos de hello solución de estado de replicación de AD pack y que se envíe datos de Hola.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable un tooOMS de datos de controlador de dominio no toosend AD
1. Compruebe que ese equipo hello es un miembro de dominio de Hola que desea toomonitor con soluciones de estado de replicación de AD de Hola.
2. [Conectar tooOMS de equipo de Windows hello](log-analytics-windows-agents.md) o [conéctela mediante su tooOMS de entorno de Operations Manager existente](log-analytics-om-agents.md), si ya no está conectado.
3. En ese equipo, establezca Hola después de la clave del registro:

   * Clave: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * Valor: **IsTarget**
   * Datos del valor: **true**

   > [!NOTE]
   > Estos cambios no surtirán efecto hasta la Hola de reinicio del servicio del agente de supervisión de Microsoft (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Descripción de los errores de replicación
Una vez que tenga datos de estado de replicación de AD enviados tooOMS, verá un toohello similar de mosaico después de imagen en el panel de OMS de Hola que indica cuántos errores de replicación tiene actualmente.  
![Icono del Estado de replicación de AD](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Errores críticos de replicación** son errores que son igual o superior al 75% de hello [desecho](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) para el bosque de Active Directory.

Al hacer clic en el icono de hello, puede ver más información sobre los errores de Hola.
![Panel del estado de replicación de AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Estado del servidor de destino y estado del servidor de origen
Estas columnas muestran el estado de Hola de servidores de destino y los servidores de origen que experimentan errores de replicación. número de Hello después de cada nombre de controlador de dominio indica Hola de errores de replicación en ese controlador de dominio.

errores de Hola para los servidores de destino y los servidores de origen se muestran debido a algunos problemas son más fácil tootroubleshoot desde la perspectiva del servidor de origen de Hola y otros desde la perspectiva del servidor de destino de Hola.

En este ejemplo, puede ver que muchos servidores de destino tienen aproximadamente Hola el mismo número de errores, pero no hay un servidor de origen (ADDC35) que tiene muchas más errores que Hola todos los otros usuarios. Es probable que haya algún problema en ADDC35 que está causando a asociados de replicación de toofail toosend datos tooits. Solucionar problemas de hello en ADDC35 puede resolver muchos de los errores de Hola que aparecen en el área de servidor de destino de Hola.

### <a name="replication-error-types"></a>Tipos de errores de replicación
Esta área proporciona información acerca de los tipos de Hola de errores detectados en toda la empresa. Cada error tiene un código numérico único y un mensaje que le permitirá determinar Hola causa del error de Hola.

anillo de Hello en la parte superior de hello ofrece una idea de que aparezcan errores más y menos frecuentemente en su entorno.

Muestra cuando varios controladores de dominio producen Hola mismo error de replicación. En este caso, puede ser capaz de toodiscover o identificar una solución en un controlador de dominio, y repita en otros controladores de dominio afectados por hello mismo error.

### <a name="tombstone-lifetime"></a>vigencia de objetos de desecho
duración de objetos de desecho de Hello determina cuánto tiempo un objeto eliminado, se hace referencia tooas un marcador de exclusión, se conserva en la base de datos de Active Directory de Hola. Cuando una duración de objetos de desecho de objeto eliminado pasadas hello, un proceso de recopilación de elementos no utilizados lo elimina automáticamente de la base de datos de Active Directory de Hola.

duración de objetos de desecho de Hello predeterminada es de 180 días para las versiones más recientes de Windows, pero era 60 días en versiones anteriores y puede cambiarse explícitamente por un administrador de Active Directory.

Es importante tooknow si experimenta errores de replicación que se aproximan a o están más allá de la duración de objetos de desecho de Hola. Si dos controladores de dominio produce un error de replicación que se conserva más allá de la duración de objetos de desecho de hello, es deshabilitar la replicación entre los dos controladores de dominio, incluso si se corrige Hola error de replicación subyacente.

Hola área desecho le ayuda a identificar los lugares donde replicación deshabilitada corre el riesgo de que ocurra. Cada error contenido en hello **más de 100% TSL** categoría representa una partición que no se ha replicado entre su servidor de origen y destino para al menos de desecho de hello para el bosque de Hola.

En esta situación, simplemente corrige los errores de replicación de hello no será suficiente. Como mínimo, necesita toomanually investigar tooidentify y limpiar objetos persistentes antes de poder reiniciar la replicación. Incluso puede que tenga toodecommission un controlador de dominio.

En suma tooidentifying los errores de replicación que se conservan más allá de la duración de objetos de desecho de hello, también desea toopay atención tooany errores caer en hello **50 y un 75% TSL** o **TSL 75-100%** categorías.

Se trata de errores que son claramente persistentes y no transitoria, por lo que es probable que necesiten su tooresolve intervención. Hola buenas noticias son que no hayan alcanzado aún desecho Hola. Si soluciona estos problemas rápidamente y *antes de* que lleguen a la duración de objetos de desecho de hello, puede reiniciar la replicación con una intervención manual mínima.

Como se indicó anteriormente, icono de panel de hello para la solución de estado de replicación de AD hello muestra el número de Hola de *crítico* en su entorno, que se define como errores que son más del 75% de duración de objetos de desecho (incluidos los errores de replicación errores de más de 100% de TSL). Procurar tookeep este número en 0.

> [!NOTE]
> Todos los cálculos de porcentaje de duración de objetos de desecho de Hola se basan en la duración de objetos de desecho real de hello para el bosque de Active Directory, por lo que puede confiar en que los porcentajes son correctas, incluso si tiene un valor de duración de objetos de desecho personalizado establecido.
>
>

### <a name="ad-replication-status-details"></a>Detalles del Estado de replicación de AD
Al hacer clic en cualquier elemento en una de las listas de hello, puede ver detalles adicionales sobre mediante la búsqueda de registros. resultados de Hello son tooshow filtrado único Hola errores relacionados toothat elemento. Por ejemplo, si hace clic en controlador de dominio de primer Hola aparece en **estado del servidor de destino (ADDC02)**, verá resultados de búsqueda filtran tooshow errores con ese controlador de dominio aparece como servidor de destino de hello:

![Errores del Estado de replicación de AD en resultados de búsqueda](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

Desde aquí, puede filtrar aún más, modifique la consulta de búsqueda de Hola y así sucesivamente. Para obtener más información acerca del uso de hello búsqueda de registros, vea [búsquedas de registro](log-analytics-log-searches.md).

Hola **HelpLink** campo muestra hello URL de una página de TechNet con detalles adicionales acerca del error específico. Puede copiar y pegar este vínculo en la información de toosee de ventana de explorador sobre solución de problemas y corregir el error de Hola.

También puede hacer clic en **exportar** tooexport Hola da como resultado tooExcel. Exportar datos de hello puede ayudarle a visualizar los datos de error de replicación en cualquier forma que desee.

![errores del Estado de replicación de AD exportados en Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>P+F del Estado de replicación de AD
**P: ¿Con qué frecuencia se actualizan los datos del Estado de replicación de AD?**
R: información de Hola se actualiza cada cinco días.

**P: ¿existe un tooconfigure de forma que la frecuencia de actualización de estos datos?**
R: De momento, no.

**P: ¿necesito tooadd todos de Mi área de trabajo de dominio controladores toomy OMS en estado de replicación de orden toosee?**
R: No, basta con que se agregue un único controlador de dominio. Si tiene varios controladores de dominio en el área de trabajo OMS, datos de todas ellas se envían tooOMS.

**P: no deseo tooadd cualquier área de trabajo OMS de dominio controladores toomy. ¿Puedo seguir usando Hola solución de estado de replicación de AD?**
R: Sí. Se puede establecer el valor de Hola de un tooenable de clave del registro. Vea [tooenable un tooOMS de datos de controlador de dominio no toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**P: ¿cuál es el nombre de hello del proceso de Hola que Hola la recopilación de datos?**
R: AdvisorAssessment.exe

**P: ¿cuánto tarda para toobe de datos que se recopilan?**
R: tiempo de recopilación de datos de depende Hola tamaño del entorno de Active Directory de hello, pero suele tarda menos de 15 minutos.

**R: ¿Qué tipo de datos se recopilan?**
R: La información de replicación se recopila a través de LDAP.

**P: ¿existe una manera tooconfigure cuando los datos se recopilan?**
R: De momento, no.

**P: ¿qué hacer permisos necesito toocollect datos?**
R: permisos de usuario normal de tooActive Directory son suficientes.

## <a name="troubleshoot-data-collection-problems"></a>Solución de problemas de recopilación de datos
Datos de pedidos toocollect, paquete de solución de estado de replicación de hello AD requiere al menos un dominio controlador toobe conectado tooyour área de trabajo OMS. Hasta que se conecte a un controlador de dominio, aparece un mensaje que indica que **todavía se están recopilando datos**.

Si necesita ayuda para conectarse a uno de los controladores de dominio, puede ver la documentación en [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md). O bien, si el controlador de dominio ya está conectado tooan entorno de System Center Operations Manager existente, puede ver la documentación en [tooLog conectar System Center Operations Manager análisis](log-analytics-om-agents.md).

Si no desea tooconnect cualquiera de los controladores de dominio directamente tooOMS o tooSCOM, consulte [tooenable un tooOMS de datos de controlador de dominio no toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de estado de replicación de Active Directory.
