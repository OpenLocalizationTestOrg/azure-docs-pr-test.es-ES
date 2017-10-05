---
title: "Problemas de inicio de sesión en una aplicación desarrollada personalizada | Microsoft Docs"
description: "Errores comunes que pueden causar la imposibilidad de iniciar sesión en una aplicación desarrollada con Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="241f1-103">Problemas de inicio de sesión en una aplicación desarrollada personalizada</span><span class="sxs-lookup"><span data-stu-id="241f1-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="241f1-104">Hay varios errores que pueden provocar que no pueda iniciar sesión en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="241f1-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="241f1-105">El principal motivo por el que los usuarios encuentran este problema son las aplicaciones mal configuradas.</span><span class="sxs-lookup"><span data-stu-id="241f1-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="241f1-106">Errores relacionados con aplicaciones mal configuradas</span><span class="sxs-lookup"><span data-stu-id="241f1-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="241f1-107">Compruebe que las configuraciones en el portal coinciden con lo que tiene en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="241f1-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="241f1-108">En concreto, compare el identificador del cliente o aplicación, las direcciones URL de respuesta, las claves y secretos de cliente, y el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="241f1-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="241f1-109">Compare el recurso del que está solicitando acceso mediante código con los permisos configurados en la pestaña **Recursos necesarios** para asegurarse de que solo se solicitan los recursos que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="241f1-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="241f1-110">Busque en [Azure AD en StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) errores o problemas similares.</span><span class="sxs-lookup"><span data-stu-id="241f1-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="241f1-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="241f1-111">Next steps</span></span>

[<span data-ttu-id="241f1-112">Guía del desarrollador de Azure AD</span><span class="sxs-lookup"><span data-stu-id="241f1-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="241f1-113">Consentimiento e integración de aplicaciones en Azure AD</span><span class="sxs-lookup"><span data-stu-id="241f1-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="241f1-114">Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD</span><span class="sxs-lookup"><span data-stu-id="241f1-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="241f1-115">Azure AD en StackOverflow</span><span class="sxs-lookup"><span data-stu-id="241f1-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
