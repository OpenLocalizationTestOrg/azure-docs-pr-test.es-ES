---
title: "aaaInstall SAP HANA en SAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "¿Cómo tooinstall SAP HANA en un SAP HANA en Azure (instancia grande)."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>¿Cómo tooinstall y configure SAP HANA (instancias de gran tamaño) en Azure

Los siguientes son algunos tooknow definiciones importantes antes de leer a esta guía. En [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) se presentan dos clases distintas de unidades de HANA (Instancias grandes) con:

- S72, S72m, S144, S144m, S192 y S192m, que nos referiremos tooas hello 'Tipo clase' de SKU.
- S384, S384m, S384xm, S576, S768 y S960, que nos referiremos tooas Hola 'Clase de tipo II' de SKU.

especificador de clase de Hello es toobe continuo utilizada a lo largo de hello HANA instancia grande documentación tooeventually consulte toodifferent capacidades y requisitos basándose en las SKU de HANA grandes instancia.

Otras definiciones que se usan con frecuencia son:
- **Marca de la instancia de gran tamaño:** una pila de infraestructura de hardware que es SAP HANA TDI certificadas y dedicado instancias de SAP HANA toorun dentro de Azure.
- **SAP HANA en Azure (instancias de gran tamaño):** nombre oficial de oferta de hello en instancias HANA toorun Azure en SAP HANA TDI certificadas hardware que se implementa en marcas de instancia grande en diferentes regiones de Azure. Hola relacionadas con los términos **instancia grande de HANA** es corto para SAP HANA en Azure (instancias de gran tamaño) y es muy utilizado esta guía de implementación técnica.


instalación de Hola de SAP HANA es su responsabilidad y puede empezar a actividad hello después de la entrega de un nuevo SAP HANA en servidor de Azure (instancias de gran tamaño). Y después se obtuvo establecida conectividad de hello entre la VNet(s) de Azure y Hola instancia grande de HANA unidades. 

> [!Note]
> Por directiva SAP, instalación de Hola de SAP HANA debe realizarse por una persona certificadas tooperform instalaciones de SAP HANA. Una persona, que ha pasado el examen Hola certificadas asociar de tecnología de SAP, exámenes de certificación de SAP HANA instalación, o por un integrador de sistema SAP certificado (SI).

Comprueba otra vez, especialmente al planear tooinstall HANA 2.0, [SAP compatibilidad Nota #2235581 - SAP HANA: sistemas operativos compatibles](https://launchpad.support.sap.com/#/notes/2235581/E) en orden toomake seguro liberar ese hello en el sistema operativo es compatible con hello SAP HANA decidió tooinstall. Tenga en cuenta que Hola sistemas operativos compatibles para HANA 2.0 es más restringido que Hola SO compatible para HANA 1.0. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Primeros pasos después de recibir Hola HANA grandes unidades de instancia

**Primer paso** después de su recepción Hola HANA grandes instancia y una vez establecido el acceso y la conectividad de instancias de toohello, es tooregister Hola SO de instancia de hello con su proveedor de sistema operativo. Este paso incluye el registro del sistema operativo Linux de SUSE en una instancia de SUSE SMT que necesite toohave implementado en una máquina virtual en Azure. unidad de instancia grande de HANA Hola puede conectar la instancia SMT de toothis (vea más adelante en esta documentación). O para su sistema operativo RedHat necesidades toobe registrado con hello necesita tooconnect para el Administrador de suscripción de Hat rojo. Vea también los comentarios de este [documento](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Este paso también es necesario toobe toopatch capaz de hello SO. Una tarea que se encuentra en la responsabilidad de Hola de cliente de Hola. Para SUSE, encontrar documentación tooinstall y configurar SMT [aquí](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Segundo paso** es toocheck para nuevas revisiones y correcciones de hello específico SO/versión de lanzamiento. Compruebe si el nivel de revisión de Hola de hello HANA grandes instancia está en estado más reciente de Hola. En función de tiempo de revisión/versiones y cambios toohello imagen del sistema operativo que puede implementar Microsoft, podría haber casos donde las últimas revisiones de hello no se pueden incluidas. Por lo tanto, es un paso obligatorio después de asumir una unidad de instancia grande de HANA toocheck si pertinentes para la seguridad, funcionalidad, disponibilidad y rendimiento se liberaron mientras tanto por proveedor determinado de Linux de Hola y necesitan toobe aplicado.

**Tercer paso** es toocheck out Hola notas pertinentes de SAP para instalar y configurar SAP HANA en hello específico SO/versión de lanzamiento. Pagar toochanging recomendaciones o cambios tooSAP notas o configuraciones que dependen de los escenarios de instalación individuales, Microsoft no siempre será capaz de toohave una unidad de instancia grande de HANA configurada perfectamente. Por lo tanto, es obligatorio para usted como un cliente, tooread hello las notas de SAP relacionado tooSAP HANA en la versión exacta de Linux. También debe comprobar las configuraciones de Hola de hello SO/versión necesario y aplicar opciones de configuración de Hola donde no ha hecho.

En específicos, compruebe Hola parámetros siguientes y finalmente ajustados para:

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

A partir de SP1 SLES12 y RHEL 7.2, se deben establecer estos parámetros en un archivo de configuración en el directorio de /etc/sysctl.d Hola. Por ejemplo, debe crearse un archivo de configuración con nombre hello 91-NetApp-HANA.conf. Para las versiones anteriores de SLES y RHEL, estos parámetros deben establecerse en in/etc/sysctl.conf.

RHEL todas las versiones y a partir de SLES12, Hola 
- sunrpc.tcp_slot_table_entries = 128

se debe establecer en in/etc/modprobe.d/sunrpc-local.conf. Si no existe el archivo hello, primero debe crearse mediante la adición de hello siguiente entrada: 
- options sunrpc tcp_max_slot_table_entries=128

**Cuarto paso** hora del sistema de hello toocheck de su unidad de instancia HANA grandes. instancias de Hola se implementan con una zona horaria del sistema que representan la ubicación de Hola de Hola Hola de región de Azure en que HANA grandes marca de la instancia se encuentra. Es libre toochange Hola la hora del sistema o zona horaria de instancias de Hola que usted es el propietario. Si lo hace y ordenar las instancias más en su inquilino, preparado que necesita tooadapt zona de horaria Hola de hello recién entregar instancias. Las operaciones de Microsoft no tienen ningún visiones Hola zona horaria del sistema que configure con instancias de hello después entrega Hola. Por lo tanto, instancias recién implementados no se podrían establecer en hello misma zona de horaria como Hola uno cambia a. Como resultado, es su responsabilidad como toocheck de cliente y si es necesario adaptar la zona horaria de Hola de todas las instancias de hello entregadas. 

**Quinto paso** es toocheck etcetera/hosts. Como hojas de hello obtengan entregue, tienen diferentes direcciones IP asignadas para propósitos diferentes (consulte la sección siguiente). Compruebe el archivo etcetera/hosts de hello. En casos donde se agregan unidades en un inquilino existente, no debería toohave etcetera/hosts de sistemas de hello recién implementado mantenidos correctamente con direcciones IP de Hola de versiones anteriores de los sistemas entregados. Por lo tanto, resulta depende de usted como la configuración correcta de cliente toocheck Hola por lo tanto, que una instancia recién implementada puede interactuar y resolver los nombres de Hola de unidades de implementada anteriormente en el inquilino. 

## <a name="networking"></a>Redes
Se supone que ha seguido las recomendaciones de hello en el diseño de sus redes virtuales de Azure y conectar esas instancias grandes de redes virtuales toohello HANA tal y como se describe en estos documentos:

- [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infraestructura y conectividad con SAP HANA en Azure (instancias grandes)](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Hay algunos detalles que vale la pena toomention acerca de las redes de Hola de unidades de hello único. Cada unidad de instancia grande de HANA viene con dos o tres direcciones IP que se asignan tootwo o tres puertos NIC de unidad de Hola. Tres direcciones IP se utilizan en las configuraciones de escalado horizontal HANA y escenario de replicación del sistema de archivos de HANA Hola. Una de las direcciones IP Hola asignado toohello NIC de unidad de hello está fuera del Hola grupo de dirección IP del servidor que se ha descrito en hello [información general de SAP HANA (instancia grande) y la arquitectura en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

distribución de Hola para las unidades con dos direcciones IP asignadas debería ser similar:

- eth0.xx debe tener una dirección IP asignada que está fuera del Hola intervalo de direcciones de grupo de IP de servidor que envió tooMicrosoft. Esta dirección IP se usará para mantener en/etc/hosts de hello SO.
- eth1.xx debe tener una dirección IP asignada que se usa para comunicación tooNFS. Por lo tanto, hacer estas direcciones **no** necesita toobe mantiene en etcetera/hosts en el tráfico de orden tooallow instancia tooinstance dentro de inquilino de Hola.

Para los casos de implementación de la replicación del sistema de HANA o el escalado horizontal de HANA, una configuración de hoja con dos direcciones IP asignadas no es adecuada. Si tiene dos direcciones IP asignadas solo y que desean toodeploy tal configuración, póngase en contacto con SAP HANA en administración de servicios de Azure tooget una tercera dirección IP en una tercera VLAN asignado. Unidades de instancia grande de HANA tener tres direcciones IP asignadas en tres puertos NIC, hello siguientes se rige por reglas:

- eth0.xx debe tener una dirección IP asignada que está fuera del Hola intervalo de direcciones de grupo de IP de servidor que envió tooMicrosoft. Por lo tanto, esta dirección IP no se usará para mantener en/etc/hosts de hello SO.
- eth1.xx debe tener una dirección IP asignada que se usa para el almacenamiento de tooNFS de comunicación. Por lo tanto, este tipo de direcciones no debe permanecer en etc/hosts.
- eth2.xx debe ser exclusivamente se mantienen en etcetera/hosts para la comunicación entre distintas instancias de hello toobe usado. Estas direcciones también sería direcciones IP de Hola que necesitan toobe mantiene en las configuraciones de escalado horizontal HANA como direcciones IP que HANA se usa para la configuración de hello entre nodos.



## <a name="storage"></a>Storage

Hello distribución de almacenamiento para SAP HANA en Azure (instancias de gran tamaño) se configura SAP HANA en administración de servicios de Azure a través de SAP recomendada las líneas de guía, como se documenta en [requisitos de almacenamiento de SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) notas del producto. Hola aproximados tamaños de volúmenes diferentes Hola con hello diferentes SKU de instancias de gran tamaño HANA obtuvo documentadas en [información general de SAP HANA (instancia grande) y la arquitectura en Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

convenciones de nomenclatura de Hola Hola de volúmenes de almacenamiento se muestran en hello en la tabla siguiente:

| Uso del almacenamiento | Nombre de montaje | Nombre del volumen | 
| --- | --- | ---|
| Datos de HANA | /hana/data/SID/mnt0000<m> | Almacenamiento IP: /hana_data_SID_mnt00001_tenant_vol |
| Registro HANA | /hana/log/SID/mnt0000<m> | Almacenamiento IP: /hana_log_SID_mnt00001_tenant_vol |
| Copia de seguridad del registro de HANA | /hana/log/backups | Almacenamiento IP: /hana_log_backups_SID_mnt00001_tenant_vol |
| HANA compartido | /hana/shared/SID | Almacenamiento IP: IP:/hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | Almacenamiento IP: /hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Donde SID = identificador de sistema de la instancia HANA Hola 

Y "tenant" = una enumeración interna de operaciones al implementar un inquilino.

Como puede ver, HANA compartido y usr/sap están compartiendo Hola mismo volumen. nomenclatura de Hola de puntos de montaje de hello incluyen hello identificador de instancias HANA hello, así como número de montaje de hello el sistema. En las implementaciones de escalado vertical solo hay un montaje, como mnt00001. Al mismo tiempo, en la implementación de escalado horizontal puede que vea tantos montajes como nodos de trabajo y principales tiene. Para entorno de escalado horizontal de hello, datos, registro, volúmenes de copia de seguridad del registro son tooeach compartido y adjunta los nodos de configuración de escalado horizontal de Hola. Ejecutar varias instancias SAP en las configuraciones, un conjunto diferente de volúmenes es la unidad de instancia grande HAN de toohello creado y conectado.

Lea el documento de Hola y buscar una unidad de la instancia de HANA grande, se tenga en cuenta que unidades Hola vienen con el volumen de disco en su lugar más amplio de HANA/datos y que tenemos un volumen HANA/registro/copia de seguridad. motivo de Hello ¿por qué se tamaño Hola HANA/datos tan grande es que ofrecemos de como un cliente usa las instantáneas de almacenamiento de Hola Hola mismo volumen de disco. Significa hello más instantáneas de almacenamiento que llevar a cabo, Hola instantáneas en los volúmenes de almacenamiento que se asignó consume más espacio. Hola HANA registro/copia de seguridad o volumen es no pensamiento toobe Hola copias de seguridad de base de datos de tooput en. Es toobe tamaño utilizado como volumen de copia de seguridad para copias de seguridad de registro de transacciones de hello HANA. En futuras versiones de almacenamiento de hello instantáneas instantáneas de autoservicio, que se aplicará a este toohave volumen específico más frecuentes. Y con el que más frecuentan sitio de recuperación ante desastres de replicaciones toohello si así lo desea toooption en para la funcionalidad de recuperación ante desastres de hello proporcionada por la infraestructura de instancia grande de HANA Hola. Vea los detalles en [Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 

Además proporciona almacenamiento toohello, puede adquirir la capacidad de almacenamiento adicional en incrementos de 1 TB. Este almacenamiento adicional puede agregarse como nuevos volúmenes tooa HANA instancias de gran tamaño.

Durante la incorporación con SAP HANA en administración de servicios de Azure, Hola el cliente especifica un identificador de usuario (UID) y el Id. de grupo (GID) de grupo de usuario y sapsys SIDADM Hola (p. ej: 1000,500) es necesario que durante la instalación de sistema de SAP HANA hello, se utilizan estos mismos valores. Como se desee toodeploy varias instancias HANA en una unidad, dispone de varios conjuntos de volúmenes (un conjunto por cada instancia). Como resultado, durante la implementación debe toodefine:

- Hola SID de distintas instancias HANA hello (SIDADM se deriva fuera de ella).
- Tamaños de memoria de distintas instancias HANA Hola. Puesto que tamaño de memoria de Hola por instancias define tamaño Hola de volúmenes de hello en cada conjunto de volúmenes individuales.

En función de las recomendaciones del proveedor de almacenamiento Hola siguientes opciones de montaje se configura para todos los volúmenes montados (excluye los LUN de inicio):

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

Estos puntos se configuran en/etcetera/fstab como se muestra en hello después de gráficos de montaje:

![fstab de volúmenes montados en la unidad de instancia grande de HANA](./media/hana-installation/image1_fstab.PNG)

salida de Hello de hello comando df -h en una unidad de instancia grande de HANA S72m sería:

![fstab de volúmenes montados en la unidad de instancia grande de HANA](./media/hana-installation/image2_df_output.PNG)


Controladora de almacenamiento de Hola y nodos de marcas de instancia grande de hello son servidores de tooNTP sincronizados. Con usted sincronizar Hola SAP HANA en unidades de Azure (instancias de gran tamaño) y máquinas virtuales de Azure en un servidor NTP, no debería haber ningún pase de una desviación de mucho tiempo entre la infraestructura de Hola y unidades de proceso de hello en Azure o instancia grande sellos.

En orden toooptimize almacenamiento de información de SAP HANA toohello utilizado por debajo, también debe establecer Hola parámetros de configuración de SAP HANA siguientes:

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
En las versiones de SAP HANA 1.0 seguridad tooSPS12, estos parámetros se pueden establecer durante la instalación de Hola de base de datos de SAP HANA hello, como se describe en [SAP nota #2267798 - configuración de base de datos de SAP HANA hello](https://launchpad.support.sap.com/#/notes/2267798)

También puede configurar parámetros de hello después de la instalación de base de datos de SAP HANA hello mediante el marco de trabajo de hello hdbparam. 

SAP HANA 2.0, el marco de trabajo de hello hdbparam está en desuso. Como resultado se deben establecer los parámetros de hello mediante comandos SQL. Para más información, consulte la [nota de SAP n.º 2399079: Eliminación de hdbparam en HANA 2](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>Sistema operativos

Espacio de intercambio de hello entregado la imagen del sistema operativo se establece GB too2 según toohello [SAP compatibilidad Nota #1999997 - preguntas más frecuentes: SAP HANA memoria](https://launchpad.support.sap.com/#/notes/1999997/E). Un valor diferente que se desee necesidades toobe establecido por el usuario como un cliente.

[SUSE Linux Enterprise Server 12 SP1 para aplicaciones de SAP](https://www.suse.com/products/sles-for-sap/hana) es Hola distribución de Linux instalado para SAP HANA en Azure (instancias de gran tamaño). Esta distribución particular proporciona capacidades específicas de SAP &quot;fuera del cuadro de hello&quot; (incluidos los parámetros predefinidos para ejecutar de forma eficaz SAP en SLES).

Vea [recurso de biblioteca/White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) en el sitio Web SUSE hello y [SAP en SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) en Hola red de la Comunidad de SAP (SCN) para varios recursos útiles relacionados con SAP HANA en SLES (incluido Hola instalación toodeploying de alta disponibilidad, operaciones de tooSAP específico de la protección de seguridad etc.).

Vínculos adicionales y útiles relacionados sobre SAP en SUSE:

- [SAP HANA on SUSE Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) (Sitio de SAP HANA en SUSE Linux)
- [Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113) (Procedimiento recomendado para SAP: poner en cola la replicación - SAP NetWeaver en SUSE Linux Enterprise 12)
- [ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (ClamSAP: protección contra virus de SLES para SAP), incluido SLES 12 para SAP Applications

SAP tooimplementing aplicable de notas de compatibilidad con SAP HANA en SLES 12:

- [Nota de compatibilidad de SAP n.º 1944799: Instrucciones de SAP HANA para la instalación de sistema operativo](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
- [Nota de compatibilidad de SAP n.º 2205917: Configuración recomendada del sistema operativo de SAP HANA DB para SLES 12 en aplicaciones SAP](https://launchpad.support.sap.com/#/notes/2205917/E)
- [Nota de compatibilidad de SAP n.º 1984787: Notas de instalación de SUSE Linux Enterprise Server 12](https://launchpad.support.sap.com/#/notes/1984787)
- [Nota de compatibilidad de SAP n.º 171356: Información general del software SAP en Linux](https://launchpad.support.sap.com/#/notes/1984787)
- [Nota de compatibilidad de SAP n.º 1391070: Soluciones UUID de Linux](https://launchpad.support.sap.com/#/notes/1391070)

[Red Hat Enterprise Linux para SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) es otra oferta para ejecutar SAP HANA en instancias grandes de HANA. Ya están disponibles las versiones de RHEL 6.7 y 7.2. 

Vínculos adicionales y útiles relacionados sobre SAP en Red Hat:
- [Sitio de SAP HANA en Red Hat Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

Notas de compatibilidad con aplicable tooimplementing SAP HANA en Red Hat de SAP:

- [Nota de compatibilidad de SAP n.º 2009879: Directrices de SAP HANA para el sistema operativo Red Hat Enterprise Linux (RHEL)](https://launchpad.support.sap.com/#/notes/2009879/E)
- [2292690 - SAP HANA DB: Configuración recomendada del sistema operativo para RHEL 7](https://launchpad.support.sap.com/#/notes/2292690)
- [Nota de compatibilidad de SAP n.º 2247020: Configuración recomendada del sistema operativo para RHEL 6.7 en SAP HANA DB](https://launchpad.support.sap.com/#/notes/2247020)
- [Nota de compatibilidad de SAP n.º 1391070: Soluciones UUID de Linux](https://launchpad.support.sap.com/#/notes/1391070)
- [Nota de compatibilidad de SAP n.º 2228351: Linux: Revisión 110 (o superior) de SAP HANA Database SPS 11 en RHEL 6 o SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [Nota de compatibilidad de SAP n.º2397039: P+F sobre SAP en RHEL](https://launchpad.support.sap.com/#/notes/2397039).
- [Nota de compatibilidad de SAP n.º 1496410: Instalación y actualización de Red Hat Enterprise Linux 6.x](https://launchpad.support.sap.com/#/notes/1496410).
- [Nota de compatibilidad de SAP n.º 2002167: Instalación y actualización de Red Hat Enterprise Linux 7.x](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Sincronización de la hora

Aplicaciones de SAP depende de la arquitectura de SAP NetWeaver Hola distinguen las diferencias de tiempo para diversos componentes que conforman la Hola Hola sistema SAP. Volcados de SAP ABAP corto con título de error de Hola de ZDATE\_grande\_tiempo\_diferencias probablemente esté familiarizado, como estos archivos de volcado cortos aparecen cuando hello hora del sistema de diferentes servidores o máquinas virtuales se deriva mucho tiempo.

Para SAP HANA en Azure (instancias grandes), sincronización de hora que se realiza en Azure &#39; t aplicar toohello unidades de proceso en marcas de hello instancia grande. Esta sincronización no se aplica para ejecutar aplicaciones de SAP en máquinas virtuales nativas de Azure, ya que Azure garantiza que la hora del sistema está correctamente sincronizada. Como resultado, un servidor debe estar configurado de tiempo independiente que puede utilizarse en servidores de aplicaciones de SAP con máquinas virtuales de Azure y Hola SAP HANA base de datos de instancias que se ejecutan en instancias grandes HANA. infraestructura de almacenamiento de Hello en marcas de instancia grande es sincronizados con los servidores NTP.

## <a name="setting-up-smt-server-for-suse-linux"></a>Configuración de servidor SMT para SUSE Linux
Instancias de SAP HANA grandes no tiene toohello de conexión directa con Internet. Por lo tanto, no es un tooregister proceso sencillo como una unidad con el proveedor del sistema operativo de Hola y toodownload y aplicar revisiones. En caso de hello de SUSE Linux, una solución podría ser tooset de un servidor de SMT en una máquina virtual de Azure. Mientras que necesita hello Azure VM toobe había hospedado en una red virtual de Azure, que está conectado toohello instancia grande de HANA. Con este tipo un servidor SMT, unidad de instancia grande de HANA Hola podría registrar y descargar revisiones. 

SUSE proporciona una guía más extensa en [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf) (Herramienta de administración de suscripciones para SLES 12 SP2). 

Como condición previa para la instalación de Hola de un servidor SMT que cumple la tarea hello para la instancia de HANA grande, deberá:

- Una red virtual de Azure que está conectado toohello circuito HANA grandes instancia ER.
- Una cuenta de SUSE que esté asociada a una organización. Mientras que la organización de hello necesitaría toohave alguna suscripción SUSE válida.

### <a name="installation-of-smt-server-on-azure-vm"></a>Instalación del servidor SMT en la máquina virtual de Azure

En este paso, instale a Hola SMT server en una máquina virtual de Azure. primera medida de Hello es toolog en toohello [centro de atención al cliente de SUSE](https://scc.suse.com/)

Tal y como se ha iniciado sesión, vaya tooOrganization--> credenciales de la organización. En esa sección debería encontrar credenciales hello tooset necesario de servidor de SMT Hola.

Hola tercer paso es tooinstall una VM de Linux SUSE Hola red virtual de Azure. Hola toodeploy VM, tomar una imagen de la Galería de SLES 12 SP2 de Azure. En el proceso de implementación de hello, no defina un nombre DNS y no use direcciones IP estáticas, tal como se muestra en esta captura de pantalla

![implementación de VM para servidor SMT](./media/hana-installation/image3_vm_deployment.png)

Hello VM implementada era una máquina virtual más pequeña y tiene la dirección IP interna de hello en hello red virtual de Azure de 10.34.1.4. Nombre de máquina virtual de hello era smtserver. Después de la instalación de hello, se comprobaba Hola conectividad toohello HANA grandes unidades de instancia. Depende de cómo se organiza la resolución de nombres tendrá que tooconfigure resolución de unidades de instancia grande de HANA hello en etcetera/hosts de máquina virtual de Azure hello. Agregar una máquina virtual que se va toobe utiliza revisiones de hello toohold toohello de disco adicional. disco de arranque de Hello propio podría ser demasiado pequeño. En el caso de hello muestra, disco de hello tenemos montada demasiado/srv/www/htdocs tal y como se muestra en la siguiente captura de pantalla de Hola. Un disco de 100 GB debería ser suficiente.

![implementación de VM para servidor SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Inicie sesión en unidades de instancia grande de HANA toohello, mantener/etc/hosts y compruebe si puede alcanzar Hola VM de Azure que se supone que el servidor de toorun Hola SMT a través de red de Hola.

Después de esta comprobación se realiza correctamente, debe toolog en toohello VM de Azure que se debe ejecutar el servidor SMT Hola. Si utilizas putty toolog en toohello VM, debe tooexecute esta secuencia de comandos en la ventana de bash:

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Después de ejecutar estos comandos, reinicie la configuración de hello tooactivate intensiva de errores. Después, inicie YAST.

En YAST, vaya tooSoftware mantenimiento y busque smt. Seleccione smt, que se activa automáticamente smt tooyast2 tal y como se muestra a continuación

![SMT en yast](./media/hana-installation/image5_smt_in_yast.PNG)


Acepte la selección de Hola para su instalación en smtserver Hola. Una vez instalado, vaya a configuración del servidor toohello SMT y especificar credenciales de la organización Hola de hello SUSE centro de atención al cliente recuperó anteriormente. Especifique también el nombre de host de máquina virtual de Azure Hola SMT dirección URL del servidor. En esta demostración, era https://smtserver como se muestra en el gráfico siguiente Hola.

![Configuración del servidor SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Como paso siguiente, es necesario tootest si funciona el centro de atención al cliente de hello conexión toohello SUSE. Como se ve en hello después de gráficos, en caso de demostración de hello, ha funcionado.

![Centro de atención al cliente de tooSUSE de conectarse de prueba](./media/hana-installation/image7_test_connect.png)

Una vez Hola SMT se inicia el programa de instalación, deberá tooprovide una contraseña de base de datos. Puesto que es una instalación nueva, debe toodefine que la contraseña tal y como se muestra en el gráfico siguiente Hola.

![Definir la contraseña de la base de datos](./media/hana-installation/image8_define_db_passwd.PNG)

interacción siguiente Hello que tiene es cuando se crea un certificado. Vaya a través del cuadro de diálogo de hello tal y como se muestra a continuación y paso Hola debe continuar.

![Crear certificado para el servidor SMT](./media/hana-installation/image9_certificate_creation.PNG)

Puede haber algunos minutos empleados en el paso de Hola de 'Comprobación de la sincronización de ejecución' final Hola de configuración de Hola. Después de la instalación de Hola y la configuración del servidor SMT hello, debería buscar repositorio de directorio de hello en hello montaje punto /srv/www/htdocs/junto con algunos subdirectorios en el repositorio. 

Reinicie el servidor SMT de Hola y sus servicios relacionados con estos comandos.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Descarga de paquetes al servidor SMT

Después de que todos hello se reinicien los servicios, seleccione Hola paquetes adecuados en la administración de SMT usando Yast. selección de paquetes de saludo depende imagen del sistema operativo Hola del servidor de instancia grande de HANA hello y no de hello SLES versión o una versión de servidor en hello VM ejecución Hola SMT. A continuación se muestra un ejemplo de pantalla de selección de bienvenida.

![Seleccionar paquetes](./media/hana-installation/image10_select_packages.PNG)

Una vez haya terminado con la selección de paquetes de saludo, necesita copia inicial de hello toostart de servidor de SMT Hola Seleccionar paquete toohello que configurar. Esta copia se desencadena en el shell de hello mediante Hola comando smt-reflejado tal y como se muestra a continuación


![Descargar paquetes tooSMT server](./media/hana-installation/image11_download_packages.PNG)

Como se ve por encima, obtener deben copiar paquetes de saludo en directorios de hello creados en hello montaje punto /srv/www/htdocs. Este proceso puede tardar unos minutos. Según el número de paquetes que seleccione, pueden tardar tooone hora o más.
Cuando finalice este proceso, deberá toomove toohello config cliente. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Configurar Hola SMT cliente en las unidades de la instancia de HANA grande

clientes de Hello en este caso son unidades de instancia grande de HANA de Hola. config de servidor de Hello copia Hola script clientSetup4SMT.sh en hello VM de Azure. Copie ese script sobre toohello unidad instancia grande de HANA desea tooconnect tooyour SMT servidor. Inicia el script de Hola con la opción -h de Hola y asígnele como nombre del parámetro hello del servidor SMT. En este ejemplo es smtserver.

![Configurar el cliente SMT](./media/hana-installation/image12_configure_client.PNG)

Puede haber un escenario donde hello carga del certificado de Hola desde servidor hello de cliente de Hola se realizó correctamente, pero el error en el registro de hello tal y como se muestra a continuación.

![Se produce un error en el registro de cliente](./media/hana-installation/image13_registration_failed.PNG)

Si el error en el registro de hello, lea esta [SUSE admite documento](https://www.suse.com/de-de/support/kb/doc/?id=7006024) y ejecutar pasos de hello descritos no existe.

> [!IMPORTANT] 
> Como nombre de servidor necesita tooprovide Hola nombre del programa Hola a máquina virtual, en este caso smtserver, sin un nombre de dominio completo de Hola. Simplemente Hola VM nombre funciona. 

Después de ejecutar estos pasos, necesita hello tooexecute siguiente comando en la unidad de instancia grande de HANA Hola

```
SUSEConnect –cleanup
```

> [!Note] 
> En nuestras pruebas siempre ha surgido toowait unos minutos después de ese paso. Hello clientSetup4SMT.sh ejecución inmediata, tras hello medidas correctoras que se describen en hello artículo SUSE, finalizó con mensajes de que ese certificado hello no sería válido aún. Para configurar correctamente el cliente normalmente se tenía que esperar 5-10 minutos y ejecutar clientSetup4SMT.sh.

Si ha ejecutado en el problema de Hola que necesitan toofix basándose en los pasos del artículo SUSE Hola Hola, se necesitará toorestart clientSetup4SMT.sh en la unidad de instancia grande de HANA Hola de nuevo. Ahora debería finalizar correctamente como se muestra a continuación.

![Registro correcto del cliente](./media/hana-installation/image14_finish_client_config.PNG)

Con este paso, configuró a Hola SMT cliente de hello instancia grande de HANA unidad tooconnect en servidor SMT Hola que instaló en hello VM de Azure. Ahora puede tomar 'zypper una' o 'zypper en' tooinstall OS revisiones instancias grandes tooHANA o instalar paquetes adicionales. Se entiende que sólo puede obtener las revisiones que se descargó antes en el servidor SMT Hola.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Ejemplo de una instalación de SAP HANA en instancias grandes de HANA
Esta sección muestra cómo tooinstall SAP HANA en una unidad de la instancia de HANA grande. estado de inicio de Hello tenemos tiene el siguiente aspecto:

- Proporciona Microsoft toodeploy de datos de hello todos los que una instancia de gran tamaño de SAP HANA.
- Hola instancia grande de SAP HANA que recibió de Microsoft.
- Crea una red virtual de Azure que está conectado tooyour en la red local.
- Conectado circuito de ExpressRotue de Hola para instancias grandes HANA toohello misma red virtual de Azure.
- Ha instalado una máquina virtual de Azure que se usa como host administrativo seguro para instancias grandes de HANA.
- Se haya asegurado de que puede conectarse desde la unidad de instancia grande de HANA de hello salto cuadro tooyour y viceversa.
- Comprueba si todos los paquetes necesarios de Hola y revisiones que se instalan.
- Lea las notas de SAP hello y documentaciones relativa a la instalación de HANA en hello OS está usando y asegurado de que versión HANA Hola de elección es compatible con la versión de SO Hola.

Lo que se muestra en las secuencias de hello siguientes es la descarga de Hola de hello HANA instalación paquetes toohello salto cuadro VM, en este caso se ejecuta en un sistema operativo de Windows, copia de Hola de unidad de hello paquetes toohello instancia grande de HANA y secuencia de hello del programa de instalación de Hola.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Descarga de bits de instalación de SAP HANA Hola
Puesto que unidades de instancia grande de HANA hello no tienen conectividad directa toohello internet, directamente no se puede descargar los paquetes de instalación de Hola de toohello SAP HANA grandes máquinas virtuales de la instancia. tooovercome Hola falta conectividad directa a internet, deberá cuadro saltar de Hola. Descargar Hola paquetes toohello salto cuadro máquina virtual.

En orden toodownload Hola HANA los paquetes de instalación, necesita un usuario de S SAP u otro usuario, lo que permite tooaccess Hola Marketplace de SAP. Después de iniciar sesión, recorra esta secuencia de pantallas:

Vaya demasiado[SAP Service Marketplace](https://support.sap.com/en/index.html) > haga clic en descargar Software > instalaciones y actualización > por índice alfabético > en H: SAP HANA Platform Edition > SAP HANA Platform Edition 2.0 > instalación > Hola de descarga archivos siguientes

![Descargar la instalación de HANA](./media/hana-installation/image16_download_hana.PNG)

En caso de demostración de hello, se descargan los paquetes de instalación de SAP HANA 2.0. En cuadro de hello salto Azure VM, expandir autoextraíbles hello en directorio de hello tal y como se muestra a continuación.

![Extraer la instalación de HANA](./media/hana-installation/image17_extract_hana.PNG)

Tal y como se extraen los archivos de hello, copie directory Hola creado por extracción hello, en caso de hello anteriormente 51052030, unidad de instancia HANA grandes toohello en volumen de /hana/shared hello en un directorio que creó.

> [!Important]
> No copie los paquetes de instalación de hello en raíz de Hola o LUN de arranque desde espacio es limitado y necesita toobe utilizado por otros procesos también.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Instalar SAP HANA en la unidad de instancia grande de HANA Hola
En orden tooinstall SAP HANA, debe toolog en como raíz del usuario. Sólo raíz tiene suficiente tooinstall permisos SAP HANA.
Hola primera cosa que necesita toodo es tooset permisos en el directorio de Hola que copió en/hana/shared. permisos de Hello necesitan tooset como

```
chmod –R 744 <Installation bits folder>
```

Si desea que tooinstall SAP HANA con hello gráfica de la instalación, Hola gtk2 paquete necesidades toobe instalado en instancias de hello HANA grandes. Compruebe si se ha instalado con el comando hello

```
rpm –qa | grep gtk2
```

En más pasos, estamos demostrar la instalación de SAP HANA Hola con interfaz gráfica de usuario de Hola. Como paso siguiente, vaya al directorio de instalación de Hola y navegue al directorio de sub hello HDB_LCM_LINUX_X86_64. Iniciar

```
./hdblcmgui 
```
desde ese directorio. Ahora se Introducción le guía a través de una secuencia de pantallas donde necesita datos de hello tooprovide para la instalación de Hola. En caso de hello muestra, se están instalando servidor de base de datos de SAP HANA hello y componentes de cliente de SAP HANA Hola. Por tanto, nuestra selección es "SAP HANA Database" (Base de datos de SAP HANA) como se muestra a continuación

![Seleccionar HANA en la instalación](./media/hana-installation/image18_hana_selection.PNG)

En la siguiente pantalla de bienvenida, se elija la opción de hello 'Instalar nuevo sistema'

![Seleccionar la nueva instalación de HANA](./media/hana-installation/image19_select_new.PNG)

Después de este paso, necesita tooselect entre varios componentes adicionales que se puede instalar además servidor de base de datos de SAP HANA toohello.

![Seleccionar componentes adicionales de HANA](./media/hana-installation/image20_select_components.PNG)

A fin de Hola de esta documentación, elegimos SAP HANA cliente Hola y Hola SAP HANA Studio. También se instala una instancia de escalado vertical. por lo tanto, en la siguiente pantalla de bienvenida, deberá toochoose 'Host único sistema' 

![Seleccionar la instalación de escala vertical](./media/hana-installation/image21_single_host.PNG)

En la siguiente pantalla de bienvenida, deberá tooprovide algunos datos

![Proporcionar el SID de SAP HANA](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Como el Id. de sistema de HANA (SID), necesita tooprovide Hola mismo SID, tal y como se proporcionó a Microsoft cuando se haya solicitado la implementación de instancia grande de HANA Hola. Elegir a un SID diferente hace instalación Hola producirá un error debido a problemas de permisos de tooaccess en volúmenes diferentes Hola

Como directorio de instalación utiliza hello /hana/shared directory. En el paso siguiente de hello, necesita tooprovide ubicaciones de Hola Hola HANA archivos de datos y archivos de registro de hello HANA


![Proporcionar la ubicación del registro de HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Debe definir como archivos de registro y datos Hola volúmenes ya suministrada con puntos de montaje de Hola que contienen Hola SID que eligió en la selección de la pantalla de hello antes de esta pantalla. Si el error de coincidencia de hello SID con hello uno que escribió en el, en la pantalla de bienvenida antes, volver atrás y ajustar el valor del SID toohello tienen en los puntos de montaje de Hola Hola.

En el paso siguiente de hello, revise el nombre de host de Hola y finalmente corregirlo. 

![Revisar el nombre de host](./media/hana-installation/image24_review_host_name.PNG)

En el paso siguiente de hello, también necesita datos tooretrieve dio tooMicrosoft cuando haya solicitado la implementación de instancia grande de HANA Hola. 

![Proporcionar el UID y GID del usuario del sistema](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Necesita tooprovide Hola el mismo Id. de usuario del sistema y el Id. de grupo de usuarios que proporciona Microsoft como pedido implementación de la unidad de Hola. Si no toogive Hola muy mismos identificadores, instalación de Hola de SAP HANA en unidad de instancia grande de HANA Hola produce un error.

En las pantallas siguientes dos hello, que no vamos a presentar en esta documentación, necesita tooprovide Hola contraseña de usuario del sistema Hola de base de datos de SAP HANA hello y una contraseña de hello para el usuario de sapadm hello, que se usa para hello agente de Host de SAP que se instala como parte de instancia de base de datos de SAP HANA Hola.

Después de definir la contraseña de hello, una pantalla de confirmación aparece. Compruebe todos los datos de hello enumeran y continuar con la instalación de Hola. Llegar a una pantalla de progreso documentos Hola progreso de la instalación, como Hola a continuación

![Comprobar el progreso de la instalación](./media/hana-installation/image27_show_progress.PNG)

Cuando finalice la instalación de hello, debería una imagen como Hola sigue uno

![La instalación ha finalizado](./media/hana-installation/image28_install_finished.PNG)

En este momento, instancia de SAP HANA Hola debe ser hasta y ejecución y listo para su uso. Debe ser capaz de tooconnect tooit desde SAP HANA Studio. También asegúrese de que busque las últimas revisiones de Hola de SAP HANA y aplicar las revisiones.
























































 







 




