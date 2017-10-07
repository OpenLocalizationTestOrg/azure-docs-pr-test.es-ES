---
title: "aaaAzure solucionar problemas de recuperación del sitio de VMware tooAzure | Documentos de Microsoft"
description: "Solución de problemas y errores al replicar máquinas virtuales de Azure"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Solución de problemas de instalación de inserción del servicio de movilidad

Este artículo detallan los problemas comunes de hello hay que hacer frente al tratar de hello tooinstall servicio de movilidad en el servidor de toosource para habilitar la protección.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Código de error 95107) No se pudo habilitar la protección.
**Código de error** | **Causas posibles:** | **Recomendaciones específicas para el error**
--- | --- | ---
95107 </br>***Mensaje:*** error en la instalación de inserción de la máquina de origen de toohello de servicio de movilidad de hello con código de error ***EP0858***. <br> Ya sea que las credenciales de hello proporcionaron servicio de movilidad de tooinstall es incorrecta o cuenta de usuario de hello tiene privilegios suficientes | Las credenciales de usuario proporcionan tooinstall servicio de movilidad en la máquina de origen no es correcto | Asegúrese de credenciales de usuario de hello proporcionado para la máquina de origen de hello en el servidor de configuración son correctas. <br> las credenciales de usuario de tooadd/editar: servidor vaya tooconfiguration > Cspsconfigtool icono > Administrar cuenta. </br> Además, compruebe a continuación de requisitos previos se toosuccessfully comprobado completa una instalación de inserción.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Código de error 95015) No se pudo habilitar la protección.
**Código de error** | **Causas posibles:** | **Recomendaciones específicas para el error**
--- | --- | ---
95105 </br>***Mensaje:*** error en la instalación de inserción de la máquina de origen de toohello de servicio de movilidad de hello con código de error ***EP0856***. <br> "Compartir impresoras y archivos" no permitido en la máquina de origen de Hola o hay problemas de conectividad de red entre el servidor de procesos de Hola y máquina de origen de Hola| Compartir archivos e impresoras no está habilitado | Permitir "Compartir impresoras y archivos" en la máquina de origen Hola Hola Firewall de Windows, vaya toohello la máquina de origen > en el Firewall de Windows > "Permitir que una aplicación o una característica a través del Firewall" > seleccione "Compartir archivos e impresoras para todos los perfiles". </br> Además, compruebe a continuación de requisitos previos se toosuccessfully comprobado completa una instalación de inserción.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Código de error 95117) No se pudo habilitar la protección.
**Código de error** | **Causas posibles:** | **Recomendaciones específicas para el error**
--- | --- | ---
95117 </br>***Mensaje:*** error en la instalación de inserción de la máquina de origen de toohello de servicio de movilidad de hello con código de error ***EP0865***. <br> No se está ejecutando la máquina de origen de Hola o hay problemas de conectividad de red entre el servidor de procesos de Hola y máquina de origen de Hola | Conectividad de red entre el servidor de procesos y el servidor de origen | Compruebe la conectividad entre el servidor de procesos y el servidor de origen. </br> Además, compruebe a continuación de requisitos previos se toosuccessfully comprobado completa una instalación de inserción.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Código de error 95103) No se pudo habilitar la protección.
**Código de error** | **Causas posibles:** | **Recomendaciones específicas para el error**
--- | --- | ---
95103 </br>***Mensaje:*** error en la instalación de inserción de la máquina de origen de toohello de servicio de movilidad de hello con código de error ***EP0854***. <br> "Windows Management Instrumentation (WMI)" no se permite en la máquina de origen de Hola o hay problemas de conectividad de red entre el servidor de procesos de Hola y máquina de origen de Hola| Windows Management Instrumentation (WMI) se bloquea en hello Firewall de Windows | Permitir que Windows Management Instrumentation (WMI) en Firewall de Windows hello. En la configuración de Firewall de Windows > "Permitir una aplicación o una característica a través de Firewall" > seleccione VMI para todos los perfiles. </br> Además, compruebe a continuación de requisitos previos se toosuccessfully comprobado completa una instalación de inserción.

## <a name="check-push-install-logs-for-errors"></a>Busque errores en los registros de la instalación de inserción

En el servidor de proceso de configuración/hello, navegue toofile 'PushinstallService' se encuentra en <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand Hola origen problema Hola y el uso por debajo de problema de hello tooresolve de pasos de solución de problemas.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Requisitos previos de instalación de inserción para Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Asegúrese de que "Compartir archivos e impresoras" esté habilitado
Permitir "Compartir impresoras y archivos" y "Instrumental de administración de Windows" en la máquina de origen Hola Hola Firewall de Windows </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Si la máquina de origen está unida a un dominio: </br>
Configure el firewall mediante la Consola de administración de directivas de grupo (GPMC).
1. Dominio de inicio de sesión tooActive directory del equipo como administrador y abra la consola de administración de directivas de grupo (GPMC. MSC, ejecute desde un inicio > Ejecutar).</br>
3. Si no está instalada GPMC, siga el vínculo de hello demasiado[Hola Install GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. En el árbol de la consola GPMC hello, haga doble clic en objetos de directiva de grupo en los dominios y bosques de Hola y navegue demasiado "Directiva predeterminada de dominio". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Haga clic con el botón derecho en "Directiva de dominio predeterminada" > Editar > se abrirá una ventana nueva del "Editor de administración de directivas de grupo". </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Hola Editor de administración de directivas de grupo vaya tooComputer configuración > directivas > plantillas administrativas > red > conexiones de red > Firewall de Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Habilitar Hola después de la configuración de perfil de dominio y perfil estándar </br>
a) Haga doble clic en la excepción "Firewall de Windows: permitir excepción Compartir archivos e impresoras entrantes". Seleccione Habilitado y haga clic en Aceptar. </br>
b) Haga doble clic en la excepción "Firewall de Windows: permitir excepción de administración remota entrante". Seleccione Habilitado y haga clic en Aceptar. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Si la máquina de origen no está unida a un dominio ni es parte de un grupo de trabajo </br>
Configure el firewall en la máquina remota (para el grupo de trabajo):
1. Vaya toohello máquina de origen,</br>
2. En la configuración de Firewall de Windows > "Permitir una aplicación o una característica a través de Firewall" > seleccione "Compartir archivos e impresoras para todos los perfiles". </br>
3. En la configuración de Firewall de Windows > "Permitir una aplicación o una característica a través de Firewall" > seleccione VMI para todos los perfiles. </br>

#### <a name="disable-remote-user-account-control-uac"></a>Deshabilitación del Control de cuentas de usuario (UAC)
Deshabilitar UAC mediante el servicio de movilidad de hello toopush clave de registro.
1. Haga clic en Inicio > Ejecutar > escriba regedit > Entrar
2. Busque y, a continuación, haga clic en siguiente subclave del registro de hello: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Si Hola entrada LocalAccountTokenFilterPolicy del registro no existe, siga estos pasos:
4. En el menú de edición de hello > Nuevo > haga clic en valor DWORD.
5. Escriba LocalAccountTokenFilterPolicy y presione Entrar.
6. Haga clic con el botón derecho en LocalAccountTokenFilterPolicy y, luego, haga clic en Modificar.
7. En el cuadro de información del valor de hello, escriba 1 y, a continuación, haga clic en Aceptar.
8. Salga del Editor del Registro.


## <a name="push-install-pre-requisites-for-linux"></a>Requisitos previos de instalación de inserción para Linux:

1. Cree un usuario raíz Hola servidor de origen Linux. (Use esta cuenta solo para la instalación de inserción de Hola y actualizaciones)</br>
2. Compruebe el archivo/etc/hosts hello en origen Hola Linux servidor tiene las entradas que se asignan direcciones de tooIP de nombre de host local de hello asociadas con todos los adaptadores de red. </br>
3. Asegúrese de hello más reciente openssh, el servidor de openssh y openssl los paquetes están instalados en el servidor de origen Linux. </br>
Compruebe si el puerto SSH 22 está habilitado y en ejecución. </br>
4. Compruebe si las entradas obsoletas de agentes ya están presentes en el servidor de origen de hello, desinstalar a agentes anteriores de Hola y reinicie el servidor de hello, vuelva a instalar a agente. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Habilitar la autenticación de subsistema y la contraseña SFTP en archivo sshd_config de hello
1. En el servidor de origen, inicie sesión como raíz. </br>
2. Hola archivo /etc/ssh/sshd_config de archivos,</br> Busque la línea de Hola que comienza con PasswordAuthentication. </br>
3. d.   Elimine línea hello y cambie el valor de Hola de "no" demasiado "Sí". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Busque Hola línea que comienza con "Subsistema" y elimine la línea hello. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Guarde los cambios de Hola y reinicie el servicio de hello sshd. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Comprobaciones de la instalación de inserción en el servidor de configuración o procesos
#### <a name="validate-credentials-for-discovery-and-installation"></a>Validación de las credenciales para la detección y la instalación

1. En el servidor de configuración, inicie Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Asegúrese de que cuenta de hello usada para la protección tiene derechos de administrador en la máquina de origen Hola. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Comprobación de la conectividad entre el servidor de procesos y el servidor de origen
1. Asegúrese de que el servidor de procesos tiene conexión a Internet.
2. Use wbemtest.exe para comprobar la conexión de WMI. </br>
En el servidor de procesos de Hola y haga clic en Inicio > Ejecutar > wbemtest.exe > se abrirá la ventana de herramienta de comprobación del Instrumental de administración de Windows como se muestra.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Haga clic en Conectar > escriba la dirección IP del servidor de origen de Hola Hola Namespace proporcionados por el nombre de usuario y contraseña (si la máquina de origen está unido al dominio, proporcionar nombre de dominio de hello junto con el nombre de usuario como "ombreDeUsuario". Si la máquina de origen está en el grupo de trabajo, proporcione sólo el nombre de usuario Hola.) Seleccione el nivel de autenticación de hello como privacidad de paquete. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Haga clic en Conectar. Ahora la conexión de WMI Hola debe estar correctamente con hello proporcionada datos y se debe mostrar la ventana de herramienta de comprobación del Instrumental de administración de Windows hello tal y como se muestra a continuación: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Si la conexión de WMI no se establece correctamente, aparecerá un mensaje de error emergente. Hola siguiente captura de pantalla muestra un intento incorrecto si la administración remota WMI y no está habilitada en firewall de Windows permitido la aplicación. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Comprobar el estado WMI de Hola y conectividad.</br>
En el servidor de proceso de configuración/hello, </br>
Haga clic en Inicio > Ejecutar > wmimgmt.msc > Acciones > más acciones > conectar tooanother equipo (máquina de origen). </br>
Escriba las credenciales de Hola de cuenta de hello utilizada para la protección y compruebe si la conectividad es un problema. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Compruebe si las carpetas compartidas en la red de la máquina de origen son accesibles desde el servidor de procesos (PS) de forma remota con credenciales especificadas.
  1. Equipo de servidor (PS) tooProcess de inicio de sesión, abra el Explorador de archivos > en el tipo de barra de direcciones de hello > "\\\source-machine-ip\C$" > haga clic en ENTRAR. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. El Explorador de archivos pedirá las credenciales. Escriba Hola username y password > haga clic en Aceptar.</br>
   Si la máquina de origen está unido al dominio, proporcione el nombre de dominio de hello junto con el nombre de usuario como "ombreDeUsuario".</br>
   Si la máquina de origen está en grupo de trabajo, proporcione solo Hola "username". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Si la conexión es correcta, puede ver las carpetas de Hola de máquina de origen remota de proceso de servidor (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Si la conexión no se establece correctamente, compruebe si se cumplen todos los requisitos previos.
>

Si no desea tooopen "Instrumental de administración de Windows", también puede instalar el servicio de movilidad manualmente en la máquina de origen Hola.</br> [Instalación manual del servicio de movilidad mediante la GUI](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Instalación a través del administrador de configuración](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Pasos siguientes
- [Habilitación de la replicación de máquinas virtuales VMware](vmware-walkthrough-enable-replication.md)
