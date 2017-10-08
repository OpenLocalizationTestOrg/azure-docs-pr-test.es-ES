---
title: "aaaTroubleshooting pertenencia dinámica para grupos | Documentos de Microsoft"
description: "Solución de problemas para la pertenencia dinámica para grupos en Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="b12d6-103">Solución de problemas relacionados con las pertenencias dinámicas para grupos</span><span class="sxs-lookup"><span data-stu-id="b12d6-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="b12d6-104">**He configurado una regla en un grupo pero ningún pertenencias a grupos se actualizan en el grupo de Hola**</span><span class="sxs-lookup"><span data-stu-id="b12d6-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="b12d6-105">Compruebe que hello **Habilitar administración de grupos delegados** opción se establece demasiado**Sí** en hello **configurar** ficha. Verá esta opción únicamente si ha iniciado sesión ya está asignado a un toowhom de usuario una licencia de Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="b12d6-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="b12d6-106">Comprobar los valores de hello para los atributos de usuario en la regla de hello: ¿hay usuarios que cumplen la regla de hello?</span><span class="sxs-lookup"><span data-stu-id="b12d6-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="b12d6-107">**He configurado una regla, pero ahora se quitan los miembros existentes de Hola de regla de Hola**</span><span class="sxs-lookup"><span data-stu-id="b12d6-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="b12d6-108">Este es el comportamiento esperado.</span><span class="sxs-lookup"><span data-stu-id="b12d6-108">This is expected behavior.</span></span> <span data-ttu-id="b12d6-109">Los miembros existentes del grupo de Hola se quitan cuando se habilita o modifica una regla.</span><span class="sxs-lookup"><span data-stu-id="b12d6-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="b12d6-110">los usuarios de Hello procedentes de la evaluación de regla de Hola se agregan como toohello grupo de miembros.</span><span class="sxs-lookup"><span data-stu-id="b12d6-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="b12d6-111">**No veo los cambios en la pertenencia al instante cuando agrego o cambio una regla, ¿por qué pasa esto?**</span><span class="sxs-lookup"><span data-stu-id="b12d6-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="b12d6-112">La evaluación de pertenencia dedicada se realiza periódicamente en un proceso asincrónico en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b12d6-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="b12d6-113">¿Durante cuánto tiempo Hola proceso toma viene determinado por número de Hola de los usuarios de su tamaño hello y directorio de los grupos de hello creado como resultado de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b12d6-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="b12d6-114">Por lo general, directorios con un número pequeño de usuarios verán los cambios de pertenencia de grupo de hello en unos pocos minutos.</span><span class="sxs-lookup"><span data-stu-id="b12d6-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="b12d6-115">Directorios con un gran número de usuarios pueden tardar 30 minutos o más toopopulate.</span><span class="sxs-lookup"><span data-stu-id="b12d6-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="b12d6-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b12d6-116">Next steps</span></span>
<span data-ttu-id="b12d6-117">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b12d6-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="b12d6-118">Administrar acceso tooresources con grupos de Active Directory de Azure</span><span class="sxs-lookup"><span data-stu-id="b12d6-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="b12d6-119">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b12d6-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b12d6-120">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b12d6-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="b12d6-121">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b12d6-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
