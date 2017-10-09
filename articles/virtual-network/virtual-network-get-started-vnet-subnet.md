---
title: aaaCreate red de su primera Virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red Virtual de Azure (VNet), se conectan dos máquinas virtuales (VM) toohello red virtual y toohello las máquinas virtuales."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Creación de su primera red virtual

Obtener información sobre cómo crear dos máquinas virtuales (VM) toocreate una red virtual (VNet) con dos subredes y conectar cada tooone VM de subredes de hello, tal y como se muestra en hello después de la imagen:

![Diagrama de red virtual](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Una red virtual (VNet) es una representación de su propia red en la nube de Hola. Puede controlar la configuración de red de Azure y definir bloques de direcciones DHCP, la configuración de DNS, las directivas de seguridad y el enrutamiento. más información acerca de conceptos de red virtual, leer hello toolearn [información general de la red Virtual](virtual-networks-overview.md) artículo. Hola completa se muestra en figura Hola de pasos toocreate Hola recursos siguientes:

1. [Cree una red virtual con dos subredes](#create-vnet)
2. [Crear dos máquinas virtuales, cada uno con una interfaz de red (NIC)](#create-vms)y asociar un tooeach (NSG) del grupo de seguridad de red NIC
3. [Conectar tooand de hello las máquinas virtuales](#connect-to-from-vms)
4. [Elimine todos los recursos](#delete-resources). Se producen cargos para algunos de los recursos de hello creados en este ejercicio, mientras que se va a aprovisionar. cargos de hello toominimize, después de completar el ejercicio de hello, asegúrese de hello toocomplete los pasos de esta sección toodelete Hola los recursos que cree.

Tendrá un conocimiento básico de cómo puede usar una red virtual después de hello completando los pasos de este artículo. Pasos siguientes se proporcionan de manera que puede aprender más acerca de cómo toouse redes virtuales en un nivel más profundo.

## <a name="create-vnet"></a>Creación de una red virtual con dos subredes

toocreate una red virtual con dos subredes, pasos de hello completa que siguen. Suelen ser distintas subredes usa flujo de hello toocontrol del tráfico entre subredes.

1. Inicie sesión en toohello [portal de Azure](<https://portal.azure.com>). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free). 
2. Hola **favoritos** panel del portal de hello, haga clic en **nuevo**.
3. Hola **New** hoja, haga clic en **red**. Hola **red** hoja, haga clic en **red Virtual**, tal y como se muestra en hello después de imagen:

    ![Diagrama de red virtual](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  Hola **red Virtual** hoja, deje *el Administrador de recursos* seleccionado como modelo de implementación de Hola y haga clic en **crear**.
5.  Hola **Crear hoja de red virtual** que aparece, escriba Hola después de valores, haga clic en **crear**:

    |**Configuración**|**Valor**|**Detalles**|
    |---|---|---|
    |**Name**|*MyVNet*|Hola nombre debe ser único en el grupo de recursos de Hola.|
    |**Espacio de direcciones**|*10.0.0.0/16*|Puede especificar cualquier espacio de direcciones que desee en notación CIDR.|
    |**Nombre de subred**|*Front-end*|nombre de subred de Hello debe ser único dentro de la red virtual de Hola.|
    |**Intervalo de direcciones de subred**|*10.0.0.0/24*| intervalo de Hola que especifique debe existir en el espacio de direcciones de hello definido para la red virtual de Hola.|
    |**Suscripción**|*[Su suscripción]*|Seleccione un saludo de toocreate red virtual de suscripción en. Una red virtual existe dentro de una sola suscripción.|
    |**Grupos de recursos**|**Crear nuevo:***MyRG*|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) artículo de información general.|
    |**Ubicación**|*Oeste de EE. UU.*| Normalmente se selecciona la ubicación de Hola que es la ubicación física de tooyour más cercano.|

    Hola toma de red virtual toocreate unos segundos. Una vez creado, vea hello Azure panel del portal.

6. Con la red virtual de hello creado, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en hello **MyVNet** red virtual en hello **todos los recursos** hoja. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir *MyVNet* en hello **filtrar por nombre...** Hola de acceso de cuadro tooeasily red virtual.
7. Hola **MyVNet** hoja se abre y muestra información sobre Hola de red virtual, como se muestra en hello después de imagen:

    ![Diagrama de red virtual](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Como se muestra en la imagen anterior de hello, haga clic en **subredes** toodisplay una lista de subredes de Hola Hola red virtual. Hello sólo la subred que existe es **front-end**, Hola subred que ha creado en el paso 5.
9. Hola MyVNet - hoja de subredes, haga clic en **+ subred** toocreate una subred con hello siguiendo la información y haga clic en **Aceptar** subred de Hola toocreate:

    |**Configuración**|**Valor**|**Detalles**|
    |---|---|---|
    |**Name**|*Back-end*|Hola nombre debe ser único dentro de la red virtual de Hola.|
    |**Intervalo de direcciones**|*10.0.1.0/24*|intervalo de Hola que especifique debe existir en el espacio de direcciones de hello definido para la red virtual de Hola.|
    |**Grupo de seguridad de red** y **Tabla de rutas**|*Ninguno* (valor predeterminado)|Los grupos de seguridad de red se tratan más adelante en este artículo. más información acerca de las rutas definidas por el usuario, leer hello toolearn [rutas definidas por el usuario](virtual-networks-udr-overview.md) artículo.|

10. Después de agrega nueva subred de hello toohello red virtual, puede cerrar hello **MyVNet – subredes** hoja y, a continuación, cierre hello **todos los recursos** hoja.

## <a name="create-vms"></a>Creación de máquinas virtuales

Con red virtual de Hola y subredes que creó, puede crear máquinas virtuales de Hola. Para este ejercicio, ambas máquinas virtuales que se ejecute el sistema de operativo de Windows Server de hello, aunque puede ejecutar cualquier sistema operativo compatible con Azure, incluidas varias distribuciones de Linux diferentes.

### <a name="create-web-server-vm"></a>Crear la máquina virtual del servidor web Hola

toocreate hello web máquina virtual del servidor, Hola completa pasos:

1. En el panel de favoritos portal Azure de hello, haga clic en **New**, **proceso**, a continuación, **Windows Server 2016 Datacenter**.
2. Hola **Windows Server 2016 Datacenter** hoja, haga clic en **crear**.
3. Hola **Fundamentos** hoja que aparece, escriba o seleccione Hola después de valores y haga clic en **Aceptar**:

    |**Configuración**| **Valor**|**Detalles**|
    |---|---|---|
    |**Name**|*MyWebServer*|Esta máquina virtual actúa como servidor web al que se conectan los recursos de Internet.|
    |**Tipo de disco de máquina virtual**|*SSD*|
    |**Nombre de usuario**|*Su elección*|
    |**Contraseña y Confirmar contraseña**|*Su elección*|
    | **Suscripción**|*<Your subscription>*|Hola suscripción debe ser Hola misma suscripción que seleccionó en el paso 5 de hello [crear una red virtual con dos subredes](#create-vnet) sección de este artículo. Hola red virtual se conecta una VM toomust existe en hello misma suscripción como Hola máquina virtual.|
    |**Grupos de recursos**|**Usar existente:** seleccione *MyRG*|Si usamos Hola al mismo grupo de recursos que hicimos con red virtual, Hola Hola recursos no tienen tooexist en hello mismo grupo de recursos.|
    |**Ubicación**|*Oeste de EE. UU.*|debe ser la ubicación de Hola Hola la misma ubicación que especificó en el paso 5 de hello [crear una red virtual con dos subredes](#create-vnet) sección de este artículo. Las máquinas virtuales y redes virtuales que se conectan toomust Hola existen en hello misma ubicación.|

4. Hola **elegir un tamaño de** hoja, haga clic en *DS1_V2 estándar*, a continuación, haga clic en **seleccione**. Hola de lectura [tamaños de máquina virtual de Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener una lista de todos los tamaños de máquina virtual de Windows compatible con Azure.
5. Hola **configuración** hoja, escriba o seleccione Hola después de valores y haga clic en **Aceptar**:

    |**Configuración**|**Valor**|**Detalles**|
    |---|---|---|
    |**Almacenamiento: Usar discos administrados**|*Sí*||
    |**Red virtual**| Seleccione *MyVNet*|Puede seleccionar cualquier red virtual que existe en hello misma ubicación como Hola VM que se va a crear. más información acerca de las redes virtuales y subredes, leer hello toolearn [red Virtual](virtual-networks-overview.md) artículo.|
    |**Subred**|Seleccione *Front-end*.|Puede seleccionar cualquier subred que se encuentra Hola red virtual.|
    |**Dirección IP pública**|Acepte el predeterminado de Hola|Una dirección IP pública permite tooconnect toohello VM de hello Internet. más información acerca de las direcciones IP públicas, leer hello toolearn [direcciones IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artículo.|
    |**Grupo de seguridad de red (firewall)**|Acepte el predeterminado de Hola|Haga clic en hello **(nuevo) MyWebServer-nsg** portal de hello NSG predeterminado creado tooview su configuración. Hola **crear grupo de seguridad de red** hoja que se abre, observe que tiene una regla que permita el tráfico TCP/3389 (RDP) desde cualquier dirección IP de origen de entrada.|
    |**Todos los demás valores**|Acepte los valores predeterminados de Hola|más información acerca de hello restantes configuración, leer hello toolearn [acerca de las máquinas virtuales](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.|

    Grupos de seguridad de red (NSG) permiten las reglas de entrada/salida de toocreate de tipo de Hola de tráfico de red que puede fluir tooand de hello máquina virtual. De forma predeterminada, todos los toohello de tráfico entrante VM se deniega. Puede agregar más reglas de entrada para TCP/80 (HTTP) y TCP/443 (HTTPS) para un servidor web de producción. No existe ninguna regla para el tráfico saliente porque, de forma predeterminada, se permite todo. Se puede agregar o quitar el tráfico de toocontrol de reglas por las directivas. Hola de lectura [grupos de seguridad de red](virtual-networks-nsg.md) artículo toolearn más información acerca de los NSG.

6.  Hola **resumen** hoja, revise la configuración de Hola y haga clic en **Aceptar** toocreate Hola máquina virtual. Un icono de estado se muestra en el panel del portal hello como Hola que crea la máquina virtual. Puede tardar unos toocreate minutos. No es necesario toowait para él toocomplete. Puede seguir toohello el paso siguiente al Hola que se crea la máquina virtual.

### <a name="create-database-server-vm"></a>Crear la máquina virtual del servidor de base de datos de Hola

toocreate Hola servidor base de datos de máquina virtual, Hola completa pasos:

1.  En el panel de favoritos de hello, haga clic en **New**, **proceso**, a continuación, **Windows Server 2016 Datacenter**.
2.  Hola **Windows Server 2016 Datacenter** hoja, haga clic en **crear**.
3.  Hola **hoja de conceptos básicos sobre la**, escriba o seleccione Hola después de valores y luego haga clic en **Aceptar**:

    |**Configuración**|**Valor**|**Detalles**|
    |---|---|---|
    |**Name**|*MyDBServer*|Esta máquina virtual actúa como un servidor de base de datos que se conecta el servidor web de Hola a, pero ese Hola Internet no se puede conectar a.|
    |**Tipo de disco de máquina virtual**|*SSD*||
    |**Nombre de usuario**|Su elección||
    |**Contraseña y Confirmar contraseña**|Su elección||
    |**Suscripción**|<Your subscription>|Hola suscripción debe ser Hola misma suscripción que seleccionó en el paso 5 de hello [crear una red virtual con dos subredes](#create-vnet) sección de este artículo.|
    |**Grupos de recursos**|**Usar existente:** seleccione *MyRG*|Si usamos Hola al mismo grupo de recursos que hicimos con red virtual, Hola Hola recursos no tienen tooexist en hello mismo grupo de recursos.|
    |**Ubicación**|*Oeste de EE. UU.*|debe ser la ubicación de Hola Hola la misma ubicación que especificó en el paso 5 de hello [crear una red virtual con dos subredes](#create-vnet) sección de este artículo.|

4.  Hola **elegir un tamaño de** hoja, haga clic en *DS1_V2 estándar*, a continuación, haga clic en **seleccione**.
5.  Hola **configuración** hoja, escriba o seleccione Hola después de valores y haga clic en **Aceptar**:

    |**Configuración**|**Valor**|**Detalles**|
    |----|----|---|
    |**Almacenamiento: Usar discos administrados**|*Sí*||
    |**Red virtual**|Seleccione *MyVNet*|Puede seleccionar cualquier red virtual que existe en hello misma ubicación como Hola VM que se va a crear.|
    |**Subred**|Seleccione *Back-end* haciendo clic en hello **subred** cuadro, a continuación, seleccione **Back-end** de hello **elija una subred** hoja|Puede seleccionar cualquier subred que se encuentra Hola red virtual.|
    |**Dirección IP pública**|None: haga clic en la dirección predeterminada hello, a continuación, haga clic en **ninguno** de hello **Elegir dirección IP pública** hoja|Sin una dirección IP pública, sólo se puede conectar toohello VM desde otro toohello de máquina virtual conectada misma red virtual. No se puede conectar tooit directamente desde Internet Hola.|
    |**Grupo de seguridad de red (firewall)**|Acepte el predeterminado de Hola| Como la predeterminada de hello que NSG creado para hello MyWebServer VM, esta NSG también tiene Hola mismo predeterminado regla de entrada. Podría agregar otra regla de entrada para TCP/1433 (MS SQL) para un servidor de bases de datos. No existe ninguna regla para el tráfico saliente porque, de forma predeterminada, se permite todo. Se puede agregar o quitar el tráfico de toocontrol de reglas por las directivas.|
    |**Todos los demás valores**|Acepte los valores predeterminados de Hola||

6.  Hola **resumen** hoja, revise la configuración de Hola y haga clic en **Aceptar** toocreate Hola máquina virtual. Un icono de estado se muestra en el panel del portal hello como Hola que crea la máquina virtual. Puede tardar unos toocreate minutos. No es necesario toowait para él toocomplete. Puede seguir toohello el paso siguiente al Hola que se crea la máquina virtual.

## <a name="review"></a>Revisión de los recursos

Si ha creado una red virtual y dos máquinas virtuales, portal de Azure creado varios recursos adicionales en el grupo de recursos de MyRG Hola Hola. Revise el contenido de Hola Hola MyRG del grupo de recursos siguiendo Hola pasos:

1. Hola **favoritos** panel, haga clic en **más servicios**.
2. Hola **más servicios** panel, escriba *grupos de recursos* en cuadro Hola con palabra Hola *filtro* en ella. Haga clic en **grupos de recursos** cuando se ve en hello filtra la lista.
3. Hola **grupos de recursos** panel, haga clic en hello *MyRG* grupo de recursos. Si tiene muchos grupos de recursos existente en su suscripción, puede escribir *MyRG* en cuadro de Hola que contiene texto hello *filtrar por nombre...* grupo de recursos de tooquickly acceso hello MyRG.
4.  Hola **MyRG** hoja, verá ese grupo de recursos de hello contiene 12 recursos, como se muestra en hello después de imagen:

    ![Contenido del grupo de recursos](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

más información acerca de las máquinas virtuales y discos, cuentas de almacenamiento, leer hello toolearn [Máquina Virtual](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [disco](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), y [cuenta de almacenamiento](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de información general. Puede ver Hola dos NSG Hola portal predeterminado creado por usted. También puede ver ese portal Hola creado dos recursos de la interfaz (NIC) de red. Una NIC habilita un recursos de máquina virtual tooconnect tooother sobre Hola red virtual. Hola de lectura [NIC](virtual-network-network-interface.md) artículo toolearn más información acerca de la NIC. portal de Hello también crea un recurso de dirección IP pública. Las direcciones IP públicas son una configuración para un recurso de dirección IP pública. más información acerca de las direcciones IP públicas, leer hello toolearn [direcciones IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artículo.

## <a name="connect-to-from-vms"></a>Conectar máquinas virtuales toohello

Con la red virtual y dos máquinas virtuales que se creó, puede conectarse ahora toohello las máquinas virtuales siguiendo los pasos de Hola Hola siguientes secciones:

### <a name="connect-from-internet"></a>Conectar máquina virtual del servidor web toohello de hello Internet

tooconnect toohello web máquina virtual del servidor de hello Internet, Hola completa pasos:

1. En el portal de hello, grupo de recursos de hello abierto MyRG siguiendo Hola pasos de hello [revisar recursos](#review) sección de este artículo.
2. Hola **MyRG** hoja, haga clic en hello **MyWebServer** máquina virtual.
3. Hola **MyWebServer** hoja, haga clic en **conectar**, tal y como se muestra en hello después de imagen:

    ![Conectar la máquina virtual del servidor tooweb](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Permitir su Hola de explorador toodownload *MyWebServer.rdp* de archivos, y vuelva a abrirla.
5. Si aparece un cuadro de diálogo que le informa que ese editor de Hola de conexión remota de hello no se puede comprobar, haga clic en **conectar**.
6. Al escribir sus credenciales, asegúrese de que haya iniciado sesión con el nombre de usuario de Hola y la contraseña que especificó en el paso 3 de hello [máquina virtual del servidor de web crear hello](#create-web-server-vm) sección de este artículo. Si hello **la seguridad de Windows** cuadro que aparece no muestra las credenciales correctas de hello, puede que tenga tooclick **más opciones**, a continuación, **Use otra cuenta**, por lo que puede Especificar nombre de usuario correctos de Hola y la contraseña). Haga clic en **Aceptar** tooconnect toohello máquina virtual.
7. Si recibe un **conexión a Escritorio remoto** cuadro que informa que no se puede comprobar que Hola la identidad del equipo remoto hello, haga clic en **Sí**.
8. Ya está conectado toohello MyWebServer VM de hello Internet. Deje conexión a Escritorio remoto hello pasos de hello toocomplete abierta en la sección siguiente Hola.

Hola la conexión remota es toohello la dirección IP pública asignada toohello IP dirección recursos Hola portal público creado en el paso 5 de hello [crear una red virtual con dos subredes](#create-vnet) sección de este artículo. se permite la conexión de Hello como regla predeterminada de hello creado en hello **MyWebServer nsg** toohello VM desde cualquier dirección IP de origen de entrada de NSG permiten TCP/3389 (RDP). Si intentas tooconnect toohello máquina virtual a través de cualquier otro puerto, Hola conexión genera un error, a menos que agregue reglas de entrada adicionales toohello NSG permitiendo Hola puertos adicionales.

>[!NOTE]
>Si agrega las reglas de entrada adicionales toohello NSG, asegúrese de que Hola mismos puertos están abiertos en firewall de Windows hello u Hola se produce un error de conexión.
>

### <a name="connect-to-internet"></a>Conectar toohello Internet desde el servidor de web Hola VM

tooconnect toohello saliente Internet del servidor de web Hola VM, Hola completa pasos:

1. Si aún no tiene un toohello de conexión remota MyWebServerVM abrir, asegúrese de una máquina virtual de conexión remota toohello siguiendo los pasos de Hola Hola [conectar toohello web máquina virtual del servidor de Internet de hello](#connect-from-internet) sección de este artículo.
2. Desde el escritorio de Windows hello, abra Internet Explorer. Hola **el programa de instalación de Internet Explorer 11** cuadro de diálogo, haga clic en **no usa la configuración recomendada**, a continuación, haga clic en **Aceptar**. Es hello tooaccept recomendada configuración recomendada para un servidor de producción.
3. En la barra de direcciones de Internet Explorer de hello, escriba [bing.com](http:www.bing.com). Si aparece un cuadro de diálogo de Internet Explorer, haga clic en **agregar**, a continuación, **agregar** en hello **sitios de confianza** cuadro de diálogo y haga clic en **cerrar**. Repita este proceso para cualquier otro cuadro de diálogo de Internet Explorer.
4. Página de búsqueda en Bing hello, escriba *whatsmyipaddress*, a continuación, haga clic en botón de lupa Hola. Bing devuelve Hola pública IP dirección asignada toohello pública recurso de dirección IP creado por el portal de hello cuando creaste Hola VM. Si examina la configuración de Hola para hello **MyWebServer ip** recursos, vea Hola misma dirección IP que se asigna el recurso de dirección IP pública toohello, tal y como se muestra en figura Hola que sigue. Hola IP dirección asignada tooyour VM es diferente sin embargo.

    ![Conectar la máquina virtual del servidor tooweb](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Deje conexión a Escritorio remoto hello pasos de hello toocomplete abierta en la sección siguiente Hola.

Es capaz de tooconnect toohello Internet de VM de hello porque toda la conectividad saliente de hello VM se permite de forma predeterminada. Puede limitar conectividad saliente mediante la adición de adición reglas toohello NSG aplica toohello NIC, Hola de subred toohello NIC está conectada a, o ambos.

Si Hola VM se pone en hello detiene estado (desasignada) mediante el portal de hello, puede cambiar la dirección IP pública Hola. Si necesita que IP pública Hola nunca dirección cambiar, puede utilizar el método de asignación estático de hello para la dirección IP de hello, en lugar del método de asignación dinámica de hello (que es el valor predeterminado de hello). Hola a toolearn Obtenga más información sobre las diferencias entre los métodos de asignación, leer hello [tipos y métodos de asignación de direcciones IP](virtual-network-ip-addresses-overview-arm.md) artículo.

### <a name="webserver-to-dbserver"></a>Conectar máquina virtual del servidor de base de datos de toohello de máquina virtual del servidor web Hola

tooconnect toohello base de datos servidor VM desde hello web servidor VM, Hola completa pasos:

1. Si aún no tiene un toohello de conexión remota MyWebServer VM abra, asegúrese de una VM de conexión remota toohello siguiendo los pasos de Hola Hola [conectar toohello web máquina virtual del servidor de Internet de hello](#connect-from-internet) sección de este artículo.
2. Haga clic en el botón de inicio de hello en la esquina inferior izquierda de Hola de escritorio de Windows hello, a continuación, comience a escribir *escritorio remoto*. Cuando muestre la lista del menú de inicio de hello **conexión a Escritorio remoto**, haga clic en él.
3. Hola **conexión a Escritorio remoto** diálogo cuadro, escriba *MiServidorBD* nombre_equipo hello y haga clic en **conectar**.
4. Escriba el nombre de usuario de Hola y contraseñas que ha escrito en el paso 3 de hello [máquina virtual del servidor de base de datos crear hello](#create-database-server-vm) sección de este artículo, a continuación, haga clic en **Aceptar**.
5. Si aparece un cuadro de diálogo que le informa que esa identidad Hola del equipo remoto hello no se puede comprobar, haga clic en **Sí**.
6. Deje conexión a Escritorio remoto hello servidores tooboth hello toocomplete abrir los pasos en la sección siguiente Hola.

Son toomake capaz de hello conexión toohello base de datos máquina virtual del servidor desde el servidor de web de hello VM para hello siguientes motivos:

- Las conexiones entrantes de TCP/3389 están habilitadas para cualquier dirección IP de origen predeterminado de hello NSG creado en el paso 5 de hello [máquina virtual del servidor de base de datos crear hello](#create-database-server-vm) sección de este artículo.
- Inició la conexión de Hola desde el servidor de web Hola máquina virtual, que está conectado toohello misma red virtual como máquina virtual del servidor de base de datos de Hola. tooconnect tooa máquina virtual que no tiene un tooit dirección asignada de IP pública, debe conectarse desde otro toohello de máquina virtual conectada misma red virtual, incluso si Hola máquina virtual está conectado tooa otra subred.
- Aunque hello las máquinas virtuales son subredes toodifferent conectado, Azure crea las rutas predeterminadas que habilitar la conectividad entre subredes. Puede invalidar las rutas predeterminadas de hello creando su propio sin embargo. Hola de lectura [rutas definidas por el usuario](virtual-networks-udr-overview.md) toolearn artículo más acerca del enrutamiento en Azure.

Si intentas tooinitiate un servidor de base de datos de conexión remota toohello VM de hello Internet, tal y como hizo en hello [conectar toohello web máquina virtual del servidor de hello Internet](#connect-from-internet) sección de este artículo, verá que hello **conectar** opción aparece atenuada. Conectar está deshabilitado porque no hay ningún toohello dirección asignada de IP pública de máquina virtual, por lo que no son posibles tooit las conexiones entrantes de hello Internet.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Conectar toohello Internet desde el servidor de base de datos de hello VM

Conectarse toohello saliente de Internet desde la máquina virtual del servidor de base de datos de Hola siguiendo los pasos de Hola:

1. Si aún no tiene un toohello de conexión remota MyDBServer VM abrir desde hello MyWebServer VM, Hola completa los pasos de hello [el servidor de base de datos de toohello de conectar máquinas virtuales de máquina virtual del servidor web hello](#webserver-to-dbserver) sección de este artículo.
2. Desde el escritorio de Windows hello en hello MyDBServer VM, abra Internet Explorer y responder cuadros de diálogo toohello tal y como hizo en los pasos 2 y 3 de hello [conectarse toohello Internet desde la máquina virtual del servidor web hello](#connect-to-internet) sección de este artículo.
3. En la barra de direcciones de hello, escriba [bing.com](http:www.bing.com).
4. Haga clic en **agregar** en el cuadro de diálogo de Internet Explorer de Hola que aparece, a continuación, **agregar**, a continuación, **cerrar** en hello **confianza** cuadro de diálogo de sitios. Complete estos pasos en los cuadros de diálogo adicionales que aparezcan.
5. Página de búsqueda en Bing hello, escriba *whatsmyipaddress*, a continuación, haga clic en botón de lupa Hola. Bing devuelve Hola pública IP dirección asignada actualmente toohello VM Hola infraestructura de Azure. 6. Cerrar Hola remoto escritorio toohello MyDBServer VM de hello MyWebServer VM, a continuación, cerrar toohello de conexión remota de hello MyWebServer VM.

conexión de salida de Hello toohello Internet está permitida porque todo el tráfico saliente se permite de forma predeterminada, incluso si un recurso de dirección IP público no está asignado toohello MyDBServer VM. Todas las máquinas virtuales, de forma predeterminada, son tooconnect capaz de salida toohello Internet, con o sin un toohello de recurso asignado VM pública para la dirección IP. No son toohello tooconnect capaz de dirección de IP pública de hello Internet sin embargo, que está hello toofor pueda MyWebServer VM que tiene una dirección IP pública redirigir recursos asignados.

## <a name="delete-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, Hola completa pasos:

1. grupo de recursos de MyRG tooview Hola creado en este artículo, complete los pasos 1 a 3 en hello [revisar recursos](#review) sección de este artículo. Una vez más, revise los recursos de hello en el grupo de recursos de Hola. Si ha creado el grupo de recursos de MyRG hello, por los pasos anteriores, vea 12 recursos Hola que se muestra en figura hello en el paso 4.
2. En la hoja de MyRG hello, haga clic en hello **eliminar** botón.
3. Hello portal requiere tootype Hola nombre del tooconfirm de grupo de recursos de Hola que desea que toodelete lo. Si ve recursos distinto de recursos de Hola se muestra en el paso 4 de hello [revisar recursos](#review) sección de este artículo, haga clic en **cancelar**. Si ve únicamente los recursos de hello 12 creados como parte de este artículo, escriba *MyRG* nombre de grupo de recursos de hello, a continuación, haga clic en **eliminar**. Al eliminar un grupo de recursos eliminan todos los recursos en el grupo de recursos de hello, por lo que siempre puede tooconfirm seguro de contenido de Hola de un grupo de recursos antes de eliminarlo. portal de Hello elimina todos los recursos incluidos en el grupo de recursos de hello, a continuación, elimina el grupo de recursos de hello propio. Este proceso tarda varios minutos.

## <a name="next-steps"></a>Pasos siguientes

En este ejercicio, ha creado una red virtual y dos máquinas virtuales. Ha especificado configuraciones personalizadas durante la creación de máquinas virtuales y ha aceptado otras predeterminadas. Le recomendamos que lea Hola siguientes artículos, antes de la implementación de producción redes virtuales y las máquinas virtuales, tooensure comprende todas las configuraciones disponibles:

- [Redes virtuales](virtual-networks-overview.md)
- [Direcciones IP públicas](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Interfaces de red](virtual-network-network-interface.md)
- [Grupos de seguridad de red](virtual-networks-nsg.md)
- [Máquinas virtuales](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
