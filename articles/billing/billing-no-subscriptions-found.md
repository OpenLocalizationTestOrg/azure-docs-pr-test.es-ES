---
title: "Error No se encontraron suscripciones al intentar iniciar sesión en Azure Portal o en el Centro de cuentas de Azure | Microsoft Docs"
description: "Proporciona la solución para un problema en el que se produce un error del tipo No se encontraron suscripciones al iniciar sesión en Azure Portal o en el Centro de cuentas de Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="94b7f-103">Error No se encontraron suscripciones en Azure Portal o en el Centro de cuentas de Azure</span><span class="sxs-lookup"><span data-stu-id="94b7f-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="94b7f-104">Puede recibir un mensaje de error "No se encontraron suscripciones" cuando intente iniciar sesión en [Azure Portal](https://portal.azure.com/) o en el [Centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="94b7f-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="94b7f-105">En este artículo se brinda una solución para este problema.</span><span class="sxs-lookup"><span data-stu-id="94b7f-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="94b7f-106">Síntoma</span><span class="sxs-lookup"><span data-stu-id="94b7f-106">Symptom</span></span>

<span data-ttu-id="94b7f-107">Cuando intenta iniciar sesión en [Azure Portal](https://portal.azure.com/) o en el [Centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions), recibe el mensaje de error siguiente: "No se encontraron suscripciones".</span><span class="sxs-lookup"><span data-stu-id="94b7f-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="94b7f-108">Causa</span><span class="sxs-lookup"><span data-stu-id="94b7f-108">Cause</span></span>

<span data-ttu-id="94b7f-109">Este problema se produce si la cuenta no tiene permisos suficientes.</span><span class="sxs-lookup"><span data-stu-id="94b7f-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="94b7f-110">Solución</span><span class="sxs-lookup"><span data-stu-id="94b7f-110">Solution</span></span>

<span data-ttu-id="94b7f-111">Asegúrese de iniciar sesión como el administrador correcto.</span><span class="sxs-lookup"><span data-stu-id="94b7f-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="94b7f-112">Un administrador de cuenta solo puede acceder al Centro de cuentas.</span><span class="sxs-lookup"><span data-stu-id="94b7f-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="94b7f-113">Los administradores de servicios (SA) y los coadministradores (CA) solo tienen permiso de acceso a Azure Portal o al Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="94b7f-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="94b7f-114">Escenario 1: Se recibe el mensaje de error en [Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="94b7f-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="94b7f-115">Para corregir este problema:</span><span class="sxs-lookup"><span data-stu-id="94b7f-115">To fix this issue:</span></span>

* <span data-ttu-id="94b7f-116">Asegúrese de que se seleccionó el directorio correcto de Azure haciendo clic en la cuenta pertinente en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="94b7f-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Selección del directorio en la parte superior derecha de Azure Portal](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="94b7f-118">Si se seleccionó el directorio correcto de Azure pero sigue recibiendo el mensaje de error, [agregue la cuenta como propietario](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="94b7f-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="94b7f-119">Escenario 2: Se recibe el mensaje de error en el [Centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="94b7f-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="94b7f-120">Compruebe si la cuenta que ha usado es el administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="94b7f-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="94b7f-121">Para comprobar quién es el administrador de cuentas, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="94b7f-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="94b7f-122">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94b7f-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="94b7f-123">En el menú de concentrador, seleccione **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="94b7f-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="94b7f-124">Seleccione la suscripción que quiera comprobar y, a continuación, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="94b7f-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="94b7f-125">Seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="94b7f-125">Select **Properties**.</span></span> <span data-ttu-id="94b7f-126">El administrador de cuentas de la suscripción se muestra en el cuadro **Administrador de cuentas** .</span><span class="sxs-lookup"><span data-stu-id="94b7f-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="94b7f-127">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="94b7f-127">Need help?</span></span> <span data-ttu-id="94b7f-128">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="94b7f-128">Contact support.</span></span>
<span data-ttu-id="94b7f-129">Si sigue necesitando ayuda, [póngase en contacto con el servicio de soporte técnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="94b7f-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
