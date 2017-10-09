---
title: "aaaPreparing su tooback entorno las máquinas virtuales de Azure | Documentos de Microsoft"
description: "Asegúrese de que el entorno está preparado para la copia de seguridad de máquinas virtuales en Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: copias de seguridad; realizar copia de seguridad
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Preparar su tooback entorno las máquinas virtuales de Azure
> [!div class="op_single_selector"]
> * [Modelo de Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modelo clásico](backup-azure-vms-prepare.md)
>
>

Para hacer copias de seguridad de una máquina virtual (VM) de Azure, deben darse tres condiciones.

* Necesita toocreate un almacén de copia de seguridad o identificar un almacén de copia de seguridad existente *Hola misma región que la máquina virtual*.
* Establecer la conectividad de red entre hello Azure Internet pública direcciones y Hola puntos de conexión de almacenamiento de Azure.
* Instalar a agente de VM de hello en hello máquina virtual.

Si sabe que estas condiciones ya existen en su entorno, a continuación, continuar toohello [el artículo de máquinas virtuales de copia de seguridad](backup-azure-vms.md). En caso contrario, siga leyendo, en este artículo le guiará Hola pasos tooprepare su tooback de entorno de una VM de Azure.

##<a name="supported-operating-system-for-backup"></a>Sistemas operativos compatibles para copia de seguridad
 * **Linux**: Copia de seguridad de Azure admite [una lista de distribuciones aprobadas por Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , con la excepción de CoreOS Linux. _Otras Bring-Your-posee-las distribuciones de Linux también pueden trabajar como agente de máquina virtual de hello está disponible en la máquina virtual de Hola y la compatibilidad con Python existe. Sin embargo, no respaldamos esas distribuciones para copia de seguridad._
 * **Windows Server**: no se admiten las versiones anteriores a Windows Server 2008 R2.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitaciones al realizar copias de seguridad y restaurar una máquina virtual
> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Hello lista siguiente proporciona las limitaciones de hello cuando se implementa en el modelo clásico de Hola.
>
>

* No se admite la copia de seguridad de máquinas virtuales con más de 16 discos de datos.
* No se admite la copia de seguridad de máquinas virtuales con una dirección IP reservada y sin puntos de conexión definidos.
* Los datos de copia de seguridad no incluyen red montada las unidades conectadas tooVM.
* No se admite el reemplazo de una máquina virtual existente durante la restauración. Eliminar primero la máquina virtual existente de Hola y los discos asociados y, a continuación, restaurar los datos de Hola de copia de seguridad.
* No se admite la restauración y copia de seguridad entre regiones.
* Copia de seguridad de máquinas virtuales mediante el servicio de copia de seguridad de Azure de hello es compatible en todas las regiones públicas de Azure (vea hello [lista de comprobación](https://azure.microsoft.com/regions/#services) de regiones admitidas). Si hoy es compatible región Hola que desea obtener, no aparecerá en la lista desplegable de Hola durante la creación del almacén.
* Copia de seguridad de máquinas virtuales mediante el servicio de copia de seguridad de Azure Hola solo se admite para las versiones de sistema operativo seleccione:
* La restauración de una máquina virtual de controlador de dominio que forma parte de una configuración de varios controladores de dominio solo se admite a través de PowerShell. Más información sobre cómo [restaurar un controlador de dominio de varios controladores de dominio](backup-azure-restore-vms.md#restoring-domain-controller-vms)
* Se admite la restauración de máquinas virtuales que tengan Hola siguiendo las configuraciones de red especiales sólo a través de PowerShell. Máquinas virtuales que cree mediante el uso de flujo de trabajo de restauración de Hola Hola interfaz de usuario no tendrá estas configuraciones de red una vez completada la operación de restauración de Hola. más información, consulte toolearn [restaurar las máquinas virtuales con las configuraciones de red especiales](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Máquinas virtuales con la configuración del equilibrador de carga (interna y externa).
  * Máquinas virtuales con varias direcciones IP reservadas.
  * Máquinas virtuales con varios adaptadores de red.

## <a name="create-a-backup-vault-for-a-vm"></a>Creación de un almacén de copia de seguridad para una máquina virtual
Un almacén de copia de seguridad es una entidad que almacena todas las copias de seguridad de Hola y puntos de recuperación que se han creado con el tiempo. almacén de copia de seguridad de Hello también contiene las directivas de copia de seguridad de Hola que serán aplicado toohello las máquinas virtuales haciendo copias de seguridad.

> [!IMPORTANT]
> A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico. Todavía se admiten los almacenes de copia de seguridad existentes, y es posible demasiado[utilizan almacenes de copia de seguridad de Azure PowerShell toocreate](./backup-client-automation-classic.md#create-a-backup-vault). Sin embargo, Microsoft recomienda que crear almacenes de servicios de recuperación de todas las implementaciones porque futuras mejoras tooRecovery los almacenes de servicios, solo aplican.


Esta imagen muestra las relaciones de hello entre Hola diversas entidades de copia de seguridad de Azure: ![entidades de copia de seguridad de Azure y relaciones](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Conectividad de red
En las instantáneas de máquina virtual de orden toomanage hello, extensión de copia de seguridad de hello necesita conectividad toohello Azure direcciones IP públicas. Sin conectividad a Internet derecho hello, HTTP solicitudes hello y tiempo de espera de copia de seguridad operación Hola la máquina virtual produce un error. Si la implementación tiene restricciones de acceso establecidas (a través de un grupo de seguridad de red (NSG), por ejemplo), elija entonces una de estas opciones para proporcionar una ruta de acceso clara para el tráfico de copia de seguridad:

* [Intervalos IP de Azure del centro de datos de lista blanca Hola](http://www.microsoft.com/en-us/download/details.aspx?id=41653) : consulte el artículo de Hola para obtener instrucciones sobre cómo toowhitelist Hola direcciones IP.
* Implementación de un servidor proxy HTTP para enrutar el tráfico.

Al decidir qué opción toouse, Hola ventajas e inconvenientes son entre la capacidad de administración, un control granular y el coste.

| Opción | Ventajas | Desventajas |
| --- | --- | --- |
| Creación de una lista blanca con intervalos IP |Sin costos adicionales.<br><br>Para abrir el acceso en un NSG, usar hello <i>AzureNetworkSecurityRule conjunto</i> cmdlet. |Toomanage complejo como el cambio de intervalos IP de hello afectado con el tiempo.<br><br>Proporciona el conjunto de toohello de acceso de Azure y no solo en el almacenamiento de información. |
| Proxy HTTP |Control granular de proxy de hello sobre el almacenamiento de Hola que permite las direcciones URL. toosetup un control granular de proxy de hello, https://\*.blob.core.windows.net/\* modelo de dirección URL debe toobe en la lista blanca. toowhitelist Hola sólo la cuenta de almacenamiento usada por hello VM, https://\<storageAccount\>.blob.core.windows.net/\* modelo de dirección URL debe toobe en la lista blanca. <br>TooVMs de acceso de punto único de Internet.<br>No tooAzure cambios en la dirección IP del firmante. |Costes adicionales para ejecutar una máquina virtual con el software de proxy de Hola. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalos de IP de centro de datos Azure Hola de lista blanca de direcciones
intervalos de IP de toowhitelist hello Azure del centro de datos, vea hello [sitio Web de Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) para obtener más información sobre los intervalos IP de hello e instrucciones.

### <a name="using-an-http-proxy-for-vm-backups"></a>Uso de un proxy HTTP para las copias de seguridad de máquinas virtuales
Cuando copia de seguridad de una máquina virtual, extensión de copia de seguridad de hello en hello VM envía Hola instantánea administración comandos tooAzure almacenamiento mediante una API de HTTPS. Redirigir el tráfico de extensión de reserva de Hola a través de proxy de hello HTTP ya que es el único componente de hello configurado para acceso toohello Internet pública.

> [!NOTE]
> No hay ninguna recomendación para el software de proxy de Hola que debe usarse. Asegúrese de que se elige a un proxy que disponga de adherencia saliente y que es compatible con los siguientes pasos de configuración de Hola. Asegúrese de que los programas de software de terceros no modificar la configuración de proxy de Hola
>
>

imagen de ejemplo de Hola siguiente muestra pasos de configuración tres Hola necesarios toouse HTTP proxy:

* Las rutas de aplicación virtual para que todo el tráfico HTTP enlazado Hola red pública de Internet a través de la máquina virtual de Proxy.
* Proxy de máquina virtual permite el tráfico entrante desde máquinas virtuales en la red virtual de Hola.
* Grupo de seguridad de red (NSG) con el nombre de bloqueo sin fondos de Hello necesita un seguridad regla permitir Internet el tráfico saliente de máquina virtual de Proxy.

![Grupo de seguridad de red con el diagrama de implementación de proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello red pública de Internet, siga estos pasos:

#### <a name="step-1-configure-outgoing-network-connections"></a>Paso 1. Configuración de las conexiones de red salientes
###### <a name="for-windows-machines"></a>Para máquinas Windows
En este paso se configura el servidor proxy para la cuenta de sistema local.

1. Descargue [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Se abrirá la ventana de Internet Explorer.
3. Vaya a tooTools -> Opciones de Internet -> conexiones -> configuración de LAN.
4. Compruebe la configuración de proxy de la cuenta del sistema. Configure la dirección IP de proxy y el puerto.
5. Cierre Internet Explorer.

Se configurará el proxy en todo el equipo y se usará para el tráfico saliente de HTTP/HTTPS.

Si tiene el programa de instalación de un servidor proxy en una cuenta de usuario actual (no una cuenta de sistema Local), use Hola siguientes script tooapply les tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Si ve el mensaje "(407) Se requiere autenticación del proxy" en el registro del servidor proxy, compruebe que su autenticación está configurada correctamente.
>
>

###### <a name="for-linux-machines"></a>Para máquinas Linux
Agregar Hola después línea toohello ```/etc/environment``` archivo:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Agregar Hola después líneas toohello ```/etc/waagent.conf``` archivo:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Paso 2: Permitir las conexiones entrantes en el servidor de proxy de hello:
1. En el servidor de proxy de hello, abra Firewall de Windows. firewall de Hola de manera más fácil de Hello tooaccess es toosearch Firewall de Windows con seguridad avanzada.

    ![Abra Hola Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. En el cuadro de diálogo de Firewall de Windows hello, haga clic en **reglas de entrada** y haga clic en **nueva regla...** .

    ![Crear una nueva regla](./media/backup-azure-vms-prepare/firewall-02.png)
3. Hola **entrada Asistente para nueva regla**, elija hello **personalizado** opción para hello **tipo de regla** y haga clic en **siguiente**.
4. En Hola de hello página tooselect **programa**, elija **todos los programas** y haga clic en **siguiente**.
5. En hello **protocolo y puertos** página, escriba Hola siguiente información y haga clic en **siguiente**:

    ![Crear una nueva regla](./media/backup-azure-vms-prepare/firewall-03.png)

   * en *Tipo de protocolo*, elija *TCP*.
   * para *puerto Local* elegir *puertos específicos*, en el siguiente campo de hello especificar hello ```<Proxy Port>``` que se ha configurado.
   * En *Puerto remoto*, seleccione *Todos los puertos*.

     Para el resto de Hola de Asistente de hello, haga clic en todos los extremos de toohello de manera hello y asigne un nombre a esta regla.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Paso 3: Agregue un toohello de regla de excepción NSG:
En un símbolo del sistema de PowerShell de Azure, escriba Hola siguiente comando:

Hola siguiente comando agrega un NSG de toohello de excepción. Esta excepción permite el tráfico TCP desde cualquier puerto 10.0.0.5 tooany dirección de Internet en el puerto 80 (HTTP) o 443 (HTTPS). Si necesita un puerto específico en Hola red pública de Internet, pueden tooadd seguro de que el puerto toohello ```-DestinationPortRange``` así.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Asegúrese de que reemplazar nombres de hello en el ejemplo de Hola con la implementación de hello detalles tooyour adecuado.*

## <a name="vm-agent"></a>Agente de máquina virtual
Antes de hacer copias de seguridad Hola máquina virtual de Azure, debe asegurarse de que ese agente de máquina virtual de Azure Hola está instalado correctamente en la máquina virtual de Hola. Puesto que el agente de máquina virtual de hello es un componente opcional en tiempo de Hola que Hola máquina virtual se crea, asegúrese de esa casilla Hola para agente de máquina virtual de hello está seleccionada antes de que se aprovisionó la máquina virtual de Hola.

### <a name="manual-installation-and-update"></a>Instalación manual y actualización
agente de máquina virtual de Hello ya está presente en las máquinas virtuales que se crean a partir de hello Galería de Azure. Sin embargo, las máquinas virtuales que se migran desde los centros de datos local no tendrán instalado el agente VM de Hola. Para que estas máquinas virtuales, agente de máquina virtual de hello debe toobe instalado explícitamente. Obtenga más información sobre [instalar agente de máquina virtual de hello en una máquina virtual existente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **operación** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalar agente de máquina virtual de Hola |<li>Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesitará la instalación de Hola de toocomplete de privilegios de administrador. <li>[Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado. |<li> Instalar más reciente hello [agente Linux](https://github.com/Azure/WALinuxAgent) desde GitHub. Necesitará la instalación de Hola de toocomplete de privilegios de administrador. <li> [Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado. |
| Actualización de agente de máquina virtual de Hola |Agente de máquina virtual de actualización hello es tan sencillo como Hola reinstalación [archivos binarios del agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad mientras se está actualizando el agente de máquina virtual de Hola. |Siga las instrucciones de hello en [actualizar Hola agente de VM de Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad mientras se está actualizando el agente de máquina virtual de Hola. |
| Validar la instalación del agente VM de Hola |<li>Navegue toohello *C:\WindowsAzure\Packages* carpeta Hola VM de Azure. <li>Debería encontrar Hola WaAppAgent.exe archivo.<li> Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** campo de versión del producto de Hola de ficha debe ser 2.6.1198.718 o superior. |N/D |

Obtenga información acerca de hello [agente de máquina virtual](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) y [cómo tooinstall lo](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Extensión de copia de seguridad
tooback la máquina virtual de hello, Hola servicio de copia de seguridad de Azure instala a un agente de máquina virtual de extensión toohello. Hola servicio copia de seguridad de Azure sin problemas actualiza y revisiones de la extensión de copia de seguridad de hello sin intervención del usuario adicional.

extensión de copia de seguridad de Hola se instala si Hola máquina virtual se está ejecutando. Una máquina virtual en ejecución también proporciona la oportunidad de mayor Hola de obtención de un punto de recuperación coherentes con la aplicación. Sin embargo, hello Azure copia de seguridad servicio continuará tooback seguridad Hola de máquina virtual, incluso si se ha desactivado y extensión de hello no se pudo instalar (también conocido como sin conexión VM). En este caso, será punto de recuperación de hello *coherente de bloqueo* según se explicó anteriormente.

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha preparado el entorno para realizar copias de seguridad de la máquina virtual, el siguiente paso lógico es toocreate una copia de seguridad. Hola planeación artículo proporciona información más detallada acerca de la copia de seguridad de las máquinas virtuales.

* [Copia de seguridad de máquinas virtuales](backup-azure-vms.md)
* [Planeación de la infraestructura de copia de seguridad de máquinas virtuales](backup-azure-vms-introduction.md)
* [Administración de copias de seguridad de máquinas virtuales](backup-azure-manage-vms.md)
