---
title: aaaConnect tooAzure pila con CLI | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomanage multiplataforma interfaz de línea de comandos (CLI) e implementar recursos en la pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>Instalar y configurar la CLI para su uso con Azure Stack

En este documento, se dirigirá en proceso de Hola de uso de recursos de interfaz de línea de comandos (CLI) de Azure toomanage Kit de desarrollo de pila de Azure entre plataformas de cliente de Linux y Mac. 

## <a name="export-hello-azure-stack-ca-root-certificate"></a>Exportar el certificado de raíz de hello entidad emisora de certificados de la pila de Azure

Si está usando CLI desde una máquina virtual que se está ejecutando en el entorno del Kit de desarrollo de Azure pila hello, certificado de raíz de hello Azure pila ya está instalado dentro de la máquina virtual de Hola para que pueda recuperar directamente. Mientras que si se usa la CLI desde una estación de trabajo fuera de kit de desarrollo de hello, debe exportar el certificado de raíz de hello entidad emisora de certificados de la pila de Azure del kit de desarrollo de Hola y agregarlo toohello Python almacén de la estación de trabajo de desarrollo (externo Linux o Mac plataforma de certificados ). 

Inicie sesión en el kit de desarrollo de tooyour y ejecute hello sigue la secuencia de comandos tooexport hello Azure pila certificado raíz en formato PEM:

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a>Instalar la CLI

A continuación debe iniciar sesión en la estación de trabajo de desarrollo de tooyour e instalar la CLI. Pila de Azure requiere la versión de Hola 2.0 de CLI de Azure, que se puede instalar mediante el uso de pasos de hello descritos en hello [instalar Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) artículo. tooverify si la instalación de hello fue correcta, abra un terminal o una ventana de símbolo del sistema y ejecución Hola siguiente comando:

```azurecli
az --version
```

Debería ver la versión de Hola de CLI de Azure y otras bibliotecas dependientes que están instalados en su equipo.

## <a name="trust-hello-azure-stack-ca-root-certificate"></a>Confiar en certificado de raíz de hello entidad emisora de certificados de la pila de Azure

tootrust Hola certificado de Azure de pila de CA raíz, también debe agregar certificado de python existente toohello. Si está ejecutando CLI desde un equipo de Linux que se crea dentro del entorno de Azure pila hello, siguiente ejecución Hola bash comando:

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

Si está ejecutando CLI desde un equipo fuera de entorno de Azure Sack hello, primero debe configurar [tooAzure de conectividad VPN pila](azure-stack-connect-azure-stack.md). Ahora copie Hola PEM certificado que exportó anteriormente en la estación de trabajo de desarrollo y ejecute hello siguientes comandos en función del sistema operativo de su desarrollo de estación de trabajo:

### <a name="linux"></a>Linux

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a>macOS

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a>Windows

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a>Establecer el punto de conexión de alias de máquina virtual de Hola

Antes de que los usuarios pueden crear máquinas virtuales mediante el uso de CLI, Administrador de la nube de hello debe configurar un extremo accesible públicamente que contiene el alias de la imagen de máquina virtual y registre este punto de conexión con la nube de Hola. Hola `endpoint-vm-image-alias-doc` parámetro Hola `az cloud register` comando se usa para este propósito. Los administradores de nube deben descargar marketplace de pila de Azure de hello imagen toohello antes de que agregan el punto de conexión de tooimage alias.
   
Por ejemplo, el contenido de Azure usa el URI siguiente: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json. Hola nube administrador debe configurar un punto de conexión similar para la pila de Azure con imágenes de Hola que están disponibles en el marketplace de Azure pila Hola.

## <a name="connect-tooazure-stack"></a>Conectar tooAzure pila

Usar hello siguiendo los pasos tooconnect tooAzure pila:

1. Registrar su entorno de pila de Azure mediante la ejecución de comando de registro de hello az en la nube.
   
   a. Hola tooregister **nube administrativa** entorno, use:

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   b. Hola tooregister **usuario** entorno, use:

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. Establecer entorno activo de hello mediante Hola siguientes comandos:

   a. Para hello **nube administrativa** entorno, use:

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   b. Para hello **usuario** entorno, use:

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. Actualice su hello toouse de configuración de entorno perfil de versión de API específica de pila de Azure. configuración de hello tooupdate, ejecute el siguiente comando de hello:

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. Inicie sesión en el entorno de Azure pila tooyour mediante hello **inicio de sesión de az** comando. Puede iniciar sesión en el entorno de Azure pila toohello como un usuario o un [entidad de servicio](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects). 

   * Inicie sesión como un **usuario**: puede especificar Hola username y password directamente dentro de comando de inicio de sesión de hello az o autenticarse mediante un explorador. Deberá toodo Hola último caso, si la cuenta tiene habilitada la autenticación multifactor.

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > Si su cuenta de usuario tiene la autenticación multifactor habilitada, puede usar el comando de inicio de sesión de hello az sin proporcionar el parámetro de hello -u. Ejecutar comando hello proporciona una dirección URL y un código que debe usar tooauthenticate.
   
   * Inicie sesión como un **entidad de servicio**: antes de iniciar sesión, [crear una entidad de servicio a través del portal de Azure de hello](azure-stack-create-service-principals.md) o CLI y asigna a una función. Ahora, inicie sesión con hello siguiente comando:

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a>Probar la conectividad de Hola

Ahora que tenemos todo lo que el programa de instalación, vamos a usar recursos CLI toocreate dentro de la pila de Azure. Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual. Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":

```azurecli
az group create \
  -n MyResourceGroup -l local
```

Si se crea correctamente el grupo de recursos de hello, Hola anterior comando da como resultado Hola propiedades del recurso de hello recién creado siguientes:

![resultado de creación del grupo de recursos](media/azure-stack-connect-cli/image1.png)

Hay algunos problemas conocidos al usar CLI 2.0 en Azure pila, toolearn acerca de estos problemas, vea hello [problemas conocidos de Azure pila CLI](azure-stack-troubleshooting.md#cli) tema. 

## <a name="next-steps"></a>Pasos siguientes

[Implementación de plantillas con la CLI de Azure](azure-stack-deploy-template-command-line.md)

[Conexión con PowerShell](azure-stack-connect-powershell.md)

[Administración de permisos de usuario](azure-stack-manage-permissions.md)

