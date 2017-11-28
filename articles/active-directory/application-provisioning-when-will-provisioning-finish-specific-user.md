---
title: "aaaFind espera cuando un usuario específico será capaz de tooaccess una aplicación | Documentos de Microsoft"
description: "Cómo toofind cuando un usuario sumamente importante ser capaz de tooaccess una aplicación se haya configurado para el aprovisionamiento de usuarios con Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="0a119-103">Determinar cuándo un usuario específico será capaz de tooaccess una aplicación</span><span class="sxs-lookup"><span data-stu-id="0a119-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="0a119-104">Cuando se utiliza el aprovisionamiento automático de usuarios con una aplicación, Azure AD aprovisiona y actualiza automáticamente las cuentas de usuario en una aplicación en función de aspectos tales como la [asignación de usuario y grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) con un intervalo programado periódicamente, normalmente cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="0a119-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="0a119-105">¿Cuánto tiempo tarda?</span><span class="sxs-lookup"><span data-stu-id="0a119-105">How long does it take?</span></span>

<span data-ttu-id="0a119-106">Hola que tarda un toobe determinado usuario aprovisionado depende principalmente de si ya se ha producido una sincronización inicial "completa".</span><span class="sxs-lookup"><span data-stu-id="0a119-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="0a119-107">Hola primera sincronización entre Azure AD y una aplicación puede tardar en cualquier parte de horas de tooseveral de 20 minutos, según el tamaño de hello del directorio de hello Azure AD y número de Hola de usuarios en el ámbito de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0a119-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="0a119-108">Las sincronizaciones posteriores después de la sincronización inicial de hello ser más rápidas (por ejemplo, dentro de 10 minutos), como almacenes de aprovisionamiento del servicio de hello las marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial hello, mejorar el rendimiento de las sincronizaciones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0a119-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="0a119-109">¿Cómo toocheck Hola estado de un usuario</span><span class="sxs-lookup"><span data-stu-id="0a119-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="0a119-110">estado de aprovisionamiento de hello toosee para un usuario seleccionado, consulte los registros de auditoría de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a119-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="0a119-111">puede tener acceso a Hola aprovisionamiento de los registros de auditoría en el portal de Azure, en Hola Hola **Azure Active Directory &gt; aplicaciones empresariales &gt; \[nombre de la aplicación\] &gt; registros de auditoría**ficha. Hola de filtro inicie sesión en hello **el aprovisionamiento de cuentas** categoría tooonly vea Hola aprovisionamiento eventos para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a119-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="0a119-112">Puede buscar usuarios en función de Hola "identificador coincidente" que se configuró para ellos en asignaciones de atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a119-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="0a119-113">Por ejemplo, si configuró Hola "nombre principal de usuario" o "dirección de correo electrónico" como Hola coincidencia de atributo en el lado de hello Azure AD y no se aprovisionamiento de usuarios de hello tiene un valor de "audrey@contoso.com", a continuación, los registros de auditoría de Hola de búsqueda para"audrey@contoso.com" y, a continuación, revisar se devuelven las entradas.</span><span class="sxs-lookup"><span data-stu-id="0a119-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="0a119-114">Hola aprovisionamiento auditoría registra registro todos hello las operaciones realizadas por hello aprovisionamiento del servicio, incluyendo:</span><span class="sxs-lookup"><span data-stu-id="0a119-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="0a119-115">Consultar en Azure AD los usuarios asignados que están en el ámbito de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="0a119-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="0a119-116">Consultar la aplicación de destino de hello existencia Hola de esos usuarios</span><span class="sxs-lookup"><span data-stu-id="0a119-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="0a119-117">Comparar objetos de usuario de hello entre sistema Hola</span><span class="sxs-lookup"><span data-stu-id="0a119-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="0a119-118">Agregar, actualizar o deshabilitar la cuenta de usuario de Hola Hola del sistema de destino en función de comparación de Hola</span><span class="sxs-lookup"><span data-stu-id="0a119-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a119-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a119-119">Next steps</span></span>
<span data-ttu-id="0a119-120">[Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''.</span><span class="sxs-lookup"><span data-stu-id="0a119-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
