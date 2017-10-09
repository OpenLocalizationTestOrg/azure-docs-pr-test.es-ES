---
title: soluciones de aaaOracle en Microsoft Azure | Documentos de Microsoft
description: Aprenda sobre las configuraciones admitidas y las limitaciones de las soluciones de Oracle en Microsoft Azure.
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Soluciones de Oracle y su implementación en Microsoft Azure
En este artículo se ofrece información de toosuccesfully necesario implementar varias soluciones de Oracle en Microsoft Azure. Estas soluciones se basan en las imágenes de máquina Virtual publicadas por Oracle en hello Azure Marketplace. una lista de imágenes disponibles actualmente, ejecute el siguiente comando de Hola tooget:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
A partir de la lista de hello 6-16-2017 de imágenes son Hola siguientes:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Estas imágenes se consideran "Traiga su propia licencia" y, por tanto, solo se le cobrarán los costos de proceso, almacenamiento y red derivados de la ejecución de una máquina virtual.  Se supone están correctamente con licencia toouse software de Oracle y que tiene un contrato de soporte técnico actual en su lugar con Oracle. Oracle ha garantizado la portabilidad de licencia de tooAzure local. Vea Hola publicado [Oracle y Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Nota para obtener más información sobre la portabilidad de licencia. 

Personas también pueden elegir toobase sus soluciones en imágenes personalizadas, crear desde cero en Azure ni cargar una imagen personalizada de sus entornos locales en.

## <a name="support-for-jd-edwards"></a>Compatibilidad con JD Edwards
Según la nota de soporte técnico de tooOracle [2178595.1 de Id. de documento](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , versiones de JD Edwards EnterpriseOne 9.2 y versiones posteriores se admiten en **cualquier público en la nube oferta** que cumpla su específico `Minimum Technical Requirements` (MTR).  Necesitará toocreate imágenes personalizadas que cumplen sus especificaciones MTR para el sistema operativo y software de compatibilidad de las aplicaciones. 

## <a name="oracle-database-virtual-machine-images"></a>Imágenes de máquina virtual de Oracle Database
Oracle admite la ejecución de las ediciones Oracle DB 12.1 Standard y Enterprise en Azure en imágenes de máquina virtual basadas en Oracle Linux.  Hola recomendados para el rendimiento de las cargas de trabajo de producción de base de datos de Oracle en Azure, sea seguro de imagen de máquina virtual de Hola de tamaño tooproperly y utilice discos administrados que están respaldados por almacenamiento Premium. Para obtener instrucciones sobre cómo tooquickly obtener una base de datos de Oracle activados y ejecutándose en Azure con hello Oracle publicada la imagen de máquina virtual, [intente Hola tutorial de inicio rápido de base de datos de Oracle](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Opciones de configuración de discos conectados

Discos conectados se basan en hello servicio de almacenamiento de blobs de Azure. Teóricamente, cada disco estándar puede realizar aproximadamente 500 operaciones de entrada/salida por segundo (IOPS). Nuestra oferta de disco premium es preferido para cargas de trabajo de base de datos de alto rendimiento y se puede lograr una too5000 de IOps por disco. Aunque puede usar un único disco si cumple con el rendimiento necesario: puede mejorar el rendimiento efectivo de IOPS de hello si usa varios discos conectados, repartir los datos de la base de datos por encima de ellos y, a continuación, usa Oracle Automatic Storage Management (ASM). Consulte la [información general sobre Oracle Automatic Storage](http://www.oracle.com/technetwork/database/index-100339.html) para más información específica de Oracle ASM. Para obtener un ejemplo de cómo tooinstall y configure Oracle ASM en una VM Linux de Azure: puede intentar hello [instalar y configurar Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.

### <a name="oracle-realtime-application-cluster-rac"></a>Clúster de aplicaciones en tiempo real (RAC) de Oracle
Oracle RAC es toomitigate diseñada Hola error de un solo nodo en una configuración de clúster de varios nodos locales.  Se basa en dos tecnologías locales que no son entornos de nube pública de escala toohyper nativo: multidifusión de red y disco compartido. Hay soluciones de terceros creadas por otras empresas [como FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) que emular estas tecnologías si necesita toodeploy RAC de Oracle en Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Consideraciones sobre la alta disponibilidad y la recuperación ante desastres
Al utilizar las bases de datos de Oracle en Azure, usted es responsable de implementar un tooavoid de solución de recuperación ante desastres y la disponibilidad alta de los tiempos de inactividad. 

La alta disponibilidad y recuperación ante desastres para Oracle Database Enterprise Edition (sin RAC) en Azure puede lograrse mediante [Protección de datos, Protección de datos activa](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) u [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), con dos bases de datos en dos máquinas virtuales independientes. Ambas máquinas virtuales deben estar en Hola mismo [red virtual](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure que pueden tener acceso entre sí a través de la dirección IP privada persistente de Hola.  Además, se recomienda colocar las máquinas virtuales Hola Hola mismo conjunto de disponibilidad de tooallow tooplace Azure ellos en diferentes dominios de error y dominios de actualización.  Si quiere redundancia geográfica toohave - puede tener estos dos bases de datos se replican entre dos regiones diferentes y conectar las dos instancias de hello con una puerta de enlace de VPN.

Tenemos un tutorial "[implemente Oracle DataGuard en Azure](configure-oracle-dataguard.md)" que le guía a través de tootrial de procedimiento de configuración básica de hello esto en Azure.  

Con la Protección de datos de Oracle, se puede lograr alta disponibilidad con una base de datos principal en una máquina virtual, una base de datos secundaria (de reserva) en otra máquina virtual y la replicación unidireccional establecida entre ellos. resultado de Hello es copia de toohello de acceso de lectura de base de datos de Hola. Con Oracle GoldenGate, puede configurar la replicación bidireccional entre dos bases de datos de Hola. toolearn tooset la solución de alta disponibilidad para bases de datos mediante estas herramientas, vea [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) y [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentación en el sitio Web de Oracle Hola. Si necesita lectura y escritura acceso toohello copia de base de datos de hello, puede usar [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Tenemos un tutorial "[implemente Oracle GoldenGate en Azure](configure-oracle-golden-gate.md)" que le guía a través de hello básico seup procedimiento tootrial esto en Azure.

A pesar de tener una solución de alta disponibilidad y recuperación ante desastres diseñada en Azure, le interesará tooensure tendrá una estrategia de copia de seguridad en lugar toorestore la base de datos.  Tenemos un tutorial [copias de seguridad y recuperar una base de datos de Oracle](oracle-backup-recovery.md) que le guía a través del procedimiento básico de Hola para establecer una copia de seguridad de consistant.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Imágenes de máquina virtual de Oracle WebLogic Server
* **La agrupación en clústeres solo se admite en Enterprise Edition.** Se concede licencia toouse WebLogic clústeres solo cuando se usa Hola Enterprise Edition de WebLogic Server. No use la agrupación en clústeres con WebLogic Server Standard Edition.
* **Tampoco se admite la multidifusión UDP.** Azure admite la unidifusión UDP, pero no admite la multidifusión ni la difusión. WebLogic Server es capaz de toorely en las capacidades de unidifusión UDP de Azure. Para mejores resultados al depender de unidifusión UDP, se recomienda que el tamaño del clúster WebLogic Hola se mantenga estático, se mantienen con no más de 10 servidores administrados incluidos en el clúster de Hola o.
* **WebLogic Server espera Hola de puertos públicos y privados toobe mismo para T3 acceso (por ejemplo, al usar Enterprise JavaBeans).** Considere un escenario de varios niveles, en el que una aplicación de capa de servicio (EJB) se ejecuta en un clúster de servidor WebLogic compuesto por dos o más máquinas virtuales, en una red virtual llamada **SLWLS**. nivel de cliente de Hello está en una subred diferente en hello misma red virtual, ejecuta un programa Java simple intentar toocall EJB en el nivel de servicio de Hola. Dado que es el nivel de servicio de tooload es necesario equilibrar hello, un extremo público con equilibrio de carga necesita toobe creado para hello máquinas virtuales en clúster de WebLogic Server Hola. Si el puerto privado Hola que especifique es diferente del puerto público de hello (por ejemplo, 7006: 7008), se produce un error como siguiente hello:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Esto es porque para cualquier acceso de T3 remoto, WebLogic Server espera que el puerto de equilibrador de carga de Hola y Hola administrado de WebLogic server puerto toobe Hola igual. Hola por encima de caso, cliente hello tiene acceso al puerto 7006 (puerto de equilibrador de carga de hello) y Hola de servidor administrado está escuchando en 7008 (puerto privado hello). Esta restricción se aplica solo al acceso T3, no a HTTP.

   tooavoid este problema, utilice uno de hello siguientes soluciones alternativas:

  * Use Hola mismo privada y números de puerto público de carga equilibrada extremos dedicados tooT3 acceso.
  * Hola después de parámetro de JVM al iniciar WebLogic Server se incluyen:

         -Dweblogic.rjvm.enableprotocolswitch=true

Para obtener información relacionada, consulte el artículo de KB **860340.1** en <http://support.oracle.com>.

* **Agrupación en clústeres dinámica y limitaciones de equilibrio de carga.** Suponga que desea toouse un clúster dinámico en WebLogic Server y exponerlo a través de un extremo con equilibrio de carga público, único en Azure. Esto puede hacerse siempre y cuando se usa un número de puerto fijo para cada una de hello (no asignados dinámicamente a partir de un rango) de servidores administrados y no inicia más servidores administrados que hay máquinas que se está realizando el seguimiento de administrador de hello (es decir, no tiene más de un servidor administrado por virt ual máquina). Si la configuración da como resultado más servidores WebLogic que se inicia de máquinas virtuales (es decir, donde varios recursos compartidos de instancias de WebLogic Server hello misma máquina virtual), entonces no es posible que más de una de esas instancias de WebLogic Server tooa de toobind de servidores con número de puerto: Hola otros miembros de esa máquina virtual se producirá un error.

   En hello otra parte, si configura Hola admin server tooautomatically asignar números de puerto exclusivos tooits administrar servidores, equilibrio de carga no es posible porque Azure no admite la asignación de un único puerto público toomultiple privada los puertos, como sería necesario para esta configuración.
* **Varias instancias de Weblogic Server en una máquina virtual.** Dependiendo de los requisitos de su implementación, puede considerar Hola opción de ejecutar varias instancias de WebLogic Server en hello misma máquina virtual, si la máquina virtual de hello es lo suficientemente grande. Por ejemplo, en una máquina virtual de tamaño medio, que contiene dos núcleos, puede elegir toorun dos instancias de WebLogic Server. Sin embargo, tenga en cuenta que todavía sigue siendo recomendable evitar introducir puntos únicos de error en la arquitectura, que sería el caso de hello si utiliza una sola máquina virtual que está ejecutando varias instancias de WebLogic Server. Usar al menos dos máquinas virtuales podría ser un mejor enfoque y, a continuación, cada una de esas máquinas virtuales puede ejecutar varias instancias de WebLogic Server. Cada una de estas instancias de WebLogic Server podría ser todavía parte del programa Hola mismo clúster. Tenga en cuenta, sin embargo, actualmente no es posible toouse equilibrar tooload Azure extremos expuestos por tales implementaciones de WebLogic Server dentro de Hola misma máquina virtual, ya que el equilibrador de carga de Azure requiere hello toobe de servidores con equilibrio de carga distribuida entre máquinas virtuales únicas.

## <a name="oracle-jdk-virtual-machine-images"></a>Imágenes de máquina virtual de Oracle JDK
* **Actualizaciones más recientes de JDK 6 y 7.** Aunque se recomienda utilizar la versión de Hola pública más recientes, admitido de Java (actualmente Java 8), Azure también permite JDK 6 y 7 imágenes estén disponibles. Esto está pensado para las aplicaciones heredadas que están todavía no se han preparado toobe había actualizado tooJDK 8. Mientras que las actualizaciones tooprevious JDK imágenes ya no pueden ser toohello disponible el público en general, dada Hola colaboración con Oracle, Hola JDK 6 y 7 imágenes proporcionadas por Azure son de Microsoft diseñado toocontain una actualización más reciente no público que normalmente ofrece Oracle tooonly a un selecto grupo de Oracle que admite a los clientes. Las nuevas versiones de imágenes JDK Hola estará disponibles con el tiempo con las versiones actualizadas de JDK 6 y 7.

   Hola JDK disponible en este JDK 6 y 7 imágenes y máquinas virtuales de Hola e imágenes derivadas de ellos, sólo pueden utilizarse dentro de Azure
* **JDK de 64 bits.** imágenes de máquina virtual de Oracle WebLogic Server Hola y las imágenes de máquina virtual de Oracle JDK Hola proporcionadas por Azure contienen las versiones de 64 bits de Hola de Windows Server y Hola JDK.

## <a name="next-steps"></a>Pasos siguientes
Ahora tiene una visión general de las soluciones actuales de Oracle en Microsoft Azure. El siguiente paso es toogo e implementar la primera base de datos de Oracle en Azure.
- Intente hello [crear una base de datos de Oracle en Azure](oracle-database-quick-create.md) tutorial tooget iniciado.
