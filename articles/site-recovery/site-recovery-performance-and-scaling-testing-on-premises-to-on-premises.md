---
title: "resultados de aaaTest para la replicación de Hyper-V entre sitios con Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo proporciona información acerca de la prueba de rendimiento de replicación de local tooon local de máquinas virtuales de Hyper-V con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Resultados de pruebas para la replicación de Hyper-V local tooon local con Site Recovery

Puede usar Microsoft Azure Site Recovery tooorchestrate y administrar la replicación de máquinas virtuales y servidores físicos tooAzure o tooa centro de datos secundario. Este artículo proporciona resultados Hola de pruebas de rendimiento que hicimos cuando la replicación de máquinas virtuales de Hyper-V entre dos centros de datos locales.

## <a name="test-goals"></a>Objetivos de la prueba

objetivo de Hola de prueba fue tooexamine cómo Azure Site Recovery se realiza durante la replicación de estado estable. La replicación de estado estable se produce cuando se ha completado la replicación inicial de máquinas virtuales y se sincronizan los cambios diferenciales. Sea toomeasure importante el rendimiento con estado estable porque lo está en estado de Hola que permanezcan mayoría de las máquinas virtuales a menos que se producen interrupciones inesperadas.

implementación de prueba de Hello constaba de dos sitios locales con un servidor VMM en cada sitio. Esta implementación de prueba es típica de una implementación de oficina central/sucursal, con la oficina central actúa como sitio primario de Hola y sucursal hello como sitio secundario o de recuperación de Hola.

## <a name="what-we-did"></a>¿Qué hicimos?

Aquí es lo que en prueba Hola pasará:

1. Cree máquinas virtuales mediante plantillas de VMM.
2. Inicie las máquinas virtuales y capture las métricas de rendimiento de línea de base  más de 12 horas.
3. Nubes creadas en servidores VMM principal y de recuperación.
4. Configure la protección de la nube en Azure Site Recovery, incluida la asignación de nubes de origen y de recuperación.
5. Habilitar la protección para máquinas virtuales y permitirles toocomplete la replicación inicial.
6. Espere un par de horas a que se haga la estabilización del sistema.
7. Capture las métricas de rendimiento más de 12 horas para asegurarse de que todas las máquinas virtuales permanecen en un estado de replicación previsto durante esas 12 horas.
8. Medir la distancia de hello entre las métricas de rendimiento de línea de base de Hola y Hola métricas de rendimiento de replicación.


## <a name="primary-server-performance"></a>Rendimiento del servidor principal

* Réplica de Hyper-V asincrónicamente realiza un seguimiento de archivo de registro del tooa cambios con sobrecarga mínima de almacenamiento en el servidor principal de Hola.
* Réplica de Hyper-V utiliza la sobrecarga de IOPS de toominimize de caché de memoria de automantenimiento automática para el seguimiento. Almacena toohello escrituras VHDX en memoria y vaciados en archivo de registro de hello antes de hello tiempo dicho registro Hola se envía toohello sitio de recuperación. Un vaciado del disco también ocurre si Hola escrituras alcanzan un límite predeterminado.
* gráfico de Hello siguiente muestra la sobrecarga de IOPS de estado estable de hello para la replicación. Podemos ver que hello tooreplication due sobrecarga de IOPS es aproximadamente el 5% que es bastante bajo.

![Resultados principales](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Réplica de Hyper-V utiliza memoria Hola principal toooptimize disco al rendimiento del servidor. Como se muestra en hello después de gráfico, sobrecarga de memoria en todos los servidores en clúster de hello principal es marginal. Hola sobrecarga de memoria mostrada es porcentaje Hola de memoria utilizada por la memoria de toohello total instalada en comparación con la replicación en el servidor de Hyper-V de Hola.

![Resultados principales](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

La réplica de Hyper-V tiene una sobrecarga de CPU como mínimo. Como se muestra en el gráfico de hello, sobrecarga de replicación está en rango de Hola de % 2 y 3.

![Resultados principales](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Rendimiento del servidor secundario (recuperación)

Réplica de Hyper-V usa una pequeña cantidad de memoria Hola recuperación server toooptimize Hola número de operaciones de almacenamiento. gráfico de Hello resume el uso de memoria de hello en el servidor de recuperación de Hola. Hola sobrecarga de memoria mostrada es porcentaje Hola de memoria utilizada por la memoria de toohello total instalada en comparación con la replicación en el servidor de Hyper-V de Hola.

![Resultados secundarios](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

cantidad de Hola de operaciones de E/S en el sitio de recuperación de hello es una función del número de Hola de operaciones de escritura en el sitio primario de Hola. Vamos a mirar Hola total las operaciones de E/S en el sitio de recuperación de hello en comparación con las operaciones de E/S total hello y operaciones de escritura en el sitio primario de Hola. gráficos de Hello Mostrar total hello que es de e/s por segundo en el sitio de recuperación de Hola

* Hola aproximadamente 1,5 veces IOPS de escritura en hello principal.
* Aproximadamente el 37% de hello total de e/s por segundo en el sitio primario de Hola.

![Resultados secundarios](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Resultados secundarios](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Repercusión en el uso de la red

Un promedio de 275 Mb por segundo de ancho de banda de red se usó entre Hola primario y nodos de recuperación (con compresión habilitada) con un ancho de banda existente de 5 Gb por segundo.

![Utilización de la red de resultados](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Repercusión en el rendimiento de la máquina virtual

Una consideración importante es el impacto de saludo de la replicación en cargas de trabajo de producción ejecutan en máquinas virtuales de Hola. Si el sitio primario de hello está adecuadamente aprovisionado para replicación, no debe haber ningún impacto en cargas de trabajo de Hola. Mecanismo de seguimiento ligero de réplica de Hyper-V se asegura de que no se vean afectadas las cargas de trabajo que se ejecutan en máquinas virtuales de Hola durante la replicación en estado estable. Esto se ilustra en hello después de gráficos.

Este gráfico muestra el IOPS realizado por máquinas virtuales que ejecutan distintas cargas de trabajo antes y después de habilitar la replicación. Puede observar que no hay ninguna diferencia entre dos Hola.

![Resultados del efecto de réplica](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Hello siguiente gráfico muestra el rendimiento de Hola de máquinas virtuales que ejecutan distintas cargas de trabajo antes y después de habilita la replicación. Puede observar que la replicación no tiene ningún impacto significativo.

![Resultado de efectos de la réplica](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Conclusión

resultados de Hello muestran claramente que Azure Site Recovery, junto con la réplica de Hyper-V, se escala bien con una sobrecarga mínima en un clúster de gran tamaño.  Azure Site Recovery proporciona una implementación, replicación, administración y supervisión simples. Réplica de Hyper-V proporciona infraestructura necesaria de hello para el escalado de replicación correcto. Para planear una implementación óptima, sugerimos descargar hello [planificador de capacidad de réplica de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Detalles del entorno de la prueba

### <a name="primary-site"></a>Sitio principal

* sitio primario de Hello tiene un clúster que contiene cinco servidores de Hyper-V que ejecutan 470 máquinas virtuales.
* máquinas virtuales de Hello ejecutan distintas cargas de trabajo y todos tienen habilitada la protección de Azure Site Recovery.
* Una red SAN iSCSI proporciona almacenamiento para el nodo de clúster de Hola. Modelo: Hitachi HUS130.
* Cada servidor del clúster tiene cuatro tarjetas de red (NIC) de un Gbps cada una.
* Dos tarjetas de red de hello son red privada de tooan conectado iSCSI y dos son redes de empresa externa de tooan conectado. Una de las redes externas Hola está reservada para las comunicaciones del clúster sólo.

![Requisitos de hardware principal](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Server | RAM | Modelo | Procesador | Número de procesadores | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Servidores de Hyper-V en clúster:  <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25 tiene 256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2,20 GHz |4 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + rol de Hyper-V |
| Servidor VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>Sitio secundario (recuperación)

* sitio secundario de Hello tiene un clúster de conmutación por error de seis nodos.
* Una red SAN iSCSI proporciona almacenamiento para el nodo de clúster de Hola. Modelo: Hitachi HUS130.

![Especificación de hardware principal](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Server | RAM | Modelo | Procesador | Número de procesadores | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Servidores de Hyper-V en clúster:  <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |Intel(R) Xeon(R) CPU E5-2630 0 a 2,30 GHz |2 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + rol de Hyper-V |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2,20 GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + rol de Hyper-V |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0 a 2,20 GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + rol de Hyper-V |
| Servidor VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Cargas de trabajo del servidor

* Para fines de prueba, elegimos cargas de trabajo que se utilizan normalmente en escenarios de clientes de empresa.
* Usamos [IOMeter](http://www.iometer.org) con característica de carga de trabajo de hello resumida en la tabla Hola de simulación.
* Todos los perfiles IOMeter se establecen patrones de escritura de peor caso de toosimulate toowrite bytes aleatorios para cargas de trabajo.

| Carga de trabajo | Tamaño de E/S (KB) | % de acceso | % de lectura | Operaciones de E/s pendientes | Patrón de E/S |
| --- | --- | --- | --- | --- | --- |
| Servidor de archivos |48163264 |60% 20 %5 %5% 10% |80% de 80 80% 80% 80% |88888 |Todos 100% aleatorios |
| SQL Server (volumen 1) SQL Server (volumen 2) |864 |100% 100% |70% %0 |88 |100% aleatorio 100% secuencial |
| Exchange |32 |100% |67% |8 |100% aleatorio |
| Estación de trabajo/VDI |464 |66% 34% |70% 95% |11 |Los dos 100% aleatorios |
| Servidor de archivos web |4864 |33% 34% 33% |95% 95 95% |888 |Todos 75% aleatorios |

### <a name="vm-configuration"></a>Configuración de VM

* 470 máquinas virtuales en clúster principal Hola.
* Todas las máquinas virtuales con disco VHDX.
* Máquinas virtuales que ejecutan cargas de trabajo que se resumen en la tabla de Hola. Todas se crearon con plantillas de VMM.

| Carga de trabajo | N.º de máquinas virtuales | RAM mínima (GB) | RAM máxima (GB) | Tamaño de disco lógico (GB) por máquina virtual | Número máximo de IOPS |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| Servidor de archivos |50 |1 |2 |552 |22 |
| VDI |149 |0,5 |1 |80 |6 |
| Servidor Web |149 |0,5 |1 |80 |6 |
| TOTAL |470 | | |96,83 TB |4108 |

### <a name="site-recovery-settings"></a>Configuración de Site Recovery

* Azure Site Recovery se configuró para protección entre instalaciones locales de tooon
* servidor VMM Hello tiene configuradas cuatro nubes, que contiene servidores de clúster de Hyper-V de Hola y sus máquinas virtuales.

| Nube de VMM principal | Máquinas virtuales protegidas en la nube de Hola | Frecuencia de replicación | Puntos de recuperación adicionales |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 minutos |None |
| PrimaryCloudRpo30s |47 |30 segundos |None |
| PrimaryCloudRpo30sArp1 |47 |30 segundos |1 |
| PrimaryCloudRpo5m |235 |5 minutos |None |

### <a name="performance-metrics"></a>Métricas de rendimiento

tabla de Hola resumen las métricas de rendimiento de Hola y contadores que se midieron en la implementación de Hola.

| Métrica | Contador |
| --- | --- |
| CPU |Procesador(_Total)\% Hora del procesador |
| Memoria disponible |\Memoria\MB disponibles |
| E/S |\Disco físico(_Total)\Transferencias de disco/s |
| Operaciones de lectura de máquinas virtuales por segundo (IOPS)/s |\Dispositivo de almacenamiento virtual de Hyper-V(<VHD>)\Operaciones de lectura/s |
| Operaciones de escritura de máquinas virtuales por segundo (IOPS)/s |\Dispositivo de almacenamiento virtual de Hyper-V(<VHD>)\Operaciones de escritura/s |
| Rendimiento de lectura de máquinas virtuales |\Dispositivo de almacenamiento virtual de Hyper-V(<VHD>)\Bytes leídos/s |
| Rendimiento de escritura de máquinas virtuales |\Dispositivo de almacenamiento virtual de Hyper-V(<VHD>)\Bytes escritos/s |

## <a name="next-steps"></a>Pasos siguientes

[Configuración de la replicación entre dos sitios VMM locales](site-recovery-vmm-to-vmm.md)
