---
title: aaaBatch y soluciones HPC en la nube de hello - Azure | Documentos de Microsoft
description: "Más información acerca de los escenarios de ejecución por lotes y de informática de alto rendimiento (HPC y Big Compute), y opciones de soluciones de Azure"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Soluciones de Batch y HPC para cargas de trabajo de procesos a gran escala

Azure ofrece soluciones en la nube eficientes y escalables para la ejecución por lotes y la informática de alto rendimiento (HPC), que también se denomina *Big Compute*. Obtenga aquí sobre las cargas de trabajo de Big Compute y toosupport de servicios de Azure ellos, o bien saltar directamente demasiado[escenarios de solución](#scenarios) más adelante en este artículo. Este artículo es principalmente para los encargados de tomar decisiones técnicas, los administradores de TI y fabricantes independientes de software, pero otros profesionales de TI y desarrolladores pueden utilizar toofamiliarize de TI a sí mismos con estas soluciones.

Las organizaciones tienen problemas informáticos a gran escala: el diseño y análisis de ingeniería, la representación de imágenes, los modelos complejos, las simulaciones de Monte Carlo, los cálculos de riesgos financieros, etc. Azure permite a las organizaciones a resolver estos problemas con los recursos de hello, la escala y la programación que necesiten. Con Azure, las organizaciones pueden:

* Crear soluciones híbridas, extender una nube local HPC cluster toooffload pico las cargas de trabajo toohello
* Ejecución de cargas de trabajo y herramientas de clúster HPC completamente en Azure
* Usar servicios de Azure administrados y escalables como [lote](https://azure.microsoft.com/documentation/services/batch/) toorun cargas de trabajo de proceso intensivo sin necesidad de toodeploy y administrar la infraestructura de proceso

Aunque queda fuera de ámbito de Hola de este artículo, Azure también proporciona a los desarrolladores y asociados un conjunto completo de capacidades, opciones de arquitectura y desarrollo herramientas toobuild a gran escala, personalizado Big Compute flujos de trabajo. Y un ecosistema de partners creciente es listo toohelp realiza las cargas de trabajo de Big Compute productivos en hello nube de Azure.

## <a name="batch-and-hpc-applications"></a>Aplicaciones HPC y de ejecución por lotes
A diferencia de las aplicaciones web y de muchas aplicaciones de línea de negocio, las aplicaciones HPC y de ejecución por lotes tienen un inicio y una finalización definidos y pueden ejecutarse de manera programada o a petición, a veces durante horas o más tiempo. La mayoría se dividen en dos categorías principales: *intrínsecamente paralelas* (a veces denominado "embarazosamente paralelo", porque Hola problemas que solucionan prestan toorunning en paralelo en varios equipos o procesadores) y *estrechamente acopladas*. Vea hello en la tabla siguiente para obtener más información acerca de estos tipos de aplicaciones. Algunas soluciones de Azure enfoques funcione mejor para un tipo o hello otro.

> [!NOTE]
> En las soluciones de HPC y de Batch, una instancia en ejecución de una aplicación se suele llamar *trabajo* y cada trabajo podría dividirse en *tareas*. Y hello recursos de proceso en clúster para la aplicación hello a menudo se denominan *nodos de proceso*.
> 
> 

| Tipo | Características | Ejemplos |
| --- | --- | --- |
| **Intrínsecamente paralelos**<br/><br/>![Intrínsecamente paralelos][parallel] |• Los equipos individuales ejecutan la lógica de la aplicación de forma independiente<br/><br/> • Agregar equipos permite Hola aplicación tooscale y disminución de tiempo de proceso.<br/><br/>• La aplicación consta de archivos ejecutables independientes o se divide en un grupo de servicios invocados por un cliente (una arquitectura orientada a servicios o SOA, aplicación) |• Modelado de riesgos financieros<br/><br/>• Representación y procesamiento de imágenes<br/><br/>• Codificación y transcodificación multimedia<br/><br/>• Simulaciones Monte Carlo<br/><br/>• Pruebas de Software |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• Aplicación requiere nodos proceso toointeract o exchange resultados intermedios<br/><br/>• Proceso nodos pueden comunicarse mediante Hola pasar interfaz mensajes (MPI), un protocolo de comunicación común para procesamiento en paralelo.<br/><br/>aplicación de hello • es ancho de banda y latencia toonetwork confidencial<br/><br/>• El rendimiento de la aplicación se puede mejorar mediante tecnologías de redes de alta velocidad como InfiniBand y acceso directo a memoria remoto (RDMA) |• Modelado de depósitos de petróleo y gas •<br/><br/>• Diseño de ingeniería y análisis, como dinámica de fluidos computacional<br/><br/>• Simulaciones físicas como choques de automóviles y reacciones nucleares<br/><br/>• Previsión meteorológica de |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Consideraciones para ejecutar aplicaciones de HPC y lote en nube Hola
Puede migrar fácilmente muchas aplicaciones que están diseñada toorun en tooAzure de clústeres HPC local o de tooa híbrida (entre entornos). Sin embargo, puede haber algunas limitaciones o consideraciones, entre las que se incluyen:

* **Disponibilidad de recursos de nube** -según tipo hello en la nube de recursos de proceso que utilice, no es posible que pueda toorely en disponibilidad continua del equipo mientras se ejecuta un trabajo. Progreso y control de estado comprueban que señala es comunes técnicas toohandle posibles errores transitorios y es necesaria más al usar recursos de nube.
* **Acceso a datos** -técnicas de acceso a datos normalmente disponibles en los clústeres de la empresa, como NFS, pueden requerir una configuración especial en la nube de Hola. O bien, podría necesitar patrones y procedimientos recomendados de acceso de datos diferentes de tooadopt para nube Hola.
* **Movimiento de datos** : para las aplicaciones que grandes cantidades de datos, las estrategias de proceso son necesarios toomove Hola datos en recursos de almacenamiento y toocompute en la nube. Es posible que necesite la conexión de redes entre instalaciones de alta velocidad como [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/). Considere también las limitaciones legales, normativas o de directivas para almacenar o acceder a esos datos.
* **Licencias** : póngase en contacto con el proveedor de Hola de cualquier aplicación comercial de licencia u otras restricciones para la ejecución hello en la nube. No todos los proveedores ofrecen licencias de pago por uso. Tal vez necesite tooplan para un servidor de licencias en la nube de Hola para su solución, o conectar el servidor de licencias de tooan local.

### <a name="big-compute-or-big-data"></a>¿Big Compute o Big Data?
Hola línea de división entre las aplicaciones de Big Compute y grandes cantidades de datos no siempre está claro y algunas aplicaciones pueden tener características de ambos. Ambas incluyen cálculos a gran escala, normalmente en clústeres de equipos. Pero pueden diferir Hola enfoques de soluciones y herramientas de soporte técnico.

• **Big Compute** tiende tooinvolve aplicaciones que se basan en la capacidad de CPU y memoria, como simulaciones de ingeniería, modelado de riesgos financieros y representación digital. infraestructura de Hola para una solución Big Compute podría incluir equipos con procesadores de varios núcleos especializados tooperform sin formato cálculo y especializados y de alta velocidad hardware tooconnect Hola equipos red.

• Los **macrodatos** solucionan problemas de análisis de datos que implican grandes cantidades de datos que no se pueden administrar mediante un único equipo o sistema de administración de bases de datos. Entre los ejemplos que pueden encontrarse se incluyen grandes volúmenes de registros web o de otros datos de inteligencia empresarial. Big Data tiene toorely más información sobre la capacidad de disco y el rendimiento de E/S que en potencia de la CPU. También hay herramientas de grandes cantidades de datos especializadas como Apache Hadoop toomanage datos de hello clúster y crear particiones Hola. (Para obtener información acerca de Azure HDInsight y otras soluciones Azure Hadoop, consulte [Hadoop](https://azure.microsoft.com/solutions/hadoop/)).

## <a name="compute-management-and-job-scheduling"></a>Administración de procesos y programación de trabajos
Ejecutar aplicaciones de lote y HPC a menudo incluye un *el Administrador de clústeres* y un *programador de trabajos* toohelp administrar recursos de proceso en clúster y asignar aplicaciones de toohello que se ejecutan trabajos de Hola. Estas funciones pueden realizarse mediante herramientas independientes o una herramienta o servicio integrado.

* **Administrador de clústeres** : aprovisiona, publica y administra recursos de proceso (o nodos de ejecución). Un administrador de clústeres puede automatizar la instalación de imágenes de sistema operativo y las aplicaciones en nodos de proceso, escalar recursos de proceso según toodemands y supervisar el rendimiento de Hola de nodos de Hola.
* **Programador de trabajos** -especifica los recursos de hello (por ejemplo, procesadores y memoria) una aplicación necesita y hello condiciones cuando se ejecuta. Un programador de trabajos mantiene una cola de trabajos y asigna toothem de recursos en función de una prioridad asignada u otras características.

Agrupación en clústeres y herramientas para los clústeres basados en Windows y Linux de la programación de trabajos pueden migrar tooAzure bien. Por ejemplo, [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)(solución de clúster de proceso gratis de Microsoft para cargas de trabajo HPC de Windows y Linux) ofrece varias opciones para ejecución en Azure. También puede crear clústeres de Linux toorun herramientas de código abierto como par y SLURM. También puede abrir como cuadrícula comercial soluciones tooAzure, [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [Symphony espectro de IBM y Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), y [Univa cuadrícula motor](http://www.univa.com/products/grid-engine).

Tal y como se muestra en las secciones siguientes de hello, también puede aprovechar las ventajas de los servicios de Azure toomanage recursos de proceso y programar las herramientas de administración de clúster tradicionales de trabajos sin (o además).

## <a name="scenarios"></a>Escenarios
Presentamos tres escenarios comunes cargas de trabajo de toorun Big Compute en Azure mediante el uso de las soluciones de clúster HPC existentes, los servicios de Azure o una combinación de hello dos. Se enumeran consideraciones clave para elegir cada escenario pero no son exhaustivas. Más sobre los servicios de Azure disponibles Hola que podría usar en la solución es más adelante en el artículo de Hola.

| Escenario | ¿Por qué elegirlo? |
| --- | --- | --- |
| **Un tooAzure de clúster HPC de ráfaga**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Más información:<br/>• [Irrumpir en instancias de trabajo tooAzure con HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Configuración de un clúster de proceso híbrido con HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [Irrumpir tooAzure por lotes con HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Combine su [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) u otro clúster local con recursos de Azure adicionales en una solución híbrida.<br/><br/>• Ampliar su toorun de cargas de trabajo de Big Compute en plataforma como una instancia de la máquina virtual de servicio (PaaS) (actualmente solo Windows Server).<br/><br/>• Acceda a un almacén de datos o a un servidor de licencias local mediante una red virtual de Azure opcional. |
| **Creación de un clúster de HPC completamente en Azure**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Más información:<br/>• [Soluciones de clúster de HPC en Azure](big-compute-resources.md)<br/><br/> |• Implemente de forma rápida y coherente las aplicaciones y herramientas de clúster en máquinas virtuales de infraestructura como servicio (IaaS) con Windows o Linux estándar o personalizadas.<br/><br/>• Ejecute diversas cargas de trabajo de Big Compute mediante el uso de la solución de su elección de la programación de trabajos de Hola.<br/><br/>• Usar servicios de Azure adicionales, como las redes y almacenamiento toocreate basada en la nube soluciones completas. |
| **Escalar horizontalmente una aplicación paralela tooAzure**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Más información:<br/>• [Conceptos básicos de Azure Batch](batch-technical-overview.md)<br/><br/>• [Empezar a trabajar con la biblioteca de hello Azure Batch para .NET](batch-dotnet-get-started.md) |• Desarrollar con [Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale out distintos toorun de cargas de trabajo de Big Compute en los grupos de máquinas virtuales de Windows o Linux.<br/><br/>• Usar una escala automática de máquinas virtuales, programación de trabajos, recuperación ante desastres, movimiento de datos, la administración de dependencias e implementación de aplicación e implementación de toomanage de servicios de plataforma Windows Azure. |

## <a name="azure-services-for-big-compute"></a>Servicios de Azure para Big Compute
Aquí es más información sobre el proceso de hello, datos, redes y servicios relacionados que se pueden combinar para las soluciones Big Compute y flujos de trabajo. Para obtener instrucciones detalladas sobre los servicios de Azure, vea Hola servicios de Azure [documentación](https://azure.microsoft.com/documentation/). Hola [escenarios](#scenarios) anteriormente en este artículo se muestran solo algunas formas de usar estos servicios.

> [!NOTE]
> Azure presenta nuevos servicios con cierta frecuencia que podrían ser útiles para su escenario. Si tiene alguna pregunta, póngase en contacto con un [asociado de Azure](https://pinpoint.microsoft.com/en-US/search?keyword=azure) o envíe un correo electrónico a *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Servicios de proceso
Servicios de proceso de Azure son la esencia de Hola de una solución Big Compute y las ventajas de oferta de servicios de proceso distinto de hello para diferentes escenarios. En un nivel básico, estos servicios ofrecen modos diferentes para las aplicaciones toorun en instancias de proceso basada en la máquina virtual que proporciona Azure con la tecnología Hyper-V de Windows Server. Estas instancias pueden ejecutar herramientas y sistemas operativos Linux y Windows estándar y personalizados. Azure permite elegir entre varios [tamaños de instancia](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con diferentes configuraciones de núcleos de CPU, memoria, capacidad de disco y otras características. Según sus necesidades, puede escalar Hola instancias toothousands de núcleos y, a continuación, se reducir verticalmente cuando se necesitan menos recursos.

> [!NOTE]
> Aprovechar las ventajas de hello Azure [instancias de proceso intensivo como Hola H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove Hola rendimiento y escalabilidad de las cargas de trabajo HPC. Estas instancias también admiten aplicaciones MPI en paralelo que requieran una red de aplicaciones de baja latencia y alto rendimiento. También están disponible [N-series](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) máquinas virtuales con un intervalo de GPU NVIDIA tooexpand Hola de escenarios de computación y la visualización en Azure.  
> 
> 

| Servicio | Description |
| --- | --- |
| **[Máquinas virtuales](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Proporcionan infraestructura de proceso como servicio (IaaS) mediante la tecnología de Microsoft Hyper-V<br/><br/>• Habilitar tooflexibly aprovisionar y administrar equipos de nube persistentes de imágenes estándar de Windows Server o Linux de hello [Azure Marketplace](https://azure.microsoft.com/marketplace/), o los discos de imágenes y los datos que proporcione<br/><br/>• Se pueden implementar y administrar como [conjuntos de escalas de VM](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild a gran escala servicios desde máquinas virtuales idénticas, con capacidad de tooincrease o disminución del escalado automático automáticamente<br/><br/>• Ejecutar de forma local aplicaciones completamente en la nube de Hola y herramientas de clúster de proceso<br/><br/> |
| **[Cloud services](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Puede ejecutar aplicaciones de Big Compute en instancias de rol de trabajo, que son máquinas virtuales que ejecutan una versión de Windows Server y están administradas completamente por Azure<br/><br/>• Hacen posibles las aplicaciones escalables y fiables con baja carga administrativa, que se ejecutan en un modelo de plataforma como servicio (PaaS)<br/><br/>• Pueden requerir herramientas adicionales o toointegrate de desarrollo con soluciones de clúster HPC local |
| **[Lote](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Ejecuta cargas de trabajo en lotes y paralelas a gran escala en un servicio totalmente administrado.<br/><br/>• Proporciona programación de trabajos y escalado automático de un grupo administrado de máquinas virtuales<br/><br/>• Permite a los desarrolladores toobuild y ejecutar aplicaciones como un servicio o nube a habilitar las aplicaciones existentes<br/> |

### <a name="storage-services"></a>Servicios de almacenamiento
Normalmente, una solución Big Compute funciona en un conjunto de datos de entrada y genera datos para sus resultados. Algunos de los servicios de almacenamiento de Azure de hello usados en las soluciones Big Compute son:

* [Almacenamiento de blobs, tablas y colas](https://azure.microsoft.com/documentation/services/storage/) : administre grandes cantidades de datos no estructurados, datos NoSQL y mensajes de flujo de trabajo y comunicación, respectivamente. Por ejemplo, puede usar el almacenamiento de blobs de grandes conjuntos de datos técnicos o de imágenes de entrada de Hola o archivos multimedia de los procesos de aplicación. Puede usar colas para la comunicación asincrónica en una solución. Vea [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md).
* [Almacenamiento de Azure archivo](https://azure.microsoft.com/services/storage/files/) -recursos compartidos archivos comunes y los datos en Azure mediante Hola protocolo SMB estándar, que es necesario para algunas soluciones de clúster HPC.
* [Almacén de Data Lake](https://azure.microsoft.com/services/data-lake-store/) -proporciona un sistema de archivos distribuido de Apache Hadoop hiperescalar Hola de nube, útil para el lote, en tiempo real, y análisis interactivo.

### <a name="data-and-analysis-services"></a>Servicios de datos y análisis
Algunos escenarios Big Compute implican flujos de datos a gran escala o generan datos que necesitan un procesamiento o análisis posterior. Azure ofrece varios servicios de datos y análisis, entre los que se incluyen:

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) : crea flujos de trabajo controlados por datos (canalizaciones) que unen, agregan y transforman datos de almacenes de datos locales, basados en la nube y de Internet.
* [Base de datos SQL](https://azure.microsoft.com/documentation/services/sql-database/) -proporciona Hola características clave de un sistema de administración de bases de datos relacionales de Microsoft SQL Server en un servicio administrado.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) : implementa y aprovisiona clústeres de Windows Server o Linux-based Apache Hadoop en hello toomanage en la nube, analizar e informar sobre big data.
* [Aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/) : le ayuda a crear, probar, operar y administrar soluciones de análisis predictivo en un servicio totalmente administrado.

### <a name="additional-services"></a>Servicios adicionales
La solución Big Compute que tenga otros servicios de Azure tooconnect tooresources locales o en otros entornos. Algunos ejemplos son:

* [Red virtual](https://azure.microsoft.com/documentation/services/virtual-network/) -crea una sección aislada lógicamente en Azure tooconnect de recursos de Azure de tooeach otros o tooyour local data center. Con una red virtual entre locales, las aplicaciones de Big Compute pueden acceder a datos locales, servicios de Active Directory y servidores de licencias
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) : crea una conexión privada entre los centros de datos de Microsoft y la infraestructura local o en un entorno de colocalización. ExpressRoute proporciona una mayor seguridad, más confiabilidad, velocidades más rápidas y latencias más bajas que las típicas conexiones a través de Internet de Hola.
* [Bus de servicio](https://azure.microsoft.com/documentation/services/service-bus/) -proporciona varios mecanismos para aplicaciones toocommunicate o intercambio de datos, independientemente de si están ubicados en Azure, en otra plataforma de nube o en un centro de datos.

## <a name="next-steps"></a>Pasos siguientes
* Vea [recursos técnicos para el lote y HPC](big-compute-resources.md) toofind orientación técnica toobuild la solución.
* Converse sobre las opciones de Azure con partners, como Cycle Computing, Rescale y UberCloud.
* Consulte más información sobre soluciones Big Compute de Azure proporcionadas por [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) y [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Para anuncios de Hola más recientes, consulte hello [blog del equipo de Microsoft HPC y lote](http://blogs.technet.com/b/windowshpc/) hello y [blog de Azure](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
