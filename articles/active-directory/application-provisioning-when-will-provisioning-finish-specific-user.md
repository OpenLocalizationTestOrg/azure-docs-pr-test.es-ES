---
title: "Averiguar cuándo un usuario específico podrá acceder a una aplicación | Microsoft Docs"
description: "Cómo averiguar cuándo un usuario sumamente importante puede acceder a una aplicación que se ha configurado para el aprovisionamiento de usuarios con Azure AD"
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="4aa3c-103">Averiguar cuándo un usuario específico podrá acceder a una aplicación</span><span class="sxs-lookup"><span data-stu-id="4aa3c-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="4aa3c-104">Cuando se utiliza el aprovisionamiento automático de usuarios con una aplicación, Azure AD aprovisiona y actualiza automáticamente las cuentas de usuario en una aplicación en función de aspectos tales como la [asignación de usuario y grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) con un intervalo programado periódicamente, normalmente cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="4aa3c-105">¿Cuánto tiempo tarda?</span><span class="sxs-lookup"><span data-stu-id="4aa3c-105">How long does it take?</span></span>

<span data-ttu-id="4aa3c-106">El tiempo necesario para aprovisionar un usuario determinado depende principalmente de si ya se ha producido una sincronización inicial "completa" o no.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="4aa3c-107">La sincronización inicial entre Azure AD y una aplicación puede tardar desde 20 minutos hasta varias horas, según el tamaño del directorio de Azure AD y el número de usuarios en el ámbito de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="4aa3c-108">Las sincronizaciones posteriores a la inicial serán más rápidas (por ejemplo, unos 10 minutos), ya que el servicio de aprovisionamiento almacena marcas de agua que representan el estado de ambos sistemas tras la sincronización inicial, lo cual mejora el rendimiento de las posteriores.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="4aa3c-109">Comprobación del estado de un usuario</span><span class="sxs-lookup"><span data-stu-id="4aa3c-109">How to check the status of a user</span></span>

<span data-ttu-id="4aa3c-110">Para ver el estado de aprovisionamiento de un usuario seleccionado, consulte los registros de auditoría de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="4aa3c-111">Puede acceder a los registros de auditoría de aprovisionamiento en Azure Portal, en la pestaña **Azure Active Directory &gt; Aplicaciones empresariales &gt; \[Nombre de la aplicación\] &gt; Registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="4aa3c-112">Filtre los registros en la categoría **Aprovisionamiento de cuentas** para ver solo los eventos de aprovisionamiento para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="4aa3c-113">Puede buscar usuarios por el "identificador de coincidencia" que se configuró para ellos en las asignaciones de atributos.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="4aa3c-114">Por ejemplo, si configuró el "nombre principal de usuario" o la "dirección de correo electrónico" como atributo de coincidencia en el lado de Azure AD y el usuario que no se aprovisiona tiene el valor "audrey@contoso.com", busque "audrey@contoso.com" en los registros de auditoría y revise las entradas devueltas.</span><span class="sxs-lookup"><span data-stu-id="4aa3c-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="4aa3c-115">Los registros de auditoría de aprovisionamiento registran todas las operaciones realizadas por el servicio de aprovisionamiento, lo que incluye:</span><span class="sxs-lookup"><span data-stu-id="4aa3c-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="4aa3c-116">Consultar en Azure AD los usuarios asignados que están en el ámbito de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="4aa3c-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="4aa3c-117">Consultar en la aplicación de destino la existencia de esos usuarios</span><span class="sxs-lookup"><span data-stu-id="4aa3c-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="4aa3c-118">Comparar los objetos de usuario entre el sistema</span><span class="sxs-lookup"><span data-stu-id="4aa3c-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="4aa3c-119">Agregar, actualizar o deshabilitar la cuenta de usuario en el sistema de destino en función de la comparación</span><span class="sxs-lookup"><span data-stu-id="4aa3c-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aa3c-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4aa3c-120">Next steps</span></span>
<span data-ttu-id="4aa3c-121">[Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)</span><span class="sxs-lookup"><span data-stu-id="4aa3c-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
