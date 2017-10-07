---
title: " Administración de un servidor de configuración en Azure Site Recovery | Microsoft Docs"
description: "Este artículo se describe cómo tooset y administrar un servidor de configuración."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Administración de un servidor de configuración

Servidor de configuración actúa como un coordinador entre servicios de recuperación de sitio de Hola y su infraestructura local. Este artículo describe cómo instalar, configurar y administrar el servidor de configuración de Hola.

## <a name="prerequisites"></a>Requisitos previos
siguiente Hola es Hola mínimos de hardware, software y tooset requerida configuración de red de un servidor de configuración.

> [!NOTE]
> [Planificación de capacidad](site-recovery-capacity-planner.md) es un tooensure paso importante implementar Hola servidor de configuración con una configuración que satisfaga los requisitos de carga. Lea más sobre los [requisitos de tamaño de un servidor de configuración](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Descargar el software de servidor de configuración de Hola
1. Inicie sesión en toohello tooyour portal y examinar Azure almacén de servicios de recuperación.
2. Examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** (en VMware para la & máquinas físicas).

  ![Página Agregar servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Haga clic en hello **+ servidores** botón.
4. En hello **Agregar servidor** página, haga clic en la clave de registro de hello descarga botón toodownload Hola. Necesita esta clave durante la tooregister de instalación del servidor de configuración de hello con servicio de Azure Site Recovery.
5. Haga clic en hello **descarga Hola configuración unificado de Microsoft Azure Site Recovery** versión más reciente Hola de vínculo toodownload de hello servidor de configuración.

  ![Página de descarga](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  La versión más reciente del programa Hola a servidor de configuración puede descargarse directamente desde [página de descarga de Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Instalación y registro de un servidor de configuración desde la interfaz gráfica de usuario
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Instalación y registro de un servidor de configuración desde la línea de comandos

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Ejemplo de uso
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Argumentos de línea de comandos del instalador del servidor de configuración
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Creación de un archivo de credenciales de MySql
El parámetro MySQLCredsFilePath toma como entrada un archivo. Crear archivo de hello mediante Hola siguiente formato y pasarla como parámetro de entrada MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Creación de un archivo de configuración de proxy
El parámetro ProxySettingsFilePath toma un archivo como entrada. Crear archivo de hello mediante Hola siguiente formato y pasarla como parámetro de entrada ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modificación de la configuración de proxy del servidor de configuración
1. Servidor de configuración de inicio de sesión tooyour.
2. Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el.
3. Haga clic en hello **registro del almacén** ficha.
4. Descargue un nuevo archivo de registro del almacén desde el portal de Hola y proporcionarlo como entrada toohello herramienta.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Proporcionar detalles de hello nuevo servidor Proxy y haga clic en hello **registrar** botón.
6. Abra una ventana de comandos de administrador de PowerShell.
7. Ejecute el siguiente comando de Hola
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Si tiene servidores de procesos de escalado horizontal adjunta toothis servidor de configuración, deberá demasiado[corrija la configuración de proxy de hello en todos los servidores de procesos de escalado horizontal de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) en su implementación.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Volver a registrar un servidor de configuración con hello mismo almacén de servicios de recuperación
  1. Servidor de configuración de inicio de sesión tooyour.
  2. Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el escritorio.
  3. Haga clic en hello **registro del almacén** ficha.
  4. Descargue un nuevo archivo de registro desde el portal de Hola y proporcionarlo como entrada toohello herramienta.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Detalles del servidor Proxy de Hola y haga clic en hello **registrar** botón.  
  6. Abra una ventana de comandos de administrador de PowerShell.
  7. Ejecute el siguiente comando de Hola

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Si tiene servidores de procesos de escalado horizontal adjunta toothis servidor de configuración, deberá demasiado[volver a registrar todos los servidores de procesos de escalado horizontal de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) en su implementación.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Registro de un servidor de configuración con un almacén de Recovery Services diferente
1. Servidor de configuración de inicio de sesión tooyour.
2. desde un símbolo del sistema de administración, ejecute el comando de Hola

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Iniciar cspsconfigtool.exe hello mediante acceso directo de hello en el.
4. Haga clic en hello **registro del almacén** ficha.
5. Descargue un nuevo archivo de registro desde el portal de Hola y proporcionarlo como entrada toohello herramienta.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Detalles del servidor Proxy de Hola y haga clic en hello **registrar** botón.  
7. Abra una ventana de comandos de administrador de PowerShell.
8. Ejecute el siguiente comando de Hola
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Retirada de un servidor de configuración
Asegúrese de siguiente de hello antes de empezar a retirar el servidor de configuración.
1. Deshabilite la protección en todas las máquinas virtuales de este servidor de configuración.
2. Desasocie todas las directivas de replicación desde el servidor de configuración de Hola.
3. Eliminar todos los hosts de servidores/vSphere vCenter que están asociado toohello servidor de configuración.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Eliminar Hola servidor de configuración de portal de Azure
1. En el portal de Azure, examinar demasiado**infraestructura del sitio de recuperación** > **servidores de configuración** desde el menú de almacén de Hola.
2. Haga clic en hello servidor de configuración que desea toodecommission.
3. En la página de detalles del servidor de configuración de hello, haga clic en el botón de eliminación de Hola.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Haga clic en **Sí** eliminación de hello tooconfirm del servidor de Hola.

  >[!WARNING]
  Si tienes máquinas virtuales, las directivas de replicación o hosts de servidores/vSphere vCenter asociados con este servidor de configuración, no se puede eliminar el servidor de Hola. Eliminar estas entidades antes de probar el almacén de hello toodelete.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Desinstalar el software de servidor de configuración de Hola y sus dependencias
  > [!TIP]
  Si tiene previsto hello tooreuse servidor de configuración con Azure Site Recovery de nuevo, a continuación, puede omitir toostep 4 directamente

1. Inicie sesión en el servidor de configuración de toohello como administrador.
2. Abra Panel de Control > Programas > Desinstalar programas.
3. Desinstalar programas Hola Hola sigue secuencia:
  * Agente de Microsoft Azure Recovery Services
  * Servicio de movilidad de Microsoft Azure Site Recovery/servidor de destino maestro
  * Proveedor de Microsoft Azure Site Recovery
  * Servidor de configuración/servidor de procesos de Microsoft Azure Site Recovery
  * Dependencias del servidor de configuración de Microsoft Azure Site Recovery
  * MySQL Server 5.5
4. Ejecute hello siguiente comando de y el símbolo del sistema de administración.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Renovación de certificados de Capa de sockets seguros (SSL) del servidor de configuración
Hola servidor de configuración tiene un servidor Web integrado, que organiza las actividades de Hola de hello servicio de movilidad, servidores de procesos, y servidores de destino maestro conectan toohello servidor de configuración. servidor Web del servidor de configuración de Hola usa un tooauthenticate de certificado SSL de sus clientes. Este certificado tiene una fecha de expiración de tres años y se puede renovar en cualquier momento con hello siguiente método:

> [!WARNING]
La expiración del certificado solo se puede realizar en la versión 9.4.XXXX.X o superior. Actualizar todos los componentes de Azure Site Recovery hello (servidor de configuración, el servidor de proceso, servidor de destino maestro, servicio de movilidad) antes de iniciar el flujo de trabajo de hello renovar certificados.

1. En Hola portal de Azure, vaya tooyour almacén > infraestructura de recuperación de sitio > servidor de configuración.
2. Haga clic en el servidor de configuración de hello para la que necesita toorenew Hola certificado SSL para.
3. En el estado del servidor de configuración de hello, puede ver fecha de expiración de Hola de hello certificado SSL.
4. Renovar certificado de hello haciendo clic en hello **renovar certificados** acción como se muestra en hello después de imagen:

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Advertencia de expiración de certificado de Capa de sockets seguros

> [!NOTE]
Hello validez del certificado SSL para todas las instalaciones que se produjeron antes de mayo de 2016 estableció tooone año. se ha iniciado viendo las notificaciones de expiración de certificado aparece en hello portal de Azure.

1. Si certificado SSL del servidor de configuración de Hola va a tooexpire en hello en los próximos dos meses, servicio de hello inicia informar a los usuarios a través de hello portal de Azure & correo electrónico (necesita toobe suscrito tooAzure Site Recovery notificaciones). Empiece a notar un banner de notificación en la página de recursos del almacén de Hola.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Haga clic en hello pancarta tooget obtener más detalles sobre caducidad del certificado Hola.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Si, en lugar del botón **Renovar ahora**, ve un botón **Actualizar ahora**, Esto significa que no hay algunos componentes en el entorno que aún no se han actualizado too9.4.xxxx.x o versiones posteriores.

## <a name="sizing-requirements-for-a-configuration-server"></a>Requisitos de tamaño de un servidor de configuración

| **CPU** | **Memoria** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz) |16 GB |< 300 GB |500 GB o menos |Replicar menos de 100 máquinas. |
| 12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Replicar entre 100 y 150 máquinas. |
| 16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Replicar entre 150 y 200 máquinas. |

  >[!TIP]
  Si la actividad diaria de datos supera los 2 TB, o piensa tooreplicate más de 200 máquinas virtuales, se recomienda toodeploy proceso adicional servidores tooload saldo Hola el tráfico de replicación. Más información sobre cómo servidores toodeploy proceso de escalabilidad horizontal.


## <a name="common-issues"></a>Problemas comunes
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
