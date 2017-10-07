---
title: aaaTroubleshoot lento copia de seguridad de archivos y carpetas de copia de seguridad de Azure | Documentos de Microsoft
description: "Proporciona instrucciones toohelp de solución de problemas diagnosticar causa Hola de problemas de rendimiento de copia de seguridad de Azure"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Solución de problemas de lentitud en la copia de seguridad de archivos y carpetas en Copia de seguridad de Azure
Este artículo proporciona orientación para la solución toohelp diagnosticar causa de Hola de rendimiento lento de copia de seguridad de archivos y carpetas cuando se usa copias de seguridad de Azure. Cuando usas tooback de agente de copia de seguridad de Azure de hello seguridad de archivos, el proceso de copia de seguridad de hello puede tardar más tiempo del esperado. Este retraso puede deberse a uno o más de hello siguientes:

* [Hay cuellos de botella de rendimiento en el equipo de Hola que se hace copia.](#cause1)
* [Otro software antivirus o proceso está interfiriendo con el proceso de copia de seguridad de Azure de Hola.](#cause2)
* [agente de copia de seguridad de saludo se está ejecutando en una máquina virtual (VM) de Azure.](#cause3)  
* [Se realiza una copia de seguridad de un número elevado (varios millones) de archivos.](#cause4)

Antes de iniciar la solución de problemas, recomendamos que descargue e instale hello [agente de copia de seguridad de Azure más reciente](http://aka.ms/azurebackup_agent). Asegúrese de toofix de agente de copia de seguridad de actualizaciones frecuentes toohello diversos problemas, agregar características y mejorar el rendimiento.

También recomendamos que revise hello [preguntas más frecuentes de servicio de copia de seguridad de Azure](backup-azure-backup-faq.md) toomake seguro no experimenta alguno de los problemas de configuración comunes de Hola.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Causa: Cuellos de botella de rendimiento en el equipo de Hola
Cuellos de botella en el equipo de Hola que se hace copia pueden provocar retrasos. Por ejemplo, hello toodisk de tooread o de escritura de capacidad del equipo o datos de toosend de ancho de banda disponible a través de la red hello, puede producir cuellos de botella.

Windows proporciona una herramienta integrada que se denomina [Monitor de rendimiento](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect estos cuellos de botella.

Estos son algunos contadores de rendimiento e intervalos que pueden resultar útiles para diagnosticar cuellos de botella, con el fin de que las copias de seguridad sean óptimas.

| Contador | Estado |
| --- | --- |
| Logical Disk(Physical Disk) [Disco lógico (disco físico)]--% de inactividad |• 100% inactivo too50% inactivo = correcto</br>• too20 inactivo 49% % inactivo = advertencia o el Monitor</br>• too0 inactivo 19% % inactivo = crítico o fuera de especificación |
| Logical Disk(Physical Disk) [Disco lógico (disco físico)]--% promedio Disk Sec Read or Write (Segundos de disco de lectura o escritura) |• 0,001 ms too0.015 ms = correcto</br>• 0,015 ms too0.025 ms = advertencia o el Monitor</br>• 0.026 o más = Situación crítica o fuera de la especificación |
| Logical Disk(Physical Disk) [Disco lógico (disco físico)] -- Longitud actual de la cola de disco (para todas las instancias) |80 solicitudes durante más de 6 minutos |
| Memoria: Pool Non Paged Bytes (Bytes de bloque no paginado) |• Menos del 60 % del grupo consumido = Correcto<br>• el 61% too80% de grupo consumido = advertencia o el Monitor</br>• Más del 80 % del grupo consumido = Situación crítica o fuera de la especificación |
| Memoria: Bytes de bloque paginado |• Menos del 60 % del grupo consumido = Correcto</br>• el 61% too80% de grupo consumido = advertencia o el Monitor</br>• Más del 80 % del grupo consumido = Situación crítica o fuera de la especificación |
| Memoria: Megabytes disponibles |• El 50 % de la memoria libre, o más, está disponible = Correcto</br>• El 25 % de la memoria libre está disponible = Supervisión</br>• El 10 % de la memoria libre está disponible = Advertencia</br>• Menos de 100 MB o del 5 % de memoria libre está disponible = Situación crítica o fuera de la especificación. |
| Procesador: \%Tiempo de procesador (todas las instancias) |• Menos del 60 % consumido = Correcto</br>• el 61% too90% consumido = Monitor o precaución</br>• 91% too100% consumido = crítico |

> [!NOTE]
> Si determina que la infraestructura de hello es culpable hello, se recomienda desfragmente los discos de hello con regularidad para mejorar el rendimiento.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Causa: otro proceso o software antivirus interfiere con Copia de seguridad de Azure.
Hemos visto varias instancias donde otros procesos en el sistema de Windows hello han afectado negativamente al rendimiento de hello proceso del agente de copia de seguridad de Azure. Por ejemplo, si usa el agente de copia de seguridad de Azure de hello y otro tooback programa los datos, o si está ejecutando software antivirus y un bloqueo en archivos toobe realizó la copia, Hola varios bloqueos de archivos podrían ocasionar la contención. En esta situación, podría producirse un error en la copia de seguridad de Hola u Hola trabajo podría tardar más tiempo del esperado.

Hola mejor recomendación en este escenario es tooturn desactivar Hola otro toosee del programa de copia de seguridad si cambia la hora de copia de seguridad de hello para el agente de copia de seguridad de Azure Hola. Por lo general, asegurándose de que no están ejecutando varios trabajos de copia de seguridad en hello el mismo tiempo es suficiente tooprevent les afecten a entre sí.

Para los programas antivirus, se recomienda que excluya siguiente Hola archivos y ubicaciones:

* C:\Archivos de programa\Microsoft Azure Recovery Services Agent\bin\cbengine.exe como proceso.
* Carpetas de C:\Archivos de programa\Microsoft Azure Recovery Services Agent\.
* Scratch ubicación (si no está utilizando la ubicación estándar de hello)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Causa: el agente de Copia de seguridad se ejecuta en una máquina virtual de Azure.
Si está ejecutando el agente de copia de seguridad de hello en una máquina virtual, rendimiento será más lento que cuando se ejecuta en una máquina física. Esto es lo esperado debido a limitaciones de tooIOPS.  Sin embargo, puede optimizar el rendimiento de hello cambiando las unidades de datos de Hola que están haciendo copias de seguridad tooAzure almacenamiento Premium. Estamos trabajando para solucionar este problema y corrección de hello estará disponible en futuras versiones.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Causa: se realiza una copia de seguridad de un número elevado (varios millones) de archivos.
El movimiento de un gran volumen de datos tarda más tiempo en realizarse el de un volumen más pequeño. En algunos casos, está relacionado con el tiempo de copia de seguridad toonot Hola sólo el tamaño de datos hello, sino también el número de Hola de archivos o carpetas. Esto es especialmente cierto cuando millones de archivos pequeños (unos tooa bytes algunos kilobytes) se esté realizando una copia.

Este comportamiento se produce porque mientras es realizar una copia de seguridad de los datos de Hola y moverlo tooAzure, Azure simultáneamente es catalogar los archivos. En algunos casos poco frecuentes, la operación de catálogo de hello podría tardar más tiempo del esperado.

Hola después indicadores puede ayudarle a entender el cuello de botella de Hola y en consecuencia funcionan sobre los pasos siguientes hello:

* **Interfaz de usuario mostrará el progreso de transferencia de datos de hello**. todavía se transfieren datos de Hola. ancho de banda de red de Hola o tamaño de Hola de datos podría estar provocando retrasos.
* **Interfaz de usuario no muestra el progreso de transferencia de datos de hello**. Hola abrir registros ubicado en Agent\Temp de servicios de recuperación de Azure C:\Microsoft y, a continuación, busque hello FileProvider::EndData entrada en los registros de Hola. Esta entrada indica que finalizó la transferencia de datos de Hola y Hola catálogo operación se realiza. No cancelar trabajos de copia de seguridad de Hola. En su lugar, espere un poco más toofinish de operación de catálogo de Hola. Si persiste el problema de hello, póngase en contacto con [soporte técnico de Azure](https://portal.azure.com/#create/Microsoft.Support).
