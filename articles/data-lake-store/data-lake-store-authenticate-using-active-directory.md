---
title: "Autenticación entre servicios: Data Lake Store con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooachieve autenticación de servicio al servicio con el almacén de Data Lake con Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticación entre servicios con Data Lake Store mediante Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticación entre servicios](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store usa Azure Active Directory para la autenticación. Antes de crear una aplicación que funcione con el almacén de Azure Data Lake o análisis de Data Lake de Azure, primero debe decidir cómo desea que tooauthenticate su aplicación con Azure Active Directory (Azure AD). Hola dos opciones principales disponibles son:

* Autenticación de usuario final 
* Autenticación entre servicios (este artículo) 

Ambas opciones como resultado de la aplicación que se proporciona con un token de OAuth 2.0, que obtiene tooeach adjunto solicitud realizada tooAzure almacén de Data Lake o análisis de Data Lake de Azure.

En este artículo se habla de cómo crear una **aplicación web de Azure AD para la autenticación entre servicios**. Para obtener instrucciones sobre la configuración de la aplicación de Azure AD para la autenticación entre servicios, vea [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Paso 1: Crear una aplicación web de Active Directory

Cree y configure una aplicación web de Azure AD para la autenticación entre servicios con Azure Data Lake Store mediante Azure Active Directory. Para obtener instrucciones, vea cómo [crear una aplicación de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Al seguir las instrucciones de hello en hello por encima del vínculo, asegúrese de seleccionar **aplicación Web / API** para el tipo de aplicación, como se muestra en la siguiente captura de pantalla de Hola.

![Crear aplicación web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Crear aplicación web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Paso 2: obtención del identificador, la clave de autenticación y el identificador de inquilino de la aplicación
Al iniciar sesión mediante programación, se necesita Id. de hello para la aplicación. Si la aplicación hello se ejecuta con sus propias credenciales, también necesitará una clave de autenticación.

* Para obtener instrucciones sobre cómo tooretrieve Hola identificador de la aplicación y la autenticación de clave (también el secreto de cliente llamado hello) para la aplicación, consulte [clave de autenticación y el Id. de aplicación de Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Para obtener instrucciones sobre cómo tooretrieve Hola Id. de inquilino, consulte [obtener Id. de inquilino](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Paso 3: Asignar el archivo de cuenta de almacén de Azure Data Lake de toohello aplicación de Azure AD de Hola o una carpeta (sólo para la autenticación de servicio a servicio)
1. Inicio de sesión toohello nueva [portal de Azure](https://portal.azure.com) y abrir cuenta de almacén de Azure Data Lake de Hola que desea que tooassociate con hello aplicación de Azure Active Directory que creó anteriormente.
2. En la hoja de su cuenta de Almacén de Data Lake, haga clic en **Explorador de datos**.
   
    ![Creación de directorios en una cuenta de Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Creación de directorios en una cuenta de Data Lake Store")
3. Hola **Explorador de datos** hoja, haga clic en el archivo de Hola o una carpeta para el que desea toohello Azure AD para tooprovide acceso a la aplicación y, a continuación, haga clic en **acceso**. archivo de tooa de acceso de tooconfigure, debe hacer clic **acceso** de hello **vista previa del archivo** hoja.
   
    ![Configuración de ACL en el sistema de archivos de Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Configuración de ACL en el sistema de archivos de Data Lake")
4. Hola **acceso** hoja enumera acceso estándar hello y acceso personalizado ya asignado toohello raíz. Haga clic en hello **agregar** icono tooadd personalizada basada en la ACL.
   
    ![Lista de accesos estándar y personalizados](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "Lista de accesos estándar y personalizados")
5. Haga clic en hello **agregar** Hola de icono tooopen **agregar acceso de personalizado** hoja. En esta hoja, haga clic en **Seleccionar usuario o grupo**y, a continuación, en **Seleccionar usuario o grupo** hoja, busque la aplicación de Azure Active Directory de Hola que creó anteriormente. Si tiene muchos grupos toosearch desde, utilice el cuadro de texto de hello en hello toofilter superior en el nombre del grupo de Hola. Haga clic en grupo de Hola que desee tooadd y, a continuación, haga clic en **seleccione**.
   
    ![Incorporación de un grupo](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Incorporación de un grupo")
6. Haga clic en **permisos Select**, seleccionar los permisos de Hola y si desea que los permisos de hello tooassign como una ACL predeterminada, tener acceso a ACL, o ambos. Haga clic en **Aceptar**.
   
    ![Asignar permisos toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "asignar permisos toogroup")
   
    Para obtener más información sobre los permisos de Data Lake Store y ACL y las ACL predeterminadas y de acceso, consulte [Control de acceso en Data Lake Store](data-lake-store-access-control.md).
7. Hola **agregar acceso de personalizado** hoja, haga clic en **Aceptar**. Hola recién agregado grupo con permisos de hello asociado, ahora se mostrarán en hello **acceso** hoja.
   
    ![Asignar permisos toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "asignar permisos toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Paso 4: Obtener el extremo de token de OAuth 2.0 de hello (sólo para aplicaciones basadas en Java)

1. Inicio de sesión toohello nueva [portal de Azure](https://portal.azure.com) y haga clic en Active Directory en el panel izquierdo de Hola.

2. En el panel izquierdo de hello, haga clic en **registros de aplicación**.

3. Desde la parte superior de la hoja de los registros de aplicación Hola Hola haga clic en **extremos**.

    ![Punto de conexión de token de OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "Punto de conexión de token de OAuth")

4. En lista de Hola de puntos de conexión, copie el extremo de token de hello OAuth 2.0.

    ![Punto de conexión de token de OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "Punto de conexión de token de OAuth")   

## <a name="next-steps"></a>Pasos siguientes
En este artículo se crea una aplicación web de Azure AD y recopila información de Hola que necesita en las aplicaciones cliente que creas mediante .NET SDK, SDK de Java, etcetera. Ahora puede continuar toohello siguientes artículos que hable acerca de cómo se autentican con almacén de Data Lake toofirst de aplicación web de toouse hello Azure AD y, a continuación, realizan otras operaciones en el almacén de Hola.

* [Introducción al Almacén de Azure Data Lake mediante SDK de .NET](data-lake-store-get-started-net-sdk.md)
* [Introducción a Azure Data Lake Store con el SDK de Java](data-lake-store-get-started-java-sdk.md)

En este artículo había visto se Hola pasos básicos necesarios tooget un usuario principal de seguridad y en ejecución para la aplicación. Puede mirar Hola siguiendo artículos tooget para obtener más información:
* [Usar a entidad de servicio de toocreate de PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Uso de certificados para la autenticación de la entidad de servicio](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Otro tooAzure de tooauthenticate métodos AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


