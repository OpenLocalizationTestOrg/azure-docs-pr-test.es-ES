---
title: aaaInstall un bosque de Active Directory en una red virtual de Azure | Documentos de Microsoft
description: "Un tutorial que explica cómo toocreate un nuevo servicio Active Directory del bosque en una máquina virtual (VM) en una red Virtual de Azure."
services: active-directory, virtual-network
keywords: "máquina virtual de Active Directory, instalación de un bosque de Active Directory, vídeos de Azure Active Directory  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Instalación de un bosque nuevo de Active Directory en una red virtual de Azure
Este tema se muestra cómo toocreate un nuevo Windows Server Active Directory entorno en red virtual de Azure en una máquina virtual (VM) en un [red virtual de Azure](../virtual-network/virtual-networks-overview.md). En este caso, Hola red virtual de Azure no es red local de tooan conectado.

Es posible que también le interesen los siguientes temas relacionados:

* Para ver un vídeo que muestra estos pasos, vea [cómo tooinstall un nuevo servicio Active Directory del bosque en una red virtual de Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* Las opciones disponibles son [configurar una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md) y, a continuación, instalar un nuevo bosque o ampliar un tooan de bosque local red virtual de Azure. Para seguir esos pasos, consulte [Instalación de un controlador de dominio réplica de Active Directory en una red virtual de Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Para obtener una orientación en cuanto a conceptos sobre la instalación de los Servicios de dominio de Active Directory (AD DS) en una red virtual de Azure, consulte [Directrices para implementar Windows Server Active Directory en máquinas virtuales de Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagrama del escenario
En este escenario, los usuarios externos necesitan que las aplicaciones de tooaccess que se ejecutan en servidores unidos a un dominio. máquinas virtuales de Hola que se ejecutan en servidores de aplicaciones de Hola y Hola VM que se ejecutan los controladores de dominio se instalan instalada en sus propios servicios de nube en una red virtual de Azure. También se incluyen dentro de un conjunto de disponibilidad para mayor tolerancia a errores.

![Bosque de Active Directory en una máquina virtual de una red virtual de Azure ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>¿En qué se diferencia del entorno local?
No existe mucha diferencia entre instalar un controlador de dominio en Azure y una instalación en el entorno local. diferencias principales de Hola se muestran en hello en la tabla siguiente.

| tooconfigure... | Local | red virtual de Azure |
| --- | --- | --- |
| **Dirección IP para el controlador de dominio de Hola** |Asignar dirección IP estática en las propiedades de adaptador de red de Hola |Ejecute hello Set-AzureStaticVNetIP cmdlet tooassign una dirección IP estática |
| **Resolución de clientes DNS** |Establecer dirección del servidor preferido y alternativo DNS en hello propiedades de adaptador de red de los miembros del dominio |Establecer dirección del servidor DNS en las propiedades de red virtual de Hola Hola |
| **Almacenamiento de base de datos de Active Directory** |Si lo desea cambiar la ubicación de almacenamiento predeterminada de Hola desde C:\ |Necesita toochange ubicación de almacenamiento predeterminada de C:\ |

## <a name="create-an-azure-virtual-network"></a>Creación de una red virtual de Azure
1. Inicie sesión en toohello portal de Azure clásico.
2. Cree una red virtual. Haga clic en **Redes** > **Crear una red virtual**. Utilizar valores de hello en hello después el Asistente de tabla toocomplete Hola.

   | En esta página del asistente… | Especifique estos valores |
   | --- | --- |
   |  **Detalles de red virtual** |<p>Nombre: escriba un nombre para la red virtual.</p><p>Región: Elija la región más cercana de Hola</p> |
   |  **DNS y VPN** |<p>Deje el servidor DNS en blanco.</p><p>No seleccione ninguna de las opciones VPN.</p> |
   |  **Espacios de direcciones de la red virtual** |<p>Nombre de subred: escriba un nombre para la subred.</p><p>IP inicial: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Crear el controlador de dominio de las máquinas virtuales toorun hello y roles de servidor DNS
Repita Hola siguiendo los pasos toocreate función de DC de Hola de máquinas virtuales toohost según sea necesario. Debe implementar al menos dos redundancia y tolerancia a errores tooprovide controladores de dominio virtual. Si hello red virtual de Azure incluye al menos dos controladores de dominio que están configurados de forma similar (es decir, son ambos catálogos globales, servidor DNS de ejecución, y no contiene ningún rol FSMO etc.), a continuación, colocar las máquinas virtuales de Hola que se ejecutan los controladores de dominio en un conjunto de disponibilidad para mayor tolerancia a errores.

Hola toocreate máquinas virtuales mediante Windows PowerShell en lugar de hello interfaz de usuario, consulte [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. En el portal clásico de hello, haga clic en **New** > **proceso** > **Máquina Virtual** > **de la galería**. Usar hello después el Asistente de hello toocomplete de valores. Acepte el valor de predeterminado de Hola para una configuración a menos que otro valor sugerido o necesarias.

   | En esta página del asistente… | Especifique estos valores |
   | --- | --- |
   |  **Elija una imagen** |Windows Server 2012 R2 Datacenter |
   |  **Configuración de la máquina virtual** |<p>Nombre de máquina virtual: escriba un nombre de etiqueta única (por ejemplo, AzureDC1).</p><p>Nuevo nombre de usuario: Tipo hello nombre de un usuario. Este usuario será un miembro del grupo de administradores local de hello en hello máquina virtual. Necesitará este toosign nombre en toohello VM para hello primera vez. cuenta integrada de Hello denominada administrador no funcionará.</p><p>Nueva contraseña/Confirmar: Escriba una contraseña</p> |
   |  **Configuración de la máquina virtual** |<p>Servicio en la nube: Elija <b>crear un nuevo servicio de nube</b> para hello primera máquina virtual y seleccione esa mismo nombre de servicio de nube al crear más máquinas virtuales que va a hospedar Hola rol de controlador de dominio.</p><p>Nombre de DNS del servicio en la nube: Especifique un nombre único global</p><p>Región/grupo de afinidad/red Virtual: especificar el nombre de red virtual de hello (por ejemplo, WestUSVNet).</p><p>Cuenta de almacenamiento: Elija <b>usar una cuenta de almacenamiento generada automáticamente</b> para hello primera VM y a continuación, seleccione el nombre misma cuenta de almacenamiento al crear más máquinas virtuales que va a hospedar Hola rol de controlador de dominio.</p><p>Conjunto de disponibilidad: elija <b>Crear un conjunto de disponibilidad</b>.</p><p>Nombre del conjunto de disponibilidad: escriba un nombre para la disponibilidad de hello establecido al crear Hola primera máquina virtual y, a continuación, seleccione el mismo nombre al crear más máquinas virtuales.</p> |
   |  **Configuración de la máquina virtual** |<p>Seleccione <b>Hola instalar agente de máquina virtual</b> y otras extensiones que necesita.</p> |
2. Adjuntar una máquina virtual que se ejecutará el rol de servidor de controlador de dominio de hello tooeach de disco. disco adicional de Hello es la base de datos de hello AD toostore necesarios, los registros y SYSVOL. Especifique un tamaño de disco hello (por ejemplo, 10 GB) y dejar hello **preferencia de caché de Host** establecido demasiado**ninguno**. Para obtener pasos hello, consulte [cómo tooAttach una máquina Virtual de Windows de disco de datos tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Después de registrarse por primera vez en toohello máquina virtual, abra **el administrador del servidor** > **File and Storage Services** toocreate un volumen en este disco con NTFS.
4. Reservar una dirección IP estática para las máquinas virtuales que se ejecutarán el rol de controlador de dominio de Hola. tooreserve una dirección IP estática, descargar Hola instalador de plataforma Web de Microsoft y [instalar Azure PowerShell](/powershell/azure/overview) y ejecute el cmdlet Set-AzureStaticVNetIP Hola. Por ejemplo:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Para obtener más información acerca de cómo establecer una dirección IP estática, consulte [Configuración de una dirección IP interna estática para una máquina virtual](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Instalación de Windows Server Active Directory
Usar Hola misma rutina demasiado[instalar AD DS](https://technet.microsoft.com/library/jj574166.aspx) usar local (es decir, puede usar Hola interfaz de usuario, un archivo de respuesta o Windows PowerShell). Debe tooinstall de credenciales de administrador de tooprovide un bosque nuevo. ubicación toospecify Hola Hola base de datos de Active Directory, los registros y SYSVOL, cambian ubicación de almacenamiento predeterminada de Hola de hello unidad toohello datos adicionales disco del sistema operativo que ha adjuntado toohello máquina virtual.

Una vez finalizada la instalación del controlador de dominio de hello, vuelva a conectar toohello VM y toohello controlador de dominio de inicio de sesión. Recordar las credenciales de dominio de toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Restablecer el servidor de DNS Hola Hola red virtual de Azure
1. Restablecer la configuración de reenviador DNS de hello en hello nuevo controlador de dominio o servidor DNS.
   1. En el administrador del servidor, haga clic en **Herramientas** > **DNS**.
   2. En **el Administrador de DNS**, haga clic en nombre de saludo del servidor DNS de Hola y haga clic en **propiedades**.
   3. En hello **reenviadores** pestaña, haga clic en la dirección IP de Hola de reenviador de Hola y haga clic en **editar**.  Seleccione la dirección IP de Hola y haga clic en **eliminar**.
   4. Haga clic en **Aceptar** tooclose editor de Hola y **Aceptar** propiedades del servidor tooclose Hola DNS nuevo.
2. Actualizar configuración de servidor DNS de hello para la red virtual de Hola.
   1. Haga clic en **redes virtuales** > haga doble clic en la red virtual de hello creaste > **configurar** > **servidores DNS**, escriba el nombre de Hola y Hola DIP de uno de Hola máquinas virtuales que se ejecuta la función de servidor DC/DNS de Hola y haga clic en **guardar**.
   2. Seleccione Hola máquina virtual y haga clic en **reiniciar** tootrigger configuración de resolución DNS Hola VM tooconfigure con la dirección IP de Hola de nuevo servidor DNS Hola.

## <a name="create-vms-for-domain-members"></a>Cree máquinas virtuales para miembros de dominio
1. Repita Hola siguiendo los pasos toocreate máquinas virtuales toorun como servidores de aplicaciones. Acepte el valor de predeterminado de Hola para una configuración a menos que otro valor sugerido o necesarias.

   | En esta página del asistente… | Especifique estos valores |
   | --- | --- |
   |  **Elija una imagen** |Windows Server 2012 R2 Datacenter |
   |  **Configuración de la máquina virtual** |<p>Nombre de máquina virtual: escriba un nombre de etiqueta única (por ejemplo, AppServer1).</p><p>Nuevo nombre de usuario: Tipo hello nombre de un usuario. Este usuario será un miembro del grupo de administradores local de hello en hello máquina virtual. Necesitará este toosign nombre en toohello VM para hello primera vez. cuenta integrada de Hello denominada administrador no funcionará.</p><p>Nueva contraseña/Confirmar: Escriba una contraseña</p> |
   |  **Configuración de la máquina virtual** |<p>Servicio en la nube: Elija **crear un nuevo servicio de nube** para hello primera máquina virtual y seleccione mismo nube nombre del servicio cuando se crea más máquinas virtuales que va a hospedar aplicación hello.</p><p>Nombre de DNS del servicio en la nube: Especifique un nombre único global</p><p>Región/grupo de afinidad/red Virtual: especificar el nombre de red virtual de hello (por ejemplo, WestUSVNet).</p><p>Cuenta de almacenamiento: Elija **usar una cuenta de almacenamiento generada automáticamente** para hello primera VM y a continuación, seleccione el nombre misma cuenta de almacenamiento al crear más máquinas virtuales que va a hospedar aplicación hello.</p><p>Conjunto de disponibilidad: elija **Crear un conjunto de disponibilidad**.</p><p>Nombre del conjunto de disponibilidad: escriba un nombre para la disponibilidad de hello establecido al crear Hola primera máquina virtual y, a continuación, seleccione el mismo nombre al crear más máquinas virtuales.</p> |
   |  **Configuración de la máquina virtual** |<p>Seleccione <b>Hola instalar agente de máquina virtual</b> y otras extensiones que necesita.</p> |
2. Después de cada máquina virtual se ha aprovisionado, inicie sesión y unirse a dominio toohello. En **Administrador del servidor**, haga clic en **servidor Local** > **GRUPO DE TRABAJO** > **Cambiar...** y, a continuación, seleccione **dominio** y el nombre de tipo hello del dominio local. Proporcione las credenciales de un usuario de dominio y reinicie unirse a un dominio Hola VM toocomplete Hola.

Hola toocreate máquinas virtuales mediante Windows PowerShell en lugar de hello interfaz de usuario, consulte [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Para más información acerca del uso de Windows PowerShell, consulte [Introducción a los cmdlets de Azure](/powershell/azure/overview) y [Azure Cmdlet Reference](/powershell/azure/get-started-azureps) (Referencia de cmdlets de Azure).

## <a name="see-also"></a>Otras referencias
* [¿Cómo tooinstall un nuevo servicio Active Directory del bosque en una red virtual de Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Directrices para implementar Windows Server Active Directory en máquinas virtuales de Microsoft Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Configuración de una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalación de un controlador de dominio de Active Directory de réplica en una red virtual de Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS para profesionales de TI: (01) Principios básicos sobre máquinas virtuales](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profesionales de TI: (05) Creación de redes virtuales y conectividad entre instalaciones](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md)
* [¿Cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Referencia de cmdlets de Azure](/powershell/azure/get-started-azureps)
* [Establecimiento de la dirección IP estática de Máquina virtual de Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [¿Cómo tooassign IP estática tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Instalación de un nuevo bosque de Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Introducción tooActive Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
