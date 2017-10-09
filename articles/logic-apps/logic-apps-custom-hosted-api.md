---
title: "llamar a aaaDeploy y autenticar las API web y las API de REST para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Implemente, autentique y llame a API web y API de REST en flujos de trabajo para integraciones de sistemas con Azure Logic Apps
keywords: API web, API de REST, conectores, flujos de trabajo, integraciones de sistemas, autenticar
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Implementación, llamada y autenticación de API personalizadas como conectores para aplicaciones lógicas

Después de [crear API personalizadas](./logic-apps-create-api-app.md) que proporcione toouse acciones o desencadenadores en la lógica de flujos de trabajo de aplicaciones, debe implementar las API antes de que se pueden llamar. Y aunque se puede llamar a cualquier API desde una aplicación de la lógica para la mejor experiencia de hello, agregue [Swagger metadatos](http://swagger.io/specification/) que describe las operaciones y los parámetros de la API. Este archivo de Swagger ayuda a que su API funcione mejor y se integre con más facilidad con aplicaciones lógicas.

Puede implementar las API como [aplicaciones web](../app-service-web/app-service-web-overview.md), pero considere la posibilidad de implementar las API como [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md), que puede facilitar su trabajo al compilar, hospedar y utilizar las API en la nube de Hola y de forma local. No tienes toochange cualquier código en las API, implemente la aplicación de API de código tooan. Puede hospedar las API en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md), un plataforma como-servicio (PaaS) de la oferta que proporciona una de las maneras de mejor, más fáciles y más escalables de hello para la API de hospedaje.

tooauthenticate las llamadas de lógica aplicaciones tooyour API, puede configurar Active Directory de Azure en hello portal de Azure para que no tenga tooupdate el código. También puede requerir y aplicar la autenticación a través del código de la API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Implementación de la API como aplicación web o aplicación de API

Para poder invocar la API personalizada desde una aplicación de lógica, implementar la API como una aplicación web o aplicación de API tooAzure servicio de aplicaciones. Además, la toomake el documento de Swagger legible por hello diseñador la lógica de aplicación, establecer las propiedades de definición de API de Hola y activar [recursos entre orígenes (CORS) de uso compartido](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para su aplicación web o aplicación de API.

1. Hola portal de Azure, seleccione la aplicación web o una aplicación de API.

2. En la hoja de Hola que se abre, en **API**, elija **definición de la API**. Conjunto hello **ubicación de la definición de API** toohello URL para el archivo swagger.json.

   Por lo general, dirección URL de hello aparece en este formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Archivo de vínculo de tooSwagger de la API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. En **API**, elija **CORS**. Establecer una directiva CORS de Hola para **permite orígenes** demasiado**'*'** (permitir todo).

   Esta configuración permite solicitudes del Diseñador de aplicación lógica.

   ![Permitir solicitudes de API de diseñador de la aplicación lógica tooyour personalizada](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Para obtener más información, consulte estos artículos:

* [Incorporación de metadatos de Swagger para las API web de ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Implementar ASP.NET web API tooAzure servicio de aplicaciones](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Llamada a la API personalizada desde flujos de trabajo de aplicación lógica

Después de configurar las propiedades de definición de API de Hola y CORS, los desencadenadores y las acciones de la API personalizada deben estar disponibles para tooinclude en el flujo de trabajo de aplicación lógica. 

*  tooview sitios Web de Hola que tiene direcciones URL de Swagger, puede examinar los sitios Web de suscripción en hello lógica el Diseñador de aplicaciones.

*  acciones disponibles tooview y entradas, que señala a un documento de Swagger usar hello [HTTP + Swagger acción](../connectors/connectors-native-http-swagger.md).

*  toocall cualquier API, incluidas las API que no tengan o exponer un documento de Swagger, siempre puede crear una solicitud con hello [acción HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Autenticar la API personalizada de llamadas tooyour

Puede proteger las llamadas tooyour API personalizada de las siguientes maneras:

* [Ningún cambio de código](#no-code): proteger su API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) a través de hello portal de Azure, por lo que no dispone de tooupdate el código o volver a implementar la API.

  > [!NOTE]
  > De forma predeterminada, la autenticación de Azure AD de hello activar Hola portal de Azure no proporciona autorización específica. Por ejemplo, esta autenticación bloquea su toojust API una específicos del inquilino, no tooa un usuario específico o una aplicación. 

* [Actualice el código de la API](#update-code): proteja su API aplicando la [autenticación de certificado](#certificate), la [autenticación básica](#basic) o la [autenticación de Azure AD](#azure-ad-code) mediante código.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Autenticar las llamadas API de tooyour sin cambiar el código

Aquí es pasos generales de Hola para este método:

1. Cree dos [identidades de aplicación de Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): una para la aplicación lógica y otra para la aplicación web (o aplicación de API).

2. tooauthenticate tooyour de llamadas API, utilice credenciales de hello (Id. de cliente y secreto) para hello [entidad de servicio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) que tiene asociados con hello identidad de aplicación de Azure AD para la aplicación lógica.

3. Incluir identificadores de aplicaciones de hello en la definición de aplicación lógica.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Parte 1: Creación de una identidad de aplicación de Azure AD para la aplicación lógica

La aplicación lógica usa este tooauthenticate de identidad de aplicación de Azure AD en Azure AD. Solo tiene tooset esta identidad de una vez para su directorio. Por ejemplo, puede elegir toouse Hola misma identidad para todas las aplicaciones lógicas, aunque puede crear identidades únicas para cada aplicación lógica. Puede configurar estas identidades en el portal de Azure, hello [portal de Azure clásico](#app-identity-logic-classic), o use [PowerShell](#powershell).

**Crear la identidad de aplicación de hello para la aplicación lógica en hello portal de Azure**

1. Hola [portal de Azure](https://portal.azure.com "https://portal.azure.com"), elija **Azure Active Directory**. 

2. Confirme que se encuentra en hello mismo directorio que la aplicación web o una aplicación de API.

   > [!TIP]
   > directorios de tooswitch, haga clic en el perfil y seleccionar otro directorio. O bien, elija **Información general** > **Cambiar directorio**.

3. En el menú de directorio de hello, en **administrar**, elija **registros de aplicaciones** > **nuevo registro de aplicación**.

   > [!TIP]
   > De forma predeterminada, lista de registros de aplicaciones de hello muestra todos los registros de aplicación en el directorio. tooview sólo los registros de aplicación, cuadro de búsqueda de toohello siguiente, seleccione **mis aplicaciones**. 

   ![Crear registro de aplicaciones](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Asigne un nombre a la identidad de aplicación, deje **tipo de aplicación** establecido demasiado**aplicación Web / API**, proporcionar una única cadena con formato como un dominio para **dirección URL de inicio de sesión**y elija  **Crear**.

   ![Proporcionar un nombre y una dirección URL de inicio de sesión para la identidad de aplicación](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   identidad de aplicación Hola que creó para la aplicación lógica ahora aparece en la lista de registros de aplicación Hola.

   ![Identidad de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. En la lista de registros de aplicaciones de hello, seleccione la nueva identidad de aplicación. Copie y guarde hello **Id. de aplicación** toouse como Hola "Id. de cliente" de la aplicación lógica en la parte 3.

   ![Copiar y guardar el identificador de aplicación para la aplicación lógica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Si la configuración de la identidad de aplicación no está visible, elija **Configuración** o **Toda la configuración**.

7. En **Acceso de API**, elija **Claves**. En **Descripción**, proporcione un nombre para la clave. En **Expira**, seleccione una duración para la clave.

   clave de Hola que va a crear actúa como de la identidad de aplicación de Hola "secreto" o la contraseña para la aplicación lógica.

   ![Crear clave para la identidad de aplicación lógica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. En la barra de herramientas de hello, elija **guardar**. En **Valor**, ahora aparece su clave. 
**Asegúrese de toocopy seguro y guardar la clave de** para su uso posterior porque la clave de hello está oculto cuando sale de hoja clave Hola.

   Cuando se configura la aplicación lógica en la parte 3, especifique esta clave como Hola "secreto" o la contraseña.

   ![Copiar y guardar la clave para más tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Crear la identidad de aplicación de hello para la aplicación lógica en hello portal de Azure clásico**

1. En el portal de Azure clásico de Hola, elija [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Seleccione Hola mismo directorio que se use para la aplicación web o una aplicación de API.

3. En hello **aplicaciones** ficha, elija **agregar** final Hola de página Hola.

4. Asigne un nombre a la identidad de aplicación y elija **Siguiente** (flecha derecha).

5. En **Propiedades de la aplicación**, proporcione una cadena única con formato de dominio para **Dirección URL de inicio de sesión** y **URI de id. de aplicación**, y elija **Completar** (marca de verificación).

6. En hello **configurar** ficha, copiar y guardar hello **Id. de cliente** para su toouse de aplicación lógica en la parte 3.

7. En **claves**, abra hello **seleccione duración** lista. Seleccione una duración para la clave.

   clave de Hola que va a crear actúa como de la identidad de aplicación de Hola "secreto" o la contraseña para la aplicación lógica.

8. En hello parte inferior de la página de hello, elija **guardar**. Es posible que tenga toowait unos segundos.

9. En **claves**, realice toocopy seguro y Guardar clave de Hola que aparece ahora. 

   Cuando se configura la aplicación lógica en la parte 3, especifique esta clave como Hola "secreto" o la contraseña.

Para obtener más información, obtenga información acerca de cómo demasiado [configurar el inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Crear la identidad de aplicación de hello para la aplicación lógica en PowerShell**

Puede realizar esta tarea mediante Azure Resource Manager con PowerShell. En PowerShell, ejecute estos comandos:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Realizar seguro hello toocopy **Id. de inquilino** Hola (GUID para el inquilino de Azure AD), **Id. de aplicación**y la contraseña de Hola que ha usado.

Para obtener más información, obtenga información acerca de cómo demasiado [crear una entidad de servicio con PowerShell tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Parte 2: Creación de una identidad de aplicación de Azure AD para la aplicación web o de API

Si ya se ha implementado la aplicación web o una aplicación de API, puede activar la autenticación y crear identidad de aplicación Hola Hola portal de Azure. En caso contrario, puede [activar la autenticación cuando implemente con una plantilla de Azure Resource Manager](#authen-deploy). 

**Crear la identidad de aplicación hello y activar la autenticación en el portal de Azure para aplicaciones implementadas de Hola**

1. Hola [portal de Azure](https://portal.azure.com "https://portal.azure.com"), busque y seleccione la aplicación web o una aplicación de API. 

2. Haga clic en **Configuración** y elija **Autenticación/autorización**. En **Autenticación de App Service**, elija **Activar** la autenticación. En **Proveedores de autenticación**, elija **Azure Active Directory**.

   ![Activar la autenticación](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Ahora cree una identidad de aplicación para la aplicación web o de API como se muestra aquí. En hello **configuración de Azure Active Directory** hoja, establezca **modo de administración** demasiado**Express**. Elija **Crear nueva aplicación de AD**. Asigne un nombre a la identidad de aplicación y elija **Aceptar**. 

   ![Crear una identidad de aplicación para la aplicación web o de API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. En hello **autenticación / hoja de autorización**, elija **guardar**.

Ahora debe buscar Id. de cliente de Hola e Id. de inquilino para identidad de aplicación Hola que esté asociada con la aplicación web o una aplicación de API. Ha usado estos identificadores en la parte 3. Por tanto, continúe con estos pasos para el portal de Azure de Hola o [portal de Azure clásico](#find-id-classic).

**Encuentra el Id. de cliente de la identidad de aplicación y el identificador de inquilinos para su aplicación web o API en hello portal de Azure**

1. En **Proveedores de autenticación**, elija **Azure Active Directory**. 

   ![Elegir "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. En hello **configuración de Azure Active Directory** hoja, establezca **modo de administración** demasiado**avanzadas**.

3. Hola copia **Id. de cliente**y guardar dicho GUID para su uso en la parte 3.

   > [!TIP] 
   > Si **Id. de cliente** y **dirección Url del emisor** no aparecen, pruebe a actualizar Hola portal de Azure y repita el paso 1.

4. En **dirección Url del emisor**, copiar y guardar solo Hola parte 3 como GUID. También puede usar este GUID en la plantilla de implementación de su aplicación web o de API, si es necesario.

   Este GUID es para su inquilino específico ("Identificador de inquilino") y debería aparecer en esta dirección URL: `https://sts.windows.net/{GUID}`

5. Sin guardar los cambios, cierre hello **configuración de Azure Active Directory** hoja.

<a name="find-id-classic"></a>

**Encuentra el Id. de cliente de la identidad de aplicación y el Id. de inquilinos para su aplicación web o API en hello portal de Azure clásico**

1. En el portal de Azure clásico de Hola, elija [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Seleccione el directorio de Hola que usas para su aplicación web o aplicación de API.

3. Hola **búsqueda** cuadro, busque y seleccione la identidad de aplicación Hola para su aplicación web o aplicación de API.

4. En hello **configurar** ficha, Hola copia **Id. de cliente**y guardar dicho GUID para su uso en la parte 3.

5. Después de obtener Id. de cliente de hello, en parte inferior de Hola de hello **configurar** ficha, elija **ver extremos**.

6. Copiar dirección URL de Hola para **documento de metadatos de federación**y busque la dirección URL de toothat.

7. En el documento de metadatos de Hola que se abre, busque raíz hello **EntityDescriptor identificador** elemento, que tiene un **entityID** atributo con este formato:`https://sts.windows.net/{GUID}` 

      Hola GUID en este atributo es GUID específico de su inquilino (identificador de inquilino).

8. Copie el Id. de inquilino de Hola y guardar ese identificador para su uso en la parte 3 así como toouse en la aplicación web o una plantilla de implementación de la aplicación de API, si es necesario.

Para más información, consulte los temas siguientes:

* [Autenticación de usuario para aplicaciones de API en Azure App Service](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Activación de la autenticación cuando implemente con una plantilla de Azure Resource Manager**

Todavía debe crear una identidad de aplicación de Azure AD para su aplicación web o API que difiera de la identidad de aplicación hello para la aplicación lógica. identidad de aplicación de hello toocreate, Hola de seguimiento anterior pasos en la parte 2 de hello portal de Azure. También puede seguir los pasos de hello en la parte 1, pero debe toouse seguro de la aplicación web o una aplicación de API real `https://{URL}` para **dirección URL de inicio de sesión** y **App ID URI**. De estos pasos, tendrá toosave tanto cliente hello identificador y el identificador de inquilino para su uso en la plantilla de implementación de la aplicación y también para parte 3.

> [!NOTE]
> Cuando se crea la identidad de aplicación hello Azure AD de su aplicación web o aplicación de API, debe usar Hola portal de Azure o portal de Azure clásico, en lugar de PowerShell. Hola PowerShell commandlet no configure los permisos de hello necesario toosign a los usuarios en un sitio Web.

Después de obtener Id. de cliente de Hola y el Id. de inquilino, incluir estos identificadores como un subresource de su aplicación web o aplicación de API en la plantilla de implementación:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically implementar una aplicación web en blanco y una aplicación lógica junto con la autenticación de Azure Active Directory, [vista Hola plantilla completa aquí](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), o haga clic en **implementar tooAzure** aquí:

[![Implementar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Parte 3: Rellenar la sección de autorización de hello en la aplicación lógica

plantilla anterior Hola ya tiene esta sección autorización configurar, pero si directamente a crear la aplicación de la lógica de hello, debe incluir la sección de hello autorización completa.

Abra la definición de aplicación lógica en la vista de código, vaya toohello **HTTP** Hola de búsqueda, en una sección de acción **autorización** sección e incluya esta línea:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Elemento | Descripción |
| ------- | ----------- |
| tenant |Hola GUID para el inquilino de hello Azure AD |
| audience |Necesario. Hola GUID para el recurso de destino de Hola que desea tooaccess - Hola Id. de cliente de la identidad de aplicación Hola para su aplicación web o aplicación de API |
| clientId |Hola GUID para solicitar acceso - Hola Id. de cliente de la identidad de aplicación hello para la aplicación lógica de cliente de Hola |
| secret |Necesario. Hola clave o contraseña de identidad de aplicación cliente de Hola que está solicitando el token de acceso de Hola Hola |
| type |tipo de autenticación de Hola. Para la autenticación ActiveDirectoryOAuth, el valor de hello es `ActiveDirectoryOAuth`. |

Por ejemplo:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Protección de las llamadas API mediante código

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Autenticación de certificados

toovalidate hello las solicitudes entrantes de su aplicación web de lógica aplicación tooyour o API, puede usar certificados de cliente. Obtenga información acerca de tooset el código, [la autenticación mutua de tooconfigure TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

Hola **autorización** sección, incluya esta línea: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Elemento | Descripción |
| ------- | ----------- |
| type |Necesario. tipo de autenticación de Hola. Para los certificados de cliente SSL, debe ser el valor de hello `ClientCertificate`. |
| Contraseña |Necesario. contraseña de Hola para acceder al certificado de cliente de hello (archivo PFX) |
| pfx |Necesario. Contenido codificado en base64 del certificado de cliente de hello (archivo PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Autenticación básica

toovalidate las solicitudes entrantes de su aplicación web de lógica aplicación tooyour o API, puede usar la autenticación básica, por ejemplo, un nombre de usuario y una contraseña. La autenticación básica es un patrón común, y puede utilizar esta autenticación en cualquier toobuild de lenguaje que se utiliza la aplicación web o una aplicación de API.

Hola **autorización** sección, incluya esta línea:

`{"type": "basic", "username": "username", "password": "password"}`.

| Elemento | Descripción |
| --- | --- |
| type |Necesario. tipo de autenticación de Hola. Para la autenticación básica, debe ser el valor de hello `Basic`. |
| nombre de usuario |Necesario. nombre de usuario de Hello para la autenticación |
| Contraseña |Necesario. contraseña de Hello para la autenticación |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Autenticación de Azure Active Directory mediante código

De forma predeterminada, la autenticación de Azure AD de hello activar Hola portal de Azure no proporciona autorización específica. Por ejemplo, esta autenticación bloquea su toojust API una específicos del inquilino, no tooa un usuario específico o una aplicación. 

acceso de aplicación lógica toorestrict API tooyour a través del código, extraer el encabezado de Hola que tiene Hola JSON web token (JWT). Comprobar la identidad del llamador de Hola y rechazar las solicitudes que no coinciden.

Si sigue adelante, tooimplement esta autenticación completamente en su propio código, no use hello y portal de Azure, obtenga información acerca de cómo demasiado [autenticarse con local de Active Directory en la aplicación de Azure](../app-service-web/web-sites-authentication-authorization.md).

toocreate una identidad de aplicación para la aplicación lógica y utiliza esa identidad toocall su API, debe seguir los pasos anteriores de Hola.

## <a name="next-steps"></a>Pasos siguientes

* [Comprobación del rendimiento de la aplicación lógica con alertas y registros de diagnóstico](logic-apps-monitor-your-logic-apps.md)