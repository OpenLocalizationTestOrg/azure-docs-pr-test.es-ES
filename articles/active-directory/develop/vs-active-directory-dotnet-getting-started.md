---
title: "Introducción a Azure AD en proyectos de MVC de Visual Studio | Microsoft Docs"
description: "Cómo empezar a usar Azure Active Directory en los proyectos de MVC después de crear un Azure AD usando los servicios conectados de Visual Studio o de conectarse a él"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: c4d49cfc9887e422b3eaed2b96348c99eca48881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="345d2-103">Introducción a Azure Active Directory y servicios conectados de Visual Studio (proyectos de MVC)</span><span class="sxs-lookup"><span data-stu-id="345d2-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="345d2-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="345d2-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="345d2-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="345d2-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="345d2-106">Requerimiento de autenticación para obtener acceso a los controladores</span><span class="sxs-lookup"><span data-stu-id="345d2-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="345d2-107">Todos los controladores de su proyecto cuentan ahora con el atributo **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="345d2-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="345d2-108">Este atributo requerirá que el usuario se autentique antes de tener acceso a estos controladores.</span><span class="sxs-lookup"><span data-stu-id="345d2-108">This attribute requires the user to be authenticated before accessing these controllers.</span></span> <span data-ttu-id="345d2-109">Para permitir el acceso anónimo al controlador, quite este atributo del controlador.</span><span class="sxs-lookup"><span data-stu-id="345d2-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="345d2-110">Si desea establecer los permisos a un nivel más detallado, aplique el atributo a cada método que requiere autorización en vez de aplicarlo a la clase del controlador.</span><span class="sxs-lookup"><span data-stu-id="345d2-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="345d2-111">Incorporación de controles SignIn / SignOut</span><span class="sxs-lookup"><span data-stu-id="345d2-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="345d2-112">Para agregar controles SignIn/SignOut a su vista, puede usar la vista parcial **_LoginPartial.cshtml** para agregar esta función a alguna de sus vistas.</span><span class="sxs-lookup"><span data-stu-id="345d2-112">To add the SignIn/SignOut controls to your view, you can use the **_LoginPartial.cshtml** partial view to add the functionality to one of your views.</span></span> <span data-ttu-id="345d2-113">Aquí se presenta un ejemplo de la función agregada a la vista estándar **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="345d2-113">Here is an example of the functionality added to the standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="345d2-114">Observe el último elemento de la sección div con la clase navbar-collapse:</span><span class="sxs-lookup"><span data-stu-id="345d2-114">(Note the last element in the div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="345d2-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="345d2-115">Next steps</span></span>
- [<span data-ttu-id="345d2-116">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="345d2-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

