---
title: "aaaInstall un controlador de dominio de Active Directory de réplica en Azure | Documentos de Microsoft"
description: "Un tutorial que explica cómo tooinstall un controlador de dominio desde un local de Active Directory del bosque en una máquina virtual de Azure."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Instalación de un controlador de dominio de Active Directory de réplica en una red virtual de Azure
Este tema se muestra cómo los controladores de dominio adicionales de tooinstall (también conocido como controladores de dominio de réplica) para un dominio de Active Directory local en Azure máquinas virtuales (VM) en una red virtual de Azure.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

Es posible que también le interesen los siguientes temas relacionados:

* Opcionalmente, puede instalar un nuevo bosque de Active Directory en una red virtual. Para realizar esos pasos, consulte [Instalación de un bosque de Active Directory nuevo en una red virtual de Azure](active-directory-new-forest-virtual-machine.md).
* Para obtener una orientación en cuanto a conceptos sobre la instalación de los Servicios de dominio de Active Directory (AD DS) en una red virtual de Azure, consulte [Directrices para implementar Windows Server Active Directory en máquinas virtuales de Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagrama del escenario
En este escenario, los usuarios externos necesitan que las aplicaciones de tooaccess que se ejecutan en servidores unidos a un dominio. Hola máquinas virtuales que se ejecutan los servidores de aplicaciones de Hola y Hola controladores de dominio de réplica se instalan en una red virtual de Azure. Hello red virtual puede ser red local de toohello conectados por un [VPN de sitio a sitio](../vpn-gateway/vpn-gateway-site-to-site-create.md) conexión, tal y como se muestra en hello siguiente diagrama, o bien puede usar [ExpressRoute](../expressroute/expressroute-locations-providers.md) para una conexión más rápida.

se implementan servidores de aplicaciones de Hola y Hola controladores de dominio dentro de los servicios de nube diferente toodistribute proceso procesamiento y dentro [conjuntos de disponibilidad](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para mayor tolerancia a errores.
controladores de dominio de Hello replican entre sí y con controladores de dominio local mediante la replicación de Active Directory. No se necesitan herramientas de sincronización.

![Diagrama de un controlador de dominio de Active Directory de réplica en una red virtual de Azure][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Crear un sitio de Active Directory para hello red virtual de Azure
Es un toocreate buena idea un sitio de Active Directory que representa Hola red región toohello red virtual correspondiente. Eso ayuda a optimizar la autenticación, la replicación y otras operaciones de ubicación del controlador de dominio. Hello pasos siguientes se explica cómo toocreate un sitio y para obtener más información, consulte [agregar un nuevo sitio](https://technet.microsoft.com/library/cc781496.aspx).

1. Abra Sitios y servicios de Active Directory: **Administrador de servidores** > **Herramientas** > **Sitios y servicios de Active Directory**.
2. Crear un área de hello toorepresent de sitio en la que creó una red virtual de Azure: haga clic en **sitios** > **acción** > **nuevo sitio** > tipo nombre de Hola de nuevo sitio hello, como Azure US West > seleccione un vínculo de sitio > **Aceptar**.
3. Crear una subred y asociar al nuevo sitio hello: haga doble clic en **sitios** > haga clic en **subredes** > **nueva subred** > escriba el intervalo de direcciones IP de Hola red virtual de Hello (como 10.1.0.0/16 en el diagrama del escenario de hello) > seleccione Hola nuevo sitio de Azure > **Aceptar**.

## <a name="create-an-azure-virtual-network"></a>Creación de una red virtual de Azure
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **New** > **servicios de red** > **red Virtual**  >  **Creación personalizada** y siguiente de hello use valores Asistente de hello toocomplete.

   | En esta página del asistente… | Especifique estos valores |
   | --- | --- |
   |  **Detalles de red virtual** |<p>Nombre: Escriba un nombre para la red virtual de hello, como WestUSVNet.</p><p>Región: Elija la región más cercana de Hola.</p> |
   |  **Conectividad DNS y VPN** |<p>Servidores DNS: Especificar nombre de Hola y dirección IP de uno o más servidores DNS local.</p><p>Conectividad: seleccione **Configurar una VPN de sitio a sitio**.</p><p>Red local: especifique una nueva red local.</p><p>Si va a usar ExpressRoute en lugar de una VPN, consulte [Configuración de una conexión ExpressRoute mediante un proveedor de Exchange](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Conectividad de sitio a sitio** |<p>Nombre: Escriba un nombre para la red local de Hola.</p><p>Dirección IP del dispositivo VPN: especifique la dirección IP pública de hello de dispositivo de Hola que se conectará toohello de red virtual. no se encuentra el dispositivo VPN de Hello detrás de un dispositivo NAT.</p><p>Dirección: Especificar intervalos de direcciones de hello para la red local (por ejemplo, 192.168.0.0/16 en el diagrama del escenario de hello).</p> |
   |  **Espacios de direcciones de la red virtual** |<p>Espacio de direcciones: Especifique el intervalo de direcciones IP de Hola para máquinas virtuales que desea toorun Hola red virtual de Azure (por ejemplo, 10.1.0.0/16 en el diagrama del escenario de hello). Este intervalo de direcciones no puede solaparse con los intervalos de direcciones de Hola de red local de Hola.</p><p>Subredes: Especifique un nombre y una dirección para una subred para servidores de aplicaciones de hello (como front-end, 10.1.1.0/24) y para hello controladores de dominio (como back-end, 10.1.2.0/24).</p><p>Haga clic en **Agregar subred de puerta de enlace**.</p> |
2. A continuación, configurará toocreate de puerta de enlace de red virtual de hello una conexión VPN de sitio a sitio segura. Vea [configurar una puerta de enlace de red Virtual](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) para obtener instrucciones de Hola.
3. Crear Hola conexión de VPN de sitio a sitio entre la nueva red virtual de Hola y el dispositivo VPN local. Vea [configurar una puerta de enlace de red Virtual](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) para obtener instrucciones de Hola.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Crear máquinas virtuales de Azure para hello roles de controlador de dominio
Repita Hola siguiendo los pasos toocreate función de DC de Hola de máquinas virtuales toohost según sea necesario. Debe implementar al menos dos redundancia y tolerancia a errores tooprovide controladores de dominio virtual. Si hello red virtual de Azure incluye al menos dos controladores de dominio que están configurados de forma similar (es decir, son ambos catálogos globales, servidor DNS de ejecución, y no contiene ningún rol FSMO etc.), a continuación, colocar las máquinas virtuales de Hola que se ejecutan los controladores de dominio en un conjunto de disponibilidad para mayor tolerancia a errores.
Hola toocreate máquinas virtuales mediante Windows PowerShell en lugar de hello interfaz de usuario, consulte [toocreate usar Azure PowerShell y preconfigurar máquinas virtuales basadas en Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **New** > **proceso** > **Máquina Virtual**  >  **De galería**. Usar hello después el Asistente de hello toocomplete de valores. Acepte el valor de predeterminado de Hola para una configuración a menos que otro valor sugerido o necesarias.

   | En esta página del asistente… | Especifique estos valores |
   | --- | --- |
   |  **Elija una imagen** |Windows Server 2012 R2 Datacenter |
   |  **Configuración de la máquina virtual** |<p>Nombre de máquina virtual: escriba un nombre de etiqueta única (por ejemplo, AzureDC1).</p><p>Nuevo nombre de usuario: Tipo hello nombre de un usuario. Este usuario será un miembro del grupo de administradores local de hello en hello máquina virtual. Necesitará este toosign nombre en toohello VM para hello primera vez. cuenta integrada de Hello denominada administrador no funcionará.</p><p>Nueva contraseña/Confirmar: Escriba una contraseña</p> |
   |  **Configuración de la máquina virtual** |<p>Servicio en la nube: Elija <b>crear un nuevo servicio de nube</b> para hello primera máquina virtual y seleccione esa mismo nombre de servicio de nube al crear más máquinas virtuales que va a hospedar Hola rol de controlador de dominio.</p><p>Nombre de DNS del servicio en la nube: Especifique un nombre único global</p><p>Región/grupo de afinidad/red Virtual: especificar el nombre de red virtual de hello (por ejemplo, WestUSVNet).</p><p>Cuenta de almacenamiento: Elija <b>usar una cuenta de almacenamiento generada automáticamente</b> para hello primera VM y a continuación, seleccione el nombre misma cuenta de almacenamiento al crear más máquinas virtuales que va a hospedar Hola rol de controlador de dominio.</p><p>Conjunto de disponibilidad: elija <b>Crear un conjunto de disponibilidad</b>.</p><p>Nombre del conjunto de disponibilidad: escriba un nombre para la disponibilidad de hello establecido al crear Hola primera máquina virtual y, a continuación, seleccione el mismo nombre al crear más máquinas virtuales.</p> |
   |  **Configuración de la máquina virtual** |<p>Seleccione <b>Hola instalar agente de máquina virtual</b> y otras extensiones que necesita.</p> |
2. Adjuntar una máquina virtual que se ejecutará el rol de servidor de controlador de dominio de hello tooeach de disco. disco adicional de Hello es la base de datos de hello AD toostore necesarios, los registros y SYSVOL. Especifique un tamaño de disco hello (por ejemplo, 10 GB) y dejar hello **preferencia de caché de Host** establecido demasiado**ninguno**. Para obtener pasos hello, consulte [cómo tooAttach una máquina Virtual de Windows de disco de datos tooa](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Después de registrarse por primera vez en toohello máquina virtual, abra **el administrador del servidor** > **File and Storage Services** toocreate un volumen en este disco con NTFS.
4. Reservar una dirección IP estática para las máquinas virtuales que se ejecutarán el rol de controlador de dominio de Hola. tooreserve una dirección IP estática, descargar Hola instalador de plataforma Web de Microsoft y [instalar Azure PowerShell](/powershell/azure/overview) y ejecute el cmdlet Set-AzureStaticVNetIP Hola. Por ejemplo:

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM

Para obtener más información acerca de cómo establecer una dirección IP estática, consulte [Configuración de una dirección IP interna estática para una máquina virtual](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Instalar AD DS en máquinas virtuales de Azure
Inicie sesión en tooa VM y compruebe que dispone de conectividad a través de tooresources de conexión de sitio a sitio VPN o ExpressRoute de hello en la red local. A continuación, instalar AD DS en hello máquinas virtuales de Azure. Puede usar el mismo proceso que usa tooinstall un controlador de dominio adicional en la red local (interfaz de usuario, Windows PowerShell o un archivo de respuesta). Tal y como se instala AD DS, asegúrese de que especificar el nuevo volumen hello para la ubicación de Hola de hello base de datos de AD, registros y SYSVOL. Si necesita hacer un repaso sobre la instalación de AD DS, consulte [Instalar servicios de dominio de Active Directory (nivel 100)](https://technet.microsoft.com/library/hh472162.aspx) o [Instalar una réplica del controlador de dominio de Windows Server 2012 en un dominio existente  (nivel 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Volver a configurar el servidor DNS para la red virtual de Hola
1. Hola [portal de Azure](https://portal.azure.com), Hola **buscar recursos** cuadro, escriba *redes virtuales*, a continuación, haga clic en **redes virtuales (clásicas)** en resultados de la búsqueda de Hola. Haga clic en nombre de Hola de red virtual de hello y, a continuación, [volver a configurar direcciones IP del servidor DNS de hello para la red virtual](../virtual-network/virtual-network-manage-network.md#dns-servers) asignar las direcciones IP estáticas de toouse hello toohello controladores de dominio de réplica en lugar de direcciones IP de Hola de un DNS local servidores.
2. Haga clic en tooensure que todas las réplicas de hello máquinas virtuales de controlador de dominio de red virtual de Hola se configuran con toouse los servidores DNS en la red virtual de hello, **máquinas virtuales**, haga clic en la columna de estado de Hola para cada máquina virtual y, a continuación, haga clic en **reiniciar** . Espere hasta que se muestra de Hola VM **ejecutando** estado antes de intentar toosign en él.

## <a name="create-vms-for-application-servers"></a>Crear máquinas virtuales para servidores de aplicaciones
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

## <a name="additional-resources"></a>Recursos adicionales
* [Directrices para implementar Windows Server Active Directory en máquinas virtuales de Microsoft Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [¿Cómo tooupload locales existentes tooAzure de controladores de dominio de Hyper-V mediante PowerShell de Azure](http://support.microsoft.com/kb/2904015)
* [Instalación de un bosque nuevo de Active Directory en una red virtual de Azure](active-directory-new-forest-virtual-machine.md)
* [Red virtual de Azure](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IaaS para profesionales de TI: (01) Principios básicos sobre máquinas virtuales](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profesionales de TI: (05) Creación de redes virtuales y conectividad entre instalaciones](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Cmdlets de administración de Azure](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
