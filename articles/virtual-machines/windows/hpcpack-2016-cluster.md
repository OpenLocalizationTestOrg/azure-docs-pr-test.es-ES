---
title: "aaaHPC 2016 de módulo de clúster en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toodeploy una 2016 de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Implementación de un clúster de HPC Pack 2016 en Azure

Siga los pasos de hello en este artículo toodeploy una [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) clúster en máquinas virtuales de Azure. HPC Pack es la solución HPC gratuita de Microsoft que se basa en las tecnologías de Microsoft Azure y Windows Server, y admite cargas de trabajo HPC.

Utilice uno de hello [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) clúster de HPC Pack 2016 hello toodeploy. Existen varias opciones de topología de clúster con distintos números de nodos principales, y con nodos de proceso Linux o Windows.

## <a name="prerequisites"></a>Requisitos previos

### <a name="pfx-certificate"></a>Certificado PFX

Un clúster de Microsoft HPC Pack 2016 requiere una comunicación de intercambio de información Personal (PFX) certificado toosecure Hola entre los nodos HPC de Hola. certificado de Hello debe cumplir Hola según los requisitos:

* Debe tener una clave privada con funcionalidad de intercambio de claves.
* El uso de la clave incluye firma digital y cifrado de claves.
* La clave mejorada incluye autenticación de cliente y autenticación de servidor.

Si ya no tiene un certificado que cumpla estos requisitos, puede solicitar certificado Hola de una entidad de certificación. Como alternativa, puede usar Hola después comandos toogenerate Hola autofirmado basada en certificados en el sistema operativo de hello en el que ejecutar el comando de Hola y exportar el certificado con formato PFX Hola con clave privada.

* **Para Windows 10 o Windows Server 2016**, ejecute hello integrado **New-SelfSignedCertificate** cmdlet de PowerShell como se indica a continuación:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Para sistemas operativos anteriores a Windows 10 o Windows Server 2016**, descargar hello [generador certificado autofirmado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de hello Microsoft Script Center. Extraer su contenido y ejecute hello siguientes comandos en un símbolo del sistema de PowerShell:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Cargar certificado tooan almacén de claves de Azure

Antes de implementar el clúster de HPC de hello, cargar Hola certificado tooan [almacén de claves de Azure](../../key-vault/index.md) como un Hola secreto y registro siguiente información para su uso durante la implementación de hello: **nombre del almacén de**,  **Grupo de recursos de almacén**, **dirección URL de certificado**, y **huella digital del certificado**.

A continuación se muestra un certificado de hello ejemplo tooupload de secuencia de comandos de PowerShell. Para obtener más información sobre cómo cargar un tooan certificado del almacén de claves de Azure, consulte [empezar a trabajar con el almacén de claves de Azure](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Topologías admitidas

Elija uno de hello [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) clúster de HPC Pack 2016 hello toodeploy. Las siguientes son arquitecturas de alto nivel de tres topologçias de clúster admitidas. Las topologías de alta disponibilidad incluyen varios nodos principales de clúster.

1. Clúster de alta disponibilidad con dominio de Active Directory

    ![Clúster de alta disponibilidad en dominio de AD](./media/hpcpack-2016-cluster/haad.png)



2. Clúster de alta disponibilidad sin dominio de Active Directory

    ![Clúster de alta disponibilidad sin dominio de AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Clúster con un único nodo principal

   ![Clúster con un único nodo principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Implementación de un clúster

clúster de hello toocreate, elija una plantilla y haga clic en **implementar tooAzure**. Hola [portal de Azure](https://portal.azure.com), especificar parámetros de plantilla de hello como se describe en hello pasos. Cada plantilla crea todos los recursos de Azure necesarios para la infraestructura de clúster HPC de Hola. Los recursos incluyen una red virtual de Azure, una dirección IP pública, un equilibrador de carga (solo para un clúster de alta disponibilidad), interfaces de red, conjuntos de disponibilidad, cuentas de almacenamiento y máquinas virtuales.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Paso 1: Seleccione la suscripción de hello, la ubicación y el grupo de recursos

Hola **suscripción** hello y **ubicación** debe ser la misma que especificó cuando se carga el certificado PFX (consulte los requisitos previos). Le recomendamos que cree una **grupo de recursos** para la implementación de Hola.

### <a name="step-2-specify-hello-parameter-settings"></a>Paso 2: Especificar la configuración de parámetros de Hola

Escriba o modifique los valores de parámetros de plantilla de Hola. Haga clic en el parámetro tooeach hello icono siguiente para obtener información de ayuda. Consulte también las instrucciones de Hola para [tamaños de máquina virtual disponibles](sizes.md).

Especificar valores de hello registrados en los requisitos previos de Hola para hello parámetros siguientes: **nombre del almacén de**, **grupo de recursos de almacén**, **dirección URL de certificado**y **Huella digital del certificado**.

### <a name="step-3-review-legal-terms-and-create"></a>Paso 3: Revisión de los términos legales y creación
Haga clic en **revisar los términos legales** términos de hello tooreview. Si los acepta, haga clic en **compra**y, a continuación, haga clic en **crear** implementación de hello toostart.

## <a name="connect-toohello-cluster"></a>Conectar el clúster toohello
1. Después de implementa el clúster de HPC Pack hello, vaya toohello [portal de Azure](https://portal.azure.com). Haga clic en **grupos de recursos**y encontrar el grupo de recursos hello en qué Hola se implementó el clúster. Puede encontrar Hola máquinas virtuales de nodo principal.

    ![Nodos principales del clúster en el portal de Hola](./media/hpcpack-2016-cluster/clusterhns.png)

2. Haga clic en un nodo principal (en un clúster de alta disponibilidad, haga clic en cualquiera de los nodos principales de hello). En **Essentials**, puede encontrar la dirección IP pública Hola o nombre DNS completo del clúster de Hola.

    ![Configuración de la conexión del clúster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Haga clic en **conectar** toolog en tooany de nodos principales hello mediante Escritorio remoto con el nombre de usuario de administrador especificado. Si el clúster de Hola implementa está en un dominio de Active Directory, nombre de usuario de hello tiene formato de hello <privateDomainName> \<adminUsername > (por ejemplo, hpc.local\hpcadmin).

## <a name="next-steps"></a>Pasos siguientes
* Enviar clúster tooyour de trabajos. Vea [enviar trabajos tooHPC un clúster de HPC Pack en Azure](hpcpack-cluster-submit-jobs.md) y [administrar un clúster de HPC Pack 2016 en Azure con Azure Active Directory](hpcpack-cluster-active-directory.md).

