---
title: Certificados aaaSSL enlace usando PowerShell
description: "Obtenga información acerca de cómo toobind SSL certificados tooyour la aplicación web mediante PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Enlace de certificados SSL con Servicio de aplicaciones de Azure mediante PowerShell
Con la versión de Hola de Microsoft Azure PowerShell versión 1.1.0 se ha agregado un nuevo cmdlet que proporcionaría Hola usuario Hola capacidad toobind nueva o existente SSL certificados tooan aplicación Web existente.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sobre el uso de Azure Resource Manager según toomanage de cmdlets de PowerShell de Azure, la protección de aplicaciones Web [Azure Resource Manager según los comandos de PowerShell para la aplicación Web de Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Carga y enlace de un nuevo certificado SSL
Escenario: usuario Hola gustaría toobind un tooone de certificado SSL de sus aplicaciones web.

Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, nombre de la aplicación hello, ruta del archivo .pfx Hola certificado en el equipo de usuario de Hola Hola contraseña de certificado de Hola y Hola nombre de host personalizado, podemos utilizar Hola después toocreate de comandos de PowerShell que Enlace de SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Tenga en cuenta que, antes de agregar una aplicación web SSL enlace tooa, debe tener un nombre de host (dominio personalizado) ya configurado. Si no está configurado el nombre de host de hello, obtendrá un error 'hostname' no existe mientras se ejecuta New-AzureRmWebAppSSLBinding. Puede agregar un nombre de host directamente desde el portal de Hola o con PowerShell de Azure. Hello siguiente fragmento de código de PowerShell puede ser el nombre de host de tooconfigure Hola antes de ejecutar AzureRmWebAppSSLBinding de nuevo.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Es importante toounderstand que Hola cmdlet Set-AzureRmWebApp sobrescribe los nombres de host de hello para la aplicación web de Hola. Por lo tanto, Hola por encima del fragmento de código de PowerShell está anexando toohello lista existente Hola de nombres de host para la aplicación web de Hola.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Carga y enlace de un certificado SSL existente
Escenario: usuario Hola gustaría toobind un tooone previamente cargado de certificado SSL de sus aplicaciones web.

Se podemos obtener Hola lista de certificados ya cargado tooa grupo de recursos específico usando el siguiente comando de Hola

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Tenga en cuenta que los certificados de hello son tooa local específico ubicación del grupo de recursos, hello usuario necesita toore carga Hola certificado si Hola configurado la aplicación de web está en una ubicación diferente y recursos grupo otros que de hello necesita certificado 

Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, Hola nombre de la aplicación web, Hola huella digital del certificado y Hola nombre de host personalizado, podemos usar Hola después toocreate de comandos de PowerShell que el enlace de SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Eliminación de un enlace SSL existente
Escenario: usuario Hola gustaría toodelete un enlace SSL existente.

Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, Hola nombre de la aplicación web y Hola nombre de host personalizado, podemos utilizar Hola después tooremove de comandos de PowerShell que el enlace de SSL:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Tenga en cuenta que si hello quita el enlace SSL fue Hola última enlace usando ese certificado en esa ubicación, por el certificado predeterminado de Hola se eliminarán, si desea que el usuario de hello certificado de hello tookeep sirve certificado Hola de hello DeleteCertificate opción tookeep

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Referencias
* [Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)
* [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)

