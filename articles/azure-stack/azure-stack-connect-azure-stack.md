---
title: aaaConnect tooAzure pila | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect la pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a>Conectar tooAzure pila

toomanage recursos, debe conectarse toohello Kit de desarrollo de pila de Azure. Este tema se detallan Hola los pasos necesarios kit de desarrollo de tooconnect toohello. Puede usar cualquiera de las siguientes opciones de conexión de hello:

* [Escritorio remoto](#connect-with-remote-desktop): permite a los usuarios simultáneos único conectarse rápidamente desde el kit de desarrollo de Hola.
* [Red privada virtual (VPN)](#connect-with-vpn): permite que varios usuarios simultáneos conectan desde los clientes fuera de la infraestructura de Azure pila hello (necesita la configuración).

## <a name="connect-tooazure-stack-with-remote-desktop"></a>Conectar tooAzure pila con Escritorio remoto
Con una conexión a Escritorio remoto, un único usuario simultáneo puede trabajar con recursos de hello toomanage portal.

1. Abra una conexión a Escritorio remoto y conéctese toohello kit de desarrollo. Escriba **AzureStack\AzureStackAdmin** como nombre de usuario de Hola y contraseña administrativa Hola que proporcionó durante la instalación de la pila de Azure.  

2. En el equipo de kit de desarrollo de hello, abra Administrador del servidor, haga clic en **servidor Local**, desactive la opción de seguridad mejorada de Internet Explorer y, a continuación, cierre el administrador del servidor.

3. usuario de hello tooopen [portal](azure-stack-key-features.md#portal), navegue demasiado (https://portal.local.azurestack.external/) e inicie sesión con las credenciales de usuario. Administrador de hello tooopen [portal](azure-stack-key-features.md#portal), navegue demasiado (https://adminportal.local.azurestack.external/) y Hola de inicio de sesión utilizando credenciales de Azure Active Directory especificadas durante la instalación.

## <a name="connect-tooazure-stack-with-vpn"></a>Conectar tooAzure pila con VPN

Puede establecer una tooan de conexión de red privada Virtual (VPN) de túnel dividido Kit de desarrollo de pila de Azure. A través de hello conexión VPN, puede acceder al portal de administrador de hello, portal de usuarios y herramientas como Visual Studio y recursos de pila de Azure PowerShell toomanage, instalado localmente. Se admite la conectividad VPN en implementaciones basadas en Azure Active Directory (AAD) y en los Servicios de federación de Active Directory (AD FS). Las conexiones VPN permiten a varios clientes tooconnect tooAzure pila en hello mismo tiempo. 

> [!NOTE] 
> Esta conexión VPN no proporciona la infraestructura de pila conectividad tooAzure de máquinas virtuales. 

### <a name="prerequisites"></a>Requisitos previos

* Instale [Azure PowerShell compatible con Azure Stack](azure-stack-powershell-install.md) en el equipo local.  
* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md). 

### <a name="configure-vpn-connectivity"></a>Configuración de la conectividad VPN

toocreate un kit de desarrollo de toohello de conexión VPN, abra una sesión de PowerShell con privilegios elevados desde el equipo local basado en Windows y ejecución Hola siguiente secuencia de comandos (asegúrese de tooupdate seguro Hola Hola IP dirección y la contraseña valores para su entorno):

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

Si Hola configurar se realiza correctamente, debería ver **azurestack** en la lista de conexiones VPN.

![Conexiones de red](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a>Conectar tooAzure pila

Conectar la instancia de la pila de Azure de toohello mediante el uso de hello siguiendo dos métodos:  

* Mediante el uso de hello `Connect-AzsVpn ` comando: 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  Cuando se le solicite, confiar hello Azure pila host e instalar certificado de Hola de **AzureStackCertificateAuthority** en el almacén de certificados del equipo local. (mensaje de Hola puede aparecer detrás de la ventana de sesión de PowerShell de hello). 

* En el equipo local, abra **Configuración de red** > **VPN** > haga clic en **azurestack** > **Conectar**. En hello inicio de sesión de símbolo del sistema, escriba Hola username (AzureStack\AzureStackAdmin) y la contraseña de Hola.

### <a name="test-hello-vpn-connectivity"></a>Hola de prueba la conectividad VPN

conexión de portal de hello tootest, abra un explorador de Internet y vaya portal de usuarios de hello tooeither (https://portal.local.azurestack.external/) o el portal de administrador de hello (https://adminportal.local.azurestack.external/), inicie sesión y crear recursos.  

## <a name="next-steps"></a>Pasos siguientes

[Hacer tooyour disponibles de máquinas virtuales que los usuarios de la pila de Azure](azure-stack-tutorial-tenant-vm.md)

