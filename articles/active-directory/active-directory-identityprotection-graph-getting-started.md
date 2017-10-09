---
title: aaaGet a trabajar con Azure Active Directory Identity Protection y Microsoft Graph | Documentos de Microsoft
description: "Proporciona un tooquery Introducción Microsoft Graph para obtener una lista de eventos de riesgos y la información asociada de Azure Active Directory."
services: active-directory
keywords: azure active directory identity protection, evento de riesgo, vulnerabilidad, directiva de seguridad, Microsoft Graph
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Introducción a Azure Active Directory Identity Protection y Microsoft Graph
Microsoft Graph es Microsoft unified extremo de la API de Hola y Hola particular de [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API. Hola primera API, **identityRiskEvents**, permite tooquery Microsoft Graph para obtener una lista de [el riesgo de eventos](active-directory-identityprotection-risk-events-types.md) y la información asociada. Este artículo es una introducción a cómo consultar esta API. Para una introducción detallada, documentación completa y acceso toohello Explorador de gráficos, vea hello [sitio Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

Hay tres pasos tooaccessing identidad protección de datos a través de Microsoft Graph:

1. Agregar una aplicación con un secreto de cliente. 
2. Use este secreto y algunas otras partes de información tooauthenticate tooMicrosoft gráfico, que recibe un token de autenticación. 
3. Use este extremo de token toomake solicitudes toohello API y obtener datos de protección de identidad.

Antes de comenzar, necesitará lo siguiente:

* Aplicación de hello de toocreate de privilegios de administrador en Azure AD
* nombre de Hola de dominio de su inquilino (por ejemplo, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Agregar una aplicación con un secreto de cliente
1. [Inicie sesión en](https://manage.windowsazure.com) tooyour portal de Azure clásico como administrador. 
2. En el panel de navegación izquierdo de hello, haga clic en **Active Directory**. 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
4. En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Haga clic en **agregar** final Hola de página Hola.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación que mi organización está desarrollando**.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. En hello **envíenos comentarios acerca de la aplicación** cuadro de diálogo, realizar Hola pasos:
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. Hola **nombre** cuadro de texto, escriba un nombre para la aplicación (p. ej.: aplicación de API de eventos de riesgo AADIP).
   
    b. Como **Tipo**, seleccione **Aplicación web y/o API web**.
   
    c. Haga clic en **Siguiente**.
8. En hello **propiedades de la aplicación** cuadro de diálogo, realizar Hola pasos:
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `http://localhost`.
   
    b. Hola **App ID URI** cuadro de texto, tipo `http://localhost`.
   
    c. Haga clic en **Completo**.

Ahora puede configurar la aplicación.

![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Conceder su hello toouse de permiso de aplicación API
1. En la página de la aplicación, en el menú de hello en la parte superior de hello, haga clic en **configurar**. 
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. Hola **permisos tooother aplicaciones** sección, haga clic en **Agregar aplicación**.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. En hello **permisos tooother aplicaciones** cuadro de diálogo, realizar Hola pasos:
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Seleccione **Microsoft Graph**.
   
    b. Haga clic en **Complete**.
4. Haga clic en **Permisos de la aplicación: 0** y seleccione **Read all identity risk event information** (Leer toda la información de eventos de riesgo de identidad).
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Haga clic en **guardar** final Hola de página Hola.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Obtención de una clave de acceso
1. En la página de su aplicación, en hello **claves** sección, seleccione 1 año como duración.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Haga clic en **guardar** final Hola de página Hola.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. en la sección de claves de hello, Copiar valor de saludo de la clave recién creada y, a continuación, péguelo en una ubicación segura.
   
    ![Creación de una aplicación](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Si pierde esta clave, tendrá tooreturn toothis sección y cree una nueva clave. Guarde esta clave como un secreto: cualquier persona que la tenga accederá a sus datos.
   > 
   > 
4. Hola **propiedades** Hola de copia, en una sección **Id. de cliente**y, a continuación, péguelo en una ubicación segura. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Autenticar hello de consulta API de eventos de riesgo de identidad y tooMicrosoft gráfico
En este momento, debe tener:

* Id. de cliente de Hola que copió anteriormente
* clave de Hola que copió anteriormente
* nombre de Hola de dominio de su inquilino

tooauthenticate, enviar una entrada de solicitud demasiado`https://login.microsoft.com` con hello parámetros en el cuerpo de hello siguientes:

* grant_type: “**client_credentials**”
* resource: “**https://graph.microsoft.com**”
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> Necesita tooprovide valores para hello **client_id** hello y **client_secret** parámetro.
> 
> 

Si se realiza correctamente, devuelve un token de autenticación.  
Hola toocall API, cree un encabezado con hello después de parámetro:

    `Authorization`=”<token_type> <access_token>"


Al autenticar, puede encontrar el tipo de token Hola y el token de acceso en hello devolvió el token.

Enviar este encabezado como un toohello de solicitud después de la dirección URL de API:`https://graph.microsoft.com/beta/identityRiskEvents`

respuesta de Hello, si es correcto, es una colección de identidad eventos de riesgo y datos en formato JSON de OData, que se pueden analizar y controlar como considere oportuno Hola asociados.

Este es el código de ejemplo para autenticar y llamar a API de hello mediante Powershell.  
Solo tiene que agregar el identificador de cliente, la clave y el dominio del inquilino.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Pasos siguientes
Enhorabuena, que acaba de crear su primer tooMicrosoft de llamada Graph.  
Ahora puede consultar los eventos de riesgo de identidad y usar datos de hello le convenga.

toolearn más información acerca de Microsoft Graph y cómo las aplicaciones que toobuild usan Hola API Graph, visite hello [documentación](https://graph.microsoft.io/docs) y mucho más en hello [sitio Microsoft Graph](https://graph.microsoft.io/). Además, asegúrese de que hello toobookmark [API de protección de Azure AD Identity](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que enumera la lista de hello las API de protección de identidad disponible en el gráfico. Cuando se agrega toowork de maneras nuevas con protección de identidad a través de API, los verá en la página.

## <a name="additional-resources"></a>Recursos adicionales
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Types of risk events detected by Azure Active Directory Identity Protection (Tipos de eventos de riesgo que detecta Azure Active Directory Identity Protection)](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Overview of Microsoft Graph (Información general de Microsoft Graph)](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection Service Root (Raíz del servicio de Azure AD Identity Protection)](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

