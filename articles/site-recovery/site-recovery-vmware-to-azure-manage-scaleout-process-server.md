---
title: " Administración de un servidor de procesos de escalado horizontal en Azure Site Recovery | Microsoft Docs"
description: "Este artículo se describe cómo tooset una copia de seguridad y administrar un servidor de procesos de escalabilidad horizontal en Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Administración de un servidor de procesos de escalado horizontal

Servidor de procesos de escalado horizontal actúa como un coordinador para transferir datos entre los servicios de recuperación de sitio de Hola y la infraestructura local. En este artículo se describe cómo instalar, configurar y administrar un servidor de procesos de escalado horizontal.

## <a name="prerequisites"></a>Requisitos previos
siguiente Hola es Hola recomienda hardware, software y red requerida configuración tooset de un servidor de proceso de escalabilidad horizontal.

> [!NOTE]
> [Planificación de capacidad](site-recovery-capacity-planner.md) es un tooensure paso importante implementar Hola servidor de procesos de escalado horizontal con una configuración que satisfaga los requisitos de carga. Lea más sobre las [características de escalado de un servidor de procesos de escalado horizontal](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Descargar el software de servidor de procesos de escalado horizontal de Hola
1. Inicie sesión en toohello tooyour portal y examinar Azure almacén de servicios de recuperación.
2. Examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** (en VMware para la & máquinas físicas).
3. Seleccione el toodrill del servidor de configuración hacia abajo en la página de detalles del servidor de configuración de Hola.
4. Haga clic en hello **+ servidor de procesos** botón.
5. Hola **servidor de proceso de agregar** página, seleccione **servidor de proceso de implementar una implementación escalada local** opción de hello **elija dónde desea toodeploy el servidor de procesos** lista desplegable.

  ![Página Agregar servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Haga clic en hello **descarga Hola configuración unificado de Microsoft Azure Site Recovery** versión más reciente Hola de vínculo toodownload de instalación del servidor de procesos de hello escalado horizontal.

  > [!WARNING]
  Hello versión el escalado horizontal del servidor de procesos debe ser igual tooor anterior a la versión del servidor de configuración de hello ejecutando en su entorno. Una compatibilidad de versiones de manera sencilla tooensure es toouse Hola mismos bits de instalador que recientemente usado tooinstall o actualizar el servidor de configuración.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Instalación y registro de un servidor de procesos de escalado horizontal desde la interfaz gráfica de usuario
Si tiene tooscale horizontalmente la implementación más allá de 200 máquinas de origen o a diario total renovación tasa de más de 2 TB, necesita el volumen de tráfico de proceso adicionales servidores toohandle Hola.

Comprobar hello [cambiar el tamaño de las recomendaciones para los servidores de proceso](#size-recommendations-for-the-process-server)y, a continuación, siga estos tooset instrucciones servidor de procesos de Hola. Después de configurar el servidor de hello, migrar toouse de máquinas de origen se.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Instalación y registro de un servidor de procesos de escalado horizontal mediante la línea de comandos

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Ejemplo de uso
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Argumentos de línea de comandos del instalador del servidor de procesos de escalado horizontal
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Creación de un archivo de configuración de proxy
El parámetro ProxySettingsFilePath toma un archivo como entrada. Crear archivo con hello siguiente formato y pasarla como parámetro de entrada ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modificación de la configuración de proxy del servidor de procesos de escalado horizontal
1. Inicie sesión en su servidor de procesos de escalado horizontal.
2. Abra una ventana de comandos de administrador de PowerShell.
3. Ejecute el siguiente comando de Hola
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. A continuación busque el directorio de toohello **%PROGRAMDATA%\ASR\Agent** y ejecución Hola siguiente comando
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Registro repetido de un servidor de procesos de escalado horizontal
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Después abra un símbolo del sistema de administrador.
* Busque el directorio de toohello **%PROGRAMDATA%\ASR\Agent** y ejecute el comando de Hola

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Actualización de un servidor de procesos de escalado horizontal
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Retirada de un servidor de procesos de escalado horizontal
1. Asegúrese de que:
  - Muestra el estado de conexión del servidor de configuración como **conectado** Hola portal de Azure
  - Servidor de procesos es todavía puede toocommunicate con el servidor de configuración de Hola.
2. Inicie sesión en el servidor de procesos de toohello como administrador
3. Abra Panel de Control > Programas > Desinstalar programas.
4. Desinstalar programas hello secuencia Hola dado que sigue:
  * Servidor de configuración/servidor de procesos de Microsoft Azure Site Recovery
  * Dependencias del servidor de configuración de Microsoft Azure Site Recovery
  * Agente de Microsoft Azure Recovery Services

Puede tardar minutos arriba too15 tooreflect de eliminación del servidor de procesos de Hola Hola portal de Azure.

  > [!NOTE]
  Si el servidor de procesos de hello es no se puede toocommunicate con servidor de configuración de hello (estado de conexión en el portal se ha desconectado), deberá toofollow Hola siguientes pasos toopurge de hello servidor de configuración.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Anulación del registro de un servidor de procesos de escalado horizontal desconectado de un servidor de configuración

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Requisitos de tamaño para un servidor de procesos de escalado horizontal

| **Servidores de procesos adicionales** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas** |
| --- | --- | --- | --- |
|4 vCPU (2 sockets * 2 núcleos @ 2,5 GHz), 8 GB de memoria |< 300 GB |250 GB o menos |Replicar 85 máquinas o menos. |
|8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz), 12 GB de memoria |600 GB |250 GB too1 TB |Replicar entre 85 y 150 máquinas. |
|12 vCPU (2 sockets * 6 núcleos @ 2,5 GHz) 24 GB de memoria |1 TB |1 TB too2 TB |Replicar entre 150 y 225 máquinas. |
