---
title: "Inicio rápido: instalación manual de una única instancia de SAP HANA en Azure Virtual Machines | Microsoft Docs"
description: "Guía de inicio rápido para la instalación manual de una única instancia de SAP HANA en Azure Virtual Machines"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Inicio rápido: instalación manual de una única instancia de SAP HANA en máquinas virtuales de Azure
## <a name="introduction"></a>Introducción
Esta guía de inicio rápido le ayuda a configurar una instancia única de SAP HANA en máquinas virtuales (VM) de Azure al instalar SAP NetWeaver 7.5 y SAP HANA 1.0 SP12 manualmente. objetivo de Hola de esta guía es sobre la implementación de SAP HANA en Azure. No sustituye a la documentación de SAP. 

>[!Note]
>En ella se describen las implementaciones de SAP HANA en máquinas virtuales de Azure. Para más información sobre la implementación de SAP HANA en instancias grandes de HANA, consulte [Uso de SAP en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Requisitos previos
En esta guía se da por supuesto que está familiarizado con los conceptos básicos de la infraestructura como servicio (IaaS), por ejemplo:
 * ¿Cómo toodeploy las máquinas virtuales o redes virtuales a través de Hola portal de Azure o PowerShell.
 * interfaz de línea de comandos de Hello Azure multiplataforma (CLI), incluidas las plantillas de hello opción toouse JavaScript Object Notation (JSON).

También se da por supuesto que está familiarizado con:
* SAP HANA y SAP NetWeaver y cómo tooinstall local en ellas.
* Instalación y funcionamiento de SAP HANA y las instancias de aplicación SAP en Azure.
* Hola siguientes conceptos y procedimientos:
   * Planeamiento de la implementación de SAP en Azure, como el planeamiento de Azure Virtual Network y el uso de Azure Storage. Consulte [SAP NetWeaver en máquinas virtuales de Azure: guía de planeación e implementación](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Implementación principios y formas toodeploy máquinas virtuales en Azure. Consulte [Implementación de Azure Virtual Machines para SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Alta disponibilidad para SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services) y ERS (Evaluated Receipt Settlement) en Azure. Consulte [Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Obtener detalles sobre cómo tooimprove eficacia en el aprovechamiento de una instalación de varios SID de ASCS/SCS en Azure. Consulte [Creación de una configuración de varios SID de SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Principios de ejecución de SAP NetWeaver basado en máquinas virtuales orientadas a Linux en Azure. Consulte [Ejecución de SAP NetWeaver en máquinas virtuales de SUSE Linux de Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Esta guía proporciona una configuración específica para Linux en máquinas virtuales de Azure y los detalles sobre cómo tooproperly adjuntar tooLinux de discos de almacenamiento de Azure máquinas virtuales.

En este momento, las máquinas virtuales de Azure solo están certificadas por SAP para configuraciones de escalado vertical de SAP HANA. Las configuraciones de escalado horizontal con cargas de trabajo de SAP HANA no se admiten aún. Para información sobre alta disponibilidad de SAP HANA en caso de configuraciones de escalado vertical, consulte [Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Si una instancia de SAP HANA o S/4HANA o sistema BW/4HANA implementado en el tiempo muy rápido que está buscando tooget, le convendrá uso Hola de [SAP en la nube dispositivo biblioteca](http://cal.sap.com). Puede encontrar documentación acerca de cómo implementar, por ejemplo, un sistema S/4HANA mediante SAP CAL en Azure en [esta guía](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). Todo lo que necesita toohave es una suscripción de Azure y un usuario de SAP que se pueden registrar con la biblioteca de dispositivo de SAP en la nube.

## <a name="additional-resources"></a>Recursos adicionales
### <a name="sap-hana-backup"></a>Copia de seguridad de SAP HANA
Para más información sobre la copia de seguridad de bases de datos SAP HANA en máquinas virtuales de Azure, consulte:
* [Guía de copia de seguridad de SAP HANA en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Azure Backup de SAP HANA en el nivel de archivo](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [Copia de seguridad de SAP HANA basada en instantáneas de almacenamiento](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP Cloud Appliance Library
Para obtener información sobre el uso de la biblioteca de dispositivo de nube de SAP toodeploy S/4HANA o BW/4HANA, consulte [implementar SAP S/4HANA o BW/4HANA en Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>Sistemas operativos compatibles con SAP HANA
Para más información sobre los sistemas operativos compatibles con SAP HANA, consulte [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E) (Nota de compatibilidad n.º 2235581: Sistemas operativos compatibles con SAP HANA). Las máquinas virtuales de Azure solo admiten un subconjunto de estos sistemas operativos. Hello siguientes sistemas operativos son compatible toodeploy SAP HANA en Azure: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Para obtener documentación de SAP adicional sobre SAP HANA y sistemas operativos Linux diferentes, consulte:

* [SAP Support Note #171356 - SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787) (Nota de compatibilidad de SAP n.º 171356: Información general del software SAP en Linux)
* [SAP Support Note #1944799 - SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html) (Nota de compatibilidad de SAP n.º 1944799: Instrucciones de SAP HANA para la instalación del sistema operativo SLES)
* [SAP Support Note #2205917 - SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E) (Nota de compatibilidad de SAP n.º 2205917: Configuración recomendada del sistema operativo de SAP HANA DB para SLES 12 en aplicaciones SAP)
* [SAP Support Note #1984787 - SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787) (Nota de compatibilidad de SAP n.º 1984787: Notas de instalación de SUSE Linux Enterprise Server 12)
* [SAP Support Note #1391070 - Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Nota de compatibilidad de SAP n.º 1391070: Soluciones UUID de Linux)
* [SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879) [Nota de soporte de SAP 2009879: directrices de SAP HANA para el sistema operativo Red Hat Enterprise Linux (RHEL)]
* [2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E) (2292690 - SAP HANA DB: configuraciones de sistema operativo recomendadas para RHEL 7)

### <a name="sap-monitoring-in-azure"></a>Supervisión de SAP en Azure
Para más información sobre la supervisión de SAP en Azure, consulte:

* [Nota de SAP 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). En esta nota se describe la supervisión mejorada de SAP con máquinas virtuales Linux en Azure. 
* [Nota de SAP 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). En esta nota se describe información sobre SAPOSCOL en Linux. 
* [Nota de SAP 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). En esta nota se describen las métricas de supervisión clave para SAP en Microsoft Azure.

### <a name="azure-vm-types"></a>Tipos de máquina virtual de Azure
Los tipos de máquina virtual de Azure y los escenarios de carga de trabajo admitidos por SAP y que se usan con SAP HANA se documentan en [SAP certified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html) (Plataformas IaaS certificadas por SAP). 

Tipos de Azure VM que están certificados por SAP para SAP NetWeaver u Hola a nivel de aplicación de S/4HANA se documentan en [1928533 de nota de SAP - aplicaciones SAP en Azure: tipos de productos compatibles y la máquina virtual de Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Integración de Linux de SAP de Azure solo se admite en el Administrador de recursos de Azure y no el modelo de implementación clásica Hola. 

## <a name="manual-installation-of-sap-hana"></a>Instalación manual de SAP HANA
Esta guía describe cómo toomanually instalar SAP HANA en máquinas virtuales de Azure de dos maneras diferentes:

* Utilizando el Administrador de aprovisionamiento de Software de SAP (SWPM) como parte de una instalación distribuida de NetWeaver en el paso de "instalar la instancia de base de datos" hello
* Mediante el uso de hello SAP HANA bases de datos herramienta de administrador del ciclo de vida, HDBLCM y, a continuación, instalar NetWeaver

También puede usar SWPM tooinstall todos los componentes (SAP HANA, servidor de aplicaciones de SAP de Hola y Hola ASCS instancia) en una sola máquina virtual, como se describe en este [anuncio del blog de SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Esta opción no está descrita en esta guía de inicio rápido, pero Hola Hola problemas que debe tener en cuenta son iguales.

Antes de iniciar una instalación, le recomendamos que lea Hola "Azure preparar las máquinas virtuales para la instalación manual de SAP HANA" sección más adelante en esta guía. Si lo hace, puede ayudar a evitar varios errores básicos que se pueden producir cuando se usa solo una configuración predeterminada de máquina virtual de Azure.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Pasos clave para la instalación de SAP HANA cuando se usa SAP SWPM
Esta sección enumeran los pasos clave de Hola para una instalación de SAP HANA manual y de instancia única al utilizar la instalación de SAP SWPM tooperform versión distribuida SAP NetWeaver 7.5. los pasos individuales de Hola se explican con más detalle en capturas de pantalla más adelante en esta guía.

1. Cree una red virtual de Azure que incluya dos máquinas virtuales de prueba.
2. Implementar Hola dos máquinas virtuales de Azure con sistemas operativos (en nuestro ejemplo, SUSE Linux Enterprise Server (SLES) y SLES para SP1 de 12 de las aplicaciones de SAP), según el modelo de Azure Resource Manager toohello.
3. Conectar dos Azure estándar o servidor de aplicaciones VM para el toohello de discos (por ejemplo, 75 GB o 500 GB) de almacenamiento premium.
4. Adjuntar premium almacenamiento discos toohello HANA DB máquina virtual del servidor. Para obtener más información, vea la sección de "Configuración de disco" de hello más adelante en esta guía.
5. Dependiendo de los requisitos de tamaño o rendimiento, adjuntar varios discos y, a continuación, crear volúmenes seccionados mediante administración de volúmenes lógicos o una herramienta de administración de varios dispositivos (MDADM) a nivel de hello SO dentro de hello VM.
6. Cree XFS file systems en volúmenes lógicos o discos de hello adjuntada.
7. Monte Hola XFS sistemas de archivos en el nivel de hello SO. Utilice un sistema de archivos para todo el software SAP Hola. Use Hola otro sistema de archivos para el directorio de /sapmnt hello y copias de seguridad, por ejemplo. En el servidor de base de datos de SAP HANA hello, montar sistemas de archivos de hello XFS en discos de almacenamiento premium de hello como /hana y /usr/sap. Este proceso es necesario tooprevent Hola raíz sistema de archivos que no es grande en máquinas virtuales de Azure de Linux, llene.
8. Escriba las direcciones IP de hello locales de las máquinas virtuales de prueba de hello en el archivo de hosts de hello/etcetera /.
9. Escriba hello **nofail** parámetro en el archivo hello/etcetera/fstab.
10. Establecer parámetros de kernel de Linux según la versión de sistema operativo Linux toohello que usa. Para obtener más información, vea las notas SAP adecuadas Hola que analizan HANA y Hola sección "Parámetros de Kernel" en esta guía.
11. Adición de espacio de intercambio.
12. Si lo desea, instale un escritorio gráfico en máquinas virtuales de prueba de Hola. De lo contrario, use una instalación remota con SAPinst.
13. Descargue el software SAP de Hola de hello SAP Service Marketplace.
14. Instalar la instancia de SAP ASCS de hello en máquina virtual del servidor de aplicación Hola.
15. Directorio compartido de /sapmnt Hola entre Hola probar las máquinas virtuales mediante el uso de NFS. máquina virtual del servidor de aplicación Hello es servidor NFS de Hola.
16. Instalar la instancia de base de datos de hello, incluida la HANA, mediante el uso de SWPM en la máquina virtual del servidor de base de datos de Hola.
17. Instalar el servidor de aplicaciones principales de hello (PAS) en la máquina virtual del servidor de aplicación Hola.
18. Inicie SAP Management Console (SAP MC). Conéctese con SAP GUI o HANA Studio, por ejemplo.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Pasos clave para la instalación de SAP HANA cuando se usa HDBLCM
Esta sección enumeran los pasos clave de Hola para una instalación de SAP HANA manual y de instancia única al utilizar la instalación de SAP HDBLCM tooperform versión distribuida SAP NetWeaver 7.5. los pasos individuales de Hola se explican con más detalle en capturas de pantalla a lo largo de esta guía.

1. Cree una red virtual de Azure que incluya dos máquinas virtuales de prueba.
2. Implementar dos máquinas virtuales de Azure con sistemas operativos (en nuestro ejemplo, SLES y SLES para SP1 de 12 de las aplicaciones de SAP) según el modelo de Azure Resource Manager toohello.
3. Conectar dos Azure estándar o premium almacenamiento discos (por ejemplo, 75 GB o 500 GB) toohello aplicación máquina virtual del servidor.
4. Adjuntar premium almacenamiento discos toohello HANA DB máquina virtual del servidor. Para obtener más información, vea la sección de "Configuración de disco" de hello más adelante en esta guía.
5. Dependiendo de los requisitos de tamaño o rendimiento, adjuntar varios discos y crear volúmenes seccionados mediante administración de volúmenes lógicos o una herramienta de administración de varios dispositivos (MDADM) a nivel de hello SO dentro de hello VM.
6. Cree XFS file systems en volúmenes lógicos o discos de hello adjuntada.
7. Monte Hola XFS sistemas de archivos en el nivel de hello SO. Utilice un sistema de archivos para todo el software SAP hello y use Hola otros uno para el directorio de /sapmnt Hola y copias de seguridad, por ejemplo. En el servidor de base de datos de SAP HANA hello, montar sistemas de archivos de hello XFS en discos de almacenamiento premium de hello como /hana y /usr/sap. Este proceso es necesario toohelp impedir que sistema de archivos de raíz de hello, que no es de gran tamaño en máquinas virtuales de Azure de Linux, se llene.
8. Escriba las direcciones IP de hello locales de las máquinas virtuales de prueba de hello en el archivo de hosts de hello/etcetera /.
9. Escriba hello **nofail** parámetro en el archivo hello/etcetera/fstab.
10. Establecer parámetros de kernel según la versión de sistema operativo Linux toohello que usa. Para obtener más información, vea las notas SAP adecuadas Hola que analizan HANA y Hola sección "Parámetros de Kernel" en esta guía.
11. Adición de espacio de intercambio.
12. Si lo desea, instale un escritorio gráfico en máquinas virtuales de prueba de Hola. De lo contrario, use una instalación remota con SAPinst.
13. Descargue el software SAP de Hola de hello SAP Service Marketplace.
14. Crear un grupo, sapsys, con el grupo identificador 1001, en la máquina virtual del servidor de base de datos de HANA Hola.
15. Instalar SAP HANA en máquina virtual del servidor de base de datos de hello mediante el Administrador de ciclo de vida de base de datos de HANA (HDBLCM).
16. Instalar la instancia de SAP ASCS de hello en máquina virtual del servidor de aplicación Hola.
17. Directorio compartido de /sapmnt Hola entre Hola probar las máquinas virtuales mediante el uso de NFS. máquina virtual del servidor de aplicación Hello es servidor NFS de Hola.
18. Instalar la instancia de base de datos de hello, incluida la HANA, mediante el uso de SWPM en la máquina virtual del servidor de base de datos de HANA Hola.
19. Instalar el servidor de aplicaciones principales de hello (PAS) en la máquina virtual del servidor de aplicación Hola.
20. Inicie SAP MC. Conectarse mediante SAP GUI o HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Preparación de las máquinas virtuales de Azure para la instalación manual de SAP HANA
Esta sección abarca Hola temas siguientes:

* Actualizaciones del sistema operativo
* Configuración de disco
* Parámetros de kernel
* Sistemas de archivos
* archivo de hosts de Hello/etcetera /
* archivo Hello/etcetera/fstab

### <a name="os-updates"></a>Actualizaciones del sistema operativo
Compruebe si hay actualizaciones y correcciones del sistema operativo Linux antes de instalar software adicional. Al instalar una revisión, es posible que pueda tooavoid un servicio de soporte técnico de llamada toohello.

Asegúrese de que está usando:
* SUSE Linux Enterprise Server for SAP Applications.
* Red Hat Enterprise Linux for SAP Applications o Red Hat Enterprise Linux for SAP HANA. 

Si no lo ha hecho ya, registrará la implementación del sistema operativo Hola con su suscripción de Linux desde un proveedor de Linux Hola. Tenga en cuenta que SUSE tiene imágenes del SO para aplicaciones SAP que ya incluyen servicios y que se registran automáticamente.

Este es un ejemplo de comprobación de las revisiones disponibles para SUSE Linux mediante el uso de hello **zypper** comando:

 `sudo zypper list-patches`

Según el tipo de saludo de problema, las revisiones se clasifican por categoría y gravedad. Los valores usados normalmente para categoría son: **seguridad**, **recomendada**, **opcional**, **característica**, **documento** o **yast**.
Los valores usados normalmente para gravedad son: **crítica**, **importante**, **moderada**, **baja** o **no especificada**.

Hola **zypper** comando busca solo para Hola de las actualizaciones que necesitan los paquetes instalados. Por ejemplo, podría utilizar este comando:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Puede agregar parámetro hello `--dry-run` tootest Hola actualización sin actualizar realmente sistema Hola.


### <a name="disk-setup"></a>Configuración de disco
sistema de archivos de raíz de Hello en una VM de Linux en Azure tiene un límite de tamaño. Por lo tanto, es necesario tooattach adicional en el disco espacio tooan máquina virtual de Azure para ejecutar SAP. Para servidor de aplicaciones de SAP máquinas virtuales de Azure, Hola de discos de almacenamiento estándar Azure puede ser suficiente. Sin embargo, para máquinas virtuales de Azure de DBMS de SAP HANA, es obligatorio usar Hola discos de almacenamiento Premium de Azure para implementaciones de producción y no es de producción.

En función de hello [requisitos de almacenamiento de SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), se sugiere Hola siguiente configuración de almacenamiento Premium de Azure: 

| SKU de la máquina virtual | RAM |  /hana/data y /hana/log <br /> seccionado con LVM o MDAADM | /hana/shared | /root volume | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

En la configuración de disco sugerido hello, volumen de datos HANA Hola y de registro se colocan en hello al mismo conjunto de discos de almacenamiento de Azure premium que se seccionan con LVM o MDADM. No es necesario toodefine cualquier redundancia RAID de nivel porque el almacenamiento Premium de Azure mantiene tres imágenes de discos de Hola para conseguir redundancia. toomake seguro de que configure suficiente almacenamiento, consulte hello [requisitos de almacenamiento de SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) y [SAP HANA servidor guía de instalación y actualización](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Considere también los discos de almacenamiento premium de Azure diferentes de volúmenes de rendimiento de disco duro virtual (VHD) diferente Hola del programa Hola a como se documenta en [discos administrados para las máquinas virtuales y almacenamiento de alto rendimiento Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Puede agregar que más espacio de almacenamiento premium discos toohello HANA DBMS las máquinas virtuales para almacenar copias de seguridad de registro de transacciones o base de datos.

Para obtener más información acerca de hello dos herramientas principales utilizadas tooconfigure creación de bandas, vea Hola siguientes artículos:

* [Configuración del software RAID en Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configuración del LVM en una máquina virtual Linux en Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Para obtener más información sobre cómo conectar discos tooAzure las máquinas virtuales ejecutan Linux como sistema operativo invitado, consulte [agregar una VM de Linux de disco tooa](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Almacenamiento Premium de Azure permite disco toodefine modos el almacenamiento en caché. Para un conjunto de hello particionado mantienen /hana/data y /hana/log, se debe deshabilitar el almacenamiento en caché de disco. Para hello otros volúmenes (discos), Hola almacenamiento en caché se debe establecer el modo demasiado**ReadOnly**.

Para más información, consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md).

plantillas de JSON de ejemplo toofind para crear máquinas virtuales, vaya demasiado[plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).
plantilla de vm-simple-sles Hello es una plantilla básica. Incluye una sección de almacenamiento, con un disco de datos adicional de 100 GB. Esta plantilla se puede usar como base. Puede adaptar la configuración específica de hello plantilla tooyour.

>[!Note]
>Se trata de disco de almacenamiento de Azure de hello tooattach importantes mediante un UUID tal como se describe en [ejecuta SAP NetWeaver en máquinas virtuales de Microsoft Azure SUSE Linux](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

En el entorno de prueba de hello, dos discos de almacenamiento estándar Azure eran servidor de aplicaciones SAP toohello adjunto de máquina virtual, tal y como se muestra en la siguiente captura de pantalla de Hola. Un disco almacena todo el software de SAP hello (incluidos NetWeaver 7.5, GUI de SAP y SAP HANA) para la instalación. segundo disco de Hello comprobó que suficiente espacio libre estaría disponible para los requisitos adicionales (por ejemplo, los datos de copia de seguridad y prueba) y para hello /sapmnt directorio (es decir, los perfiles de SAP) toobe compartido entre todas las máquinas virtuales que pertenecen toohello panorama SAP mismo.

![Ventana de discos de servidor de aplicaciones de SAP HANA que muestra dos discos de datos y sus tamaños](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Parámetros de kernel
SAP HANA requiere configuración de kernel de Linux específica, que no forman parte de imágenes de la Galería de Azure estándar de Hola y debe establecerse manualmente. Dependiendo de si utiliza SUSE o Red Hat, parámetros de hello podrían ser diferentes. las notas de SAP de Hello enumeradas anteriormente proporcionan información acerca de los parámetros. En capturas de pantalla de Hola que se muestra, se usó SUSE Linux 12 SP1. 

SLES para GA de 12 de las aplicaciones de SAP y SLES para SP1 de 12 de las aplicaciones de SAP tienen una nueva herramienta, **adm optimizado**, que reemplaza Hola antiguo **sapconf** herramienta. Hay un perfil de SAP HANA especial disponible para **tuned-adm**. sistema de hello tootune para SAP HANA, escriba siguiente de Hola como un usuario raíz:

   `tuned-adm profile sap-hana`

Para obtener más información acerca de **adm optimizado**, vea hello [documentación SUSE sobre adm optimizado](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

En la siguiente captura de pantalla de hello, puede ver cómo **adm optimizado** Hola modificada `transparent_hugepage` y `numa_balancing` valores, según toohello la configuración de SAP HANA necesaria.

![herramienta de adm optimizado Hola cambia los valores según toorequired configuración de SAP HANA](./media/hana-get-started/image005.jpg)

configuración de kernel de SAP HANA de Hola de toomake permanentes, use **grub2** en SLES 12. Para obtener más información acerca de **grub2**, vaya toohello [estructura de archivos de configuración](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sección de hello documentación SUSE.

Hello captura de pantalla siguiente muestra cómo Hola kernel configuración se ha cambiado en el archivo de configuración de hello y, a continuación, compilado con **grub2 mkconfig**:

![Configuración de kernel cambiado en el archivo de configuración de Hola y compilado mediante grub2 mkconfig](./media/hana-get-started/image006.jpg)

Otra opción es configuración de hello toochange mediante hello y YaST **cargador de arranque** > **parámetros de Kernel** configuración:

![ficha de configuración de parámetros de Kernel de Hello en YaST cargador de arranque](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Sistemas de archivos
Hello captura de pantalla siguiente muestra dos sistemas de archivos que se crearon en el servidor de aplicaciones SAP de hello VM encima de dos discos de almacenamiento de Azure conectado estándar Hola. Ambos sistemas de archivos son del tipo XFS y están montado demasiado/SAP y /sapsoftware.

Es no siempre es así toostructure los sistemas de archivos de esta manera. Tiene otras opciones para estructurar el espacio en disco Hola. consideración más importante de Hello es tooprevent Hola filesystem raíz de quedarse sin espacio libre.

![Dos sistemas de archivos que creó en la máquina virtual del servidor de aplicaciones SAP de Hola](./media/hana-get-started/image008.jpg)

Con respecto a hello y Hola VM de base de datos de SAP HANA, durante una instalación de base de datos, cuando se usa SAPinst (SWPM) **típico** opción de instalación, todo se ha instalado en /hana y /usr/sap. ubicación predeterminada de Hola para copia de seguridad del registro de hello SAP HANA está bajo /usr/sap. De nuevo, dado que es importante tooprevent Hola filesystem raíz de quedarse sin espacio de almacenamiento, asegúrese de que hay suficiente espacio libre en /hana y /usr/sap antes de instalar SAP HANA mediante SWPM.

Para obtener una descripción del diseño del sistema de archivos estándar de Hola de SAP HANA, vea hello [SAP HANA servidor guía de instalación y actualización](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Sistemas de archivos adicionales que se crea en la máquina virtual del servidor de aplicaciones SAP de Hola](./media/hana-get-started/image009.jpg)

Cuando se instala SAP NetWeaver en un SLES/SLES estándar para la imagen de la Galería de Azure de 12 de las aplicaciones de SAP, se muestra un mensaje que indica que no hay ningún espacio de intercambio, como se muestra en la siguiente captura de pantalla de Hola. toodismiss este mensaje, puede agregar manualmente un archivo de intercambio mediante **dd**, **mkswap**, y **swapon**. toolearn, busque "Agregar manualmente un archivo de intercambio" Hola [Using Hola YaST particionador](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sección de hello documentación SUSE.

Otra opción es tooconfigure de espacio de intercambio mediante el uso de hello agente de VM de Linux. Para obtener más información, vea hello [Guía de usuario de agente de Linux de Azure](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Mensaje emergente que avisa de que no hay espacio de intercambio suficiente](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>archivo de hosts de Hello/etcetera /
Antes de empezar tooinstall SAP, asegúrese de que incluir los nombres de host de Hola y direcciones IP de máquinas virtuales de SAP de hello en el archivo/etc/hosts de hello. Implementar todas las máquinas virtuales de SAP de hello en una red virtual de Azure y, a continuación, utilice las direcciones IP internas hello, como se muestra aquí:

![Los nombres de host y direcciones IP de máquinas virtuales de SAP de hello enumeran en el archivo/etc/hosts de hello](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>archivo Hello/etcetera/fstab

Resulta útil tooadd hello **nofail** archivo de parámetros toohello fstab. De esta manera, si algo va mal con discos de Hola Hola VM no se bloquea en proceso de arranque de Hola. Pero recuerde que más espacio en disco podría no estar disponible y procesos podrían se llene de sistema de archivos de hello raíz. Si falta /hana, SAP HANA no se iniciará.

![Agregar archivo fstab de hello nofail parámetro toohello](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Escritorio GNOME gráfico en SLES 12/SLES for SAP Applications 12
Esta sección abarca Hola temas siguientes:

* Instalar escritorio GNOME de Hola y xrdp en SLES 12/SLES para 12 de las aplicaciones de SAP
* Ejecución de la consola de administración de SAP basada en Java mediante Firefox en SLES 12/SLES-for-SAP Applications 12

También puede usar otras alternativas, como Xterminal o VNC (no se describen en esta guía).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Instalar escritorio GNOME de Hola y xrdp en SLES 12/SLES para 12 de las aplicaciones de SAP
Si tiene un fondo de Windows, puede fácilmente usan un escritorio gráfico directamente dentro de hello máquinas virtuales de Linux de SAP toorun Firefox, SAPinst, GUI de SAP, SAP MC o HANA Studio y conéctese toohello máquina virtual a través de hello protocolo de escritorio remoto (RDP) desde un equipo de Windows. Interfaz gráfica de usuario depende de las directivas de la empresa acerca de cómo agregar sistemas basados en Linux tooproduction y no es de producción, quizás quiera tooinstall GNOME en el servidor. escritorio GNOME de hello tooinstall en un Azure SLES 12/SLES para VM de 12 de las aplicaciones de SAP:

1. Instalar escritorio GNOME Hola escribiendo el siguiente comando (por ejemplo, en una ventana de PuTTY) de hello:

   `zypper in -t pattern gnome-basic`

2. Instalar xrdp tooallow una máquina virtual a través de RDP toohello de conexión:

   `zypper in xrdp`

3. Edite /etc/sysconfig/windowmanager y establezca Hola predeterminado ventana Administrador tooGNOME:

   `DEFAULT_WM="gnome"`

4. Ejecutar **chkconfig** toomake seguro de que xrdp se inicia automáticamente después de reiniciar el equipo:

   `chkconfig -level 3 xrdp on`

5. Si tiene un problema con hello conexión RDP, intente toorestart (desde una ventana de PuTTY, por ejemplo):

   `/etc/xrdp/xrdp.sh restart`

6. Si un reinicio xrdp se menciona en hello anterior paso no funciona, busque un archivo .pid:

   `check /var/run` 

   Busque `xrdp.pid`. Si te parece, quítelo y vuelva a intentarlo toorestart.

### <a name="starting-sap-mc"></a>Inicio de SAP MC
Después de instalar escritorio GNOME de hello, a partir de hello gráfica basados en Java SAP MC de Firefox mientras se ejecuta en un Azure SLES 12/SLES para VM de 12 de las aplicaciones de SAP puede mostrar un error debido a Hola falta el complemento de explorador de Java.

Hola de toostart de dirección URL de Hola MC SAP es `<server>:5<instance_number>13`.

Para obtener más información, consulte [iniciando Hola consola de administración de SAP basada en Web](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Hello captura de pantalla siguiente muestra hello mensaje de error que se muestra cuando falta Hola complemento de explorador de Java:

![Mensaje de error que indica que falta el complemento del explorador de Java](./media/hana-get-started/image013.jpg)

Problema de hello toosolve unidireccional es hello tooinstall falta el complemento utilizando YaST, tal y como se muestra en la siguiente captura de pantalla de hello:

![Usar tooinstall YaST falta el complemento](./media/hana-get-started/image014.jpg)

Cuando vuelva a escribir Hola URL de consola de administración de SAP, aparece un mensaje preguntándole se tooactivate Hola complemento:

![Cuadro de diálogo que solicita la activación del complemento](./media/hana-get-started/image015.jpg)

Puede que también reciba un mensaje de error sobre un archivo que falta, javafx.properties. Se trata de requisito de toohello relacionados de Oracle Java 1.8 7.4 de GUI de SAP. (Consulte la [nota de SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424)). Hola versión de IBM Java ni paquete openjdk de hello entregado con SLES/SLES 12 de las aplicaciones de SAP incluye archivo de hello javafx.properties necesarios. solución de Hello es toodownload e instale Java SE 8 de Oracle.

Para obtener información sobre un problema similar con openjdk openSUSE, vea el subproceso de discusión de hello [SAPGui 7.4 Java para openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Instalación manual de SAP HANA: SWPM
serie de Hola de capturas de pantalla en esta sección muestra Hola pasos principales para la instalación de SAP NetWeaver 7.5 y SAP HANA SP12 cuando usa SWPM (SAPinst). Como parte de una instalación de NetWeaver 7.5, SWPM también puede instalar la base de datos de hello HANA como una sola instancia.

En el entorno de prueba de ejemplo, se instaló un solo servidor de aplicaciones de Advanced Business Application Programming (ABAP). Como se muestra en la siguiente captura de pantalla de hello, hemos usado hello **sistema distribuido** opción tooinstall Hola ASCS y las instancias de servidor principal de la aplicación en una máquina virtual de Azure y SAP HANA como sistema de base de datos de hello en otra máquina virtual de Azure.

![ASCS y las instancias de servidor principal de la aplicación instalados con opción de sistema distribuido de Hola](./media/hana-get-started/image012.jpg)

Una vez instancia de hello ASCS está instalado en la máquina virtual del servidor de aplicación Hola y está establecido demasiado "verde" Hola consola de administración de SAP (se muestra en la siguiente captura de pantalla de hello), hello /sapmnt directorio (incluido el directorio del perfil SAP de hello) debe compartirse con la máquina virtual del servidor de base de datos de SAP HANA Hola. paso de instalación de Hola DB necesita tener acceso a información de toothis. el acceso de tooprovide de manera mejor de Hello es toouse NFS, que se pueden configurar mediante el uso de YaST.

![Instancia de SAP consola de administración que muestra hello ASCS instalado en la máquina virtual del servidor de aplicación hello y establezca demasiado "verde"](./media/hana-get-started/image016.jpg)

En la máquina virtual del servidor de aplicación Hola, Hola/sapmnt directorio debe compartirse a través de NFS mediante el uso de hello **rw** y **no_root_squash** opciones. Hello valores predeterminados son **ro** y **root_squash**, lo que podría provocar tooproblems cuando se instala la instancia de base de datos de Hola.

![Compartir el directorio de /sapmnt de Hola a través de NFS con las opciones de hello rw y no_root_squash](./media/hana-get-started/image017b.jpg)

Tal y como se muestra en la siguiente captura de pantalla de hello, recurso compartido de /sapmnt Hola de máquina virtual del servidor de aplicación Hola debe configurarse en la máquina virtual del servidor de base de datos de SAP HANA hello mediante el uso de **cliente NFS** (y YaST).

![recurso compartido de /sapmnt Hola configurado mediante el uso de cliente para NFS](./media/hana-get-started/image018b.jpg)

instalación tooperform versión 7.5 NetWeaver distribuida (**instancia de base de datos**), como se muestra en hello siguiente captura de pantalla, inicie sesión en la máquina virtual del servidor de base de datos de SAP HANA toohello e iniciar SWPM.

![Instalar una instancia de base de datos al iniciar sesión en la máquina virtual del servidor de base de datos de SAP HANA toohello e iniciar SWPM](./media/hana-get-started/image019.jpg)

Después de seleccionar **típico** instalación y medios de instalación de toohello de ruta de acceso de hello, escriba un SID de la base de datos, el nombre de host de hello, el número de instancia de Hola y el contraseña del administrador del sistema Hola DB.

![página de Hello SAP HANA base de datos del sistema administrador inicio de sesión de](./media/hana-get-started/image035b.jpg)

Escriba la contraseña de hello para el esquema de Hola DBACOCKPIT:

![cuadro de entrada de contraseña de Hello para el esquema de hello DBACOCKPIT](./media/hana-get-started/image036b.jpg)

Escriba una pregunta de contraseña de hello SAPABAP1 esquema:

![Escriba una pregunta de contraseña de esquema de hello SAPABAP1](./media/hana-get-started/image037b.jpg)

Una vez completada cada tarea, una marca de verificación verde se muestra la siguiente fase de tooeach de hello proceso de instalación de base de datos. mensaje de bienvenida de "ejecución de... Database Instance has completed" (Ejecución de la instancia de base de datos… completada).

![Ventana de tarea completada con el mensaje de confirmación](./media/hana-get-started/image023.jpg)

Después de la instalación correcta, Hola consola de administración de SAP debe mostrar la instancia de base de datos de hello como "verde" y mostrar hello lista completa de los procesos de SAP HANA (hdbindexserver, hdbcompileserver y así sucesivamente).

![Ventana de la consola de administración de SAP con la lista de procesos de SAP HANA](./media/hana-get-started/image024.jpg)

Hello captura de pantalla siguiente muestra las partes de Hola de estructura de archivos de hello en directorio de /hana/shared Hola que SWPM creado durante la instalación de HANA Hola. Porque no hay ninguna opción toospecify otra ruta de acceso, es importante toomount espacio en disco adicional en directorio de hello /hana antes de la instalación de SAP HANA hello mediante SWPM. Esto impide que sistema de archivos de raíz de hello quedarse sin espacio libre.

![estructura de archivos de Hello /hana/shared directorio creado durante la instalación de HANA](./media/hana-get-started/image025.jpg)

Esta captura de pantalla muestra la estructura de archivo de hello del directorio de Hola /usr/sap:

![estructura de archivos de directorios de Hello /usr/sap](./media/hana-get-started/image026.jpg)

Hola último paso de instalación de ABAP Hola distribuida es instancia de servidor principal de la aplicación de tooinstall hello:

![Instancia del servidor de aplicación principal ABAP instalación que se muestra como paso final de Hola](./media/hana-get-started/image027b.jpg)

Después de instalan instancia del servidor principal de la aplicación hello y GUI de SAP, usar hello **DBA cabina** tooconfirm de transacción que Hola instalación de SAP HANA ha finalizado correctamente:

![Ventana DBA Cockpit que confirma la instalación correcta](./media/hana-get-started/image028b.jpg)

Como paso final, podría desea instalar toofirst HANA Studio en la máquina virtual del servidor de aplicaciones SAP de hello y, a continuación, conectar la instancia de SAP HANA toohello que se ejecuta en la máquina virtual del servidor de base de datos de hello:

![Instalación de SAP HANA Studio en la máquina virtual del servidor de aplicaciones SAP de Hola](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Instalación manual de SAP HANA: HDBLCM
En suma tooinstalling SAP HANA como parte de una instalación distribuida mediante el uso de SWPM, puede instalar en primer lugar, Hola HANA independiente mediante el uso de HDBLCM. A continuación, puede instalar, por ejemplo, SAP NetWeaver 7.5. capturas de pantalla de Hello en esta sección muestran cómo funciona este proceso.

Para obtener más información acerca de la herramienta de HANA HDBLCM hello, vea:

* [Hola eligiendo la opción correcto SAP HANA HDBLCM para la tarea](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools (Herramientas de administración del ciclo de vida SAP Hana)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide (Guía de instalación y actualización del servidor SAP Hana)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

problemas tooavoid su valor predeterminado es grupo Configuración del identificador de hello `\<HANA SID\>adm user` (creado por la herramienta de hello HDBLCM), definir un nuevo grupo denominado `sapsys` mediante el uso de Id. de grupo `1001` antes de instalar SAP HANA a través de HDBLCM:

![Nuevo grupo "sapsys" definido mediante el uso del identificador de grupo 1001](./media/hana-get-started/image030.jpg)

Al iniciar hello HDBLCM por primera vez, se muestra un menú de inicio simple. Seleccionar elemento 1, **instalar nuevo sistema**, tal y como se muestra en la siguiente captura de pantalla de hello:

![Opción "Instalar el nuevo sistema" en la ventana de inicio de hello HDBLCM](./media/hana-get-started/image031.jpg)

Hello captura de pantalla siguiente muestra todas las opciones de clave de Hola que seleccionó anteriormente.

> [!IMPORTANT]
> Directorios que tengan un nombre de registro HANA y volúmenes de datos, así como ruta de acceso de instalación de hello (/ hana/shared en este ejemplo) y /usr/sap, no deben formar parte del sistema de archivos de hello raíz. Estos directorios pertenecen los discos de datos de Azure toohello que estaban conectado toohello VM (descrito en la sección "configuración del disco" hello). Este enfoque ayuda a evitar que sistema de archivos de raíz de hello quedarse sin espacio. En la siguiente captura de pantalla de hello, puede ver que Administrador de sistema HANA hello tiene un identificador de usuario `1005` y forma parte del programa Hola a `sapsys` grupo (Id. de `1001`) que se definió antes de la instalación de Hola.

![Lista de todos los componentes de SAP HANA principales seleccionados anteriormente](./media/hana-get-started/image032.jpg)

Puede comprobar hello `\<HANA SID\>adm user` (`azdadm` en la siguiente captura de pantalla de hello) detalles en el directorio/hello/etcetera/passwd:

![HANA \<HANA SID\>en el directorio/hello/etcetera/passwd muestran detalles de usuario de adm](./media/hana-get-started/image033.jpg)

Después de instalar SAP HANA mediante HDBLCM, puede ver la estructura de archivos de hello en SAP HANA Studio, tal y como se muestra en la siguiente captura de pantalla de Hola. esquema de SAPABAP1 Hello, que incluye todas las tablas de SAP NetWeaver hello, aún no está disponible.

![Estructura de archivos de SAP HANA en SAP HANA Studio](./media/hana-get-started/image034.jpg)

Después de instalar SAP HANA, puede instalar SAP NetWeaver sobre él. Como Hola se muestra en la siguiente captura de pantalla de instalación de Hola se realizó como una instalación distribuida mediante el uso de SWPM (como se describe en la sección anterior de hello). Cuando se instala la instancia de base de datos de hello utilizando SWPM, escriba Hola mismos datos mediante el uso de HDBLCM (por ejemplo, nombre de host, HANA SID y el número de instancia). SWPM, a continuación, utiliza la instalación existente de HANA de Hola y agrega más esquemas.

![Una instalación distribuida que se ha realizado mediante SWPM](./media/hana-get-started/image035b.jpg)

Hello captura de pantalla siguiente muestra el paso de instalación de hello SWPM donde escribir los datos acerca del esquema de Hola DBACOCKPIT:

![paso de instalación de Hello SWPM donde se escribe los datos del esquema DBACOCKPIT](./media/hana-get-started/image036b.jpg)

Especificar los datos sobre el esquema de Hola SAPABAP1:

![Especificar los datos de esquema de hello SAPABAP1](./media/hana-get-started/image037b.jpg)

Una vez completada la instalación SWPM de la instancia de base de datos de hello, puede ver el esquema de SAPABAP1 hello en SAP HANA Studio:

![esquema de Hello SAPABAP1 en SAP HANA Studio](./media/hana-get-started/image038b.jpg)

Por último, cuando se completen el servidor de aplicaciones SAP de Hola y las instalaciones de GUI de SAP, puede comprobar la instancia de base de datos de HANA hello mediante hello **DBA cabina** transacciones:

![instancia de base de datos de HANA Hola comprobados con hello transacción cabina de DBA](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Descargas de software de SAP
Puede descargar el software de Hola SAP Service Marketplace, tal como se muestra en las siguientes capturas de pantalla de Hola.

Descargue NetWeaver 7.5 para Linux/HANA:

 ![Ventana de instalación y actualización de SAP Service para la descarga de NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Descargue HANA SP12 Platform Edition:

 ![Ventana de instalación y actualización de SAP Service para la descarga de HANA SP12 Platform Edition](./media/hana-get-started/image002.jpg)

