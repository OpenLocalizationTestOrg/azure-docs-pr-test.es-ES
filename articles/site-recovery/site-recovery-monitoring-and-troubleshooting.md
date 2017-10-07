---
title: "aaaMonitor y solucionar problemas de protección para máquinas virtuales y servidores físicos | Documentos de Microsoft"
description: "Azure Site Recovery coordina la replicación de hello, la conmutación por error y la recuperación de máquinas virtuales ubicadas en tooAzure de servidores locales o un centro de datos secundaria. Use este artículo toomonitor y solucionar problemas de protección de sitios de Hyper-V o Virtual Machine Manager."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Protección de supervisión y solución de problemas para las máquinas virtuales y los servidores físicos
Esta supervisión y solución de problemas es útil guía para saber cómo tootrack el estado de replicación y técnicas de solución de problemas para Azure Site Recovery.

## <a name="understand-hello-components"></a>Descripción de los componentes de Hola
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Implementación de sitios de servidores físicos o máquinas virtuales de VMware para su replicación entre una ubicación local y Azure.
tooset la recuperación de la base de datos entre una máquina virtual de VMware local o servidor físico y Azure, deberá tooset servidor de configuración de hello, servidor de destino maestro y componentes de servidor de proceso en su máquina virtual o el servidor. Al habilitar la protección para el servidor de origen de hello, Azure Site Recovery instala la característica de aplicaciones móviles de Hola de servicio de aplicaciones de Microsoft Azure. Después de una interrupción del servicio local y después Hola origen server se produce un error en tooAzure, los clientes necesitan tooset seguridad de un servidor de proceso de Azure y un servidor de destino maestro en servidor de origen local toorebuild Hola de forma local.

![Implementación del sitio de VMware o físico para la replicación entre una ubicación local y Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Implementación del sitio de Virtual Machine Manager para la replicación entre sitios locales
tooset la recuperación de la base de datos entre dos ubicaciones local, también necesita el proveedor de Azure Site Recovery toodownload Hola e instalarlo en el servidor de Virtual Machine Manager de Hola. proveedor de Hello debe tooensure de conectividad de Internet que todas las operaciones de Hola que se desencadenan de hello portal de Azure obtienen operaciones local tooon traducidos.

![Implementación del sitio de Virtual Machine Manager para la replicación entre sitios locales](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Implementación de sitios de Virtual Machine Manager para su replicación entre ubicaciones locales y Azure.
Cuando configure la recuperación de la base de datos entre ubicaciones locales y Azure, también necesita el proveedor de Azure Site Recovery de hello toodownload e instalarlo en el servidor de Virtual Machine Manager de Hola. También deberá hello tooinstall agente de servicios de recuperación de Azure, que debe toobe instalado en cada host de Hyper-V. Haga clic aquí para [obtener más información](site-recovery-hyper-v-azure-architecture.md).

![Implementación de sitios de Virtual Machine Manager para su replicación entre ubicaciones locales y Azure.](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Implementación de sitios de Hyper-V para la replicación entre ubicaciones locales y Azure
Este proceso es similar tooVirtual Machine Manager implementación. Hola la única diferencia es que el proveedor de Azure Site Recovery hello y agente de servicios de recuperación de Azure se instalan en el propio host de Hyper-V Hola. [Más información](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Supervisión de las operaciones de configuración, protección y recuperación
Cada operación en Azure Site Recovery se auditan y realiza un seguimiento en hello **trabajos** ficha. Para cualquier configuración, protección o error de recuperación, vaya toohello **trabajos** ficha y busque errores.

![filtro de error de Hello en la ficha trabajos de Hola](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Si encuentra errores en hello **trabajos** pestaña, haga clic en trabajo hello y haga clic en **detalles del ERROR** para ese trabajo.

![botón de detalles del ERROR de Hola](media/site-recovery-monitoring-and-troubleshooting/image4.png)

Detalles del error Hola le ayudará a identificar una causa posible y la recomendación para el problema de Hola.

![Cuadro de diálogo que muestra los detalles del error para un trabajo específico](media/site-recovery-monitoring-and-troubleshooting/image5.png)

En el ejemplo anterior de hello, otra operación está en curso parece toobe provocando toofail de configuración de protección de Hola. Resolver el problema Hola según la recomendación de hello y, a continuación, haga clic en **RESART** tooinitiate Hola intentarlo.

![botón de reinicio de Hello en la ficha trabajos de Hola](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Hola **reiniciar** opción no está disponible para todas las operaciones. Si una operación no tiene hello **reiniciar** opción, vuelva atrás toohello objeto y rehacer la operación de Hola de nuevo. Puede cancelar cualquier trabajo que está en curso utilizando hello **cancelar** botón.

![botón de cancelación de Hola](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Supervisión del estado de mantenimiento de la replicación de las máquinas virtuales
Puedes usar proveedores de Azure Site Recovery de monitor de hello Azure tooremotely portal para cada una de las entidades de hello protegido. Haga clic en **ELEMENTOS PROTEGIDOS** y, a continuación, en **NUBES VMM** o **GRUPOS DE PROTECCIÓN**. Hola **NUBES de VMM** ficha solo está disponible para las implementaciones que se basan en el Administrador de máquina Virtual. Para otros escenarios, las entidades de hello protegido están bajo hello **grupos de protección** ficha.

![Opciones de nubes de VMM y grupos de protección de Hola](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Haga clic en una entidad protegida en hello respectivos en la nube o protección grupo toosee que todas las operaciones disponibles se muestran en el panel inferior de Hola.

![Opciones disponibles para una entidad protegida seleccionada](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Como se muestra en la captura de pantalla anterior de hello, el estado de máquina virtual de hello es **crítico**. Puede hacer clic en hello **detalles del ERROR** botón después de un error de hello inferior toosee Hola. En función de hello **posibles causas** y **recomendación**, resuelva el problema de Hola.

![botón de detalles del Error de Hola](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Errores y las recomendaciones de cuadro de diálogo Detalles del Error de Hola](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Si las operaciones activas en curso o error, visite toohello **trabajos** vista como se mencionó error de hello tooview anterior para un trabajo específico.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Solucionar problemas de Hyper-V locales
Conectar la consola de administrador de Hyper-V toohello local, máquina virtual de hello seleccione y ver el estado de replicación de Hola.

![Estado de replicación de tooview opción en la consola de administrador de hello Hyper-V](media/site-recovery-monitoring-and-troubleshooting/image12.png)

En este caso, **Mantenimiento de la replicación** es **Crítico**. Haga clic en la máquina virtual de hello y, a continuación, haga clic en **replicación** > **ver mantenimiento de replicación** detalles de hello toosee.

![Estado de mantenimiento de la replicación de una máquina virtual concreta](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Si se pausó la replicación de máquina virtual de hello, haga clic en la máquina virtual de hello y, a continuación, haga clic en **replicación** > **Reanudar replicación**.

![Opción de replicación en la consola del Administrador de Hyper-V de hello tooresume](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Si una máquina virtual se migra un nuevo host de Hyper-V que está dentro de clúster de Hola o en un equipo independiente y se ha configurado el host de Hyper-V de Hola a través de Azure Site Recovery, replicación de máquina virtual de hello no verse afectada. Asegúrese de ese nuevo host de Hyper-V Hola cumple todos los requisitos previos de Hola y se configura mediante el uso de Azure Site Recovery.

### <a name="event-log"></a>Registro de eventos
| Orígenes de eventos | Detalles |
| --- |:--- |
| **Registros de aplicaciones y servicios/Microsoft/VirtualMachineManager/Server/Admin** (Servidor Virtual Machine Manager) |Proporciona registro útil tootroubleshoot muchos problemas de Virtual Machine Manager diferente. |
| **Registros de aplicaciones y servicios/MicrosoftAzureRecoveryServices/Replication** (Host de Hyper-V) |Proporciona registro útil tootroubleshoot muchos problemas de agente de servicios de recuperación de Microsoft Azure. <br/> ![Ubicación de replicación del origen de eventos para el host de Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Registros de aplicaciones y servicios/Microsoft/Azure Site Recovery/Provider/Operational** (Host de Hyper-V) |Proporciona registro útil tootroubleshoot muchos problemas de servicio de Microsoft Azure Site Recovery. <br/> ![Ubicación del origen de eventos operativo para el host de Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Registros de aplicaciones y servicios/Microsoft/Windows/Hyper-V-VMMS/Admin** (Host de Hyper-V) |Proporciona registro útil tootroubleshoot muchos problemas de administración de máquinas virtuales de Hyper-V. <br/> ![Ubicación del origen de eventos de Virtual Machine Manager para el host de Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Opciones de registro de replicación de Hyper-V
Se registran todos los eventos que pertenecen replicación tooHyper-V en hello Hyper-V-VMMS\\inicio de sesión administrador ubicado en registros de aplicaciones y servicios\\Microsoft\\Windows. Además, puede habilitar un registro analítico para el servicio de administración de máquinas virtuales de Hyper-V de Hola. tooenable este registro, asegúrese primero de Hola analítico y depuración registros pueden verse en el Visor de eventos de Hola. Abra el Visor de eventos y, a continuación, haga clic en **Ver** > **Mostrar registros analíticos y de depuración**.

![Hola opción Mostrar registros analíticos y de depuración](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Puede verse un registro analítico en **Hyper-V-VMMS**.

![Hola analítico de registro en el árbol del Visor de eventos de Hola](media/site-recovery-monitoring-and-troubleshooting/image15.png)

Hola **acciones** panel, haga clic en **Habilitar registro**. Una vez habilitado, aparece en **Monitor de rendimiento** como **sesión de seguimiento de eventos** situada en **Conjuntos de recopiladores de datos**.

![Sesiones de seguimiento de eventos en el árbol de Monitor de rendimiento de Hola](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview Hola información recopilada, detenga primero la sesión de seguimiento de hello deshabilitando el registro de hello. Guardar registro de hello y vuelva a abrirlo en el Visor de eventos o usar otra herramientas tooconvert como desee.

## <a name="reach-out-for-microsoft-support"></a>Contacto con el soporte técnico de Microsoft
### <a name="log-collection"></a>Recopilación de registros
Para la protección del sitio de Virtual Machine Manager, consulte demasiado[recopilación de registros de Azure Site Recovery mediante la herramienta de la plataforma de diagnóstico de soporte técnico (SDP)](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect Hola necesario registros.

Para la protección del sitio de Hyper-V, descargue el [herramienta](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) y lo ejecuta en hello Hyper-V host toocollect Hola registros.

Para escenarios de servidores físicos/VMware, consulte demasiado[recopilación de registros de Azure Site Recovery para VMware y la protección de sitio físico](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect Hola necesario registros.

herramienta de Hello recopila registros de hello localmente en una subcarpeta con nombre aleatorio bajo % LocalAppData%\ElevatedDiagnostics.

![Pasos de ejemplo que se muestran en la protección del sitio de Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Abrir una incidencia de soporte técnico
tooraise una incidencia de soporte técnico para Azure Site Recovery, acérquese tooAzure soporte técnico mediante la dirección URL en <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Artículos de Knowledge Base
* [Cómo toopreserve letra de unidad de Hola para protege máquinas virtuales que se conmuten por error o se migren tooAzure](http://support.microsoft.com/kb/3031135)
* [¿Cómo toomanage local uso de ancho de banda de red de tooAzure protección](https://support.microsoft.com/kb/3056159)
* [Error de Azure Site Recovery: "recurso de clúster de hello no se encontró" cuando intente tooenable protección para una máquina virtual](http://support.microsoft.com/kb/3010979)
* [Understand &amp; Troubleshoot Hyper-V Replica Guide](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx) (Guía de descripción y solución de problemas de Réplica de Hyper-V)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Errores comunes de Azure Site Recovery y sus soluciones
A continuación, se muestran los errores comunes y sus soluciones. Cada uno de los errores se documenta en una página Wiki independiente.

### <a name="general"></a>General
* <span style="color:green;">NUEVO</span>[Trabajos que presentan el error "Operación en curso". Error 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">NUEVA</span> [trabajos con errores con el error "Servidor no está conectado toohello Internet". Error 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Configuración
* [no se puede registrar el servidor de Virtual Machine Manager de Hello debido a error interno de tooan. Consulte toohello vista de trabajos en el portal de Site Recovery de Hola para obtener más detalles sobre el error de Hola. Ejecute el programa de instalación nuevo servidor de hello tooregister.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Una conexión no puede ser el almacén del Administrador de recuperación de Hyper-V toohello establecida. Compruebe la configuración de proxy de Hola o inténtelo de nuevo más tarde.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Configuración
* [No se puede toocreate grupo de protección: se produjo un error al recuperar la lista de Hola de servidores.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Clúster de hosts de Hyper-V contiene al menos un adaptador de red estático o no de los adaptadores conectados son toouse configurado DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager no tiene permisos toocomplete una acción.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [No se puede seleccionar la cuenta de almacenamiento de hello dentro de suscripción de hello al configurar la protección.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Protección
* <span style="color:green;">NUEVA</span> [Habilitar protección presenta el error "No se pudo configurar la protección de máquina virtual de Hola". Error 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">NUEVA</span> [Habilitar protección presenta el error "No se pudo habilitar la protección de la máquina virtual de hello." Error 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">NUEVA</span> [error de migración en vivo 23848 - máquina virtual de hello va toobe movido con el tipo Live. Esto podría afectar el estado de protección de recuperación de Hola de máquina virtual de Hola.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Error al habilitar la protección, ya que el agente no está instalado en el equipo host.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [No se encuentra ningún host adecuado para la máquina virtual de réplica de hello - debido a los recursos de proceso toolow.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [No se encuentra ningún host adecuado para la máquina virtual de réplica de hello - debido conectados a la red lógica toono.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [No se puede conectar el equipo de host de réplica de toohello - no se pudo establecer conexión.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Recuperación
* Virtual Machine Manager no se puede completar la operación del host hello:
  * [Conmutar por error toohello selecciona el punto de recuperación para la máquina virtual: error de denegación de acceso General.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Toofail error de Hyper-V sobre toohello seleccionado punto de recuperación de máquina virtual: operación anulada.  Pruebe con un punto de recuperación más reciente. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * No puede realizarse una conexión con el servidor de hello establecida (0x00002EFD).
    * [Hyper-V no pudo tooenable la replicación inversa para la máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-V no pudo tooenable la replicación de máquina virtual de máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [No se pudo confirmar la conmutación por error de la máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [plan de recuperación de Hello contiene máquinas virtuales que no están listos para la conmutación por error planeada.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [máquina virtual de Hello no está lista para conmutación por error planeada.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [La máquina virtual no se está ejecutando y no está apagada.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Se produjo una operación fuera de banda en una máquina virtual y no se realizó la conmutación por error.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Probar conmutación por error
  * [No se pudo iniciar la conmutación por error ya que la conmutación por error de prueba está en curso.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NUEVA</span> conmutación por error agota el tiempo con 'PreFailoverWorkflow tarea WaitForScriptExecutionTaskTimeout' debido a valores de configuración de toohello en hello grupo de seguridad de red asociado a Hola Máquina Virtual o una máquina de hello subred toowhich Hola al que pertenece. Consulte demasiado['PreFailoverWorkflow tarea WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) para obtener más información.

### <a name="configuration-server-process-server-master-target"></a>Servidor de configuración, servidor de procesos y destino principal
* [se produce un error en el host ESXi de Hello en qué Hola PS/CS se hospeda como una máquina virtual con una pantalla de color púrpura de muerte.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Solución de problemas del escritorio remoto después de la conmutación por error
* Muchos clientes que han enfrentado problemas tooconnect toohello conmutado por máquina virtual de Azure. [Hola de uso tooRDP de documento de solución de problemas en la máquina virtual de hello](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Adición de una dirección IP pública en una máquina virtual de administrador de recursos
Si hello **conectar** botón en el portal de hello está atenuado y no está conectado tooAzure a través de una conexión VPN de sitio a sitio o de Express Route, necesita toocreate y asignar una dirección IP pública de la máquina virtual para poder usar remoto Shell de escritorio o compartido. A continuación, puede agregar una dirección IP pública en la interfaz de red de Hola de máquina virtual de Hola.  

![Agregar una dirección IP pública en la interfaz de red Hola conmutado por máquina virtual](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
