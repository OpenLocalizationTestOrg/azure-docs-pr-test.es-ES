---
title: "Solución de errores de copia de seguridad con una máquina virtual de Azure | Microsoft Docs"
description: "Solución de problemas de copia de seguridad y restauración de máquinas virtuales de Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: dbd70bdbb17d99c5025018e76ea756b1b1528a3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Solución de problemas de copia de seguridad de máquinas virtuales de Azure
> [!div class="op_single_selector"]
> * [Almacén de Recovery Services](backup-azure-vms-troubleshoot.md)
> * [Almacén de Backup](backup-azure-vms-troubleshoot-classic.md)
>
>

Puede solucionar los errores detectados al usar Azure Backup con la información incluida en la tabla siguiente.

## <a name="backup"></a>Copia de seguridad
| Detalles del error | Solución alternativa |
| --- | --- |
| No se pudo realizar la operación porque la máquina virtual ya no existe. Ya no se protege la máquina virtual sin eliminar los datos de la copia de seguridad. En http://go.microsoft.com/fwlink/?LinkId=808124 encontrará más información |Esto sucede cuando se elimina la máquina virtual principal, pero la directiva de copia de seguridad continúa buscando una máquina virtual para realizar la copia de seguridad. Para solucionar este error:  <ol><li> Vuelva a crear la máquina virtual con el mismo nombre y el mismo nombre de grupo de recursos [nombre del servicio en la nube],<br>O BIEN</li><li> Deje de proteger la máquina virtual eliminando o sin eliminar los datos de la copia de seguridad. [Más detalles](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Error de la operación de instantánea debido a que no hay conectividad de red en la máquina virtual: asegúrese de que la máquina virtual tiene acceso a la red. Para que la instantánea se ejecuta correctamente, agregue los intervalos del centro de datos de Azure a la lista blanca o configure un servidor proxy para el acceso a la red. Para más detalles, consulte http://go.microsoft.com/fwlink/?LinkId=800034. Si ya usa un servidor proxy, asegúrese de que esté configurado correctamente | Este error se produce cuando se deniega la conectividad saliente a Internet en la máquina virtual. Se requiere conectividad a Internet para que la extensión de instantánea de máquina virtual tome una instantánea de los discos subyacentes de la máquina virtual. [Más información](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) sobre cómo corregir errores de instantánea debido al acceso bloqueado a la red. |
| El agente de máquina virtual no se puede comunicar con el servicio Azure Backup. - Asegúrese de que la máquina virtual tiene conectividad de red y que el agente de máquina virtual sea el más reciente y esté en ejecución. Para más información, consulte http://go.microsoft.com/fwlink/?LinkId=800034 |Este error se produce si hay un problema con el agente de la máquina virtual o cuando el acceso de red a la infraestructura de Azure está bloqueado por algún motivo. [Aprenda más](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) sobre los problemas de las instantáneas de la máquina virtual.<br> Si el agente de la máquina virtual no está causando problemas, reinicie la máquina virtual. A veces, un estado incorrecto de la máquina virtual puede causar problemas, y reiniciar la máquina virtual restablece este "mal estado". |
| La máquina virtual está en un estado de aprovisionamiento erróneo: reinicie la máquina virtual y asegúrese de que el estado de la máquina virtual es de apagado o en ejecución | Esto ocurre cuando uno de los errores de extensión lleva a que el estado de la máquina virtual sea de aprovisionamiento erróneo. Vaya a la lista de extensiones y vea si hay una extensión errónea, quítela e intente reiniciar la máquina virtual. Si todas las extensiones están en estado de ejecución, compruebe si el servicio del agente de máquina virtual está en ejecución. Si no es así, reinicie el servicio del agente de máquina virtual. | 
| Error en la operación de extensión VMSnapshot para discos administrados: reintente la operación de copia de seguridad. Si el problema se repite, siga las instrucciones que se indican en "http://go.microsoft.com/fwlink/?LinkId=800034". Si a pesar de todo el problema continúa, póngase en contacto con el soporte técnico de Microsoft | Este error se produce cuando el servicio de Azure Backup no puede desencadenar una instantánea. [Más información](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) sobre cómo depurar problemas de las instantáneas de máquina virtual. |
| No se pudo copiar la instantánea de la máquina virtual porque no había suficiente espacio disponible en la cuenta de almacenamiento: asegúrese de que el espacio disponible en la cuenta de almacenamiento sea equivalente al de los datos presentes en los discos de almacenamiento premium conectados a la máquina virtual | En el caso de máquinas virtuales premium, la instantánea se copia a la cuenta de almacenamiento. Esto se hace para garantizar que el tráfico de administración de copias de seguridad, que trabaja en la instantánea, no limite el número de E/S por segundo disponibles para la aplicación con discos premium. Microsoft recomienda asignar solo 50% del espacio total de la cuenta de almacenamiento a fin de que el servicio de Azure Backup pueda copiar la instantánea a la cuenta de almacenamiento y transferir datos desde la ubicación copiada en la cuenta de almacenamiento al almacén. | 
| No se puede realizar la operación porque VM Agent no está respondiendo |Este error se produce si hay un problema con el agente de la máquina virtual o cuando el acceso de red a la infraestructura de Azure está bloqueado por algún motivo. Para las máquinas virtuales de Windows, compruebe el estado del servicio VM Agent en los servicios y si el agente aparece en los programas del panel de control. Intente quitar el programa desde el panel de control y vuelva a instalar el agente, como se indica [a continuación](#vm-agent). Después de volver a instalar al agente, realice una copia de seguridad ad hoc para realizar la comprobación. |
| Error en la operación de extensión de Recovery Services. Asegúrese de que el agente de la máquina virtual más reciente está en la máquina virtual y el servicio del agente se está ejecutando. Vuelva a intentar la operación de copia de seguridad y, si se produce un error, póngase en contacto con el servicio de soporte técnico de Microsoft. |Este error se produce cuando el agente de la máquina virtual no está actualizado. Consulte la sección "Actualizar el agente de la máquina virtual" para actualizar dicho agente. |
| No existe la máquina virtual. Asegúrese de que la máquina virtual existe, o bien seleccione otra máquina virtual. |Esto sucede cuando se elimina la máquina virtual principal, pero la directiva de copia de seguridad continúa buscando una máquina virtual para realizar la copia de seguridad. Para solucionar este error:  <ol><li> Vuelva a crear la máquina virtual con el mismo nombre y el mismo nombre de grupo de recursos [nombre del servicio en la nube],<br>O BIEN<br></li><li>Deje de proteger la máquina virtual sin eliminar los datos de la copia de seguridad. [Más detalles](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Error en la ejecución del comando. - Otra operación está actualmente en curso en este elemento. Espere hasta que se complete la operación anterior y vuelva a intentarlo. |Se está ejecutando una copia de seguridad existente de la máquina virtual y no se puede iniciar un nuevo trabajo mientras haya otro en ejecución. |
| Al copiar discos duros virtuales desde el almacén de Backup se agotó el tiempo de espera. Vuelva a intentar la operación en unos minutos. Si el persiste el problema, póngase en contacto con el Soporte técnico de Microsoft. | Esto ocurre si se produce un error transitorio en el almacenamiento o si el servicio Backup no obtiene suficientes E/S por segundo desde la cuenta de almacenamiento en la que se hospeda la máquina virtual como para poder transferir los datos al almacén durante el período de tiempo de espera. No olvide seguir los [procedimientos recomendados](backup-azure-vms-introduction.md#best-practices) cuando configure la copia de seguridad. Pruebe a transferir la máquina virtual a otra cuenta de almacenamiento que no esté cargada e intente realizar de nuevo la copia de seguridad.|
| Error interno en la copia de seguridad. Vuelva a intentar la operación en unos minutos. Si el problema persiste, póngase en contacto con el Servicio técnico de Microsoft. |Este error puede aparecer por dos razones:  <ol><li> Hay un problema transitorio al acceder al almacenamiento de la máquina virtual. Compruebe el [estado de Azure](https://azure.microsoft.com/en-us/status/) para ver si hay algún problema recurrente relacionado con los procesos, el almacenamiento o la red en la región. Luego, vuelva a intentar el trabajo de copia de seguridad una vez que se haya resuelto el problema. <li>Se ha eliminado la máquina virtual original y, por tanto, no se puede tomar el punto de recuperación. Para mantener los datos de copia de seguridad de una máquina virtual eliminada y, a la vez, eliminar los errores de copia de seguridad, quite la protección de la máquina virtual y elija la opción de conservar los datos. Esta acción detiene el trabajo de copia de seguridad programado y los mensajes de error recurrentes. |
| No se pudo instalar la extensión de Azure Recovery Services en el elemento seleccionado. El agente de máquina virtual es un requisito previo para la extensión de Azure Recovery Services. Instale el agente de la máquina virtual de Azure y reinicie el funcionamiento del registro |<ol> <li>Compruebe si el agente de la máquina virtual se ha instalado correctamente. <li>Asegúrese de que la marca de la configuración de la máquina virtual se haya establecido correctamente.</ol> [Más información](#validating-vm-agent-installation) acerca de la instalación del agente de la máquina virtual y de cómo validar dicha instalación. |
| Error de instalación de la extensión "COM+ no pudo realizar la conexión con MS DTC (Microsoft Distributed Transaction Coordinator)" |Normalmente, esto significa que el servicio COM+ no se ejecuta. Para obtener ayuda acerca de cómo solucionar este problema, póngase en contacto con el servicio de soporte técnico de Microsoft. |
| Error en la operación de instantánea con el error de operación de VSS "El Cifrado de unidad BitLocker está bloqueando esta unidad" Esta unidad se debe desbloquear en el Panel de control. |Desactive BitLocker para todas las unidades de la máquina virtual y observe si se resuelve el problema VSS |
| El estado de la máquina virtual no permite realizar copias de seguridad. |<ul><li>Compruebe si la máquina virtual se encuentra en un estado transitorio entre En ejecución y Apagar. Si es así, espere a que la máquina virtual adopte uno de estos estados y vuelva a desencadenar la copia de seguridad. <li> Si se trata de una máquina virtual de Linux que utiliza el módulo de kernel [Security Enhanced Linux], deberá excluir la ruta del agente de Linux (_/var/lib/waagent_) de la directiva de seguridad para asegurarse de que la extensión de copia de seguridad puede instalarse correctamente.  |
| Máquina virtual de Azure no encontrada. |Esto sucede cuando se elimina la máquina virtual principal, pero la directiva de copia de seguridad continúa buscando una máquina virtual para realizar la copia de seguridad. Para solucionar este error:  <ol><li>Vuelva a crear la máquina virtual con el mismo nombre y el mismo nombre de grupo de recursos [nombre del servicio en la nube], <br>O BIEN <li> Deshabilite la protección de esta máquina virtual para que no se creen los trabajos de copia de seguridad. </ol> |
| El agente de máquina virtual no está presente en la máquina virtual. Instale los requisitos previos y el agente de máquina virtual, y reinicie la operación. |[Obtenga más información](#vm-agent) acerca del agente de la máquina virtual y sobre cómo validar su instalación. |
| Error en la operación de instantánea debido a VSS Writer en mal estado |Debe reiniciar los VSS Writer (Volume Shadow copy Service) que se encuentran en mal estado. Para lograrlo, desde un símbolo del sistema con privilegios elevados, ejecute _escritores de lista vssadmin_. La salida contiene todos los VSS Writer y su estado. Para cada VSS Writer cuyo estado no sea "[1] Estable", ejecute el VSS Writer mediante la ejecución de los siguientes comandos desde un símbolo del sistema con privilegios elevados:<br> _net stop serviceName_ <br> _net start serviceName_|
| Error de operación de instantánea debido a un error de análisis de la configuración |Esto sucede debido a permisos modificados en el directorio MachineKeys: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Ejecute el comando siguiente y compruebe que los permisos en el directorio MachineKeys sean los predeterminados:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> Los permisos predeterminados son:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>Si ve permisos en el directorio MachineKeys distintos del predeterminado, siga los pasos siguientes para corregir los permisos, eliminar el certificado y desencadenar la copia de seguridad.<ol><li>Corrija los permisos en el directorio MachineKeys.<br>Mediante las propiedades de seguridad del explorador y la configuración de seguridad avanzada en el directorio, restablezca los valores predeterminados de los permisos, quite cualquier objeto de usuario adicional (de forma predeterminada) del directorio y asegúrese de que los permisos de 'todos' dispongan de un acceso especial para:<br>- Enumerar carpeta/leer datos <br>- Leer atributos <br>- Leer atributos ampliados <br>- Crear archivos/escribir datos <br>- Crear carpetas/anexar datos<br>- Escribir atributos<br>- Escribir atributos ampliados<br>- Leer permisos<br><br><li>Elimine todos los certificados con el campo ‘Issued To’ = "Windows Azure Service Management para extensiones" o "Windows Azure CRP Certificate Generator".<ul><li>[Abra la consola de certificados (equipo local).](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Elimine todos los certificados (en Personal -> Certificados) con el campo ‘Issued To’ = "Windows Azure Service Management para extensiones" o "Windows Azure CRP Certificate Generator".</ul><li>Active la copia de seguridad de máquina virtual. </ol>|
| La validación produjo un error debido a que la máquina virtual se ha cifrado solo con BEK. Las copias de seguridad se pueden habilitar únicamente para las máquinas virtuales cifradas con BEK y KEK. |La máquina virtual debe cifrarse con la clave de cifrado BitLocker y la clave de cifrado de claves. Después de eso, debe habilitarse la copia de seguridad. |
| El servicio Azure Backup no tiene los permisos suficientes para acceder a Key Vault para realizar copias de seguridad de máquinas virtuales cifradas. |El servicio Backup puede proporcionar estos permisos en PowerShell siguiendo los pasos de la sección **Habilitar Backup** de la [documentación de PowerShell](backup-azure-vms-automation.md). |
|Error de instalación de la extensión de la instantánea "COM+ no pudo realizar la conexión con MS DTC (Microsoft Distributed Transaction Coordinator)" | Pruebe a iniciar el servicio de Windows "Aplicación del sistema COM+" (desde un símbolo del sistema con privilegios elevados: _net start COMSysApp_). <br>Si se produce un error al iniciarse, siga estos pasos:<ol><li> Asegúrese de que la cuenta de inicio de sesión del servicio "Coordinador de transacciones distribuidas " sea "Servicio de red". Si no es así, cámbiela a "Servicio de red", reinicie este servicio y, a continuación, intente iniciar el servicio "Aplicación del sistema COM+".<li>Si se sigue produciendo un error al iniciar este servicio, desinstale y vuelva a instalar el servicio "Coordinador de transacciones distribuidas" siguiendo estos pasos:<br> - Detenga el servicio MSDTC.<br> - Abra el símbolo del sistema (cmd). <br> - Ejecute el comando "msdtc-uninstall". <br> - Ejecute el comando "msdtc-install". <br> - Inicie el servicio MSDTC.<li>Inicie el servicio de Windows "Aplicación del sistema COM+" y, una vez iniciado, desencadene la copia de seguridad desde el portal.</ol> |
|  Error en la operación de instantánea debido a error de COM+ | Se recomienda iniciar el servicio de Windows "Aplicación del sistema COM+" (desde un símbolo del sistema con privilegios elevados: _net start COMSysApp_). Si el problema persiste, reinicie la máquina virtual. Si al reiniciar la máquina virtual no se soluciona el problema, intente [quitar la extensión VMSnapshot](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) y active manualmente la copia de seguridad. |
| Error al inmovilizar uno o varios puntos de montaje de la máquina virtual para tomar una instantánea coherente del sistema de archivos | Para ello, siga los pasos que se describen a continuación: <ol><li>Compruebe el estado del sistema de archivos de todos los dispositivos montados con el comando _'tune2fs'_.<br> Por ejemplo: tune2fs -l /dev/sdb1 \| grep "Filesystem state" <li>Desmonte los dispositivos que no tengan un estado limpio del sistema de archivos mediante el comando _'umount'_. <li> Ejecute la comprobación de coherencia del sistema de archivos en estos dispositivos con el comando _'fsck'_. <li> Vuelva a montar los dispositivos e intente realizar la copia de seguridad.</ol> |
| Error en la operación de instantánea debido a un error en la creación de un canal de comunicación de red segura | <ol><Li> Ejecute regedit.exe para abrir el Editor del Registro en modo elevado. <li> Identifique todas las versiones de. NetFramework presentes en el sistema. Se encuentran en la jerarquía de la clave del Registro "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft". <li> Para cada versión de .NetFramework presente en la clave del Registro, agregue la siguiente clave: <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| Error en la operación de instantánea debido a un error en la instalación de Visual C++ Redistributable para Visual Studio 2012 | Vaya a C:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion e instale vcredist2012_x64. Asegúrese de que el valor de la clave del Registro para permitir la instalación del servicio esté establecido en el valor correcto, es decir, que el valor de la clave del Registro _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_ está establecido en 3 y no en 4. Si todavía experimenta problemas con la instalación, reinicie el servicio de instalación mediante la ejecución de _MSIEXEC /UNREGISTER_ seguido de _MSIEXEC /REGISTER_ desde un símbolo del sistema con privilegios elevados.  |


## <a name="jobs"></a>Trabajos
| Detalles del error | Solución alternativa |
| --- | --- |
| No se admite la cancelación para este tipo de trabajo; espere hasta que finalice el trabajo. |None |
| El trabajo no está en un estado que se pueda cancelar; espere hasta que finalice el trabajo. <br>OR<br> El trabajo seleccionado no está en un estado en que se pueda cancelar; espere hasta que finalice el trabajo. |Con toda probabilidad, el trabajo se ha casi completado. Espere hasta que se complete el trabajo.|
| No se puede cancelar el trabajo porque no está en curso; solo se admite la cancelación de trabajos que están en curso. Intente cancelar un trabajo que esté en curso. |Esto sucede debido a un estado transitorio. Espere un momento y reintente la operación de cancelación. |
| No se pudo cancelar el trabajo; espere hasta que finalice el trabajo. |None |

## <a name="restore"></a>Restauración
| Detalles del error | Solución alternativa |
| --- | --- |
| Error en la restauración con error interno de nube |<ol><li>El servicio de nube que está intentando restaurar está configurado con la configuración de DNS. Puede consultar  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Si hay una dirección configurada, significa que se ha configurado DNS.<br> <li>El servicio en la nube al que está tratando restaurar está configurado con la IP reservada y las máquinas virtuales del servicio en la nube tienen un estado de detenido.<br>Puede comprobar que un servicio en la nube tiene una IP reservada utilizando los siguientes cmdlets de PowerShell:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Está intentando restaurar una máquina virtual con las siguientes configuraciones de red especiales en el mismo servicio en la nube. <br>- Máquinas virtuales con la configuración del equilibrador de carga (interna y externa)<br>- Máquinas virtuales con varias direcciones IP reservadas<br>- Máquinas virtuales con varias NIC<br>Seleccione un nuevo servicio en la nube en la interfaz de usuario o consulte las [consideraciones de restauración](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations) de las máquinas virtuales con las configuraciones de red especiales.</ol> |
| El nombre DNS seleccionado ya existe: especifique otro nombre DNS y vuelva a intentarlo. |El nombre DNS aquí hace referencia al nombre del servicio en la nube (normalmente terminados con .cloudapp.net). Debe ser único. Si se produce este error, deberá elegir otro nombre para la máquina virtual durante la restauración. <br><br> Este error solo se muestra a los usuarios de Azure Portal. La operación de restauración a través de PowerShell se realizará correctamente porque solo restaura los discos y no crea la máquina virtual. El error aparecerá cuando el usuario crea explícitamente la máquina virtual después de la operación de restauración del disco. |
| La configuración de red virtual especificada no es correcta: especifique otra configuración de red virtual y vuelva a intentarlo. |None |
| El servicio en la nube especificado usa una dirección IP reservada, que no coincide con la configuración de la máquina virtual que se está restaurando: especifique otro servicio en la nube que no use la IP reservada o elija otro punto de recuperación desde el que restaurar. |None |
| El Servicio en la nube alcanzó el límite del número de puntos de entrada finales, vuelva a intentar la operación mediante la especificación de otro servicio en la nube o mediante un extremo existente. |None |
| La cuenta de almacenamiento de destino y el almacén de Backup están en dos regiones diferentes: compruebe que la cuenta de almacenamiento especificada en la operación de restauración se encuentra en la misma región de Azure que el almacén de Backup. |None |
| La cuenta de almacenamiento especificada para la operación de restauración no se admite: solo se admiten las cuentas de almacenamiento básicas o estándar con una configuración de réplica con redundancia local o redundancia geográfica. Seleccione una cuenta de almacenamiento compatible |None |
| El tipo de cuenta de almacenamiento especificado para la operación de restauración no está en línea: asegúrese de que la cuenta de almacenamiento especificada en la operación de restauración está en línea |Esto puede suceder debido a un error transitorio en Azure Storage o debido a una interrupción. Elija otra cuenta de almacenamiento. |
| Se alcanzó la cuota del grupo de recursos: elimine algunos grupos de recursos desde Azure Portal o póngase en contacto con el soporte técnico de Azure para aumentar los límites. |None |
| La subred seleccionada no existe: seleccione una subred que exista |None |
| El servicio Backup no tiene autorización para acceder a los recursos de su suscripción. |Para resolver este problema, en primer lugar es preciso restaurar los discos, para lo que hay que seguir los pasos que se indican en la sección **Restaurar discos en copia de seguridad** de [Elección de una configuración de restauración para una máquina virtual](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Después, siga los pasos de PowerShell que se indican en [Creación de una máquina virtual a partir de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para crear una máquina virtual completa a partir de discos restaurados. |

## <a name="backup-or-restore-taking-time"></a>Tiempo excesivo en operaciones de copia de seguridad y restauración
Si se indica que el tiempo en realizar la copia de seguridad es (>12 horas) o en realizar la restauración (>6 horas):
* Averigüe los [factores que influyen en la duración de la copia de seguridad](backup-azure-vms-introduction.md#total-vm-backup-time) y los [factores que influyen en el tiempo de la restauración](backup-azure-vms-introduction.md#total-restore-time).
* Asegúrese de que sigue las [Prácticas recomendadas para la copia de seguridad](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>Agente de máquina virtual
### <a name="setting-up-the-vm-agent"></a>Configuración del agente de la máquina virtual
Normalmente, el agente de la máquina virtual ya está presente en las máquinas virtuales que se crean desde la Galería de Azure. Sin embargo, las máquinas virtuales que se migran desde los centros de datos locales no tienen instalado el agente de la máquina virtual. Para dichas máquinas virtuales, el agente de la máquina virtual debe instalarse explícitamente.

Para las máquinas virtuales de Windows:

* Descargue e instale el [MSI del agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Para completar la instalación, necesita privilegios de administrador.
* En el caso de las máquinas virtuales clásicas, [actualice la propiedad de la máquina virtual](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) para indicar que el agente está instalado. Este paso no es necesario para las máquinas virtuales Resource Manager.

Máquinas virtuales de Linux:

* Instale la versión más reciente del repositorio de distribución. Es **muy recomendable** instalar el agente solo a través del repositorio de distribución. Para más información sobre el nombre del paquete, consulte el [repositorio del agente de Linux](https://github.com/Azure/WALinuxAgent) 
* En el caso de máquinas virtuales clásicas, [actualice la propiedad de la máquina virtual](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) para indicar que el agente está instalado. Este paso no es necesario para las máquinas virtuales Resource Manager.

### <a name="updating-the-vm-agent"></a>Actualización del agente de la máquina virtual
Para las máquinas virtuales de Windows:

* Actualizar el agente de la máquina virtual es tan sencillo como volver a instalar los [archivos binarios del agente de la máquina virtual](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sin embargo, deberá asegurarse de que no se está ejecutando ninguna operación de copia de seguridad mientras se actualiza el agente de la máquina virtual.

Máquinas virtuales de Linux:

* Siga las instrucciones proporcionadas en [Actualización del agente de máquina virtual Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Se **recomienda fehacientemente** actualizar el agente solo a través del repositorio de distribución. No recomendamos descargar el código de agente desde github directamente y actualizarlo. Si el último agente no está disponible para su distribución, vaya al soporte técnico de distribución para obtener instrucciones sobre cómo instalar el agente más reciente. Puede comprobar la información del [agente Linux de Windows Azure](https://github.com/Azure/WALinuxAgent/releases) más reciente en el repositorio de github.

### <a name="validating-vm-agent-installation"></a>Validación de la instalación del agente de la máquina virtual
Cómo comprobar la versión del agente de la máquina virtual en máquinas virtuales de Windows:

1. Inicie sesión en la máquina virtual de Azure y vaya a la carpeta *C:\WindowsAzure\Packages*. El archivo WaAppAgent.exe debe estar ahí.
2. Haga clic con el botón derecho en el archivo, desplácese hasta **Propiedades** y seleccione la pestaña **Detalles**. En el campo de versión del producto, debe aparecer el valor 2.6.1198.718 o uno superior.

## <a name="troubleshoot-vm-snapshot-issues"></a>Solucionar problemas de instantáneas de máquina virtual
La copia de seguridad de máquinas virtuales se basa en la emisión de comandos de instantánea para el almacenamiento subyacente. No tener acceso al almacenamiento o los retrasos en la ejecución de las tarea de instantáneas puede generar un error en el trabajo de copia de seguridad. Lo siguiente puede producir un error en la tarea de instantáneas.

1. Se bloquea el acceso de red a Almacenamiento mediante NSG<br>
    Aprenda más sobre cómo [habilitar el acceso de red](backup-azure-vms-prepare.md#network-connectivity) en Storage mediante la lista blanca de direcciones IP o a través del servidor proxy.
2. Las máquinas virtuales con copia de seguridad de SQL Server configurado pueden provocar un retraso de la tarea de instantánea <br>
   De forma predeterminada, la copia de seguridad de máquinas virtuales genera una copia de seguridad completa de VSS en máquinas virtuales de Windows. En las máquinas virtuales que ejecutan servidores SQL Server y la copia de seguridad de SQL Server está configurada, esto podría provocar el retraso en la ejecución de la instantánea. Establezca la siguiente clave del Registro si se producen errores de la copia de seguridad debido a problemas de instantáneas.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. Estado de la máquina virtual notificado incorrectamente porque la máquina virtual está apagada en RDP.  <br>
   Si ha apagado la máquina virtual en RDP, vuelva a comprobar en el portal que el estado de la máquina virtual se refleja correctamente. Si no es así, apague la máquina virtual en el portal mediante la opción 'Apagado' en el panel de la máquina virtual.
4. Si más de cuatro máquinas virtuales comparten el mismo servicio en la nube, configure varias directivas de copia de seguridad para organizar los tiempos de copia de seguridad, de modo que no más de cuatro copias de seguridad de máquina virtual se inicien al mismo tiempo. Intente distribuir las horas de inicio de la copia de seguridad con una hora de diferencia entre las directivas.
5. La máquina virtual se ejecuta con un uso elevado de CPU o memoria.<br>
   Si está ejecutando la máquina virtual con un uso de CPU o memoria altos (más del 90 %), la tarea de instantáneas se pone en cola, se retrasa y el tiempo de espera se agotará finalmente. Pruebe la copia de seguridad a petición en esas situaciones.

<br>

## <a name="networking"></a>Redes
Al igual que todas las extensiones, la de copia de seguridad necesita tener acceso a Internet para funcionar. Si no tiene acceso público a Internet, se pueden producir estos problemas:

* Se puede producir un error en la instalación de la extensión.
* Se puede producir un error en las operaciones de copia de seguridad (como al realizar la instantánea de disco).
* Se puede producir un error en la operación para mostrar el estado de la operación de copia de seguridad.

La necesidad de resolver direcciones públicas de Internet se describe [aquí](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). Deberá comprobar las configuraciones de DNS para la red virtual y asegurarse de que se puedan resolver los URI de Azure.

Una vez que la resolución de nombres se haya realizado correctamente, también hay que proporcionar acceso a las direcciones IP de Azure. Para desbloquear el acceso a la infraestructura de Azure, siga uno de estos pasos:

1. Preparar una lista blanca con los intervalos IP del centro de datos de Azure.
   * Obtenga la lista de [IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) que van a formar parte de la lista de direcciones IP aprobadas.
   * Desbloquee las direcciones IP usando el cmdlet [New-NetRoute](https://technet.microsoft.com/library/hh826148.aspx) . Ejecute este cmdlet en la máquina virtual de Azure, en una ventana de PowerShell con privilegios elevados (realice la ejecución como administrador).
   * Agregar reglas al NSG (si dispone de uno implementado) para permitir el acceso a las direcciones IP.
2. Crear una ruta de acceso para el flujo del tráfico HTTP
   * Si tiene alguna restricción de red implementada (por ejemplo, un grupo de seguridad de red), implemente un servidor proxy HTTP para enrutar el tráfico. [Aquí](backup-azure-vms-prepare.md#network-connectivity) se pueden encontrar los pasos necesarios para implementar un servidor proxy HTTP.
   * Agregue reglas al NSG (si dispone de uno implementado) para permitir el acceso a INTERNET desde el proxy HTTP.

> [!NOTE]
> DHCP debe estar habilitado dentro del invitado para que la copia de seguridad de máquinas virtuales de IaaS funcione.  Si necesita una dirección IP privada estática, debe configurarla a través de la plataforma. La opción DHCP dentro de la máquina virtual debe continuar habilitada.
> Vea más información sobre el [Establecimiento de una dirección IP privada interna estática](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>