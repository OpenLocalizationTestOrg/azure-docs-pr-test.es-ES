---
title: "capacidad de replicación de aaaEstimate en Azure | Documentos de Microsoft"
description: "Utilizar esta capacidad de tooestimate de artículo al replicar con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Planeación de la capacidad para la protección de máquinas virtuales y de los servidores físicos en Azure Site Recovery

herramienta de programador de capacidad de recuperación de sitio de Azure Hola ayuda a toofigure a sus necesidades de capacidad al replicar las máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos de Windows o Linux, con Azure Site Recovery.

Usar Hola planificador de capacidad de recuperación de sitio tooanalyze su entorno de origen y las cargas de trabajo, calcular las necesidades de ancho de banda y recursos del servidor que necesitará para la ubicación de origen de Hola y recursos de hello (máquinas virtuales y almacenamiento etcetera), que necesita en el destino de Hola ubicación.

Puede ejecutar la herramienta Hola de dos modos:

* **Planeación de rápido**: ejecutar la herramienta de hello en este modo tooget red y el servidor las proyecciones basadas en un número medio de las máquinas virtuales, discos, almacenamiento y tasa de cambio.
* **Planificación detallada**: ejecutar la herramienta de hello en este modo y proporcionar detalles de cada carga de trabajo en el nivel de máquina virtual. Analice la compatibilidad de la máquina virtual y obtenga proyecciones de red y del servidor.

## <a name="before-you-start"></a>Antes de comenzar


1. Recopile información sobre su entorno, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.
2. Identifique la tasa de cambio (renovación) diaria para los datos replicados. toodo esto:

   * Si replica máquinas virtuales de Hyper-V, a continuación, descargue hello [herramienta de planeación de capacidad de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tasa de cambio de tooget Hola. [Más información](site-recovery-capacity-planning-for-hyper-v-replication.md) sobre esta herramienta. Se recomienda que ejecutar esta herramienta en una semana toocapture promedios.
   * Si replica máquinas virtuales de VMware, usar hello [planificador de implementación de recuperación de sitio de Azure](./site-recovery-deployment-planner.md) toofigure out Hola tasa de renovación.
   * Si se están replicando servidores físicos, deberá tooestimate manualmente.

## <a name="run-hello-quick-planner"></a>Ejecute hello Planner rápido
1. Descargue y abra hello [planificador de capacidad de recuperación de sitio de Azure](http://aka.ms/asr-capacity-planner-excel) herramienta. Necesita toorun macros, así que seleccione Edición tooenable y habilitar contenido cuando se le solicite.
2. En **seleccione un tipo de programador** seleccione **rápido Planner** Hola cuadro de lista.

   ![Introducción](./media/site-recovery-capacity-planner/getting-started.png)
3. Hola **Capacity Planner** hoja de cálculo, escriba información de hello necesario. Debe completar todos los campos de hello con un círculo rojo en la siguiente captura de pantalla de Hola.

   * En **seleccionar el escenario**, elija **tooAzure de Hyper-V** o **tooAzure físicos/VMware**.
   * En **(%) de la tasa de cambio de datos diarios medio**, colocar información de hello recopilar usando hello [herramienta de planeación de capacidad de Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) o hello [planificador de implementación de recuperación de sitio de Azure](./site-recovery-deployment-planner.md).  
   * **Compresión** solo se aplica toocompression que ofrece al replicar máquinas virtuales de VMware o tooAzure de servidores físicos. Estimar el 30% o más, pero puede modificar la configuración de hello según sea necesario. Para la replicación de máquinas virtuales de Hyper-V tooAzure compresión, puede usar un dispositivo de terceros como Riverbed.
   * En **Entradas de retención** especifique durante cuánto tiempo hay que conservar las réplicas. Si replica VMware o servidores físicos, el valor de Hola de entrada en días. Si replica Hyper-V, especifique tiempo hello en horas.
   * En **debe completarse el número de horas en que la replicación inicial para el lote de Hola de máquinas virtuales** y **número de máquinas virtuales por lote de la replicación inicial**, entrada de configuración que se usa requisitos de la replicación inicial de toocompute.  Cuando se implementa la recuperación del sitio, se debe cargar el conjunto de datos inicial completa Hola.

   ![Entradas](./media/site-recovery-capacity-planner/inputs.png)
4. Una vez que haya colocado en valores de hello para el entorno de origen de hello, salida mostrada incluye:

   * **Ancho de banda necesario para la replicación diferencial** (MB/s). Ancho de banda de red para la replicación de datos se calcula en hello promedio tasa de cambio de datos diario.
   * **Ancho de banda necesario para la replicación inicial** (MB/s). Ancho de banda de red para la replicación inicial se calcula en valores de la replicación inicial de Hola que coloque en.
   * **Almacenamiento necesario (en GB)** es Hola almacenamiento de Azure total necesario.
   * **Total de e/s por segundo en las cuentas de almacenamiento estándar** se calcula basándose en el tamaño de unidad IOPS de 8 K Hola total estándar en cuentas de almacenamiento.  Para hello Planner rápido, número de Hola se calcula según en todos los discos de máquinas virtuales de origen de Hola y diariamente de tasa de cambio de datos. Para Hola Planner detallada, número de hello es calculado en función de número total de máquinas virtuales que están asignada toostandard máquinas virtuales de Azure y velocidad en esas máquinas virtuales de cambio de datos.
   * **Número de cuentas de almacenamiento estándar** proporciona el número total de Hola de almacenamiento estándar las cuentas necesarias tooprotect hello las máquinas virtuales. Una cuenta de almacenamiento estándar puede contener una too20000 e/s por segundo en todas las máquinas virtuales de hello en un almacenamiento estándar y se admite un máximo de 500 IOPS por disco.
   * **Número de discos de blob necesarios** proporciona Hola número de discos que se creará en el almacenamiento de Azure.
   * **Número de cuentas de almacenamiento premium requerido** proporciona el número total de Hola de tooprotect de las cuentas necesarias de almacenamiento premium hello las máquinas virtuales. Una máquina virtual de origen con una IOPS elevada (más de 20000) necesita una cuenta de Premium Storage. Una cuenta de almacenamiento premium puede contener una too80000 e/s por segundo.
   * **Total de e/s por segundo en almacenamiento premium** se calcula basándose en el tamaño de la unidad de 256 K IOPS Hola premium total en cuentas de almacenamiento.  Para hello Planner rápido, número de Hola se calcula según en todos los discos de máquinas virtuales de origen de Hola y diariamente de tasa de cambio de datos. Para Hola Planner detallada, número de hello es número total de hello según calculado de máquinas virtuales que están asignada toopremium (serie DS y GS) de la máquina virtual de Azure y datos Hola cambian frecuencia en esas máquinas virtuales.
   * **Número de servidores de configuración necesarios** muestra cuántos servidores de configuración son necesarios para la implementación de Hola.
   * **Número de servidores de proceso adicionales necesarios** muestra si los servidores de proceso adicionales son necesarios, en el servidor de procesos de toohello de suma que se ejecuta en el servidor de configuración de Hola de forma predeterminada.
   * **almacenamiento adicional de 100% en el origen de hello** muestra si se requiere almacenamiento adicional en la ubicación de origen de Hola.

   ![Salida](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Ejecución Hola Planner detallada

1. Descargue y abra hello [planificador de capacidad de recuperación de sitio de Azure](http://aka.ms/asr-capacity-planner-excel) herramienta. Necesita toorun macros, así que seleccione Edición tooenable y habilitar contenido cuando se le solicite.
2. En **seleccione un tipo de programador**, seleccione **Planner detallada** Hola cuadro de lista.

   ![Introducción](./media/site-recovery-capacity-planner/getting-started-2.png)
3. Hola **calificación de carga de trabajo** hoja de cálculo, escriba información de hello necesario. Debe completar Hola todos los campos marcados.

   * En **núcleos de procesador**, especifique el número total de Hola de núcleos en un servidor de origen.
   * En **la asignación de memoria en MB**, especifique el tamaño de hello RAM de un servidor de origen.
   * Hola **número de NIC**, especifique el número de Hola de adaptadores de red en un servidor de origen.
   * En **Total de almacenamiento (en GB)**, especifique el tamaño total de Hola Hola de almacenamiento de VM. Por ejemplo, si el servidor de origen de hello tiene 3 discos con 500 GB, el tamaño de almacenamiento total es 1500 GB.
   * En **número de discos conectados**, especifique el número total de Hola de discos de un servidor de origen.
   * En **utilización de la capacidad de disco**, especificar la utilización media de Hola.
   * En **(%) de velocidad de cambio diariamente**, especificar datos diario de hello tasa de cambio de un servidor de origen.
   * En **tamaño de asignación de Azure**, escriba el tamaño de VM de Azure de Hola que desea toomap. Si no desea toodo este manualmente, haga clic en **máquinas virtuales de IaaS de proceso**. Si una configuración manual de entrada y, a continuación, haga clic en máquinas virtuales de IaaS de proceso, configuración manual de hello podría sobrescribirse porque el proceso de cálculo de hello identifica automáticamente la mejor coincidencia de hello en el tamaño de la máquina virtual de Azure.

   ![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Al hacer clic en **Procesar máquinas virtuales de IaaS** :

   * Valida las entradas obligatorias de Hola.
   * Calcula las IOPS y sugiere Hola mejor VM de Azure aize coincidencia para cada VM, que es apto para la replicación tooAzure. Se produce un error si no se detecta un tamaño adecuado para la máquina virtual de Azure. Por ejemplo, si el número de Hola de discos conectados en 65, se emite un error porque el tamaño máximo de hello VM de Azure es 64.
   * Sugiere una cuenta de almacenamiento que puede usar para una máquina virtual de Azure.
   * Calcula el número total de Hola de cuentas de almacenamiento estándar y cuentas de almacenamiento premium necesarias para la carga de trabajo de Hola. Desplácese hacia abajo tooview Hola tipo de almacenamiento de Azure y cuenta de almacenamiento de Hola que puede usarse para un servidor de origen.
   * Completa y ordena el resto de Hola de tabla de hello en función de tipo de almacenamiento necesaria (standard o premium) asignado para una máquina virtual y el número de Hola de los discos conectados. Para todas las máquinas virtuales que cumplen los requisitos de Hola de Azure, Hola columna **VM está calificado?** muestra **Sí**. Si una máquina virtual no puede hacerse tooAzure, se muestra un error.

Columnas AA tooAE salida y proporcionan información para cada máquina virtual.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Ejemplo
Por ejemplo, para seis máquinas virtuales con valores de hello que se muestra en la tabla de hello, herramienta de hello calcula y asigna la mejor coincidencia de máquina virtual de Azure hello y requisitos de almacenamiento de Azure de Hola.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* En la salida de ejemplo de Hola, tenga en cuenta Hola siguiente:

  * Hola primera columna es una columna de validación para las máquinas virtuales de hello, discos y la renovación.
  * Se requieren dos cuentas de almacenamiento estándar y una cuenta de almacenamiento premium para las cinco máquinas virtuales.
  * VM3 no cumple los requisitos para la protección porque uno o más discos tienen más de 1 TB.
  * VM1 y VM2 pueden usar la primera cuenta de almacenamiento estándar Hola
  * VM4 puede usar la segunda cuenta de almacenamiento estándar Hola.
  * VM5 y VM6 necesitan una cuenta de Premium Storage y ambas pueden usar una única cuenta.

    > [!NOTE]
    > E/s por segundo en almacenamiento estándar y premium se calculan en hello nivel de máquina virtual y no en el nivel de disco. Una máquina virtual estándar puede controlar la too500 de IOPS por disco. Si las IOPS de un disco son más de 500, necesitará Premium Storage. Sin embargo, si IOPS para un disco son más de 500, pero IOPS para discos de máquina virtual total Hola son dentro de hello es compatible con límites de máquina virtual de Azure estándares (tamaño de máquina virtual, número de discos, número de adaptadores, CPU, memoria), programador de hello toma una máquina virtual y no Hola DS o GS serie estándar. Necesita celda de tamaño de Azure de asignación de Hola de actualización de toomanually con serie DS o GS correspondiente máquina virtual.


Después de que todos los detalles de hello están instalados, haga clic en **herramienta de planeación de enviar datos toohello** tooopen hello **Capacity Planner** cargas de trabajo resaltado, tooshow si son aptos para la protección o no.

### <a name="submit-data-in-hello-capacity-planner"></a>Enviar datos de hello Capacity Planner
1. Cuando abre hello **Capacity Planner** hoja de cálculo se rellena en función de configuración de Hola que haya especificado. Hello word 'Carga de trabajo' aparece en hello **origen de entradas de Infra** celda, tooshow que Hola entrada es hello **calificación de carga de trabajo** hoja de cálculo.
2. Si desea que los cambios de toomake, necesita hello toomodify **calificación de carga de trabajo** hoja de cálculo y haga clic en **herramienta de planeación de enviar datos toohello** nuevo.  

   ![Capacity Planner](./media/site-recovery-capacity-planner/capacity-planner.png)
