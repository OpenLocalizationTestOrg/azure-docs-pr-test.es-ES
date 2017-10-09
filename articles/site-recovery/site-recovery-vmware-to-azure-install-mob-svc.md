---
title: "aaaInstall Mobility Service (VMware o tooAzure físico) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Hola tooprotect de agente del servicio de movilidad sus equipos locales."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Instalar servicio de movilidad (VMware o tooAzure físico)
Servicio de movilidad de Azure Site Recovery captura escrituras de datos en un equipo y, a continuación, reenvía el servidor de procesos de toohello. Implementar el servicio de movilidad tooevery equipo (VM de VMware o servidor físico) que desea tooreplicate tooAzure. Puede implementar servidores de toohello de servicio de movilidad que desea tooprotect usando Hola siguientes métodos:


* [Instalación de Mobility Service mediante herramientas de implementación herramientas de implementación de software como System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Instalación de Mobility Service mediante Azure Automation y la configuración de estado deseado (DSC de Automatización)](site-recovery-automate-mobility-service-install.md)
* [Instalar manualmente el servicio de movilidad mediante interfaz gráfica de usuario de hello (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Instalación manual de Mobility Service mediante la línea de comandos](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Instalación de Mobility Service mediante la instalación de inserción de Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> A partir de la versión 9.7.0.0, en máquinas virtuales (VM) de Windows hello Mobility Service instalador también instala hello más reciente disponible [agente de máquina virtual de Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Cuando se produce un error en un equipo a través de tooAzure, equipo de hello cumple instalación del agente Hola requisitos previo para utilizar cualquier extensión de máquina virtual.

## <a name="prerequisites"></a>Requisitos previos
Complete estos pasos de requisitos previos antes de instalar manualmente Mobility Service en el servidor:
1. Inicie sesión en el servidor de configuración de tooyour y, a continuación, abra una ventana del símbolo del sistema como administrador.
2. Cambie la carpeta bin de hello directorio toohello y, a continuación, cree un archivo de frase de contraseña:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Almacene el archivo de frase de contraseña de hello en una ubicación segura. Utilice el archivo hello durante la instalación del servicio de movilidad de Hola.
4. Instaladores de servicio de movilidad para todos los sistemas operativos compatibles están en la carpeta %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository de Hola.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Instalador de Mobility Service para la asignación de sistemas operativos

| Nombre de plantilla de archivo de instalador| Sistema operativo |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 bits) </br> Windows Server 2012 (64 bits) </br> Windows Server 2012 R2 (64 bits) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (solo 64 bits) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (solo 64 bits) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (solo 64-bit) </br> CentOS 7.0, 7.1, 7.2 (solo 64-bit)</br> CentOs 7.3 (solo en la migración) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (solo 64 bits)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (solo 64-bit)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (solo 64 bits)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (solo 64-bit)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Instalar manualmente el servicio de movilidad mediante GUI Hola

>[!IMPORTANT]
> Si usas un **servidor de configuración** tooreplicate **máquinas virtuales de IaaS de Azure** desde una tooanother de suscripción o la región de Azure, a continuación, **usar Hola de instalación basada en línea de comandos**  (método)

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Instalación manual de Mobility Service mediante la línea de comandos

### <a name="command-line-installation-on-a-windows-computer"></a>Instalación de la línea de comandos en un equipo Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Instalación de la línea de comandos en un equipo Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Instalación de Mobility Service mediante la instalación de inserción de Azure Site Recovery
toodo una instalación de inserción del servicio de movilidad mediante el uso de Site Recovery, todos los equipos de destino deben cumplir Hola siguiendo los requisitos previos.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Después de instalar el servicio de movilidad, Hola portal de Azure, seleccione hello **replicar** toostart botón proteger estas máquinas virtuales.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Desinstalación de Mobility Service en un equipo de Windows Server
Utilice uno de hello siguiendo métodos toouninstall Mobility Service en un equipo con Windows Server.

### <a name="uninstall-by-using-hello-gui"></a>Desinstalar mediante la GUI de Hola
1. En el Panel de Control, seleccione **Programas**.
2. Seleccione **Microsoft Azure Site Recovery Mobility Service/Servidor de destino maestro** y, a continuación, haga clic en**Desinstalar**.

### <a name="uninstall-at-a-command-prompt"></a>Desinstalación en un símbolo del sistema
1. Abra una ventana de símbolo del sistema como administrador.
2. toouninstall servicio de movilidad, ejecute el siguiente comando de hello:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Desinstalación de Mobility Service en equipos Linux
1. En el servidor Linux, inicie sesión como un usuario **raíz**.
2. En un terminal, vaya demasiado/usuario/local/ASR.
3. toouninstall servicio de movilidad, ejecute el siguiente comando de hello:

```
uninstall.sh -Y
```
