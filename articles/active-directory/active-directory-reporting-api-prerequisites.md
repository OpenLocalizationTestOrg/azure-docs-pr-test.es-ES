---
title: "API de generación de informes de aaaPrerequisites tooaccess hello Azure AD. | Microsoft Docs"
description: "Aprender sobre la API de generación de informes de hello requisitos previos tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de generación de informes de requisitos previos tooaccess hello Azure AD
Hola [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST. Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.

Hola reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toohello web API de tooauthorize acceso. 

tooprepare su toohello acceso a API de informes, debe:

1. Crear una aplicación en el inquilino de Azure AD 
2. Tooaccess de los permisos adecuados de concesión Hola aplicación Hola datos de Azure AD
3. Recopilar los valores de configuración del directorio

Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Creación de una aplicación de Azure AD
tooconfigure su API directory tooaccess hello Azure AD informes, debe iniciar sesión en toohello portal de Azure clásico con una cuenta de administrador de suscripción de Azure que también es un miembro del rol de directorio de administrador Global de hello en el inquilino de Azure AD.

> [!IMPORTANT]
> Aplicaciones que se ejecutan bajo las credenciales con privilegios de "admin" similar al siguiente pueden ser muy eficaces, por lo que Ten credenciales de Id. / secreto de la aplicación de seguro tookeep Hola segura.
> 
> 

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De hello **active directory** lista, seleccione el directorio.
3. En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. En la barra de la parte inferior de hello, haga clic en **agregar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/03.png) 
5. En hello **especifique qué desea toodo?** cuadro de diálogo, haga clic en **agregar una aplicación que mi organización está desarrollando**. 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/04.png) 
6. En hello **envíenos comentarios acerca de la aplicación** cuadro de diálogo, realizar Hola pasos: 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. Hola **nombre** cuadro de texto, escriba un nombre (p. ej.: aplicación de API de informes).
   
    b. Seleccione **Aplicación web y/o API web**.
   
    c. Haga clic en **Siguiente**.
7. En hello **propiedades de la aplicación** cuadro de diálogo, realizar Hola pasos: 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `https://localhost`.
   
    b. Hola **App ID URI** cuadro de texto, tipo ```https://localhost/ReportingApiApp```.
   
    c. Haga clic en **Completo**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Conceder su hello toouse de permiso de aplicación API
1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De hello **active directory** lista, seleccione el directorio.
3. En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png)
4. En la lista de aplicaciones de hello, seleccione la aplicación recién creada.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. En el menú de hello en la parte superior de hello, haga clic en **configurar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. Hola **permisos tooother aplicaciones** sección para hello **Azure Active Directory** recursos, haga clic en hello **permisos de aplicación** la lista desplegable y, a continuación, Seleccione **leer datos de directorio**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/09.png)
7. En la barra de la parte inferior de hello, haga clic en **guardar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Recopilar los valores de configuración del directorio
Esta sección muestra cómo hello tooget siguiendo la configuración de su directorio:

* Nombre de dominio
* id. de cliente
* Secreto del cliente

Necesitará estos valores al configurar la API de generación de informes de toohello de llamadas. 

### <a name="get-your-domain-name"></a>Obtención del nombre de dominio
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De hello **active directory** lista, seleccione el directorio.
3. En el menú de hello en la parte superior de hello, haga clic en **dominios**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/11.png) 
4. Hola **nombre de dominio** columna, copie el nombre de dominio.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Obtener Id. de cliente de la aplicación hello
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De hello **active directory** lista, seleccione el directorio.
3. En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. En la lista de aplicaciones de hello, seleccione la aplicación recién creada.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. En el menú de hello en la parte superior de hello, haga clic en **configurar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. Copie el **id. de cliente**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Obtener el secreto de cliente de la aplicación hello
tooget cliente de su aplicación secreta, que necesita toocreate una nueva clave y guardar su valor al guardar la nueva clave de hello porque no es posible tooretrieve este valor más tarde ya.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De hello **active directory** lista, seleccione el directorio.
3. En el menú de hello en la parte superior de hello, haga clic en **aplicaciones**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/02.png) 
4. En la lista de aplicaciones de hello, seleccione la aplicación recién creada.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/07.png)
5. En el menú de hello en la parte superior de hello, haga clic en **configurar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/08.png)
6. Hola **claves** sección, lleve a cabo Hola pasos: 
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. En lista de duración de hello, seleccione una duración
   
    b. En la barra de la parte inferior de hello, haga clic en **guardar**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Copie el valor de clave de Hola.

## <a name="next-steps"></a>Pasos siguientes
* ¿Se como tooaccess Hola datos de hello Azure AD API de informes de una manera mediante programación? Extraer del repositorio [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).
* Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).  

