---
title: aaaGet datos mediante Hola AD Reporting API de Azure con certificados | Documentos de Microsoft
description: "Explica cómo toouse Hola AD Reporting API de Azure con los datos de tooget de credenciales de certificado de directorios sin intervención del usuario."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Obtener datos utilizando la API de generación de informes de hello Azure AD con certificados
Este artículo describe cómo toouse Hola AD Reporting API de Azure con los datos de tooget de credenciales de certificado de directorios sin intervención del usuario. 

## <a name="use-hello-azure-ad-reporting-api"></a>Use Hola API Reporting de Azure AD 
API de informes de Azure AD requiere que se complete Hola pasos:
 *  Requisitos previos de instalación
 *  Configure el certificado de hello en la aplicación
 *  Obtención de un token de acceso
 *  Usar Hola acceso toocall token hello API Graph

Para más información sobre el código fuente, consulte el [módulo Leverage Report API](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Uso de Report API). 

### <a name="install-prerequisites"></a>Requisitos previos de instalación
Necesitará toohave V2 de PowerShell de Azure AD y módulo AzureADUtils instalado.

1. Descargar e instalar Azure AD Powershell V2, siga las instrucciones de hello en [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Descargar el módulo de Azure AD Utils Hola de [organización/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Este módulo proporciona varios cmdlets de utilidades incluidos los siguientes:
   * versión más reciente de Hola de AAL mediante Nuget
   * Los tokens de acceso de usuario, las claves de aplicación y los certificados mediante ADAL
   * API Graph con control de resultados paginados

**módulo de Azure AD Utils de Hola tooinstall:**

1. Crear un módulo de utilidades de hello directorio toosave (por ejemplo, c:\azureAD) y descargue el módulo de Hola desde GitHub.
2. Abra una sesión de PowerShell y vaya a directorio toohello que acaba de crear. 
3. Importar el módulo de hello e instalarlo en la ruta de módulo de PowerShell de hello mediante el cmdlet de hello AzureADUtilsModule de instalación. 

sesión de Hello debe tener un aspecto similar pantalla toothis:

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Configure el certificado de hello en la aplicación
1. Si ya tiene una aplicación, obtener su identificador de objeto de hello Portal de Azure. 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Abra una sesión de PowerShell y conéctese tooAzure AD mediante el cmdlet de hello organización conectar.

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Use el cmdlet de nuevo AzureADApplicationCertificateCredential Hola de AzureADUtils tooadd un tooit de credencial de certificado. 

>[!Note]
>Se necesita tooprovide Hola aplicación Id. de objeto que ha capturado anteriormente, así como Hola objeto de certificado (obtener esta mediante Hola Cert: unidad).
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Obtención de un token de acceso

tooget un token de acceso, use el cmdlet de Get-AzureADGraphAPIAccessTokenFromCert de Hola desde AzureADUtils. 

>[!NOTE]
>Necesita toouse Hola Id. de aplicación en lugar de Id. de objeto que utilizó en la última sección de Hola Hola.
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Usar Hola acceso toocall token hello API Graph

Ahora puede crear script de Hola. A continuación se muestra un ejemplo de cómo utilizar el cmdlet Invoke-AzureADGraphAPIQuery Hola de hello AzureADUtils. Este cmdlet controla los resultados de varias páginas y, a continuación, envía esos canalización de PowerShell de toohello de resultados. 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

Ahora está listo tooexport tooa CSV y guardar tooa SIEM sistema. También puede ajustar la secuencia de comandos en un tooget de tarea programada datos de Azure AD desde el inquilino periódicamente sin necesidad de toostore claves de aplicación en el código fuente de Hola. 

## <a name="next-steps"></a>Pasos siguientes
[aspectos básicos de Hola de administración de identidades de Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



