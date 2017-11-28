---
title: "aaa \"plantillas de perfil de usuario en la administración de API de Azure | Documentos de Microsoft\""
description: "Obtenga información acerca de cómo las páginas toocustomize contenido de Hola de hello perfil de usuario en el portal para desarrolladores de hello en la administración de API de Azure."
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
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="aed9e-103">Plantillas de perfil de usuario en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="aed9e-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="aed9e-104">Administración de API de Azure proporciona que Hola contenido de hello toocustomize de capacidad de páginas del portal para desarrolladores con un conjunto de plantillas que configure su contenido.</span><span class="sxs-lookup"><span data-stu-id="aed9e-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="aed9e-105">Usar [DotLiquid](http://dotliquidmarkup.org/) editor hello y sintaxis de su elección, como [DotLiquid a los diseñadores](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), o cambie de tamaño un conjunto proporcionado de [los recursos de cadena](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), y [página controles](api-management-page-controls.md), tienen contenido de gran flexibilidad tooconfigure Hola de páginas de Hola como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="aed9e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="aed9e-106">las plantillas de Hello en esta sección permiten contenido de hello toocustomize de páginas de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="aed9e-107">Perfil</span><span class="sxs-lookup"><span data-stu-id="aed9e-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="aed9e-108">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="aed9e-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="aed9e-109">Applications</span><span class="sxs-lookup"><span data-stu-id="aed9e-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="aed9e-110">Update account info</span><span class="sxs-lookup"><span data-stu-id="aed9e-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="aed9e-111">Plantillas predeterminadas de ejemplo se incluyen en hello siguiendo documentación, pero están toochange asunto debido toocontinuous mejoras.</span><span class="sxs-lookup"><span data-stu-id="aed9e-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="aed9e-112">Puede ver plantillas de hello predeterminado en vivo en el portal para desarrolladores de hello desplazándose plantillas individuales toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="aed9e-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="aed9e-113">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="aed9e-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="aed9e-114"><a name="Profile"></a> Perfil</span><span class="sxs-lookup"><span data-stu-id="aed9e-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="aed9e-115">Hola **perfil** plantilla permite sección de perfil de usuario de toocustomize Hola de página de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="aed9e-116">![Página de perfil de usuario](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Página de perfil de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="aed9e-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="aed9e-117">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="aed9e-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="aed9e-118">Controles</span><span class="sxs-lookup"><span data-stu-id="aed9e-118">Controls</span></span>  
 <span data-ttu-id="aed9e-119">Esta plantilla no puede utilizar los [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="aed9e-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="aed9e-120">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="aed9e-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="aed9e-121">Hola [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) plantillas compartan Hola mismos datos de modelo y reciban Hola datos de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="aed9e-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="aed9e-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="aed9e-122">Property</span></span>|<span data-ttu-id="aed9e-123">Escriba</span><span class="sxs-lookup"><span data-stu-id="aed9e-123">Type</span></span>|<span data-ttu-id="aed9e-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="aed9e-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="aed9e-125">firstName</span><span class="sxs-lookup"><span data-stu-id="aed9e-125">firstName</span></span>|<span data-ttu-id="aed9e-126">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-126">string</span></span>|<span data-ttu-id="aed9e-127">Nombre del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-128">lastName</span><span class="sxs-lookup"><span data-stu-id="aed9e-128">lastName</span></span>|<span data-ttu-id="aed9e-129">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-129">string</span></span>|<span data-ttu-id="aed9e-130">Apellido del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-131">companyName</span><span class="sxs-lookup"><span data-stu-id="aed9e-131">companyName</span></span>|<span data-ttu-id="aed9e-132">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-132">string</span></span>|<span data-ttu-id="aed9e-133">nombre de la compañía de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="aed9e-134">addresserEmail</span></span>|<span data-ttu-id="aed9e-135">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-135">string</span></span>|<span data-ttu-id="aed9e-136">Dirección de correo electrónico del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="aed9e-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="aed9e-138">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-138">string</span></span>|<span data-ttu-id="aed9e-139">Análisis de tooview dirección URL relativa para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="aed9e-140">subscriptions</span></span>|<span data-ttu-id="aed9e-141">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="aed9e-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="aed9e-142">suscripciones de Hello para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-143">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="aed9e-143">applications</span></span>|<span data-ttu-id="aed9e-144">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="aed9e-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="aed9e-145">aplicaciones de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-146">changePasswordUrl</span></span>|<span data-ttu-id="aed9e-147">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-147">string</span></span>|<span data-ttu-id="aed9e-148">Hola relativa URL toochange Hola contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="aed9e-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="aed9e-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="aed9e-150">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-150">string</span></span>|<span data-ttu-id="aed9e-151">Hola relativa toochange Hola nombre y la URL correo electrónico para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="aed9e-152">canChangePassword</span></span>|<span data-ttu-id="aed9e-153">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-153">boolean</span></span>|<span data-ttu-id="aed9e-154">Si el usuario actual de hello puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="aed9e-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="aed9e-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="aed9e-155">isSystemUser</span></span>|<span data-ttu-id="aed9e-156">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-156">boolean</span></span>|<span data-ttu-id="aed9e-157">Si el usuario actual de hello es miembro de uno de hello integrados [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="aed9e-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="aed9e-158">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="aed9e-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="aed9e-159"><a name="Subscriptions"></a> Suscripciones</span><span class="sxs-lookup"><span data-stu-id="aed9e-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="aed9e-160">Hola **suscripciones** plantilla permite sección de suscripciones de hello toocustomize de página de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="aed9e-161">![Página de suscripción de usuario](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Página de suscripción de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="aed9e-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="aed9e-162">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="aed9e-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="aed9e-163">Controles</span><span class="sxs-lookup"><span data-stu-id="aed9e-163">Controls</span></span>  
 <span data-ttu-id="aed9e-164">Esta plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="aed9e-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="aed9e-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="aed9e-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="aed9e-166">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="aed9e-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="aed9e-167">Hola [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) plantillas compartan Hola mismos datos de modelo y reciban Hola datos de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="aed9e-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="aed9e-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="aed9e-168">Property</span></span>|<span data-ttu-id="aed9e-169">Escriba</span><span class="sxs-lookup"><span data-stu-id="aed9e-169">Type</span></span>|<span data-ttu-id="aed9e-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="aed9e-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="aed9e-171">firstName</span><span class="sxs-lookup"><span data-stu-id="aed9e-171">firstName</span></span>|<span data-ttu-id="aed9e-172">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-172">string</span></span>|<span data-ttu-id="aed9e-173">Nombre del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-174">lastName</span><span class="sxs-lookup"><span data-stu-id="aed9e-174">lastName</span></span>|<span data-ttu-id="aed9e-175">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-175">string</span></span>|<span data-ttu-id="aed9e-176">Apellido del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-177">companyName</span><span class="sxs-lookup"><span data-stu-id="aed9e-177">companyName</span></span>|<span data-ttu-id="aed9e-178">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-178">string</span></span>|<span data-ttu-id="aed9e-179">nombre de la compañía de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="aed9e-180">addresserEmail</span></span>|<span data-ttu-id="aed9e-181">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-181">string</span></span>|<span data-ttu-id="aed9e-182">Dirección de correo electrónico del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="aed9e-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="aed9e-184">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-184">string</span></span>|<span data-ttu-id="aed9e-185">Análisis de tooview dirección URL relativa para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="aed9e-186">subscriptions</span></span>|<span data-ttu-id="aed9e-187">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="aed9e-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="aed9e-188">suscripciones de Hello para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-189">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="aed9e-189">applications</span></span>|<span data-ttu-id="aed9e-190">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="aed9e-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="aed9e-191">aplicaciones de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-192">changePasswordUrl</span></span>|<span data-ttu-id="aed9e-193">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-193">string</span></span>|<span data-ttu-id="aed9e-194">Hola relativa URL toochange Hola contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="aed9e-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="aed9e-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="aed9e-196">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-196">string</span></span>|<span data-ttu-id="aed9e-197">Hola relativa toochange Hola nombre y la URL correo electrónico para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="aed9e-198">canChangePassword</span></span>|<span data-ttu-id="aed9e-199">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-199">boolean</span></span>|<span data-ttu-id="aed9e-200">Si el usuario actual de hello puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="aed9e-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="aed9e-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="aed9e-201">isSystemUser</span></span>|<span data-ttu-id="aed9e-202">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-202">boolean</span></span>|<span data-ttu-id="aed9e-203">Si el usuario actual de hello es miembro de uno de hello integrados [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="aed9e-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="aed9e-204">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="aed9e-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="aed9e-205"><a name="Applications"></a> Aplicaciones</span><span class="sxs-lookup"><span data-stu-id="aed9e-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="aed9e-206">Hola **aplicaciones** plantilla permite sección de suscripciones de hello toocustomize de página de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="aed9e-207">![Página de aplicaciones de cuenta de usuario](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Página de aplicaciones de cuenta de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="aed9e-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="aed9e-208">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="aed9e-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="aed9e-209">Controles</span><span class="sxs-lookup"><span data-stu-id="aed9e-209">Controls</span></span>  
 <span data-ttu-id="aed9e-210">Esta plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="aed9e-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="aed9e-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="aed9e-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="aed9e-212">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="aed9e-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="aed9e-213">Hola [perfil](#Profile), [aplicaciones](#Applications), y [suscripciones](#Subscriptions) plantillas compartan Hola mismos datos de modelo y reciban Hola datos de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="aed9e-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="aed9e-214">Propiedad</span><span class="sxs-lookup"><span data-stu-id="aed9e-214">Property</span></span>|<span data-ttu-id="aed9e-215">Escriba</span><span class="sxs-lookup"><span data-stu-id="aed9e-215">Type</span></span>|<span data-ttu-id="aed9e-216">Descripción</span><span class="sxs-lookup"><span data-stu-id="aed9e-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="aed9e-217">firstName</span><span class="sxs-lookup"><span data-stu-id="aed9e-217">firstName</span></span>|<span data-ttu-id="aed9e-218">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-218">string</span></span>|<span data-ttu-id="aed9e-219">Nombre del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-220">lastName</span><span class="sxs-lookup"><span data-stu-id="aed9e-220">lastName</span></span>|<span data-ttu-id="aed9e-221">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-221">string</span></span>|<span data-ttu-id="aed9e-222">Apellido del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-223">companyName</span><span class="sxs-lookup"><span data-stu-id="aed9e-223">companyName</span></span>|<span data-ttu-id="aed9e-224">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-224">string</span></span>|<span data-ttu-id="aed9e-225">nombre de la compañía de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="aed9e-226">addresserEmail</span></span>|<span data-ttu-id="aed9e-227">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-227">string</span></span>|<span data-ttu-id="aed9e-228">Dirección de correo electrónico del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="aed9e-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="aed9e-230">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-230">string</span></span>|<span data-ttu-id="aed9e-231">Análisis de tooview dirección URL relativa para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="aed9e-232">subscriptions</span></span>|<span data-ttu-id="aed9e-233">Colección de entidades de [suscripción](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="aed9e-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="aed9e-234">suscripciones de Hello para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-235">aplicaciones de escala de web</span><span class="sxs-lookup"><span data-stu-id="aed9e-235">applications</span></span>|<span data-ttu-id="aed9e-236">Colección de entidades de [aplicación](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="aed9e-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="aed9e-237">aplicaciones de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="aed9e-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-238">changePasswordUrl</span></span>|<span data-ttu-id="aed9e-239">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-239">string</span></span>|<span data-ttu-id="aed9e-240">Hola relativa URL toochange Hola contraseña del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="aed9e-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="aed9e-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="aed9e-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="aed9e-242">cadena</span><span class="sxs-lookup"><span data-stu-id="aed9e-242">string</span></span>|<span data-ttu-id="aed9e-243">Hola relativa toochange Hola nombre y la URL correo electrónico para el usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="aed9e-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="aed9e-244">canChangePassword</span></span>|<span data-ttu-id="aed9e-245">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-245">boolean</span></span>|<span data-ttu-id="aed9e-246">Si el usuario actual de hello puede cambiar su contraseña.</span><span class="sxs-lookup"><span data-stu-id="aed9e-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="aed9e-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="aed9e-247">isSystemUser</span></span>|<span data-ttu-id="aed9e-248">boolean</span><span class="sxs-lookup"><span data-stu-id="aed9e-248">boolean</span></span>|<span data-ttu-id="aed9e-249">Si el usuario actual de hello es miembro de uno de hello integrados [grupos](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="aed9e-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="aed9e-250">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="aed9e-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="aed9e-251"><a name="UpdateAccountInfo"></a> Update account info</span><span class="sxs-lookup"><span data-stu-id="aed9e-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="aed9e-252">Hola **información de la cuenta de Uodate** plantilla permite hello toocustomize **actualizar información de cuenta** página de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="aed9e-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="aed9e-253">![Plantillas del portal para desarrolladores de la página de información de cuenta de usuario](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Plantillas del portal para desarrolladores de la página de información de cuenta de usuario de APIM")</span><span class="sxs-lookup"><span data-stu-id="aed9e-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="aed9e-254">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="aed9e-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="aed9e-255">Controles</span><span class="sxs-lookup"><span data-stu-id="aed9e-255">Controls</span></span>  
 <span data-ttu-id="aed9e-256">Esta plantilla no puede utilizar los [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="aed9e-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="aed9e-257">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="aed9e-257">Data model</span></span>  
 <span data-ttu-id="aed9e-258">Entidad [Información de cuenta de usuario](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="aed9e-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="aed9e-259">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="aed9e-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="aed9e-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aed9e-260">Next steps</span></span>
<span data-ttu-id="aed9e-261">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aed9e-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
