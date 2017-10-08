---
title: "controles de página de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de los controles de página de hello disponibles para su uso en plantillas del portal de desarrollador en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Controles de página de Azure API Management
Administración de API de Azure proporciona Hola siguientes controles para su uso en plantillas del portal para desarrolladores de Hola.  
  
 toouse un control, póngalo en ubicación de hello deseado en la plantilla del portal para desarrolladores de Hola. Algunos controles, como hello [aplicación acciones](#app-actions) controlar, tienen parámetros, como se muestra en el siguiente ejemplo de Hola.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 valores de Hello para parámetros de Hola se pasan como parte del modelo de datos de hello para la plantilla de Hola. En la mayoría de los casos, simplemente puede pegar en hello previstas ejemplo para cada control se toowork correctamente. Para obtener más información sobre los valores de parámetro hello, puede ver la sección de modelo de datos de Hola para cada plantilla en la que se utiliza un control.  
  
 Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Controles de página de las plantillas del portal para desarrolladores  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [providers](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 Hola `app-actions` control proporciona una interfaz de usuario para interactuar con las aplicaciones en la página de perfil de usuario de hello en el portal para desarrolladores de Hola.  
  
 ![app&amp;#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "Control app-actions de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>parameters  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|appId|Hola Id. de aplicación hello.|  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `app-actions` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Applications](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 Hola `basic-signin` control proporciona un control de inicio de sesión de usuario recopilar información en hello iniciar sesión en la página de portal para desarrolladores de Hola.  
  
 ![basic&amp;#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "Control basic-signin de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `basic-signin` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Sign in](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 Hola `paging-control` proporciona funcionalidad de paginación en developer páginas del portal que muestran una lista de elementos.  
  
 ![paging control](./media/api-management-page-controls/APIM-paging-control.png "Paging control de APIM ")  
  
### <a name="usage"></a>Uso  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `paging-control` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [API list](api-management-api-templates.md#APIList)  
  
-   [Issue list](api-management-issue-templates.md#IssueList)  
  
-   [Product list](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 Hola `providers` control proporciona un control para la selección de proveedores de autenticación de inicio de sesión de hello en la página de portal para desarrolladores de Hola.  
  
 ![control providers](./media/api-management-page-controls/APIM-providers-control.png "Control providers de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `providers` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Sign in](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 Hola `search-control` proporciona funcionalidad de búsqueda en developer páginas del portal que muestran una lista de elementos.  
  
 ![search control](./media/api-management-page-controls/APIM-search-control.png "Search control de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `search-control` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [API list](api-management-api-templates.md#APIList)  
  
-   [Product list](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 Hola `sign-up` control proporciona un control para recopilar información de perfil de usuario en la página de portal para desarrolladores de Hola de registro Hola.  
  
 ![sign&amp;#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "Sign-up control de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `sign-up` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Sign up](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 Hola `subscribe-button` proporciona un control para suscribirse a un producto de tooa de usuario.  
  
 ![subscribe&amp;#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "Control subscribe-button de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>parameters  
 Ninguno.  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `subscribe-button` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Producto](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 Hola `subscription-cancel` control proporciona un control para cancelar un producto de tooa de suscripción en la página de perfil de usuario de hello en el portal para desarrolladores de Hola.  
  
 ![subscription&amp;#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Control subscription-cancel de APIM")  
  
### <a name="usage"></a>Uso  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>parameters  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|subscriptionId|Id. de Hola de hello toocancel de suscripción.|  
|cancelUrl|suscripción de Hello cancelar la dirección URL.|  
  
### <a name="developer-portal-templates"></a>Plantillas del portal para desarrolladores  
 Hola `subscription-cancel` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.  
  
-   [Producto](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).
