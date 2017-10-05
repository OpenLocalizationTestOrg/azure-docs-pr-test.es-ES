---
title: "Incorporación de una nueva cuenta de inquilino de Azure Stack en Azure Active Directory | Microsoft Docs"
description: "Después de implementar Microsoft Azure Stack Development Kit, tendrá que crear una cuenta de usuario de al menos un inquilino para poder explorar el portal del inquilino."
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
ms.openlocfilehash: 4401de010dec808f080f5460298bb738ddd39312
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="87042-103">Adición de una nueva cuenta de inquilino de Azure Stack en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87042-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="87042-104">Después de [implementar Azure Stack Development Kit](azure-stack-run-powershell-script.md), necesitará una cuenta de usuario inquilino para explorar el portal del inquilino y probar las ofertas y los planes.</span><span class="sxs-lookup"><span data-stu-id="87042-104">After [deploying the Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore the tenant portal and test your offers and plans.</span></span> <span data-ttu-id="87042-105">Puede crear una cuenta de inquilino con [Azure Portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) o con [PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="87042-105">You can create a tenant account by [using the Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-the-azure-portal"></a><span data-ttu-id="87042-106">Creación de una cuenta de inquilino de Azure Stack con el Portal de Azure+</span><span class="sxs-lookup"><span data-stu-id="87042-106">Create an Azure Stack tenant account using the Azure portal</span></span>
<span data-ttu-id="87042-107">Debe tener una suscripción de Azure para usar el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="87042-107">You must have an Azure subscription to use the Azure portal.</span></span>

1. <span data-ttu-id="87042-108">Inicie sesión en [Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="87042-108">Log in to [Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="87042-109">En la barra de navegación izquierda de Microsoft Azure, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87042-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="87042-110">En la lista de directorios, haga clic en el directorio que desea usar para Azure Stack o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="87042-110">In the directory list, click the directory that you want to use for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="87042-111">En este directorio, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="87042-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="87042-112">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="87042-112">Click **Add user**.</span></span>
6. <span data-ttu-id="87042-113">En el **Asistente para agregar usuario**, en la lista **Tipo de usuario**, elija **nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="87042-113">In the **Add user** wizard, in the **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="87042-114">En el cuadro **Nombre de usuario** escriba un nombre para el usuario.</span><span class="sxs-lookup"><span data-stu-id="87042-114">In the **User name** box, type a name for the user.</span></span>
8. <span data-ttu-id="87042-115">En el asistente **@** , seleccione la entrada apropiada.</span><span class="sxs-lookup"><span data-stu-id="87042-115">In the **@** box, choose the appropriate entry.</span></span>
9. <span data-ttu-id="87042-116">Haga clic en la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="87042-116">Click the next arrow.</span></span>
10. <span data-ttu-id="87042-117">En la página **Perfil de usuario** del asistente, escriba un **Nombre**, **Apellidos** y **Nombre para mostrar**.</span><span class="sxs-lookup"><span data-stu-id="87042-117">In the **User profile** page of the wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="87042-118">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="87042-118">In the **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="87042-119">Haga clic en la flecha siguiente.</span><span class="sxs-lookup"><span data-stu-id="87042-119">Click the next arrow.</span></span>
13. <span data-ttu-id="87042-120">En la página **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="87042-120">On the **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="87042-121">Copie la **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="87042-121">Copy the **New password**.</span></span>
15. <span data-ttu-id="87042-122">Inicie sesión en Microsoft Azure con la nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="87042-122">Log in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="87042-123">Cambie la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="87042-123">Change the password when prompted.</span></span>
16. <span data-ttu-id="87042-124">Inicie sesión en `https://portal.local.azurestack.external` con la nueva cuenta para ver el portal del inquilino.</span><span class="sxs-lookup"><span data-stu-id="87042-124">Log in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="87042-125">Creación de una cuenta de inquilino de Azure Stack con PowerShell</span><span class="sxs-lookup"><span data-stu-id="87042-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="87042-126">Si no tiene una suscripción de Azure, no puede usar Azure Portal para agregar una cuenta de usuario de inquilino.</span><span class="sxs-lookup"><span data-stu-id="87042-126">If you don't have an Azure subscription, you can't use the Azure portal to add a tenant user account.</span></span> <span data-ttu-id="87042-127">En este caso, puede usar el módulo Azure Active Directory para Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87042-127">In this case, you can use the Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="87042-128">Si usa una cuenta Microsoft (Live ID) para implementar Azure Stack Development Kit, no se puede usar PowerShell de AAD para crear la cuenta de inquilino.</span><span class="sxs-lookup"><span data-stu-id="87042-128">If you are using Microsoft Account (Live ID) to deploy Azure Stack Development Kit, you can't use AAD PowerShell to create tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="87042-129">Instale el [Ayudante para el inicio de sesión de Microsoft Online Services para profesionales de TI (RTW)](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="87042-129">Install the [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="87042-130">Instale el [módulo de Azure Active Directory para Windows PowerShell (versión de 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) y ábralo.</span><span class="sxs-lookup"><span data-stu-id="87042-130">Install the [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="87042-131">Ejecute los siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="87042-131">Run the following cmdlets:</span></span>

    ```powershell
    # Provide the AAD credential you use to deploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with the initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="87042-132">Inicie sesión en Microsoft Azure con la nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="87042-132">Sign in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="87042-133">Cambie la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="87042-133">Change the password when prompted.</span></span>
2. <span data-ttu-id="87042-134">Inicie sesión en `https://portal.local.azurestack.external` con la nueva cuenta para ver el portal del inquilino.</span><span class="sxs-lookup"><span data-stu-id="87042-134">Sign in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

