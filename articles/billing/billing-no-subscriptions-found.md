---
title: las suscripciones de aaaNo error encontraron cuando intente toosign en tooAzure portal o el centro de la cuenta de Azure | Documentos de Microsoft
description: "Proporciona soluciones de Hola para un problema en el que las suscripciones No encontraron el error se produce cuando inicien sesión en el portal de tooAzure o el centro de la cuenta de Azure."
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
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="9cb13-103">Error No se encontraron suscripciones en Azure Portal o en el Centro de cuentas de Azure</span><span class="sxs-lookup"><span data-stu-id="9cb13-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="9cb13-104">Puede recibir un mensaje de error "No se han encontrado suscripciones" cuando intente toosign en toohello [portal de Azure](https://portal.azure.com/) o hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="9cb13-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="9cb13-105">En este artículo se brinda una solución para este problema.</span><span class="sxs-lookup"><span data-stu-id="9cb13-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="9cb13-106">Síntoma</span><span class="sxs-lookup"><span data-stu-id="9cb13-106">Symptom</span></span>

<span data-ttu-id="9cb13-107">Cuando intente toosign en toohello [portal de Azure](https://portal.azure.com/) o hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions), recibirá Hola siguiente mensaje de error: "No se han encontrado suscripciones".</span><span class="sxs-lookup"><span data-stu-id="9cb13-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="9cb13-108">Causa</span><span class="sxs-lookup"><span data-stu-id="9cb13-108">Cause</span></span>

<span data-ttu-id="9cb13-109">Este problema se produce si la cuenta no tiene permisos suficientes.</span><span class="sxs-lookup"><span data-stu-id="9cb13-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="9cb13-110">Solución</span><span class="sxs-lookup"><span data-stu-id="9cb13-110">Solution</span></span>

<span data-ttu-id="9cb13-111">Asegúrese de que inicie sesión como administrador correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb13-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="9cb13-112">Administrador de la cuenta puede tener acceso a solo el centro de cuentas Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb13-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="9cb13-113">Los administradores de servicios (SA) y los coadministradores (CA) tienen acceso permiso solo toohello portal de Azure u Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="9cb13-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="9cb13-114">Escenario 1: Mensaje de Error se recibe en hello [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="9cb13-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="9cb13-115">toofix este problema:</span><span class="sxs-lookup"><span data-stu-id="9cb13-115">toofix this issue:</span></span>

* <span data-ttu-id="9cb13-116">Asegúrese de que ese Hola correcto de directorio de Azure está seleccionada, haga clic en su cuenta en la parte superior de hello derecha.</span><span class="sxs-lookup"><span data-stu-id="9cb13-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Directorio de SELECT hello en hello esquina superior derecha del programa Hola a portal de Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="9cb13-118">Si hay hello directory derecha Azure seleccionada pero sigue recibiendo un mensaje de error hello [tenga la cuenta que se agrega como un propietario](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="9cb13-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="9cb13-119">Escenario 2: Mensaje de Error se recibe en hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="9cb13-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="9cb13-120">Compruebe si cuenta de hello que usó es Hola Administrador de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="9cb13-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="9cb13-121">es tooverify que Hola Administrador de la cuenta, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9cb13-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="9cb13-122">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cb13-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cb13-123">En el menú del concentrador hello, seleccione **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="9cb13-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="9cb13-124">Seleccione la suscripción de Hola que desee toocheck y, a continuación, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="9cb13-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="9cb13-125">Seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="9cb13-125">Select **Properties**.</span></span> <span data-ttu-id="9cb13-126">Administrador de la cuenta de suscripción de Hola Hola se muestra en hello **Administrador de la cuenta** cuadro.</span><span class="sxs-lookup"><span data-stu-id="9cb13-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="9cb13-127">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="9cb13-127">Need help?</span></span> <span data-ttu-id="9cb13-128">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="9cb13-128">Contact support.</span></span>
<span data-ttu-id="9cb13-129">Si aún necesita ayuda, [póngase en contacto con soporte técnico](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="9cb13-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
