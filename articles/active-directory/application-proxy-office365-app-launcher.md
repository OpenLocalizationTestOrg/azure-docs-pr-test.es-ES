---
title: "aaaSet una página de inicio personalizada para las aplicaciones publicadas mediante el uso de Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Abarca conceptos básicos de hello acerca de los conectores de Proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el Proxy de aplicación de Azure AD

Este artículo se describe cómo tooconfigure aplicaciones toodirect usuarios tooa página principal personalizada. Al publicar una aplicación con el Proxy de aplicación, establecer una dirección URL interna pero a veces no es página Hola que los usuarios deben ver en primer lugar. Establecer una página principal personalizada para que los usuarios entren página derecha toohello cuando tienen acceso a aplicaciones de Hola de Hola Panel de acceso de Azure Active Directory o iniciador de aplicaciones de Office 365 Hola.

Cuando los usuarios inicien la aplicación hello, se le dirige por predeterminada toohello raíz dirección URL del dominio de aplicación publicados de hello. página de aterrizaje de Hello normalmente se establece como dirección URL de página principal de Hola. Utilice direcciones URL de página principal personalizada de hello Azure AD PowerShell módulo toodefine cuando desee tooland de los usuarios de aplicación en una página específica dentro de la aplicación hello. 

Por ejemplo:
- Dentro de la red corporativa, los usuarios ir demasiado*https://ExpenseApp/login/login.aspx* toosign en y tener acceso a la aplicación.
- Porque tiene otros recursos como imágenes que el Proxy de aplicación necesita tooaccess en nivel superior de Hola de estructura de carpetas de hello, publicar la aplicación hello con *https://ExpenseApp* como Hola URL interna.
- Hola predeterminado es la dirección URL externa *https://ExpenseApp-contoso.msappproxy.net*, que no toma su inicio de sesión de toohello de usuarios en la página.  
- Establecer *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* como Hola toogive de dirección URL de página principal de los usuarios una experiencia sin problemas. 

>[!NOTE]
>Cuando concede a los usuarios acceso toopublished aplicaciones, aplicaciones de Hola se muestran en hello [Panel de acceso de Azure AD](active-directory-saas-access-panel-introduction.md) hello y [iniciador de aplicaciones de Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Antes de comenzar

Antes de configurar URL de la página de inicio de hello, tenga en hello cuenta según los requisitos:

* Asegúrese de esa ruta de acceso de hello especificada es una ruta de acceso de subdominio de hello dirección URL raíz del dominio.

  Si es la dirección URL del dominio raíz de hello, por ejemplo, https://apps.contoso.com/app1/, dirección URL de la página principal de Hola que configure debe empezar por https://apps.contoso.com/app1/.

* Si realiza un cambio toohello publica la aplicación, cambio Hola puede restablecer el valor de Hola de dirección URL de página principal de Hola. Cuando se actualiza la aplicación hello en hello futuras, debe volver a comprobar y, si es necesario, actualice la dirección URL de página principal de Hola.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Cambiar la página principal Hola Hola portal de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador.
2. Navegue demasiado**Azure Active Directory** > **registros de aplicación** y elija la aplicación de lista de Hola. 
3. Seleccione **propiedades** de configuración de Hola.
4. Hola de actualización **URL de la página de inicio** campo con la nueva ruta de acceso. 

   ![Especifique la nueva dirección URL de la página principal](./media/application-proxy-office365-app-launcher/homepage.png)

5. Seleccione **Guardar**.

## <a name="change-hello-home-page-with-powershell"></a>Cambiar la página principal Hola con PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Instalar el módulo de PowerShell de Azure AD Hola

Antes de definir una dirección URL de la página principal personalizada mediante el uso de PowerShell, instale el módulo de PowerShell de Azure AD de Hola. Puede descargar paquetes de saludo de hello [Galería de PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), que usa Hola extremo de API Graph. 

Hola tooinstall del paquete, siga estos pasos:

1. Abra una ventana de PowerShell estándar y, a continuación, ejecute el siguiente comando de hello:

    ```
     Install-Module -Name AzureAD
    ```
    Si está ejecutando el comando hello como sin derechos administrativos, utilice hello `-scope currentuser` opción.
2. Durante la instalación de hello, seleccione **Y** tooinstall dos paquetes en Nuget.org. Se requieren ambos paquetes. 

### <a name="find-hello-objectid-of-hello-app"></a>Buscar Hola ObjectID de aplicación hello

Obtener Hola ObjectID de aplicación hello y, a continuación, busque aplicación hello por su página de inicio.

1. Abrir PowerShell e importe el módulo de hello Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Inicie sesión en toohello módulo de Azure AD como administrador de inquilinos de Hola.

    ```
    Connect-AzureAD
    ```
3. Buscar la aplicación hello en función de su dirección URL de la página principal. Puede encontrar direcciones URL de hello en portal de hello yendo demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones**. Este ejemplo usa *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Debería obtener un resultado que es toohello similar que se muestra aquí. Copie hello toouse ObjectID GUID en la sección siguiente Hola.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Dirección URL de página principal de actualización Hola

Hola mismo módulo de PowerShell que usó para el paso 1, realizar Hola pasos:

1. Confirme que tiene Hola corregir la aplicación y reemplace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* con hello ObjectID que ha copiado en hello anterior paso.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Ahora que ha confirmado la aplicación hello, está listo tooupdate Hola portada, como se indica a continuación.

2. Crear un toohold de objeto de aplicación vacía cambios de Hola que desea toomake. Esta variable contiene valores de hello que desea tooupdate. En este paso no se crea nada.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Establecer el valor de toohello de dirección URL de página principal de Hola que desee. valor de Hello debe ser una ruta de acceso de subdominio de la aplicación publicada Hola. Por ejemplo, si cambia Hola URL de la página de inicio de *https://sharepoint-iddemo.msappproxy.net/* demasiado*https://sharepoint-iddemo.msappproxy.net/hybrid/*, los usuarios de la aplicación vaya directamente toohello personalizado página principal.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Asegúrese de Hola actualización mediante el uso de hello GUID (ObjectID) que ha copiado en "paso 1: buscar Hola ObjectID de aplicación hello."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm que Hola se cambió correctamente, reinicie la aplicación hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Los cambios que realice toohello aplicación podrían restablecer URL de la página de inicio de Hola. Si se restablecer la dirección URL de la página principal, repita el paso 2.

## <a name="next-steps"></a>Pasos siguientes

- [Habilitar acceso remoto tooSharePoint con el Proxy de aplicación de Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Habilita el Proxy de aplicación en hello portal de Azure](active-directory-application-proxy-enable.md)
