---
title: "API de generación de informes de aaaPrerequisites tooaccess hello Azure AD | Documentos de Microsoft"
description: "Aprender sobre la API de generación de informes de hello requisitos previos tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de generación de informes de requisitos previos tooaccess hello Azure AD

Hola [Azure AD reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST. Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.

Hola reporting utiliza API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toohello web API de tooauthorize acceso. 

tooget tener acceso a los datos de informes de toohello a través de API de hello, deberá toohave uno Hola siguiendo los roles asignados:

- Lector de seguridad
- Administrador de seguridad
- Administrador global


tooprepare su toohello acceso a API de informes, debe:

1. Registro de una aplicación 
2. Concesión de permisos 
3. Recopilación de configuraciones 

Si tiene preguntas, problemas o comentarios, [abra una incidencia de soporte técnico](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Registro de una aplicación de Azure Active Directory

Debe tooregister una aplicación incluso si tiene acceso hello mediante un script de API de informes. Esto le ofrece un **Id. de aplicación**, lo cual es necesario para una llamada de autorización y permite los tokens de tooreceive de código.

tooconfigure su API directory tooaccess hello Azure AD informes, debe iniciar sesión en toohello portal de Azure con una cuenta de administrador de Azure que también es un miembro de hello **administrador Global** rol del directorio en el inquilino de Azure AD .

> [!IMPORTANT]
> Aplicaciones que se ejecutan bajo las credenciales con privilegios de "admin" similar al siguiente pueden ser muy eficaces, por lo que Ten credenciales de Id. / secreto de la aplicación de seguro tookeep Hola segura.
> 


**tooregister una aplicación de Azure Active Directory:**

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. En hello **Azure Active Directory** hoja, haga clic en **registros de aplicación**.

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. En hello **registros de aplicaciones** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **nuevo registro de aplicación**.

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. En hello **crear** hoja, realizar Hola pasos:

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. Hola **nombre** cuadro de texto, tipo `Reporting API application`.

    b. Seleccione **Aplicación web o API** como **Tipo de aplicación**.

    c. Hola **dirección URL de inicio de sesión** cuadro de texto, tipo `https://localhost`.

    d. Haga clic en **Crear**. 


## <a name="grant-permissions"></a>Concesión de permisos 

objetivo de Hola de este paso es la aplicación de toogrant **leer datos de directorio** permisos toohello **Windows Azure Active Directory** API.

![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant su hello toouse de permiso de aplicación API:**

1. En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.

2. En hello **aplicación de API de Reporting** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. En hello **configuración** hoja, haga clic en **los permisos necesarios**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. En hello **los permisos necesarios** hoja en hello **API** lista, haga clic en **Windows Azure Active Directory**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. En hello **habilitar acceso** hoja, seleccione **leer datos de directorio**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. En la barra de herramientas de hello en la parte superior de hello, haga clic en **guardar**.

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Recopilación de configuraciones 
Esta sección muestra cómo hello tooget siguiendo la configuración de su directorio:

* Nombre de dominio
* id. de cliente
* Secreto del cliente

Necesitará estos valores al configurar la API de generación de informes de toohello de llamadas. 

### <a name="get-your-domain-name"></a>Obtención del nombre de dominio

**tooget el nombre de dominio:**

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. En hello **Azure Active Directory** hoja, haga clic en **nombres de dominio**.

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Copie el nombre de dominio de lista de Hola de dominios.


### <a name="get-your-applications-client-id"></a>Obtención del id. de cliente de la aplicación

**tooget Id. de cliente de la aplicación:**

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.

3. En hello **aplicación de API de Reporting** hoja en hello **Id. de aplicación**, haga clic en **haga clic en toocopy**.

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Obtención del secreto de cliente de la aplicación
tooget cliente de su aplicación secreta, que necesita toocreate una nueva clave y guardar su valor al guardar la nueva clave de hello porque no es posible tooretrieve este valor más tarde ya.

**tooget secreto del cliente de su aplicación:**

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. En hello **registros de aplicaciones** hoja, en la lista de aplicaciones de hello, haga clic en **aplicación de API de Reporting**.


3. En hello **aplicación de API de Reporting** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. En hello **configuración** hoja en hello **APIR acceso** sección, haga clic en **claves**. 

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. En hello **claves** hoja, realizar Hola pasos:

    ![Registre la aplicación](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. Hola **descripción** cuadro de texto, tipo `Reporting API`.

    b. En **Expiración**, seleccione **En 2 años**.

    c. Haga clic en **Guardar**.

    d. Copie el valor de clave de Hola.


## <a name="next-steps"></a>Pasos siguientes
* ¿Se como tooaccess Hola datos de hello Azure AD API de informes de una manera mediante programación? Extraer del repositorio [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).
* Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).  

