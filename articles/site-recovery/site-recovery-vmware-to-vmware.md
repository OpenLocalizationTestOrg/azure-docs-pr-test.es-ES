---
title: "aaaReplicate máquinas virtuales de VMware o un sitio de tooanother servidores físicos (portal de Azure clásico) | Documentos de Microsoft"
description: "Use este artículo tooreplicate máquinas virtuales de VMware o de Windows/Linux servidores físicos tooa sitio secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Replicar máquinas virtuales de VMware en local o un sitio secundario de tooa servidores físicos en el portal de Azure clásico Hola

## <a name="overview"></a>Información general
InMage Scout en Azure Site Recovery proporciona características de replicación en tiempo real entre los sitios locales de VMware. InMage Scout se incluye en las suscripciones al servicio Azure Site Recovery. 

## <a name="prerequisites"></a>Requisitos previos
**Cuenta de Azure**: necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). [Más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery.

## <a name="step-1-create-a-vault"></a>Paso 1: Creación de un almacén
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en Nuevo > Administración > Backup and Site Recovery (OMS) (Copia de seguridad y recuperación del sitio [OMS]). También puede hacer clic en Examinar > Almacén de Servicios de recuperación > Agregar.
3. En **nombre** especificar un almacén de hello tooidentify nombre descriptivo. Si tiene más de una suscripción, seleccione una de ellas.
4. En **Grupo de recursos**, cree un grupo de recursos o seleccione uno existente. Especifique un campos de toocomplete necesario de la región de Azure.
5. En **ubicación**, seleccione Hola región geográfica para el almacén de Hola. regiones de toocheck compatibles, consulte [precios de recuperación de sitio de Azure](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Si desea que tooquickly acceso Hola almacén de hello panel haga clic en toodashboard de Pin y, a continuación, haga clic en crear.
7. nuevo almacén de Hola aparecerá en el panel hello > todos los recursos, y en hello principal de los servicios de recuperación almacenes de credenciales de hoja.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Paso 2: Configurar el almacén de Hola y descargar los componentes de InMage Scout
1. En la hoja de almacenes de servicios de recuperación de Hola seleccione el almacén y haga clic en configuración.
2. En **Configuración** > **Introducción**, haga clic en **Site Recovery** > **Paso 1: Preparar infraestructura** > **Objetivo de protección**.
3. En **objetivo de protección** seleccione sitio toorecovery y se selecciona Sí, con hipervisor de VMware vSphere. A continuación, haga clic en Aceptar.
4. En **el programa de instalación de Scout**, haga clic en la clave de software y el registro de toodownload InMage Scout 8.0.1 GA de descarga. archivos de instalación de Hola de hello todos componentes necesitan están en el archivo .zip descargado de hello.

## <a name="step-3-install-component-updates"></a>Paso 3: Instalación de actualizaciones de componentes
Conozca más reciente hello [actualizaciones](#updates). Archivos de actualización de hello en los servidores se deben instalar en hello siguiendo el orden:

1. Servidor RX si hay alguno
2. Servidores de configuración
3. Servidores de proceso
4. Servidores de destino maestros
5. Servidores de vContinuum
6. Servidor de origen (tanto servidor de Windows como de Linux)

Instalar actualizaciones de hello como sigue:

1. Descargar hello [actualizar](https://aka.ms/asr-scout-update5) archivo .zip. Este archivo .zip contiene Hola siguientes archivos:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA actualización 4 bits para RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Extraiga los archivos .zip Hola.<br>
3. **Para servidor de hello RX**: copia **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** servidor de RX toohello y extráigalo. Hola extraído carpeta, ejecute **/instalar**.<br>
4. **Para servidor de proceso del servidor de configuración de hello**: copia **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello servidores de configuración y procesos. Haga doble clic en toorun se.<br>
5. **Para el servidor de destino maestro de Windows hello**: Hola tooupdate unificado agente, copia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de destino maestro. Haga doble clic en él toorun lo. Tenga en cuenta que Hola a agente unificada también es aplicable toohello servidor de origen si no se actualiza el origen hasta Update4. Debe instalarlo en el servidor de origen de hello, tal y como se mencionó más adelante en esta lista.<br>
6. **Para servidor de hello vContinuum**: copia **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum server.  Asegúrese de que ha cerrado el Asistente de vContinuum Hola. Haga doble clic en hello archivo toorun.<br>
7. **Para el servidor de destino maestro de Linux de hello**: Hola tooupdate unificado agente, copia **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello servidor de destino maestro y extráigalo. Hola extraído carpeta, ejecute **/instalar**.<br>
8. **Para el servidor de origen de Windows hello**: agente tooinstall actualización 5 de origen no es necesario si el origen ya está en update4. Si es menor que update4, aplicar el agente de Windows update 5 Hola.
Hola tooupdate unificado agente, copia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de origen. Haga doble clic en él toorun lo. <br>
9. **Para el servidor de origen Linux Hola**: tooupdate Hola agente unificado, copie la versión correspondiente UA toohello Linux del servidor de archivos y extráigalo. Hola extraído carpeta, ejecute **/instalar**.  Ejemplo: Servidor de RHEL 6.7 de 64 bits, copie **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello server y extráigalo. Hola extraído carpeta, ejecute **/instalar**.

## <a name="step-4-set-up-replication"></a>Paso 4: Configuración de la replicación
1. Configurar la replicación entre el origen de Hola y de destino VMware sitios.
2. Para obtener instrucciones, use Hola documentación de InMage Scout que se descarga con el producto de Hola. Como alternativa, se puede obtener acceso a Hola documentación como se indica a continuación:

   * [Notas de la versión](https://aka.ms/asr-scout-release-notes)
   * [Matriz de compatibilidad](https://aka.ms/asr-scout-cm)
   * [Guía de usuario](https://aka.ms/asr-scout-user-guide)
   * [Guía de usuario de RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Guía de instalación rápida](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Actualizaciones
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 actualización 5
La actualización 5 de Scout es una actualización acumulativa. Tiene todas las correcciones de Hola de actualización 1 hasta update4 y seguir nuevas correcciones de errores y mejoras.
Correcciones que se agregan de ASR Scout update4 tooupdate5 son componentes de destino y vContinuum tooMaster específico. Si todos los servidores de origen, destino maestro, el servidor de configuración, el servidor de procesos y RX ya están en ASR Scout update4, a continuación, se necesita actualizar tooapply 5 solo en el servidor de destino maestro. 

**Nueva compatibilidad con plataformas**
* SUSE Linux Enterprise Server 11 Service Pack 4 (SP4)

> [!NOTE]
> **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** de SLES 11 SP4 de 64 bits se incluye con el paquete base de Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Descargue el paquete de Scout GA del portal como se mencionó en el [paso 1](#step-1-create-a-vault).
>

**Mejoras y correcciones de errores**

* Aumentar la confiabilidad de la compatibilidad con clústeres de Windows
    * Algún día corregido algunos Hola P2V MSCS discos de clúster se convierten en RAW después de la recuperación
    * Se produce un error en la recuperación de un clúster MSCS de P2V fixed-debido discrepancia de criterio de toodisk
    * Corregido: se produce un error en la operación de agregar discos del clúster de MSCS con falta de coincidencia en el tamaño de disco.
    * Corregido: se produce un error en la comprobación de preparación de la asignación del clúster de MSCS de origen con LUN de RDM en la comprobación del tamaño.
    * Se produce un error en la protección de clúster de nodo único de fixed-debido problema de discrepancia de tooSCSI 
    * Volver a Fixed-proteger Hola P2V Windows servidor de clúster produce un error si no hay discos de clúster de destino. 
    
* Durante la protección de conmutación por recuperación, si MT seleccionado no está en Hola mismo servidor ESXi como de hello protegido máquina de origen (durante la protección al día), entonces vContinuum recoge MT incorrecto de Hola durante la recuperación de la conmutación por recuperación y posteriormente se produce un error en la operación de recuperación.

> [!NOTE]
> 
> * Por encima de correcciones de clúster de P2V es tooonly aplicable esos clúster MSCS físico que recién están protegidas con ASR Scout update5. tooavail Hola clúster correcciones en hello ya protegido clúster MSCS P2V con las actualizaciones más antiguas, deberá toofollow Hola pasos de actualización que se mencionan en la sección de hello 12, actualización protegido tooScout de clúster de MSCS P2V Update5 de [ASR Scout versión Notas de](https://aka.ms/asr-scout-release-notes).
> 
> * Vuelva a proteger de clúster MSCS físico puede volver a usar los discos de destino existentes solo si en el momento de Hola de protección nuevo, hello al mismo conjunto de discos están activos en cada clúster Hola nodos como estaban cuando inicialmente protegidos. Si no es así, a continuación, hay pasos manuales tal y como se mencionó en la sección 12 de [notas de la versión de ASR Scout](https://aka.ms/asr-scout-release-notes) demasiado mover Hola destino lado discos toohello almacén de datos correcta ruta de acceso toore-utilice usarlas durante la protección de nuevo. Si se vuelva a proteger clústeres MSCS hello en el modo de P2V sin seguir los pasos de actualización, a continuación, creará nuevo disco en hello destino ESXi servidor. Necesitará toomanually delete Hola antiguo discos desde el almacén de datos de Hola.
> 
> * Origen cada vez que SLES11 o SLES11 con cualquier servidor de módulo de servicio se reinicia correctamente y, a continuación, uno debe marcar manualmente hello **raíz** pares de replicación para volver a sincronizar en disco como no se notificará en CX UI. Si no lo hace ' marca Hola raíz disco para volver a sincronizar, pueden producirse problemas de integridad (DI) de datos.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1, actualización 4
La actualización 4 de Scout es una actualización acumulativa. Tiene todas las correcciones de Hola de actualización 1 hasta update3 y seguir nuevas correcciones de errores y mejoras.

**Nueva compatibilidad con plataformas**

* Se ha agregado compatibilidad con vCenter/vSphere 6.0, 6.1 y 6.2.
* Se ha agregado compatibilidad con los siguientes sistemas operativos Linux.
  * Red Hat Enterprise Linux (RHEL)7.0, 7.1 y 7.2
  * CentOS 7.0, 7.1 y 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** de RHEL/CentOS 7 de 64 bits se incluye con el paquete base de Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Descargue el paquete de Scout GA del portal como se mencionó en el [paso 1](#step-1-create-a-vault).
>
>

**Mejoras y correcciones de errores**

* Cierre mejorado del control siguiente Linux OSes y clones tooprevent problemas no deseados, volver a sincronizar.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Para Linux, restringir el acceso de carpeta completa permisos en el directorio de instalación de agente unificada son ahora sólo toohello de usuario local.
* En Windows, el problema de agotamiento del tiempo de espera al emitir un marcador común de coherencia distribuida en aplicaciones distribuidas de alta carga, como los clústeres de SQL y SharePoint.
* Se ha añadido una corrección relacionada con el registro en el instalador base de CX.
* Vínculo de descarga de VMware vCLI 6.0 se agrega tooWindows instalador de base de destino maestro.
* Se han agregado más comprobaciones y registros de los cambios de configuración de red durante las simulaciones de conmutación por error y recuperación ante desastres.
* Información de algún día retención no está incluido toohello CX.  
* Para el clúster físico, se producen errores en la operación de cambio de tamaño del volumen mediante el asistente de vContinuum cuando se reduce el volumen.
* Error con el error "Error de firma de disco de toofind Hola" de la protección del clúster al disco de clúster es disco PRDM.
* El servidor de transporte cxps se bloquea por una excepción de valor fuera de intervalo.
* Ahora se puede modificar el tamaño de las columnas Nombre del servidor e IP en la página de instalación de inserción del asistente de vContinuum.
* Mejoras de la API de RX
  * Ofrece los cinco puntos de coherencia comunes disponibles más recientes (solo las etiquetas garantizadas).
  * Proporciona detalles de capacidad y espacio libre para todos los dispositivos protegidos de Hola.
  * Ofrece el estado del controlador de Scout en el servidor de origen.

> [!NOTE]
> * Ahora el paquete base de **InMage_Scout_Standard_8.0.1_GA.zip** ha actualizado el instalador base de CX **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** y el instalador base de destino maestro de Windows **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Para una instalación completamente nueva, use los nuevos bits de GA de CX y del destino maestro de Windows.
> * La actualización 4 se puede aplicar directamente en 8.0.1 GA.
> * servidor de configuración de Hola y RX actualizaciones no se puede revertir después se aplican en el sistema de Hola.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 actualización 3
La actualización 3 incluye siguiente de hello correcciones de errores y mejoras:

* servidor de configuración de Hola y RX producirá un error en el almacén de Site Recovery toohello tooregister cuando están detrás de proxy de Hola.
* Hello número de horas que Hola objetivo de punto de recuperación (RPO) no se cumple no se actualizan en el informe de mantenimiento de Hola.
* servidor de configuración de Hello no está sincronizando con RX cuando los detalles de hardware ESX de Hola o detalles de la red contienen cualquier carácter UTF-8.
* Controladores de dominio de Windows Server 2008 R2 no tooboot después de la recuperación.
* La sincronización sin conexión no funciona según lo esperado.
* Después de la conmutación por error de la máquina virtual (VM), eliminación de pares de replicación se queda bloqueado en hello CX UI durante mucho tiempo y los usuarios no se Hola conmutación por recuperación completa o reanudar la operación.
* En general se han optimizado las operaciones de instantánea que se realizan mediante el trabajo de coherencia de hello toohelp reducir aplicación desconecta al igual que los clientes SQL.
* se ha mejorado el rendimiento de Hola de herramienta de coherencia de hello (VACP.exe) reduciendo su uso de memoria de Hola que se requiere para crear instantáneas en Windows.
* errores del servicio de la instalación de inserción de Hello cuando contraseña hello es mayor que 16 caracteres.
* vContinuum no está comprobando y solicitar nuevas credenciales de vCenter cuando se cambien las credenciales de Hola.
* En Linux, Administrador de caché de destino maestro de hello (cachemgr) no descarga archivos Hola servidor de procesos, que da lugar a la limitación de par de replicación.
* Una vez orden del disco de clúster (MSCS) de hello físico de conmutación por error no Hola igual en todos los nodos de hello, la replicación no está establecida para algunos de los volúmenes de clúster Hola.
  <br/>Tenga en cuenta que ese clúster Hola necesita toobe vuelto a proteger tootake aprovechar esta corrección.  
* Funcionalidad de SMTP no funciona como se esperaba después RX se actualiza desde Scout 7.1 tooScout 8.0.1.
* Se han agregado estadísticas más en el registro de hello por vez Hola reversión operación tootrack Hola se ha tardado toocomplete lo.
* Se ha agregado compatibilidad para los sistemas operativos de Linux en el servidor de origen de hello:
  * Red Hat Enterprise Linux (RHEL) 6 actualización 7
  * CentOS 6 actualización 7
* Hola CX e interfaz de usuario de RX ahora pueden mostrar la notificación de hello para el par de hello, que entra en modo de mapa de bits.
* Hello correcciones de seguridad siguientes se han agregado en RX:

| **Descripción del problema** | **Procedimientos de implementación** |
| --- | --- |
| Omisión de la autorización mediante la alteración de parámetros |Usuarios con acceso restringido toonon aplicables. |
| Falsificación de solicitudes entre sitios |Concepto de símbolo (token) de la página Hola implementada, que se genera aleatoriamente para cada página. <br/>Con esto, verá lo siguiente: <li> Hay solo una única inicio de sesión de instancia para hello mismo usuario.</li><li>Actualice la página no funciona--redirigirá toohello panel.</li> |
| Carga de archivos malintencionados |Extensiones de toocertain de archivos restringidos. Se permiten las siguientes extensiones: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml y zip. |
| Scripting entre sitios persistente |Se han agregado validaciones de entrada. |

> [!NOTE]
> * Todas las actualizaciones de Site Recovery son acumulativas. La actualización 3 tiene todas las correcciones de Hola de Update 1 y 2 de la actualización. La actualización 3 se puede aplicar directamente en 8.0.1 GA.
> * servidor de configuración de Hola y RX actualizaciones no se puede revertir después se aplican en el sistema de Hola.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 actualización 2 (actualización del 3 de diciembre de 2015)
Las revisiones de la actualización 2 incluyen:

* **Servidor de configuración**: corrección para un problema que impedía la característica de medición libre Hola 31 días de trabajo según lo esperado cuando hello servidor de configuración se ha registrado en Site Recovery.
* **Agente unificada**: corrección para un problema en Update 1 dan como resultado actualización hello no se instale en el servidor de destino maestro de hello cuando se actualizó desde too8.0.1 versión 8.0.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 actualización 1
Actualización 1 incluye siguiente Hola correcciones de errores y características nuevas:

* 31 días de protección gratuita por instancia de servidor. Esto le permite la funcionalidad de tootest o configurar una prueba de concepto.
  * Todas las operaciones en el servidor de hello, incluida la conmutación por error y conmutación por recuperación, son gratuitos para hello primera 31 días, desde el tiempo de Hola que un servidor está protegido en primer lugar con Scout de recuperación del sitio.
  * De hello 32nd día en adelante, cada servidor protegido se cobrará a velocidad de instancias estándar de hello para el sitio de propiedad del cliente de tooa de protección de Azure Site Recovery.
  * En cualquier momento, el número de Hola de servidores protegidos que están actualmente se cobra es disponible en la página del panel Hola de almacén de Azure Site Recovery Hola.
* Compatibilidad agregada para la interfaz de la línea de comandos (vCLI) de vSphere 5.5 Update 2.
* Se agregó compatibilidad de sistemas operativos de Linux en el servidor de origen de hello:
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Correcciones de errores Hola de tooaddress problemas siguientes:
  * Se produce un error en el registro del almacén para servidor de configuración de Hola o servidor de recepción.
  * Los volúmenes de clúster no aparecen del modo esperado cuando las máquinas virtuales agrupadas en clústeres se vuelven a proteger al reanudarse.
  * Se produce un error en la conmutación por recuperación al servidor de destino maestro de Hola se hospeda en un servidor de ESXi diferentes desde máquinas virtuales de hello local producción.
  * Permisos de archivo de configuración se cambian al actualizar too8.0.1, lo que afecta a la protección y las operaciones.
  * umbral de resincronización de Hello no se exige según lo esperado, lo que provoca el comportamiento de la replicación de tooinconsistent.
  * configuración de RPO de Hello no aparecen correctamente en la interfaz de servidor de configuración de Hola. valor de los datos sin comprimir de Hello incorrectamente muestra el valor de hello comprimido.
  * operación de eliminación de Hello no se elimina según lo previsto en el Asistente para vContinuum de Hola y la replicación no se ha eliminado de la interfaz de servidor de configuración de Hola.
  * En el Asistente para vContinuum de hello, disco hello es no seleccionado automáticamente al hacer clic en **detalles** en la vista de disco de Hola durante la protección de máquinas virtuales MSCS.
  * Cuando se realiza Hola máquina física a virtual (P2V), requiere servicios de HP, como CIMnotify y CqMgHost, no ha movido toomanual en recuperación de máquina virtual. Esto provoca que se produzca un tiempo de arranque adicional.
  * Se produce un error en la protección de máquinas virtuales de Linux cuando hay más de 26 discos en el servidor de destino maestro Hola.

## <a name="next-steps"></a>Pasos siguientes
Publique las preguntas que existen en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
