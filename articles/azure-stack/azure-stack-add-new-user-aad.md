---
title: aaaAdd una nueva cuenta de inquilino de pila de Azure en Azure Active Directory | Documentos de Microsoft
description: "Después de implementar el Kit de desarrollo de pila de Microsoft Azure, necesitará toocreate al menos una cuenta de usuario de inquilinos para que puedan explorar el portal del inquilino de Hola."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="a8b81-103">Adición de una nueva cuenta de inquilino de Azure Stack en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8b81-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="a8b81-104">Después de [implementar Hola Kit de desarrollo de Azure pila](azure-stack-run-powershell-script.md), necesitará una cuenta de usuario inquilino para que pueda explorar el portal del inquilino de Hola y sus ofertas y planes de pruebas.</span><span class="sxs-lookup"><span data-stu-id="a8b81-104">After [deploying hello Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore hello tenant portal and test your offers and plans.</span></span> <span data-ttu-id="a8b81-105">Puede crear una cuenta de inquilino por [utilizando Hola portal de Azure](#create-an-azure-stack-tenant-account-using-the-azure-portal) o [con PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="a8b81-105">You can create a tenant account by [using hello Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a><span data-ttu-id="a8b81-106">Crear una cuenta de inquilino de Azure pila utilizando Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a8b81-106">Create an Azure Stack tenant account using hello Azure portal</span></span>
<span data-ttu-id="a8b81-107">Debe tener un hello toouse de suscripción de Azure portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8b81-107">You must have an Azure subscription toouse hello Azure portal.</span></span>

1. <span data-ttu-id="a8b81-108">Inicie sesión demasiado[Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a8b81-108">Log in too[Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a8b81-109">En la barra de navegación izquierda de Microsoft Azure, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="a8b81-110">En la lista de directorios de hello, haga clic en directorio de Hola que desee toouse para la pila de Azure, o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="a8b81-110">In hello directory list, click hello directory that you want toouse for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="a8b81-111">En este directorio, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="a8b81-112">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-112">Click **Add user**.</span></span>
6. <span data-ttu-id="a8b81-113">Hola **para agregar un usuario** asistente, hello **tipo de usuario** elija **nuevo usuario de su organización**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-113">In hello **Add user** wizard, in hello **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="a8b81-114">Hola **nombre de usuario** , escriba un nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8b81-114">In hello **User name** box, type a name for hello user.</span></span>
8. <span data-ttu-id="a8b81-115">Hola  **@**  cuadro, seleccione la entrada adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8b81-115">In hello **@** box, choose hello appropriate entry.</span></span>
9. <span data-ttu-id="a8b81-116">Haga clic en la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a8b81-116">Click hello next arrow.</span></span>
10. <span data-ttu-id="a8b81-117">Hola **perfil de usuario** página del Asistente de hello, escriba un **nombre**, **apellidos**, y **nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-117">In hello **User profile** page of hello wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="a8b81-118">Hola **rol** elija **usuario**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-118">In hello **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="a8b81-119">Haga clic en la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="a8b81-119">Click hello next arrow.</span></span>
13. <span data-ttu-id="a8b81-120">En hello **obtener contraseña temporal** página, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-120">On hello **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="a8b81-121">Hola copia **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a8b81-121">Copy hello **New password**.</span></span>
15. <span data-ttu-id="a8b81-122">Inicie sesión en tooMicrosoft Azure con la nueva cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="a8b81-122">Log in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="a8b81-123">Cambiar la contraseña de hello cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="a8b81-123">Change hello password when prompted.</span></span>
16. <span data-ttu-id="a8b81-124">Inicie sesión demasiado`https://portal.local.azurestack.external` con hello nueva toosee Hola inquilino portal de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a8b81-124">Log in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="a8b81-125">Creación de una cuenta de inquilino de Azure Stack con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8b81-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="a8b81-126">Si no tiene una suscripción de Azure, no se puede usar hello tooadd portal Azure una cuenta de usuario de inquilino.</span><span class="sxs-lookup"><span data-stu-id="a8b81-126">If you don't have an Azure subscription, you can't use hello Azure portal tooadd a tenant user account.</span></span> <span data-ttu-id="a8b81-127">En este caso, puede usar hello Azure módulo Active Directory para Windows PowerShell en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a8b81-127">In this case, you can use hello Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="a8b81-128">Si usas Microsoft Account (Live ID) toodeploy Kit de desarrollo de pila de Azure, no puede usar la cuenta de inquilino de AAD PowerShell toocreate.</span><span class="sxs-lookup"><span data-stu-id="a8b81-128">If you are using Microsoft Account (Live ID) toodeploy Azure Stack Development Kit, you can't use AAD PowerShell toocreate tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="a8b81-129">Instalar hello [Microsoft Online Services Sign-In Assistant para profesionales de TI RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="a8b81-129">Install hello [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="a8b81-130">Instalar hello [Azure módulo Active Directory para Windows PowerShell (versión de 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) y ábralo.</span><span class="sxs-lookup"><span data-stu-id="a8b81-130">Install hello [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="a8b81-131">Ejecute hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="a8b81-131">Run hello following cmdlets:</span></span>

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="a8b81-132">Inicie sesión en tooMicrosoft Azure con la nueva cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="a8b81-132">Sign in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="a8b81-133">Cambiar la contraseña de hello cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="a8b81-133">Change hello password when prompted.</span></span>
2. <span data-ttu-id="a8b81-134">Inicie sesión en demasiado`https://portal.local.azurestack.external` con hello nueva toosee Hola inquilino portal de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a8b81-134">Sign in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

