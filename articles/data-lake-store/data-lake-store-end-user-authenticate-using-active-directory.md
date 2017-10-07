---
title: "Autenticación de usuario final: Data Lake Store con Azure Active Directory | Microsoft Docs"
description: "Obtenga información acerca de cómo tooachieve la autenticación del usuario final con el almacén de Data Lake con Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Autenticación de usuario final con Data Lake Store mediante Azure Active Directory
> [!div class="op_single_selector"]
> * [Autenticación entre servicios](data-lake-store-authenticate-using-active-directory.md)
> * [Autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store usa Azure Active Directory para la autenticación. Antes de crear una aplicación que funcione con el almacén de Azure Data Lake o análisis de Data Lake de Azure, primero debe decidir cómo desea que tooauthenticate su aplicación con Azure Active Directory (Azure AD). Hola dos opciones principales disponibles son:

* Autenticación de usuario final (este artículo)
* Autenticación entre servicios

Ambas opciones como resultado de la aplicación que se proporciona con un token de OAuth 2.0, que obtiene tooeach adjunto solicitud realizada tooAzure almacén de Data Lake o análisis de Data Lake de Azure.

En este artículo se habla de cómo crear una **aplicación nativa de Azure AD para la autenticación de usuario final**. Para obtener instrucciones sobre la configuración de la aplicación de Azure AD para la autenticación entre servicios, vea [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md) (Autenticación entre servicios con Data Lake Store mediante Azure Active Directory).

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Consulte [How to get Azure Free trial for testing Hadoop in HDInsight (Obtención de una versión de prueba gratuita de Azure para probar Hadoop en HDInsight)](https://azure.microsoft.com/pricing/free-trial/).

* El identificador de suscripción. Puede recuperarlo desde Hola Portal de Azure. Por ejemplo, está disponible desde la hoja de cuenta de almacén de Data Lake Hola.
  
    ![Obtener id. de suscripción](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* El nombre de dominio de Azure AD. Puede recuperarlo mediante el desplazamiento del mouse de hello en la esquina superior derecha de Hola de hello Portal de Azure. En la captura de pantalla de Hola a continuación, nombre de dominio de hello es **contoso.onmicrosoft.com**, y Hola GUID entre corchetes es el identificador del inquilino Hola. 
  
    ![Obtener dominio de AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Autenticación de usuario final
Se trata de hello enfoque recomendado si desea que un toolog por el usuario final en la aplicación de tooyour a través de Azure AD. La aplicación será capaz de tooaccess recursos de Azure con hello mismo nivel de acceso como usuario final de Hola que ha iniciado sesión. El usuario final deberá tooprovide sus credenciales periódicamente en orden para el acceso a la aplicación toomaintain.

resultado de Hello de la existencia del usuario final de hello sesión es que la aplicación recibe un token de acceso y un token de actualización. token de acceso de Hello obtiene solicitud tooeach adjunto realizado tooData Lake almacén o análisis de Data Lake y tiene una validez de una hora de forma predeterminada. token de actualización de Hello puede ser usado tooobtain un nuevo token de acceso y es válido para semanas tootwo de forma predeterminada, si se utiliza con regularidad. Puede usar dos enfoques distintos para el inicio de sesión del usuario final.

### <a name="using-hello-oauth-20-pop-up"></a>Utilizando la ventana emergente de hello OAuth 2.0
La aplicación puede desencadenar un menú emergente de autorización OAuth 2.0, en qué hello para el usuario final puede escribir sus credenciales. Este elemento emergente también funciona con el proceso de autenticación en dos fases de Azure AD (2FA) de hello, si es necesario. 

> [!NOTE]
> Este método no se admite todavía en hello biblioteca de autenticación de Azure AD (AAL) para Python o Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Transmisión directa de credenciales de usuario
La aplicación puede proporcionar directamente tooAzure de credenciales de usuario AD. Este método solo funciona con cuentas de usuario con identificador de organización; no es compatible con cuentas de usuario personales de tipo "Live ID", incluidas las que terminan en @outlook.com o @live.com. Además, este método no es compatible con las cuentas de usuario que requieren la autenticación en dos pasos (2FA) de Azure AD.

### <a name="what-do-i-need-toouse-this-approach"></a>¿Qué necesito toouse este enfoque?
* El nombre de dominio de Azure AD. Esto ya aparece en el requisito previo de Hola de este artículo.
* **Aplicación nativa** de Azure AD
* Identificador de la aplicación para aplicación nativa de hello Azure AD
* URI de redirección de hello aplicación nativa de Azure AD
* Establecimiento de permisos delegados


## <a name="step-1-create-an-active-directory-native-application"></a>Paso 1: Crear una aplicación nativa de Active Directory

Cree y configure una aplicación nativa de Azure AD para la autenticación de usuario final con Azure Data Lake Store mediante Azure Active Directory. Para obtener instrucciones, vea cómo [crear una aplicación de Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Al seguir las instrucciones de hello en hello por encima del vínculo, asegúrese de seleccionar **nativo** para el tipo de aplicación, como se muestra en la siguiente captura de pantalla de Hola.

![Crear aplicación de web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Crear aplicación nativa")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Paso 2: Obtener el identificador de aplicación y el URI de redirección

Vea [obtener identificador de la aplicación hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Hola Id. de aplicación (también denominado identificador de cliente de hello en hello portal de Azure clásico) de la aplicación nativa de hello Azure AD.

Hola tooretrieve URI de redireccionamiento, siga estos pasos Hola.

1. En hello Portal de Azure, seleccione **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, busque y haga clic en la aplicación nativa de hello Azure AD que acaba de crear.

2. De hello **configuración** hoja para la aplicación hello, haga clic en **URI de redireccionamiento**.

    ![Obtener URI de redirección](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Copiar valor de hello mostrado.


## <a name="step-3-set-permissions"></a>Paso 3: Establecer permisos

1. En hello Portal de Azure, seleccione **Azure Active Directory**, haga clic en **registros de aplicación**y, a continuación, busque y haga clic en la aplicación nativa de hello Azure AD que acaba de crear.

2. De hello **configuración** hoja para la aplicación hello, haga clic en **los permisos necesarios**y, a continuación, haga clic en **agregar**.

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. Hola **agregar acceso de API** hoja, haga clic en **seleccionar una API**, haga clic en **Azure Data Lake**y, a continuación, haga clic en **seleccione**.

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  Hola **agregar acceso de API** hoja, haga clic en **seleccione permisos**, seleccione Hola casilla toogive **acceso total tooData Lake almacén**y, a continuación, haga clic en **seleccionar** .

    ![ID. DE CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Haga clic en **Done**(Listo).

5. Hola repetición últimos dos pasos permisos toogrant para **API de administración de servicios de Windows Azure** así.
   
## <a name="next-steps"></a>Pasos siguientes
En este artículo se crea una aplicación nativa de Azure AD y recopila información de Hola que necesita en las aplicaciones cliente que creas mediante .NET SDK, SDK de Java, API de REST, etcetera. Ahora puede continuar toohello siguientes artículos que hable acerca de cómo se autentican con almacén de Data Lake toofirst de aplicación web de toouse hello Azure AD y, a continuación, realizan otras operaciones en el almacén de Hola.

* [Introducción al Almacén de Azure Data Lake mediante SDK de .NET](data-lake-store-get-started-net-sdk.md)
* [Introducción a Azure Data Lake Store con el SDK de Java](data-lake-store-get-started-java-sdk.md)
* [Introducción a Azure Data Lake Store mediante la API de REST](data-lake-store-get-started-rest-api.md)

