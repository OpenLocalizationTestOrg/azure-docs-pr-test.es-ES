---
title: aaaTroubleshoot grupos de seguridad de red - Portal | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot grupos de seguridad de red en la implementación de Azure Resource Manager Hola modelados con hello Portal de Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Solucionar problemas de grupos de seguridad de red mediante Hola Portal de Azure
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Si configura los grupos de seguridad de red (NSG) en la máquina virtual (VM) y están experimentando problemas de conectividad de la máquina virtual, este artículo proporciona información general sobre las capacidades de diagnóstico para los NSG toohelp seguir solucionando el problema.

Los NSG permiten tipos de hello toocontrol de tráfico que fluyen dentro y fuera de sus máquinas virtuales (VM). Los NSG pueden toosubnets aplicados en una red Virtual de Azure (VNet), interfaces de red (NIC) o ambos. Hola efectivo reglas que se aplican tooa NIC son una agregación de reglas de Hola que existan en hello NSG aplicadas tooa hello y formación subred está conectado a. Las reglas en estos NSG a veces pueden entrar en conflicto entre sí y afectar la conectividad de red de la máquina virtual.  

Puede ver todas las reglas de seguridad eficaz Hola desde sus NSG, tal como se aplica en NIC de la máquina virtual. Este artículo muestra cómo los problemas de conectividad VM tootroubleshoot utilizando estas reglas en Hola modelo de implementación de Azure Resource Manager. Si no está familiarizado con conceptos de red virtual y NSG, leer hello [red Virtual](virtual-networks-overview.md) y [grupos de seguridad de red](virtual-networks-nsg.md) artículos de información general.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Utilizando el flujo de tráfico de las reglas de seguridad efectivo tootroubleshoot VM
escenario de Hola que sigue es un ejemplo de un problema de conexión comunes:

Una máquina virtual denominada *VM1* forma parte de una subred *Subnet1* dentro de una red virtual denominada *WestUS VNet1*. Un toohello de tooconnect de intento de máquinas virtuales mediante RDP a través del puerto TCP 3389 se produce un error. Los NSG se aplican en ambos Hola NIC *VM1 NIC1* y Hola subred *subred1*. Se permite tráfico tooTCP puerto 3389 en hello NSG asociado a la interfaz de red de hello *VM1 NIC1*; sin embargo, produce un error de tooVM1 puerto 3389 de ping de TCP.

Aunque este ejemplo utiliza el puerto TCP 3389, Hola lo siguiente puede ser usado toodetermine errores de conexión entrantes y salientes a través de cualquier puerto.

### <a name="vm"></a>Visualización de las reglas de seguridad vigentes para una máquina virtual
Completar Hola siguiendo los pasos tootroubleshoot NSG para una máquina virtual:

Puede ver una lista completa de reglas de seguridad eficaz de hello en una NIC de hello propia máquina virtual. También puede agregar, modificar y eliminar reglas del NSG NIC y subred de hoja de reglas efectivo de hello, si tiene permisos tooperform estas operaciones.

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **más servicios**, a continuación, haga clic en **máquinas virtuales** en lista de Hola que aparece.
3. Seleccione una máquina virtual tootroubleshoot de lista de Hola que aparece y aparece una hoja de máquina virtual con opciones.
4. Haga clic en **Diagnosticar y solucionar problemas** y, a continuación, seleccione un problema común. En este ejemplo, **toomy VM de Windows no se puede conectar** está seleccionada. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Pasos aparecen bajo el problema de hello, como se muestra en hello después de imagen: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Haga clic en *las reglas del grupo de seguridad eficaz* en lista de Hola de pasos recomendados.
6. Hola **obtener reglas de seguridad eficaz** aparece hoja, como se muestra en hello después de imagen:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Tenga en cuenta Hola siguientes secciones de imagen de hello:
   
   * **Ámbito:** establecido demasiado*VM1*, Hola VM seleccionado en el paso 3.
   * **Interfaz de red:***VM1- NIC1* está seleccionada. Una máquina virtual puede tener varias interfaces de red (NIC). Cada NIC puede tener sus propias reglas de seguridad vigentes. Cuando solucione problemas, puede que necesite reglas de seguridad eficaz de tooview Hola para cada NIC.
   * **Los asociados NSG:** NSG pueden ser aplicada tooboth Hola Hola y NIC subred Hola NIC está conectada a. En la imagen de hello, un NSG ha sido aplicada tooboth Hola NIC y Hola la subred a que está conectado. Puede hacer clic en los nombres de NSG hello toodirectly modificar reglas de hello NSG.
   * **Pestaña VM1 nsg:** lista de Hola de reglas que se muestran en la imagen de hello es hello NSG apliquen toohello equipo NIC. Azure crea varias reglas predeterminadas cuando se crea un NSG. No se puede quitar las reglas predeterminadas de hello, pero puede invalidar con las reglas de prioridad más alta. más información acerca de las reglas predeterminadas, leer hello toolearn [información general NSG](virtual-networks-nsg.md#default-rules) artículo.
   * **Columna de destino:** algunas de las reglas de hello con texto en la columna de hello, mientras que otros prefijos de direcciones. texto Hello es el nombre de Hola de regla de seguridad de manera predeterminada etiquetas aplicadas toohello cuando se creó. etiquetas de Hello son identificadores proporcionados por el sistema que representan varios prefijos. Seleccionar una regla con una etiqueta, como *AllowInternetOutBound*, enumera los prefijos de Hola Hola **prefijos de dirección** hoja.
   * **Descarga:** lista Hola de reglas puede ser largo. Puede descargar un archivo .csv de reglas de hello para el análisis sin conexión, haga clic en **descargar** y guardar el archivo hello.
   * **AllowRDP** regla de entrada: esta regla permite toohello de las conexiones RDP máquina virtual.
7. Haga clic en hello **NSG subred1** ficha tooview Hola efectivo aplican las reglas de hello NSG toohello subred, como se muestra en hello después de la imagen: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Hola aviso *denyRDP* **entrada** regla. Las reglas de entrada aplicadas en la subred de Hola se evalúan antes que las reglas que se aplican en la interfaz de red de Hola. Puesto que Hola denegar la regla se aplica en la subred de hello, Hola solicitud tooconnect tooTCP 3389 produce un error, porque regla de permiso de hello en hello NIC nunca se evalúa. 
   
    Hola *denyRDP* regla es el motivo de hello ¿por qué se producen errores en hello conexión RDP. Quitando debería resolver el problema de Hola.
   
   > [!NOTE]
   > Si Hola VM asociadas con hello NIC no está en estado de ejecución, o los NSG no hayan sido aplicada toohello NIC o la subred, no se muestra ninguna regla.
   > 
   > 
8. reglas NSG tooedit, haga clic en *subred1 NSG* en hello **NSG asociados** sección.
   Se abrirá hello **NSG subred1** hoja. Puede editar directamente las reglas de hello haciendo clic en **reglas de seguridad de entrada**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Después de quitar hello *denyRDP* regla de entrada en hello **subred1 NSG** y agregando un *allowRDP* regla, lista de reglas efectivo de hello aspecto Hola después de imagen:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Confirme que el puerto TCP 3389 está abierto abriendo una toohello de conexión RDP VM o utilizando la herramienta de PsPing Hola. Se puede obtener más información acerca de PsPing por leer hello [página de descarga de PsPing](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Visualización de las reglas de seguridad vigentes para una interfaz de red
Si se ve afectado al flujo de tráfico de la máquina virtual de una NIC específica, puede ver una lista completa de reglas efectivo Hola de Hola NIC desde el contexto de interfaces de red de hello siguiendo Hola pasos:

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **más servicios**, a continuación, haga clic en **interfaces de red** en lista de Hola que aparece.
3. Seleccione una interfaz de red. Hola después de la imagen, se denomina una NIC *VM1 NIC1* está seleccionada.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Tenga en cuenta que hello **ámbito** se establece la interfaz de red toohello seleccionado. Obtenga más información sobre toolearn Hola información adicional que se muestra, lea el paso 6 de Hola **solucionar NSG para una máquina virtual** sección de este artículo.
   
   > [!NOTE]
   > Si se quita un NSG de una interfaz de red, subred hello NSG todavía es eficaz en hello dado NIC. En este caso, salida de hello solo muestra las reglas de la subred de hello NSG. Las reglas solo aparecen si Hola NIC está adjunto tooa máquina virtual.
   > 
   > 
4. Puede editar directamente las reglas para los NSG asociados con una subred y una NIC. toolearn cómo hacerlo, vea el paso 8 de hello **ver las reglas de seguridad eficaz para una máquina virtual** sección de este artículo.

## <a name="nsg"></a>Visualización de las reglas de seguridad vigentes para un grupo de seguridad de red (NSG)
Para modificar las reglas NSG, puede que desee impacto de hello tooreview de reglas de Hola que se agrega en una máquina virtual concreta. Puede ver una lista completa de reglas de seguridad eficaz de Hola para todos Hola NIC que se aplica un NSG determinado, sin necesidad de contexto tooswitch de hello dada la hoja NSG. tootroubleshoot reglas efectivo en un NSG, Hola completa pasos:

1. Portal de Azure en https://portal.azure.com de toohello de inicio de sesión.
2. Haga clic en **más servicios**, a continuación, haga clic en **grupos de seguridad de red** en lista de Hola que aparece.
3. Seleccione un NSG. Hola después de la imagen, se seleccionó un NSG denominado VM1 nsg.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Tenga en cuenta Hola siguientes secciones de la imagen anterior de hello:
   
   * **Ámbito:** establecer toohello NSG seleccionado.
   * **Máquina virtual:** cuando un NSG es tooa aplicado subred, se tooall aplicado interfaces tooall adjunto máquinas virtuales conectados toohello subred. Esta lista muestra todas las máquinas virtuales a las que se aplica este NSG. Puede seleccionar todas las máquinas virtuales de lista de Hola.
     
     > [!NOTE]
     > Si un NSG está aplicada tooonly una subred vacía, no se mostrarán las máquinas virtuales. Si un NSG está aplicada tooa NIC que no está asociado a una máquina virtual, las NIC también no aparecerá. 
     > 
     > 
   * **Interfaz de red:** una VM puede tener varias interfaces de red. Puede seleccionar una interfaz de red toohello adjunto seleccionado de máquina virtual.
   * **AssociatedNSGs:** en cualquier momento, puede tener una NIC hasta tootwo NSG efectivo, uno aplicado toohello NIC y Hola otra subred toohello. Aunque el ámbito de Hola se selecciona como VM1-nsg, si Hola NIC tiene una subred efectivo NSG, salida de hello mostrará ambos NSG.
4. Puede editar directamente las reglas para los NSG asociados con una subred o una NIC. toolearn cómo hacerlo, vea el paso 8 de hello **ver las reglas de seguridad eficaz para una máquina virtual** sección de este artículo.

Obtenga más información sobre toolearn Hola información adicional que se muestra, lea el paso 6 de Hola **ver las reglas de seguridad eficaz para una máquina virtual** sección de este artículo.

> [!NOTE]
> Aunque una subred y una NIC pueden tener solo un toothem NSG aplica, puede ser un NSG toomultiple asociado de NIC y varias subredes.
> 
> 

## <a name="considerations"></a>Consideraciones
Considere la posibilidad de hello siguientes puntos al solucionar problemas de conectividad:

* Reglas NSG predeterminadas bloqueará el acceso entrante de hello tráfico entrante de internet y sólo permitir red virtual. Las reglas deben agregarse explícitamente tooallow acceso de entrada desde Internet, según sea necesario.
* Si no hay ninguna regla de seguridad NSG causa toofail de conectividad de red de la máquina virtual, el problema de hello causa puede ser:
  * Software de firewall que se ejecuta en el sistema operativo de la máquina virtual de Hola
  * Rutas configuradas para dispositivos virtuales o para el tráfico local. Tráfico de Internet puede ser redirigido tooon local a través de tunelización forzada. Una conexión RDP/SSH de hello Internet tooyour VM no funcionen con esta configuración, dependiendo de cómo administra el hardware de red local de hello este tráfico. Hola de lectura [solución de problemas de rutas](virtual-network-routes-troubleshoot-powershell.md) artículo toolearn cómo toodiagnose dirigir los problemas que pueden ser y se impide Hola flujo de tráfico dentro y fuera de Hola máquina virtual. 
* Si ha emparejar las redes virtuales, de forma predeterminada, Hola etiqueta VIRTUAL_NETWORK expandirá automáticamente tooinclude prefijos para emparejar redes virtuales. Puede ver estos prefijos en hello **ExpandedAddressPrefix** enumerar, tootroubleshoot cualquier tooVNet relacionados problemas emparejamiento conectividad. 
* Las reglas de seguridad eficaz solo se muestran si hay que un NSG asociada a la máquina virtual de hello NIC y o subred. 
* Si no hay ningún NSG asociados con hello NIC o subred y tiene una dirección IP pública asignada tooyour VM, todos los puertos se abrirán para el acceso entrante y saliente. Si Hola máquina virtual tiene una dirección IP pública, aplicar los NSG toohello NIC o la subred se recomienda.

