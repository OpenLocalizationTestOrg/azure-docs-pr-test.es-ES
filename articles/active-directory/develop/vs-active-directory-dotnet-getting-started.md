---
title: aaaGet iniciado con Azure AD en los proyectos de MVC de Visual Studio | Documentos de Microsoft
description: "Cómo tooget iniciado con Azure Active Directory en los proyectos MVC después de conectarse tooor creación de un anuncio de Azure con Visual Studio servicios conectados"
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
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Introducción a Azure Active Directory y servicios conectados de Visual Studio (proyectos de MVC)
> [!div class="op_single_selector"]
> * [Introducción](vs-active-directory-dotnet-getting-started.md)
> * [¿Qué ha ocurrido?](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Controladores de tooaccess de autenticación necesaria
Todos los controladores en el proyecto se complementadas con hello **Authorize** atributo. Este atributo requiere hello toobe de usuario autenticado antes de acceder a estos controladores. tooallow Hola controlador toobe acceso anónimo, a quitar este atributo de controlador de Hola. Si desea tooset Hola permisos en un nivel más granular, aplicar el método de tooeach de atributo de Hola que requiera una autorización en lugar de aplicar la clase de controlador de toohello.

## <a name="adding-signin--signout-controls"></a>Incorporación de controles SignIn / SignOut
Hola tooadd SignIn/SignOut controla tooyour vista, puede usar hello **_LoginPartial.cshtml** tooone de funcionalidad de vista parcial tooadd Hola de sus vistas. Este es un ejemplo de Hola funcionalidad agregada toohello estándar **_Layout.cshtml** vista. (Tenga en cuenta Hola último elemento div Hola con clase barra de navegación y contracción):

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

## <a name="next-steps"></a>Pasos siguientes
- [Más información acerca de Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 

