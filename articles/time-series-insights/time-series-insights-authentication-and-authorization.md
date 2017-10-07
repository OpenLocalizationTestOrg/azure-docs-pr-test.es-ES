---
title: "aaaConfigure autenticación y autorización para una aplicación personalizada que llama hello Azure tiempo serie visión API | Documentos de Microsoft"
description: "Este tutorial le explica cómo tooconfigure autenticación y autorización para una aplicación personalizada que llama hello Azure tiempo serie visión API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Autenticación y autorización para la API de Azure Time Series Insights

Este artículo explica cómo tooconfigure una aplicación personalizada que llama hello Azure tiempo serie visión API.

## <a name="service-principal"></a>Entidad de servicio

Esta sección explica cómo tooconfigure tooaccess de una aplicación Hola tiempo serie visión API en nombre de la aplicación hello. aplicación Hello puede consultar datos o publicar datos de referencia en entorno de visión de la serie de tiempo de hello con credenciales de la aplicación y no las credenciales de usuario de Hola.

Cuando haya una aplicación que necesite tooaccess visión de la serie de tiempo, debe configurar una aplicación de Azure Active Directory y asignar directivas de acceso de datos de hello en entorno de visión de la serie de tiempo de Hola. Este enfoque es preferible toorunning Hola aplicación bajo sus propias credenciales porque:

* Puede asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos. Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo. Por ejemplo, puede permitir Hola aplicación tooonly lee datos en un entorno de visión de la serie de tiempo determinado.
* No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades.
* Puede usar una autenticación de certificados o una aplicación clave tooautomate si ejecuta un script de instalación desatendida.

Este artículo muestra cómo tooperform los pasos a través de Hola portal de Azure. Se centra en una aplicación de inquilino único donde la aplicación hello es toorun previsto en sólo una organización. El usuario normalmente usa aplicaciones de un único inquilino para aplicaciones de línea de negocio que se ejecutan en la organización.

flujo del programa de instalación de Hello consta de tres pasos principales:

1. Creación de una aplicación en Azure Active Directory.
2. Autorizar este entorno de visión de la serie de tiempo de aplicación tooaccess Hola.
3. Usar Id. de aplicación de Hola y clave tooacquire un token toohello `"https://api.timeseries.azure.com/"` público o recurso. símbolo (token) de Hello, a continuación, puede ser hello toocall usa API de visión de Series de tiempo.

Estos son los pasos detallados de Hola:

1. Hola portal de Azure, seleccione **Azure Active Directory** > **registros de aplicaciones** > **nuevo registro de aplicación**.

   ![Nuevo registro de aplicaciones en Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Asigne aplicación hello un toobe del tipo de nombre, seleccione hello **aplicación Web / API**, seleccione cualquier URI válido para **dirección URL de inicio de sesión**y haga clic en **crear**.

   ![Crear aplicación hello en Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Seleccione la aplicación recién creada y copie su editor de texto favorito de tooyour de Id. de aplicación.

   ![Copie el identificador de la aplicación hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Seleccione **claves**, escriba el nombre de clave de hello, expiración de hello seleccione y haga clic en **guardar**.

   ![Selección de las claves de aplicación](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Escriba el nombre de clave de Hola y de expiración y haga clic en Guardar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Copiar clave tooyour de hello, editor de texto que prefiera.

   ![Copie la clave de la aplicación hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Para entorno de visión de la serie de tiempo de hello, seleccione **directivas de acceso de datos** y haga clic en **agregar**.

   ![Agregar entorno de visión de la serie de tiempo de toohello directiva de acceso de datos nueva](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. Hola **Seleccionar usuario** cuadro de diálogo, nombre de la aplicación hello pegar (del paso 2) o identificador de la aplicación (del paso 3).

   ![Buscar una aplicación en el cuadro de diálogo Seleccionar usuario Hola](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Rol de hello seleccione (**lector** para consultar los datos, **colaborador** para consultar los datos y cambiar los datos de referencia) y haga clic en **Aceptar**.

   ![Selección de lector o colaborador en el cuadro de diálogo Seleccionar rol Hola](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Guardar directiva Hola haciendo clic en **Aceptar**.

10. Id. de aplicación de uso hello (del paso 3) y token de hello tooacquire clave (del paso 5) la aplicación en nombre de la aplicación hello. Hello token, a continuación, se puede pasar en hello `Authorization` encabezado cuando las llamadas de aplicación Hola Hola API de visión de Series de tiempo.

    Si está utilizando C#, puede usar Hola después código tooacquire Hola símbolo (token) en nombre de la aplicación hello. Para obtener un ejemplo completo, vea [Consulta de datos mediante C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Pasos siguientes

Identificador de la aplicación de uso hello y clave en la aplicación. Para el código de ejemplo que llama Hola tiempo serie visión API, consulte [consultar datos utilizando C#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Otras referencias

* [API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) de referencia de API de consulta completa Hola
* [Crear un servicio principal Hola portal de Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
