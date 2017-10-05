---
title: Plantillas de perfil de usuario en Azure API Management | Microsoft Docs
description: "Aprenda a personalizar el contenido de las páginas de perfil de usuario del portal para desarrolladores en Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="5cb28-103">Plantillas de perfil de usuario en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5cb28-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="5cb28-104">Azure API Management le ofrece la posibilidad de personalizar el contenido de las páginas del portal para desarrolladores mediante un conjunto de plantillas que configuran su contenido.</span><span class="sxs-lookup"><span data-stu-id="5cb28-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5cb28-105">Por medio de la sintaxis [DotLiquid](http://dotliquidmarkup.org/) y el editor que prefiera, como [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) (DotLiquid para diseñadores), y un conjunto proporcionado de [recursos de cadena](api-management-template-resources.md#strings), [recursos de glifo](api-management-template-resources.md#glyphs) y [controles de página](api-management-page-controls.md) localizados, puede disponer de una gran flexibilidad para configurar el contenido de las páginas como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="5cb28-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5cb28-106">Las plantillas de esta sección le permiten personalizar el contenido de las páginas de perfil de usuario en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cb28-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="5cb28-107">Perfil</span><span class="sxs-lookup"><span data-stu-id="5cb28-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="5cb28-108">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="5cb28-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="5cb28-109">Applications</span><span class="sxs-lookup"><span data-stu-id="5cb28-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="5cb28-110">Update account info</span><span class="sxs-lookup"><span data-stu-id="5cb28-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="5cb28-111">En la siguiente documentación se incluyen plantillas predeterminadas de ejemplo; sin embargo, están sujetas a cambios debido a mejoras continuas.</span><span class="sxs-lookup"><span data-stu-id="5cb28-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="5cb28-112">Puede ver las plantillas predeterminadas en vivo en el portal para desarrolladores; para ello, vaya hasta a las plantillas individuales que desee.</span><span class="sxs-lookup"><span data-stu-id="5cb28-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="5cb28-113">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="5cb28-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5cb28-114"><a name="Profile"></a> Perfil</span><span class="sxs-lookup"><span data-stu-id="5cb28-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="5cb28-115">La plantilla de **perfil** le permite personalizar la sección de perfil de usuario de la página de perfil de usuario en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cb28-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="5cb28-116">![Página de perfil de usuario](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Página de perfil de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="5cb28-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5cb28-117">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="5cb28-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5cb28-118">Controles</span><span class="sxs-lookup"><span data-stu-id="5cb28-118">Controls</span></span>  
 <span data-ttu-id="5cb28-119">Esta plantilla no puede utilizar los [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5cb28-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5cb28-120">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="5cb28-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5cb28-121">Las plantillas de [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) comparten el mismo modelo de datos y reciben los mismos datos de plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cb28-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="5cb28-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5cb28-122">Property</span></span>|<span data-ttu-id="5cb28-123">Escriba</span><span class="sxs-lookup"><span data-stu-id="5cb28-123">Type</span></span>|<span data-ttu-id="5cb28-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="5cb28-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5cb28-125">firstName</span><span class="sxs-lookup"><span data-stu-id="5cb28-125">firstName</span></span>|<span data-ttu-id="5cb28-126">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-126">string</span></span>|<span data-ttu-id="5cb28-127">Nombre del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-127">First name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-128">lastName</span><span class="sxs-lookup"><span data-stu-id="5cb28-128">lastName</span></span>|<span data-ttu-id="5cb28-129">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-129">string</span></span>|<span data-ttu-id="5cb28-130">Apellido del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-131">companyName</span><span class="sxs-lookup"><span data-stu-id="5cb28-131">companyName</span></span>|<span data-ttu-id="5cb28-132">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-132">string</span></span>|<span data-ttu-id="5cb28-133">El nombre de la empresa del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5cb28-134">addresserEmail</span></span>|<span data-ttu-id="5cb28-135">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-135">string</span></span>|<span data-ttu-id="5cb28-136">Dirección de correo electrónico del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="5cb28-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5cb28-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5cb28-138">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-138">string</span></span>|<span data-ttu-id="5cb28-139">Dirección URL relativa para ver el análisis para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="5cb28-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5cb28-140">subscriptions</span></span>|<span data-ttu-id="5cb28-141">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5cb28-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5cb28-142">Las suscripciones para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="5cb28-143">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="5cb28-143">applications</span></span>|<span data-ttu-id="5cb28-144">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5cb28-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5cb28-145">Las aplicaciones del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="5cb28-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-146">changePasswordUrl</span></span>|<span data-ttu-id="5cb28-147">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-147">string</span></span>|<span data-ttu-id="5cb28-148">La dirección URL relativa para cambiar la contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="5cb28-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5cb28-150">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-150">string</span></span>|<span data-ttu-id="5cb28-151">La dirección URL relativa para cambiar el nombre y el correo electrónico para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="5cb28-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5cb28-152">canChangePassword</span></span>|<span data-ttu-id="5cb28-153">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-153">boolean</span></span>|<span data-ttu-id="5cb28-154">Si el usuario actual puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="5cb28-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="5cb28-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5cb28-155">isSystemUser</span></span>|<span data-ttu-id="5cb28-156">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-156">boolean</span></span>|<span data-ttu-id="5cb28-157">Si el usuario actual es miembro de uno de los [grupos](api-management-key-concepts.md#groups) integrados.</span><span class="sxs-lookup"><span data-stu-id="5cb28-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5cb28-158">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="5cb28-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="5cb28-159"><a name="Subscriptions"></a> Suscripciones</span><span class="sxs-lookup"><span data-stu-id="5cb28-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="5cb28-160">La plantilla de **suscripciones** le permite personalizar la sección de suscripciones de la página de perfil de usuario en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cb28-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="5cb28-161">![Página de suscripción de usuario](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Página de suscripción de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="5cb28-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5cb28-162">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="5cb28-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5cb28-163">Controles</span><span class="sxs-lookup"><span data-stu-id="5cb28-163">Controls</span></span>  
 <span data-ttu-id="5cb28-164">Esta plantilla puede utilizar los siguientes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5cb28-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5cb28-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="5cb28-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="5cb28-166">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="5cb28-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5cb28-167">Las plantillas de [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) comparten el mismo modelo de datos y reciben los mismos datos de plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cb28-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="5cb28-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5cb28-168">Property</span></span>|<span data-ttu-id="5cb28-169">Escriba</span><span class="sxs-lookup"><span data-stu-id="5cb28-169">Type</span></span>|<span data-ttu-id="5cb28-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="5cb28-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5cb28-171">firstName</span><span class="sxs-lookup"><span data-stu-id="5cb28-171">firstName</span></span>|<span data-ttu-id="5cb28-172">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-172">string</span></span>|<span data-ttu-id="5cb28-173">Nombre del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-173">First name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-174">lastName</span><span class="sxs-lookup"><span data-stu-id="5cb28-174">lastName</span></span>|<span data-ttu-id="5cb28-175">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-175">string</span></span>|<span data-ttu-id="5cb28-176">Apellido del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-177">companyName</span><span class="sxs-lookup"><span data-stu-id="5cb28-177">companyName</span></span>|<span data-ttu-id="5cb28-178">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-178">string</span></span>|<span data-ttu-id="5cb28-179">El nombre de la empresa del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5cb28-180">addresserEmail</span></span>|<span data-ttu-id="5cb28-181">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-181">string</span></span>|<span data-ttu-id="5cb28-182">Dirección de correo electrónico del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="5cb28-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5cb28-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5cb28-184">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-184">string</span></span>|<span data-ttu-id="5cb28-185">Dirección URL relativa para ver el análisis para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="5cb28-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5cb28-186">subscriptions</span></span>|<span data-ttu-id="5cb28-187">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5cb28-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5cb28-188">Las suscripciones para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="5cb28-189">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="5cb28-189">applications</span></span>|<span data-ttu-id="5cb28-190">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5cb28-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5cb28-191">Las aplicaciones del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="5cb28-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-192">changePasswordUrl</span></span>|<span data-ttu-id="5cb28-193">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-193">string</span></span>|<span data-ttu-id="5cb28-194">La dirección URL relativa para cambiar la contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="5cb28-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5cb28-196">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-196">string</span></span>|<span data-ttu-id="5cb28-197">La dirección URL relativa para cambiar el nombre y el correo electrónico para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="5cb28-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5cb28-198">canChangePassword</span></span>|<span data-ttu-id="5cb28-199">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-199">boolean</span></span>|<span data-ttu-id="5cb28-200">Si el usuario actual puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="5cb28-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="5cb28-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5cb28-201">isSystemUser</span></span>|<span data-ttu-id="5cb28-202">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-202">boolean</span></span>|<span data-ttu-id="5cb28-203">Si el usuario actual es miembro de uno de los [grupos](api-management-key-concepts.md#groups) integrados.</span><span class="sxs-lookup"><span data-stu-id="5cb28-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5cb28-204">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="5cb28-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="5cb28-205"><a name="Applications"></a> Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5cb28-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="5cb28-206">La plantilla de **aplicaciones** le permite personalizar la sección de suscripciones de la página de perfil de usuario en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cb28-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="5cb28-207">![Página de aplicaciones de cuenta de usuario](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Página de aplicaciones de cuenta de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="5cb28-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5cb28-208">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="5cb28-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5cb28-209">Controles</span><span class="sxs-lookup"><span data-stu-id="5cb28-209">Controls</span></span>  
 <span data-ttu-id="5cb28-210">Esta plantilla puede utilizar los siguientes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5cb28-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5cb28-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="5cb28-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="5cb28-212">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="5cb28-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5cb28-213">Las plantillas de [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) comparten el mismo modelo de datos y reciben los mismos datos de plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cb28-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="5cb28-214">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5cb28-214">Property</span></span>|<span data-ttu-id="5cb28-215">Escriba</span><span class="sxs-lookup"><span data-stu-id="5cb28-215">Type</span></span>|<span data-ttu-id="5cb28-216">Descripción</span><span class="sxs-lookup"><span data-stu-id="5cb28-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5cb28-217">firstName</span><span class="sxs-lookup"><span data-stu-id="5cb28-217">firstName</span></span>|<span data-ttu-id="5cb28-218">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-218">string</span></span>|<span data-ttu-id="5cb28-219">Nombre del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-219">First name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-220">lastName</span><span class="sxs-lookup"><span data-stu-id="5cb28-220">lastName</span></span>|<span data-ttu-id="5cb28-221">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-221">string</span></span>|<span data-ttu-id="5cb28-222">Apellido del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-223">companyName</span><span class="sxs-lookup"><span data-stu-id="5cb28-223">companyName</span></span>|<span data-ttu-id="5cb28-224">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-224">string</span></span>|<span data-ttu-id="5cb28-225">El nombre de la empresa del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="5cb28-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5cb28-226">addresserEmail</span></span>|<span data-ttu-id="5cb28-227">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-227">string</span></span>|<span data-ttu-id="5cb28-228">Dirección de correo electrónico del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="5cb28-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5cb28-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5cb28-230">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-230">string</span></span>|<span data-ttu-id="5cb28-231">Dirección URL relativa para ver el análisis para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="5cb28-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5cb28-232">subscriptions</span></span>|<span data-ttu-id="5cb28-233">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5cb28-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5cb28-234">Las suscripciones para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="5cb28-235">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="5cb28-235">applications</span></span>|<span data-ttu-id="5cb28-236">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5cb28-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5cb28-237">Las aplicaciones del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="5cb28-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-238">changePasswordUrl</span></span>|<span data-ttu-id="5cb28-239">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-239">string</span></span>|<span data-ttu-id="5cb28-240">La dirección URL relativa para cambiar la contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="5cb28-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5cb28-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5cb28-242">string</span><span class="sxs-lookup"><span data-stu-id="5cb28-242">string</span></span>|<span data-ttu-id="5cb28-243">La dirección URL relativa para cambiar el nombre y el correo electrónico para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="5cb28-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="5cb28-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5cb28-244">canChangePassword</span></span>|<span data-ttu-id="5cb28-245">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-245">boolean</span></span>|<span data-ttu-id="5cb28-246">Si el usuario actual puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="5cb28-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="5cb28-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5cb28-247">isSystemUser</span></span>|<span data-ttu-id="5cb28-248">boolean</span><span class="sxs-lookup"><span data-stu-id="5cb28-248">boolean</span></span>|<span data-ttu-id="5cb28-249">Si el usuario actual es miembro de uno de los [grupos](api-management-key-concepts.md#groups) integrados.</span><span class="sxs-lookup"><span data-stu-id="5cb28-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5cb28-250">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="5cb28-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="5cb28-251"><a name="UpdateAccountInfo"></a> Update account info</span><span class="sxs-lookup"><span data-stu-id="5cb28-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="5cb28-252">La plantilla para **actualizar información de cuenta** le permite personalizar la página **Actualizar información de cuenta** en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cb28-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="5cb28-253">![Plantillas del portal para desarrolladores de la página de información de cuenta de usuario](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de información de cuenta de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="5cb28-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5cb28-254">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="5cb28-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="5cb28-255">Controles</span><span class="sxs-lookup"><span data-stu-id="5cb28-255">Controls</span></span>  
 <span data-ttu-id="5cb28-256">Esta plantilla no puede utilizar los [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5cb28-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5cb28-257">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="5cb28-257">Data model</span></span>  
 <span data-ttu-id="5cb28-258">Entidad [Información de cuenta de usuario](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="5cb28-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="5cb28-259">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="5cb28-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="5cb28-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cb28-260">Next steps</span></span>
<span data-ttu-id="5cb28-261">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cb28-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>