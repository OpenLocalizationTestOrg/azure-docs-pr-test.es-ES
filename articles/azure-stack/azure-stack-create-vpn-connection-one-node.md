---
title: "aaaCreate una conexión de VPN de sitio a sitio entre dos redes virtuales en diferentes entornos de Kit de desarrollo de pila de Azure | Documentos de Microsoft"
description: "Procedimiento paso a paso que un administrador de la nube utiliza la conexión de VPN de toocreate un sitio a sitio entre dos entornos de Kit de desarrollo de pila de Azure de nodo único."
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: 74225a82efae7d9ca6dc08b45ff04c578fae785c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a>Creación de una conexión VPN de sitio a sitio entre dos redes virtuales en diferentes entornos de Azure Stack Development Kit
## <a name="overview"></a>Información general
Este artículo muestra cómo toocreate una conexión de VPN de sitio a sitio entre dos redes virtuales en dos entornos independientes de Kit de desarrollo de pila de Azure. Al configurar conexiones de hello, aprenderá cómo funcionan las puertas de enlace VPN en la pila de Azure.

### <a name="connection-diagram"></a>Diagrama de conexión
Hola siguiente diagrama se muestra la configuración de conexión de hello debería ser similar a cuando haya terminado.

![Configuración de una conexión VPN de sitio a sitio](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a>Antes de empezar
configuración de conexión de toocomplete hello, asegúrese de que tiene Hola siguientes elementos antes de empezar:

* Dos servidores que cumplan los requisitos de hardware del Kit de desarrollo de Azure pila hello, que se definen de hello [requisitos previos de implementación de Azure pila](azure-stack-deploy.md). Asegúrese de que Hola otros requisitos previos que aparecen en hello [artículo](azure-stack-deploy.md) completadas demasiado.
* Hola [Kit de desarrollo de Azure pila](https://azure.microsoft.com/en-us/overview/azure-stack/try/) paquete de implementación.

## <a name="deploy-hello-azure-stack-development-kit-environments"></a>Implementar entornos de hello Kit de desarrollo de pila de Azure
configuración de conexión de hello toocomplete, debe implementar dos entornos de Kit de desarrollo de pila de Azure.
> [!NOTE] 
> Para cada Kit de desarrollo de pila de Azure que se implementa, siga hello [instrucciones de implementación](azure-stack-run-powershell-script.md). En este artículo, se denominan entornos del Kit de desarrollo de Azure pila hello *POC1* y *POC2*.


## <a name="prepare-an-offer-on-poc1-and-poc2"></a>Preparación de una oferta en POC1 y POC2
En POC1 y POC2, prepare una oferta para que un usuario puede suscribirse toohello oferta e implementar máquinas virtuales de Hola. Para obtener información acerca de cómo toocreate una oferta, vea [tooyour disponibles de máquinas virtuales de hacer que los usuarios de Azure pila](azure-stack-tutorial-tenant-vm.md).

## <a name="review-and-complete-hello-network-configuration-table"></a>Revisión y la tabla de configuración de red de hello completa
Hello en la tabla siguiente resume la configuración de red de Hola para ambos entornos del Kit de desarrollo de pila de Azure. Utilice el procedimiento de Hola que aparece después de hello tooadd de tabla Hola dirección BGPNAT externo que sea específico de la red.

**Tabla de configuración de red**
|   |POC1|POC2|
|---------|---------|---------|
|Nombre de la red virtual     |VNET-01|VNET-02 |
|Espacio de direcciones de red virtual |10.0.10.0/23|10.0.20.0/23|
|Nombre de subred     |Subnet-01|Subnet-02|
|Intervalo de direcciones de subred|10.0.10.0/24 |10.0.20.0/24 |
|Subred de puerta de enlace     |10.0.11.0/24|10.0.21.0/24|
|Dirección BGPNAT externa     |         |         |

> [!NOTE]
> las direcciones IP de BGPNAT de Hello externas en el entorno de ejemplo de Hola son 10.16.167.195 para POC1 y 10.16.169.131 para POC2. Usar hello siguiendo el procedimiento toodetermine hello BGPNAT las direcciones IP externas para los hosts del Kit de desarrollo de pila de Azure y, a continuación, agregarlos toohello tabla anterior de la configuración de red.


### <a name="get-hello-ip-address-of-hello-external-adapter-of-hello-nat-vm"></a>Obtener dirección IP de Hola de adaptador externo de Hola de hello NAT VM
1. Inicie sesión en toohello máquina física de pila de Azure para POC1.
2. Editar Hola después Powershell código tooreplace su contraseña de administrador y, a continuación, ejecutar código de hello en el host de prueba de concepto de hello:

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. Agregar hello toohello red configuración tabla de direcciones IP que aparece en la sección anterior de Hola.

4. Repita este procedimiento en POC2.

## <a name="create-hello-network-resources-in-poc1"></a>Crear recursos de red de hello en POC1
Ahora cree hello POC1 recursos de red que debe tooset una de las puertas de enlace. Hola siguiendo instrucciones muestra cómo toocreate recursos de hello mediante el uso de Hola portal de usuarios. También puede usar recursos de Hola de toocreate de código de PowerShell.

![Flujo de trabajo que usa toocreate recursos](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a>Inicio de sesión como un inquilino
Un administrador de servicios puede iniciar sesión como un tootest inquilino Hola planes, ofertas y suscripciones que puedan usar sus inquilinos. Si aún no tiene una, [cree una cuenta de inquilino](azure-stack-add-new-user-aad.md) antes de iniciar sesión.

### <a name="create-hello-virtual-network-and-vm-subnet"></a>Crear red virtual de Hola y subred de VM
1. Utilice un toosign de cuenta de inquilino en el portal de usuarios de toohello.
2. En el portal de usuarios de hello, seleccione **nuevo**.

    ![Creación de una nueva red virtual](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
4. Seleccione **Red virtual**.
5. Para **nombre**, **espacio de direcciones**, **nombre de subred**, y **intervalo de direcciones de subred**, usar los valores de hello anteriormente aparecen en Hola red tabla de configuración.
6. En **suscripción**, aparece la suscripción de Hola que creó anteriormente.
7. Para **Grupo de recursos**, puede crear un grupo de recursos o, si ya tiene uno, seleccione **Usar existente**.
8. Compruebe la ubicación predeterminada de Hola.
9. Seleccione **toodashboard Pin**.
10. Seleccione **Crear**.

### <a name="create-hello-gateway-subnet"></a>Crear una subred de puerta de enlace de Hola
1. En panel de hello, abra el recurso de red virtual de red virtual 01 de Hola que creó anteriormente.
2. En hello **configuración** hoja, seleccione **subredes**.
3. Seleccione una subred de puerta de enlace a red virtual de hello, tooadd **subred de puerta de enlace**.
   
    ![Agregación de subred de puerta de enlace](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. De forma predeterminada, se establece demasiado nombre de subred de hello**GatewaySubnet**.
   Las subredes de puerta de enlace son especiales. toofunction correctamente, deben utilizar hello *GatewaySubnet* nombre.
5. En **intervalo de direcciones**, compruebe que la dirección de hello es **10.0.11.0/24**.
6. Seleccione **Aceptar** subred de puerta de enlace de toocreate Hola.

### <a name="create-hello-virtual-network-gateway"></a>Crear puerta de enlace de red virtual de Hola
1. Hola portal de Azure, seleccione **nuevo**. 
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
3. En la lista Hola de recursos de red, seleccione **puerta de enlace de red Virtual**.
4. En **Nombre**, escriba **GW1**.
5. Seleccione hello **red Virtual** elemento toochoose una red virtual.
   Seleccione **VNET-01** de lista de Hola.
6. Seleccione hello **dirección IP pública** elemento de menú. Cuando Hola **Elegir dirección IP pública** hoja se abre, seleccione **crear nuevo**.
7. En **Nombre**, escriba **GW1-PiP** y, a continuación, seleccione **Aceptar**.
8.  De forma predeterminada, para **Tipo de VPN**, está seleccionado **Basada en enrutamiento**.
    Mantener hello **basadas en enrutamiento** tipo de VPN.
9. Compruebe que la **Suscripción** y la **Ubicación** son correctas. Puede anclar el panel de información de hello recursos toohello. Seleccione **Crear**.

### <a name="create-hello-local-network-gateway"></a>Crear puerta de enlace de red local de Hola
Hola de implementación de un *puerta de enlace de red local* en esta pila Azure implementación de evaluación es un poco diferente en una implementación real de Azure.

En una implementación de Azure, una puerta de enlace de red local representa un dispositivo físico local (en el inquilino de hello), que usar puerta de enlace de red virtual de tooconnect tooa en Azure. En esta implementación de evaluación de la pila de Azure, ambos extremos de conexión de hello son puertas de enlace de red virtual.

Un toothink de manera sobre esta forma más genérica es que recursos de puerta de enlace de red local de hello siempre indica a puerta de enlace remoto hello en hello otro extremo de conexión de Hola. Debido a Hola Hola de manera que se diseñó el Kit de desarrollo de pila de Azure, necesita tooprovide dirección IP de Hola Hola externo del adaptador de red en la traducción de direcciones de red de hello (NAT) VM de hello otros Azure pila Kit de desarrollo como Hola dirección IP pública de Hola puerta de enlace de red local. A continuación, cree asignaciones de NAT en hello NAT VM toomake seguro de que ambos extremos estén conectados correctamente.


### <a name="create-hello-local-network-gateway-resource"></a>Crear recursos de puerta de enlace de red local de Hola
1. Inicie sesión en toohello máquina física de pila de Azure para POC1.
2. En el portal de usuarios de hello, seleccione **nuevo**.
3. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
4. En la lista Hola de recursos, seleccione **puerta de enlace de red local**.
5. En **Nombre**, escriba **POC2-GW**.
6. En **dirección IP**, escriba la dirección de BGPNAT externo de Hola para POC2. Esta dirección aparece anteriormente en la tabla de configuración de red de Hola.
7. En **espacio de direcciones**, para el espacio de direcciones de Hola de red virtual de POC2 que se crean después de hello, escriba **10.0.20.0/23**.
8. Compruebe que la **Suscripción**, **Grupo de recursos** y **Ubicación** son correctos y seleccione **Crear**.

### <a name="create-hello-connection"></a>Crear conexiones de Hola
1. En el portal de usuarios de hello, seleccione **nuevo**.
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
3. En la lista Hola de recursos, seleccione **conexión**.
4. En hello **Fundamentos** hoja de configuración, para hello **tipo de conexión**, seleccione **(IPSec) de sitio a sitio**.
5. Seleccione hello **suscripción**, **grupo de recursos**, y **ubicación**y, a continuación, seleccione **Aceptar**.
6. En hello **configuración** hoja, seleccione **puerta de enlace de red Virtual**y, a continuación, seleccione **GW1**.
7. Seleccione **Puerta de enlace de red local** y, a continuación, seleccione **POC2-GW**.
8. En **Nombre de la conexión**, escriba **POC1-POC2**.
9. En **Clave compartida (PSK)**, escriba **12345** y, a continuación, seleccione **Aceptar**.
10. En hello **resumen** hoja, seleccione **Aceptar**.

### <a name="create-a-vm"></a>Creación de una VM
datos de hello toovalidate que pasan por hello conexión VPN, debe Hola toosend de máquinas virtuales y recibir datos en cada Kit de desarrollo de la pila de Azure. Ahora, cree una máquina virtual en POC1 y colóquela en la subred de máquina virtual en la red virtual.

1. Hola portal de Azure, seleccione **nuevo**.
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **proceso**.
3. En lista de Hola de imágenes de máquina virtual, seleccione hello **Eval de centro de datos de Windows Server 2016** imagen.
4. En hello **Fundamentos** hoja, en **nombre**, escriba **VM01**.
5. Escriba un nombre de usuario válido y una contraseña. Utilice esta cuenta toosign en toohello VM después de crearlo.
6. Proporcione una **Suscripción**, **Grupo de recursos** y **Ubicación** y, a continuación, seleccione **Aceptar**.
7. En hello **tamaño** hoja, de esta instancia, seleccione un tamaño de máquina virtual y, a continuación, seleccione **seleccione**.
8. En hello **configuración** hoja, acepte los valores predeterminados de Hola. Asegúrese de que hello **VNET-01** está seleccionada la red virtual. Compruebe que la subred Hola está establecida demasiado**10.0.10.0/24**. Después seleccione **Aceptar**.
9. En hello **resumen** hoja, revise la configuración de hello y, a continuación, seleccione **Aceptar**.



## <a name="create-hello-network-resources-in-poc2"></a>Crear recursos de red de hello en POC2

Hola siguiente paso es recursos de red de hello toocreate para POC2. Hola siguiendo instrucciones muestra cómo toocreate recursos de hello mediante el uso de Hola portal de usuarios.

### <a name="sign-in-as-a-tenant"></a>Inicio de sesión como un inquilino
Un administrador de servicios puede iniciar sesión como un tootest inquilino Hola planes, ofertas y suscripciones que puedan usar sus inquilinos. Si aún no tiene una, [cree una cuenta de inquilino](azure-stack-add-new-user-aad.md) antes de iniciar sesión.

### <a name="create-hello-virtual-network-and-vm-subnet"></a>Crear red virtual de Hola y subred de VM

1. Inicie sesión con una cuenta de inquilino.
2. En el portal de usuarios de hello, seleccione **nuevo**.
3. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
4. Seleccione **Red virtual**.
5. Usar información de Hola que aparecen anteriormente en hello red tabla tooidentify Hola valores de configuración hello POC2 **nombre**, **espacio de direcciones**, **nombre de subred**y  **Intervalo de direcciones de subred**.
6. En **suscripción**, aparece la suscripción de Hola que creó anteriormente.
7. Para **Grupo de recursos**, cree un nuevo grupo de recursos o, si ya tiene uno, seleccione **Usar existente**.
8. Compruebe el valor predeterminado de Hola **ubicación**.
9. Seleccione **toodashboard Pin**.
10. Seleccione **Crear**.

### <a name="create-hello-gateway-subnet"></a>Crear hello subred de puerta de enlace
1. Abrir el recurso de red Virtual de Hola que creó (**VNET-02**) desde el panel de Hola.
2. En hello **configuración** hoja, seleccione **subredes**.
3. Seleccione **subred de puerta de enlace** tooadd una subred de puerta de enlace a la red virtual de Hola.
4. nombre de Hola de subred de Hola se establece demasiado**GatewaySubnet** de forma predeterminada.
   Subredes de puerta de enlace son especiales y deben tener correctamente este toofunction nombre específico.
5. Hola **intervalo de direcciones** , a continuación, compruebe la dirección de hello es **10.0.21.0/24**.
6. Seleccione **Aceptar** subred de puerta de enlace de toocreate Hola.

### <a name="create-hello-virtual-network-gateway"></a>Crear puerta de enlace de red virtual de Hola
1. Hola portal de Azure, seleccione **nuevo**.  
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
3. En la lista Hola de recursos de red, seleccione **puerta de enlace de red Virtual**.
4. En **Nombre**, escriba **GW2**.
5. Seleccione una red virtual, toochoose **red Virtual**. A continuación, seleccione **VNET-02** de lista de Hola.
6. Seleccione **Dirección IP pública**. Cuando Hola **Elegir dirección IP pública** hoja se abre, seleccione **crear nuevo**.
7. En **Nombre**, escriba **GW2-PiP** y, a continuación, seleccione **Aceptar**.
8. De forma predeterminada, para **Tipo de VPN**, está seleccionado **Basada en enrutamiento**.
    Mantener hello **basadas en enrutamiento** tipo de VPN.
9. Compruebe que la **Suscripción** y la **Ubicación** son correctas. Puede anclar el panel de información de hello recursos toohello. Seleccione **Crear**.

### <a name="create-hello-local-network-gateway-resource"></a>Crear recursos de puerta de enlace de red local de Hola

1. En el portal de usuarios de hello POC2, seleccione **nuevo**. 
4. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
5. En la lista Hola de recursos, seleccione **puerta de enlace de red Local**.
6. En **Nombre**, escriba **POC1-GW**.
7. En **dirección IP**, escriba Hola externo BGPNAT dirección POC1 que se indicaron anteriormente en la tabla de configuración de red de Hola.
8. En **espacio de direcciones**, en POC1, escriba Hola **10.0.10.0/23** espacio de direcciones de **VNET-01**.
9. Compruebe que la **Suscripción**, **Grupo de recursos** y **Ubicación** son correctos y seleccione **Crear**.

## <a name="create-hello-connection"></a>Crear conexiones de Hola
1. En el portal de usuarios de hello, seleccione **nuevo**. 
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **red**.
3. En la lista Hola de recursos, seleccione **conexión**.
4. En hello **básica** hoja de configuración, para hello **tipo de conexión**, elija **(IPSec) de sitio a sitio**.
5. Seleccione hello **suscripción**, **grupo de recursos**, y **ubicación**y, a continuación, seleccione **Aceptar**.
6. En hello **configuración** hoja, seleccione **puerta de enlace de red Virtual**y, a continuación, seleccione **GW2**.
7. Seleccione **Puerta de enlace de red local** y, a continuación, seleccione **POC1-GW**.
8. En **Nombre de la conexión**, escriba **POC2-POC1**.
9. En **Clave compartida (PSK)**, escriba **12345**. Si elige un valor diferente, recuerde que TI *debe* coinciden con los valores de hello de clave compartida de Hola que creaste en POC1. Seleccione **Aceptar**.
10. Hola de revisión **resumen** hoja y, a continuación, seleccione **Aceptar**.

## <a name="create-a-virtual-machine"></a>de una máquina virtual
Ahora, cree una máquina virtual en POC2 y colóquela en la subred de máquina virtual en la red virtual.

1. Hola portal de Azure, seleccione **nuevo**.
2. Vaya demasiado**Marketplace**y, a continuación, seleccione **proceso**.
3. En lista de Hola de imágenes de máquina virtual, seleccione hello **Eval de centro de datos de Windows Server 2016** imagen.
4. En hello **Fundamentos** hoja, para **nombre**, escriba **VM02**.
5. Escriba un nombre de usuario válido y una contraseña. Utilice este toosign de cuenta en la máquina virtual de toohello después de crearlo.
6. Proporcione una **Suscripción**, **Grupo de recursos** y **Ubicación** y, a continuación, seleccione **Aceptar**.
7. En hello **tamaño** hoja, seleccione una máquina virtual de tamaño de esta instancia y, a continuación, seleccione **seleccione**.
8. En hello **configuración** hoja, puede aceptar los valores predeterminados de Hola. Asegúrese de que hello **VNET-02** red virtual está seleccionada y compruebe que la subred Hola está establecida demasiado**10.0.20.0/24**. Seleccione **Aceptar**.
9. Revisar la configuración de hello en hello **resumen** hoja y, a continuación, seleccione **Aceptar**.

## <a name="configure-hello-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a>Configurar la máquina virtual NAT de hello en cada Kit de desarrollo de la pila de Azure para el cruce seguro de puerta de enlace
Hola porque hello Kit de desarrollo de pila de Azure es independiente y aislado de la red en qué Hola se implementa el host físico, *externo* red de VIP que las puertas de enlace de hello están conectados toois externo no realmente. En su lugar, la red de VIP de hello está oculto detrás de un enrutador que realiza la traducción de direcciones de red. 

El enrutador es una máquina virtual de Windows Server, denominada *AzS bgpnat01*, que ejecuta Enrutamiento y rol de servicios de acceso remoto (RRAS) en Hola infraestructura de Azure Kit de desarrollo de pila. Debe configurar NAT en hello AzS bgpnat01 máquina virtual tooallow Hola sitio a sitio VPN conexión tooconnect en ambos extremos. 

conexión de VPN de hello tooconfigure, debe crear una ruta estática de asignación NAT que se asigna la interfaz externa Hola Hola BGPNAT máquina virtual toohello VIP de hello grupo de puerta de enlace de borde. Se necesita una ruta de asignación de NAT estática para cada puerto en una conexión VPN.

> [!NOTE]
> Esta configuración es necesaria solo para entornos de Azure Stack Development Kit.
> 
> 

### <a name="configure-hello-nat"></a>Configurar Hola NAT
> [!IMPORTANT]
> Debe realizar este procedimiento para *ambos* entornos de Azure Stack Development Kit.

1. Determinar hello **dirección IP interna** toouse Hola siguiente script de PowerShell. Puerta de enlace de red virtual de hello abierto (GW1 y GW2) y, a continuación, en hello **Introducción** hoja, guardar el valor de Hola para hello **dirección IP pública** para su uso posterior.
![Dirección IP interna](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)
2. Inicie sesión en toohello máquina física de pila de Azure para POC1.
3. Copiar y editar Hola siguiente script de PowerShell. Hola tooconfigure NAT en cada Kit de desarrollo de la pila de Azure, ejecute el script de Hola en un equipo con Windows PowerShell ISE con privilegios elevados. En el script de Hola, agregar valores toohello *dirección BGPNAT externo* y *dirección IP interna* marcadores de posición:

   ```powershell
   # Designate hello external NAT address for hello ports that use hello IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping toomap hello external address toohello Gateway
   # Public IP Address toomap hello ISAKMP port 500 for PHASE 1 of hello IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish hello complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. Repita este procedimiento en POC2.

## <a name="test-hello-connection"></a>Probar conexión Hola
Ahora que se establece la conexión de sitio a sitio de hello, debe validar que pueden recibir tráfico que fluye a través de él. toovalidate, inicio de sesión tooone de máquinas virtuales de Hola que creó en cualquier entorno de Kit de desarrollo de pila de Azure. A continuación, la máquina virtual de ping Hola que creó en Hola otro entorno. 

tooensure que enviar tráfico de Hola a través de la conexión de sitio a sitio de hello, asegúrese de que ping dirección de Direct IP (DIP) de Hola de máquina virtual de hello en subred remota hello, no Hola VIP. toodo esto, buscar Hola DIP resuelve en Hola otro extremo de conexión de Hola. Guarde la dirección de Hola para su uso posterior.

### <a name="sign-in-toohello-tenant-vm-in-poc1"></a>Inicie sesión toohello inquilino VM en POC1
1. Inicie sesión en la máquina física de toohello pila de Azure para POC1 y, a continuación, utilice un toosign de cuenta de inquilino en el portal de usuarios de toohello.
2. En la barra de navegación izquierda de hello, seleccione **proceso**.
3. En la lista de Hola de máquinas virtuales, busque **VM01** que creó anteriormente y, a continuación, selecciónelo.
4. En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**y, a continuación, abra el archivo de VM01.rdp de Hola.
   
     ![Botón Conectar](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. Inicie sesión con la cuenta de hello que configuró al crear máquinas virtuales de Hola.
6. Abra una ventana de **Windows PowerShell** con privilegios elevados.
7. Escriba **ipconfig /all**.
8. En la salida de hello, busque hello **dirección IPv4**y, a continuación, guarde la dirección Hola para su uso posterior. Ésta es la dirección de Hola que hará ping desde POC2. En el entorno de ejemplo de Hola, la dirección es **10.0.10.4**, pero en su entorno puede ser diferente. Deben estar dentro de hello **10.0.10.0/24** subred que creó anteriormente.
9. una regla de firewall que permita Hola máquina virtual toorespond toopings, ejecute el siguiente comando de PowerShell de Hola toocreate:

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-toohello-tenant-vm-in-poc2"></a>Inicie sesión toohello inquilino VM en POC2
1. Inicie sesión en la máquina física de toohello pila de Azure para POC2 y, a continuación, utilice un toosign de cuenta de inquilino en el portal de usuarios de toohello.
2. En la barra de navegación izquierda de hello, haga clic en **proceso**.
3. En la lista de Hola de máquinas virtuales, observa **VM02** que creó anteriormente y, a continuación, selecciónelo.
4. En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**.
5. Inicie sesión con la cuenta de hello que configuró al crear máquinas virtuales de Hola.
6. Abra una ventana de **Windows PowerShell** con privilegios elevados.
7. Escriba **ipconfig /all**.
8. Debería ver una dirección IPv4 que se encuentre dentro de **10.0.20.0/24**. En el entorno de ejemplo de Hola, dirección de hello es **10.0.20.4**, pero la dirección puede ser diferente.
9. una regla de firewall que permita Hola máquina virtual toorespond toopings, ejecute el siguiente comando de PowerShell de Hola toocreate:

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. De la máquina virtual de hello en POC2, haga ping a máquina virtual de hello en POC1, a través de túnel de Hola. toodo, ping Hola DIP que registró de VM01.
   En el entorno de ejemplo de Hola, sería **10.0.10.4**, pero estar seguro de dirección de hello tooping que anotó en el laboratorio. Debería ver un resultado similar Hola siguientes:
   
    ![Ping correcto](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. Una respuesta de la máquina virtual remoto de hello indica una prueba correcta. Puede cerrar la ventana de la máquina virtual de hello. tootest la conexión, puede probar otros tipos de transferencias de datos como una copia de archivos.

### <a name="viewing-data-transfer-statistics-through-hello-gateway-connection"></a>Transferencia de datos de visualización de estadísticas a través de la conexión de puerta de enlace de Hola
Si desea que tooknow la cantidad de datos pasa a través de la conexión de sitio a sitio, esta información está disponible en hello **conexión** hoja. Esta prueba también es otra manera de tooverify que Hola ping que acabamos de enviar llegó a través de la conexión de VPN de Hola.

1. Mientras ha iniciado sesión en toohello las máquinas virtuales en POC2, utilice el toosign de cuenta de inquilino en el portal de usuarios de toothe.
2. Vaya demasiado**todos los recursos**y, a continuación, seleccione hello **POC2 POC1** conexión. Aparece **Conexiones**.
4. En hello **conexión** hoja, las estadísticas de Hola para **datos en** y **datos de salida** aparecen. En la siguiente captura de pantalla de Hola se atribuyen Hola grandes cantidades tooadditional transferencia de archivos. Debería ver algunos valores distintos de cero.
   
    ![Datos de entrada y salida](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
