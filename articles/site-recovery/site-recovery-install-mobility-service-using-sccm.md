---
title: "instalación del servicio de movilidad para Azure Site Recovery mediante las herramientas de implementación de software aaaAutomate | Documentos de Microsoft"
description: "Este artículo le ayuda a automatizar la instalación de Mobility Service mediante herramientas de implementación de software como System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Automatización de la instalación de Mobility Service mediante herramientas de implementación de software

>[!IMPORTANT]
En este documento se da por supuesto que está utilizando la versión **9.9.4510.1** o superior.

En este artículo se proporciona un ejemplo de cómo puede usar System Center Configuration Manager toodeploy Hola servicio de movilidad de Azure Site Recovery en el centro de datos. Mediante una herramienta de implementación de software como el Administrador de configuración tiene Hola siguientes ventajas:
* Programación de la implementación de la instalación, ya sean instalaciones nuevas o actualizaciones, durante la ventana de mantenimiento planeada para las actualizaciones de software
* Ajuste de escala toohundreds de implementación de servidores al mismo tiempo


> [!NOTE]
> En este artículo usa la actividad de implementación de System Center Configuration Manager 2012 R2 toodemonstrate Hola. También puede automatizar la instalación de Mobility Service mediante [Azure Automation y la configuración de estado deseado](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Requisitos previos
1. Una herramienta de implementación de software, como Configuration Manager, que ya esté implementada en el entorno.
  Cree dos [recopilaciones de dispositivos](https://technet.microsoft.com/library/gg682169.aspx), uno para todos los **servidores Windows**y otro para todos los **servidores Linux**, que desea que tooprotect mediante el uso de Site Recovery.
3. Un servidor de configuración que ya esté registrado con Site Recovery.
4. Un red segura recurso compartido de archivos (recurso compartido de bloque de mensajes de servidor) que se puede acceder al servidor de Configuration Manager de Hola.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Implementación de Mobility Service en equipos que ejecutan Windows
> [!NOTE]
> Este artículo se supone que dirección IP de Hola Hola del servidor de configuración es 192.168.3.121, y ese recurso compartido de red segura archivos hello \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Paso 1: Preparación de la implementación
1. Cree una carpeta en el recurso compartido de red de Hola y asígnele el nombre **MobSvcWindows**.
2. Inicie sesión en el servidor de configuración de tooyour y abra un símbolo del sistema administrativo.
3. Siguiente ejecución Hola comandos toogenerate un archivo de frase de contraseña:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hola copia **MobSvc.passphrase** archivo en hello **MobSvcWindows** carpeta de recurso compartido de red.
5. Examinar toohello repositorio de instalador en el servidor de configuración de hello ejecutando Hola siguiente comando:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Hola copia  **Microsoft ASR\_UA\_*versión*\_Windows\_GA\_*fecha* \_ Release.exe** toohello **MobSvcWindows** carpeta de recurso compartido de red.
7. Copiar el siguiente código de hello y guárdelo como **install.bat** en hello **MobSvcWindows** carpeta.

   > [!NOTE]
   > Reemplace los marcadores de posición de hello [CSIP] en esta secuencia de comandos con valores reales de Hola de dirección IP de Hola de su servidor de configuración.

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a>Paso 2: Creación de un paquete

1. Inicie sesión en la consola de Configuration Manager tooyour.
2. Examinar demasiado**biblioteca de Software** > **administración de aplicaciones** > **paquetes**.
3. Haga clic con el botón derecho en **Paquetes** y seleccione **Crear paquete**.
4. Proporcione valores de versión, descripción, fabricante, idioma y nombre de Hola.
5. Seleccione hello **este paquete contiene archivos de código fuente** casilla de verificación.
6. Haga clic en **examinar**y el recurso compartido de red de hello seleccione donde se almacena el instalador de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. En hello **Elegir tipo de programa Hola que desea toocreate** página, seleccione **programa estándar**y haga clic en **siguiente**.

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. En hello **especifique información acerca de este programa estándar** página, proporcione Hola después de entradas y haga clic en **siguiente**. (hello otras entradas pueden utilizar sus valores predeterminados.)

  | **Nombre de parámetro** | **Valor** |
  |--|--|
  | Nombre | Instalación del Servicio de movilidad de Microsoft Azure (Windows) |
  | Línea de comandos | install.bat |
  | El programa se puede ejecutar | Tanto si un usuario inició sesión como si no |

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. En la página siguiente de hello, seleccionar sistemas operativos de destino de Hola. Mobility Service se puede instalar solo en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2.

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. Asistente de hello toocomplete, haga clic en **siguiente** dos veces.


> [!NOTE]
> script de Hola es compatible con las nuevas instalaciones de agentes de servicio de movilidad y actualiza tooagents que ya están instalados.

### <a name="step-3-deploy-hello-package"></a>Paso 3: Implementar el paquete de Hola
1. En la consola de Configuration Manager de hello, haga clic en el paquete y seleccione **distribuir contenido**.
  ![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Seleccione hello  **[puntos de distribución](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  en toowhich deben copiarse los paquetes de saludo.
3. Asistente de hello completa. paquete de Hello, a continuación, inicia replicar toohello especifica puntos de distribución.
4. Después de realiza la distribución de paquetes de saludo, haga clic en el paquete de Hola y seleccione **implementar**.
  ![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Seleccione la recopilación de dispositivos de Windows Server de Hola que creó en la sección de requisitos previos de hello como recopilación de destino de hello para la implementación.

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. En hello **especificar destino de contenido de hello** página, seleccione la **puntos de distribución**.
7. En hello **toocontrol de configuración de especificar cómo se implementará este software** página, asegúrese de que el objetivo de hello es **requiere**.

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. En hello **especificar la programación de Hola para esta implementación** página, especifique una programación. Para más información, consulte [Programación de paquetes](https://technet.microsoft.com/library/gg682178.aspx).
9. En hello **puntos de distribución** página, configurar las propiedades de hello según las necesidades toohello del centro de datos. A continuación, complete el Asistente de Hola.

> [!TIP]
> tooavoid innecesario que se reinicie, instalación de paquete de programación Hola durante la ventana de mantenimiento mensual o la ventana actualizaciones de software.

Puede supervisar el progreso de la implementación de hello mediante la consola de Configuration Manager Hola. Vaya demasiado**supervisión** > **implementaciones** > *[el nombre del paquete]*.

  ![Implementaciones de toomonitor de opción de captura de pantalla de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Implementación de Mobility Service en equipos que ejecutan Linux
> [!NOTE]
> Este artículo se supone que dirección IP de Hola Hola del servidor de configuración es 192.168.3.121, y ese recurso compartido de red segura archivos hello \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Paso 1: Preparación de la implementación
1. Cree una carpeta en el recurso compartido de red de Hola y asígnele el nombre como **MobSvcLinux**.
2. Inicie sesión en el servidor de configuración de tooyour y abra un símbolo del sistema administrativo.
3. Siguiente ejecución Hola comandos toogenerate un archivo de frase de contraseña:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hola copia **MobSvc.passphrase** archivo en hello **MobSvcLinux** carpeta de recurso compartido de red.
5. Examinar toohello repositorio de instalador en el servidor de configuración de hello mediante la ejecución de comando hello:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Siguiente de hello copia archivos toohello **MobSvcLinux** carpeta de recurso compartido de red:
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. Copiar el siguiente código de hello y guárdelo como **install_linux.sh** en hello **MobSvcLinux** carpeta.
   > [!NOTE]
   > Reemplace los marcadores de posición de hello [CSIP] en esta secuencia de comandos con valores reales de Hola de dirección IP de Hola de su servidor de configuración.

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a>Paso 2: Creación de un paquete

1. Inicie sesión en la consola de Configuration Manager tooyour.
2. Examinar demasiado**biblioteca de Software** > **administración de aplicaciones** > **paquetes**.
3. Haga clic con el botón derecho en **Paquetes** y seleccione **Crear paquete**.
4. Proporcione valores de versión, descripción, fabricante, idioma y nombre de Hola.
5. Seleccione hello **este paquete contiene archivos de código fuente** casilla de verificación.
6. Haga clic en **examinar**y el recurso compartido de red de hello seleccione donde se almacena el instalador de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. En hello **Elegir tipo de programa Hola que desea toocreate** página, seleccione **programa estándar**y haga clic en **siguiente**.

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. En hello **especifique información acerca de este programa estándar** página, proporcione Hola después de entradas y haga clic en **siguiente**. (hello otras entradas pueden utilizar sus valores predeterminados.)

    | **Nombre de parámetro** | **Valor** |
  |--|--|
  | Nombre | Instalación del Servicio de movilidad de Microsoft Azure (Linux) |
  | Línea de comandos | ./install_linux.sh |
  | El programa se puede ejecutar | Tanto si un usuario inició sesión como si no |

  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. En la página siguiente de hello, seleccione **este programa puede ejecutarse en cualquier plataforma**.
  ![Captura de pantalla del Asistente para crear paquetes y programas](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. Asistente de hello toocomplete, haga clic en **siguiente** dos veces.

> [!NOTE]
> script de Hola es compatible con las nuevas instalaciones de agentes de servicio de movilidad y actualiza tooagents que ya están instalados.

### <a name="step-3-deploy-hello-package"></a>Paso 3: Implementar el paquete de Hola
1. En la consola de Configuration Manager de hello, haga clic en el paquete y seleccione **distribuir contenido**.
  ![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Seleccione hello  **[puntos de distribución](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  en toowhich deben copiarse los paquetes de saludo.
3. Asistente de hello completa. paquete de Hello, a continuación, inicia replicar toohello especifica puntos de distribución.
4. Después de realiza la distribución de paquetes de saludo, haga clic en el paquete de Hola y seleccione **implementar**.
  ![Captura de pantalla de la consola de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Seleccione Hola recopilación de dispositivos de servidor Linux que creó en la sección de requisitos previos de hello como recopilación de destino de hello para la implementación.

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. En hello **especificar destino de contenido de hello** página, seleccione la **puntos de distribución**.
7. En hello **toocontrol de configuración de especificar cómo se implementará este software** página, asegúrese de que el objetivo de hello es **requiere**.

  ![Captura de pantalla del Asistente para implementar software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. En hello **especificar la programación de Hola para esta implementación** página, especifique una programación. Para más información, consulte [Programación de paquetes](https://technet.microsoft.com/library/gg682178.aspx).
9. En hello **puntos de distribución** página, configurar las propiedades de hello según las necesidades toohello del centro de datos. A continuación, complete el Asistente de Hola.

Servicio de movilidad se instalará en la recopilación de dispositivos de servidor de Linux, según la programación de toohello configuró Hola.

## <a name="other-methods-tooinstall-mobility-service"></a>Otro tooinstall métodos del servicio de movilidad
Aquí tiene otras opciones para instalar Mobility Service:
* [Instalación manual mediante la GUI](http://aka.ms/mobsvcmanualinstall)
* [Instalación manual mediante la línea de comandos](http://aka.ms/mobsvcmanualinstallcli)
* [Instalación de inserción mediante el servidor de configuración](http://aka.ms/pushinstall)
* [Instalación automatizada mediante Azure Automation y la configuración de estado deseado](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Desinstalación de Mobility Service
Puede crear paquetes de Configuration Manager toouninstall servicio de movilidad. El script siguiente de Hola de uso toodo así:

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a>Pasos siguientes
Ya estás listo demasiado[habilitar la protección](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) para las máquinas virtuales.
