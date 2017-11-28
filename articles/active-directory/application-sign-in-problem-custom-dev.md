---
title: "aaaProblems iniciar sesión en aplicaciones personalizadas de tooan | Documentos de Microsoft"
description: "Errores comunes que pudieron estar causando toonot ser capaz de toosign en una aplicación que haya desarrollado con Azure AD"
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
ms.openlocfilehash: cc302e68ae6c129b74387c6fc5ba4fb45ccb8fb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-custom-developed-application"></a><span data-ttu-id="18ebf-103">Problemas para iniciar sesión en aplicaciones personalizadas de tooan</span><span class="sxs-lookup"><span data-stu-id="18ebf-103">Problems signing in tooan custom-developed application</span></span>

<span data-ttu-id="18ebf-104">Existen varios errores que podrían provocar toonot ser capaz de toosign en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ebf-104">There are several errors that could be causing you toonot be able toosign into an app.</span></span> <span data-ttu-id="18ebf-105">motivo mayor Hola personas produce este problema es mala configuración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="18ebf-105">hello biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-too-misconfigured-apps"></a><span data-ttu-id="18ebf-106">Errores relacionados con aplicaciones demasiado mal configuradas</span><span class="sxs-lookup"><span data-stu-id="18ebf-106">Errors related too misconfigured apps</span></span>

* <span data-ttu-id="18ebf-107">Compruebe las configuraciones de hello en el portal de hello coincide con lo que tiene en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ebf-107">Verify both hello configurations in hello portal match what you have in your app.</span></span> <span data-ttu-id="18ebf-108">En concreto, compare el identificador del cliente o aplicación, las direcciones URL de respuesta, las claves y secretos de cliente, y el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18ebf-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="18ebf-109">Comparar recursos Hola están solicitando acceso tooin código con permisos de hello configurado en hello **recursos necesarios** toomake ficha seguro solo solicitar recursos que haya configurado.</span><span class="sxs-lookup"><span data-stu-id="18ebf-109">Compare hello resource you’re requesting access tooin code with hello configured permissions in hello **Required Resources** tab toomake sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="18ebf-110">Busque en [Azure AD en StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) errores o problemas similares.</span><span class="sxs-lookup"><span data-stu-id="18ebf-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ebf-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18ebf-111">Next steps</span></span>

[<span data-ttu-id="18ebf-112">Guía del desarrollador de Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ebf-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="18ebf-113">Integración de aplicaciones y consentimiento tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="18ebf-113">Consent and Integrating Apps tooAzure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="18ebf-114">Consentimiento y permisos para las aplicaciones convergentes v2.0 de Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ebf-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="18ebf-115">Azure AD en StackOverflow</span><span class="sxs-lookup"><span data-stu-id="18ebf-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
