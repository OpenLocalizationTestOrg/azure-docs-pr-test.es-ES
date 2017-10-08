---
title: aaaQuickstart para hello Azure AD Graph API | Documentos de Microsoft
description: "Hola API Graph de Azure Active Directory proporciona acceso mediante programación tooAzure AD a través de extremos de API de REST de OData. Las aplicaciones pueden usar Hola API Graph tooperform crear, leer, actualizar y eliminar operaciones (CRUD) en objetos y datos de directorio."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Inicio rápido para hello Azure AD Graph API
Hola API Graph de Azure Active Directory (AD) proporciona acceso mediante programación tooAzure AD a través de extremos de API de REST de OData. Las aplicaciones pueden usar Hola API Graph tooperform crear, leer, actualizar y eliminar operaciones (CRUD) en objetos y datos de directorio. Por ejemplo, puede usar la API Graph hello toocreate un nuevo usuario, vista o actualizar las propiedades del usuario, cambiar la contraseña del usuario, compruebe la pertenencia a grupos de acceso basado en roles, deshabilitar o eliminar Hola usuario. Para obtener más información sobre las características de la API de gráficos de Hola y escenarios de aplicaciones, consulte [API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) y [los requisitos previos de Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Se recomienda encarecidamente que utilice [Microsoft Graph](https://developer.microsoft.com/graph) en lugar de Azure AD Graph API tooaccess recursos de Active Directory. Nuestros esfuerzos de desarrollo ahora se centran en Microsoft Graph y no están previstas realizar mejoras adicionales para la API de Azure AD Graph. Hay un número muy limitado de escenarios para los que Azure AD Graph API todavía podría ser adecuado; Para obtener más información, vea hello [Microsoft Graph o hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) entrada de blog en hello centro de desarrollo de Office.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>¿Cómo tooconstruct una URL de la API de Graph
En la API Graph, datos de directorio tooaccess y objetos (es decir, recursos o entidades) con el que desea que las operaciones CRUD tooperform, puede utilizar direcciones URL basadas en hello protocolo Open Data (OData). Hello direcciones URL usadas en la API Graph constan de cuatro partes principales: raíz, identificador del inquilino, ruta de acceso de recursos y opciones de cadena de consulta de servicio: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Ejemplo hello de hello después de la dirección URL: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Raíz del servicio**: en la API de Graph de Azure AD, raíz del servicio hello es siempre https://graph.windows.net.
* **Identificador de inquilino**: en esta sección puede ser un nombre de dominio (registrado) comprobado, Hola anterior ejemplo, contoso.com. También puede ser un inquilino objeto identificador o hello "myorganization" o "me" alias. Para obtener más información, consulte [dirigirse a entidades y operaciones en hello API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Ruta de acceso del recurso**: en esta sección de una dirección URL identifica el recurso de hello toobe interactuado con (usuarios, grupos, un usuario determinado, o un grupo determinado, etcetera.) En el ejemplo de Hola anterior, es Hola "grupos de nivel superior" tooaddress este conjunto de recursos. También se puede dirigir una entidad concreta, como por ejemplo, “users/{objectId}” o “users/userPrincipalName”.
* **Parámetros de consulta**: un signo de interrogación (?) separa la sección de ruta de acceso de recursos de Hola de sección de parámetros de consulta de Hola. parámetro de consulta "api-version" Hello es necesario en todas las solicitudes de hello API Graph. Hola API Graph también admite Hola siguientes opciones de consulta de OData: **$filter**, **$orderby**, **$expand**, **$top**y **$format**. Hola siguientes opciones de consulta no se admite actualmente: **$count**, **$inlinecount**, y **$skip**. Para obtener más información, consulte [Consultas admitidas, filtros y opciones de paginación en la API de gráficos de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Versiones de la API Graph
Especificar versión de Hola para una solicitud de API Graph en el parámetro de consulta "api-version" Hola. En el caso de la versión 1.5 y posterior, use un valor de versión numérico; api-version=1.6. Para las versiones anteriores, se utiliza una cadena de fecha que se adhiera toohello formato aaaa-MM-DD; Por ejemplo, api-version = 2013-11-08. Características de vista previa, usar cadena de Hola "beta"; Por ejemplo, api-version = beta. Para más información sobre las diferencias entre las distintas versiones de la API Graph, consulte [Control de versiones de API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Metadatos de la API Graph
Hola tooreturn archivo de metadatos de API Graph, agregar segmento "$metadata" hello después de identificador de inquilino de hello en hello URL. por ejemplo, hello sigue URL devuelve metadatos para una compañía de demostración: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Puede escribir esta dirección URL en la barra de direcciones de Hola de un explorador de web toosee Hola metadatos. Hello documento de metadatos CSDL devuelto describe entidades de Hola y tipos complejos, sus propiedades y las funciones hello y acciones expuestas por la versión de Hola de API de Graph solicitado. La omisión de parámetro de versión de la api de hello devuelve los metadatos para la versión más reciente de Hola.

## <a name="common-queries"></a>Consultas comunes
[Azure AD Graph API Common consultas](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) enumeran las consultas comunes que pueden usarse con hello Azure AD Graph, incluidas las consultas que pueden ser recursos de nivel superior de tooaccess utilizadas en las operaciones de tooperform de directorio y las consultas en el directorio.

Por ejemplo, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` devuelve la información de la compañía en el directorio contoso.com.

O `https://graph.windows.net/contoso.com/users?api-version=1.6` enumera todos los objetos de usuario en el directorio de hello contoso.com.

## <a name="using-hello-graph-explorer"></a>Uso de hello Explorador de gráficos
Puede usar Hola Explorador de gráficos para datos de directorio de Azure AD Graph API tooquery Hola Hola que compile su aplicación.

Hello siguiente es resultado de hello vea si tuviera toonavigate toohello Explorador de gráficos, inicie sesión en y escriba `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay todos los usuarios de Hola Hola directorio del usuario que inició sesión:

![Azure AD api graph explorador](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Hola carga Explorador de gráficos**: Hola tooload herramienta, vaya demasiado[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Haga clic en **inicio de sesión** e inicie sesión con su toorun de credenciales de cuenta de Azure AD Hola Explorador de gráficos en su inquilino. Si ejecuta el Explorador de gráficos en su propio inquilino, usted o su administrador necesita tooconsent durante el inicio de sesión. Si dispone de una suscripción a Office 365, tendrá automáticamente un inquilino de Azure AD. credenciales de Hello usar toosign en tooOffice 365 son, de hecho, cuentas de Azure AD y se pueden usar estas credenciales con el Explorador de gráfico.

**Ejecutar una consulta**: toorun una consulta, escriba la consulta en el cuadro de texto de solicitud de Hola y haga clic en **obtener** o haga clic en hello **escriba** clave. resultados de Hola se muestran en el cuadro de respuesta de Hola. Por ejemplo, `https://graph.windows.net/myorganization/groups?api-version=1.6` enumera todos los objetos de grupo en hello firmado en el directorio del usuario.

Hola nota después de características y limitaciones de hello Explorador de gráficos:

* Funcionalidad Autocompletar en conjuntos de recursos. toosee esta funcionalidad, haga clic en hello solicitar cuadro de texto (donde aparece dirección URL de la empresa de hello). Puede seleccionar un conjunto de lista desplegable de Hola de recursos.
* Admite Hola "me" y "myorganization" alias de direccionamiento. Por ejemplo, puede usar `https://graph.windows.net/me?api-version=1.6` tooreturn Hola objeto usuario Hola con sesión iniciada o `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn todos los usuarios en el directorio actual de Hola.
* Una sección de encabezados de respuesta. Esta sección se puede utilizar toohelp solucionar los problemas que se producen al ejecutar las consultas.
* Un visor JSON de respuesta de hello con capacidades de expansión y contracción.
* No permite mostrar fotos en miniatura.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Uso de Fiddler toowrite toohello directory
Para fines de Hola de esta guía de inicio rápido, puede usar Hola depurador Web de Fiddler toopractice realizar operaciones en el directorio de Azure AD ' escritura'. Para obtener más información y tooinstall Fiddler, consulte [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

En el ejemplo de Hola siguiente, se usa depurador Web de Fiddler toocreate un nuevo grupo de seguridad 'MyTestGroup' en su directorio Azure AD.

**Obtener un token de acceso**: tooaccess Azure AD Graph, los clientes son toosuccessfully necesario autenticar tooAzure AD primero. Para obtener más información, consulte [Escenarios de autenticación en Azure AD](active-directory-authentication-scenarios.md).

**Crear y ejecutar una consulta**: Hola completa pasos:

1. Abra el depurador Web de Fiddler y cambie toohello **compositor** ficha.
2. Debido a que desea toocreate un nuevo grupo de seguridad, seleccione **Post** como Hola método HTTP en el menú desplegable de Hola. Para obtener más información sobre las operaciones y permisos en un objeto de grupo, consulte [grupo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) en hello [referencia de API de REST de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. Hola campo junto demasiado**Post**, escriba en el siguiente hello como dirección URL de solicitud de Hola: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Debe sustituir mytenantdomain por nombre de dominio de Hola de su propio directorio de Azure AD.
   > 
   > 
4. En el campo de hello directamente debajo de la entrada de lista desplegable, escriba Hola siguiente:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Sustituya el &lt;el token de acceso&gt; con el token de acceso de hello para el directorio de Azure AD.
   > 
   > 
5. Hola **cuerpo de la solicitud** , a continuación, escriba Hola siguiente:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Para más información sobre la creación de grupos, consulte [Crear un grupo](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Para obtener más información sobre las entidades de Azure AD y los tipos expuestos por Graph e información acerca de las operaciones de Hola que se pueden realizar en ellos con Graph, vea [referencia de API de REST de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Más información sobre [los ámbitos de permiso de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

