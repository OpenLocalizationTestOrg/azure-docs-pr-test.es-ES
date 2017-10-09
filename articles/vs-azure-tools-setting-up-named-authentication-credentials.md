---
title: "aaaSetting seguridad denominado las credenciales de autenticación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo el servicio de nube credenciales tootooprovide que Visual Studio pueda utilizar tooauthenticate solicitudes tooAzure toopublish una tooAzure de aplicación desde Visual Studio o toomonitor existente... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="a28c5-103">Configuración de credenciales de autenticación con nombre</span><span class="sxs-lookup"><span data-stu-id="a28c5-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="a28c5-104">toopublish una tooAzure de aplicación desde Visual Studio o toomonitor un servicio de nube existente, debe proporcionar las credenciales que Visual Studio pueda utilizar tooauthenticate solicita tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a28c5-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="a28c5-105">Hay varios lugares en Visual Studio donde puede iniciar sesión en tooprovide estas credenciales.</span><span class="sxs-lookup"><span data-stu-id="a28c5-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="a28c5-106">Por ejemplo, en Explorador de servidores de hello, puede abrir menú contextual Hola Hola **Azure** nodo y elija **conectar tooMicrosoft suscripción de Azure...** . Al iniciar sesión, información de suscripción de hello asociada con su cuenta de Azure está disponible en Visual Studio y no hay nada más que tiene toodo.</span><span class="sxs-lookup"><span data-stu-id="a28c5-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="a28c5-107">Herramientas de Azure también admite una forma más antigua de proporcionar credenciales, mediante el archivo de suscripción de hello (archivo .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="a28c5-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="a28c5-108">En este tema se describe este método, que todavía se admite en el SDK 2.2 de Azure.</span><span class="sxs-lookup"><span data-stu-id="a28c5-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="a28c5-109">Hola siguientes elementos es necesario para la autenticación tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a28c5-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="a28c5-110">Su Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="a28c5-110">Your subscription ID</span></span>
* <span data-ttu-id="a28c5-111">Un certificado X.509 v3 válido</span><span class="sxs-lookup"><span data-stu-id="a28c5-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="a28c5-112">longitud de Hola de clave del certificado X.509 v3 Hola debe ser al menos 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="a28c5-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="a28c5-113">Azure rechazará cualquier certificado que no cumpla este requisito o que no sea válido.</span><span class="sxs-lookup"><span data-stu-id="a28c5-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="a28c5-114">Visual Studio usa el identificador de suscripción junto con los datos del certificado hello como credenciales.</span><span class="sxs-lookup"><span data-stu-id="a28c5-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="a28c5-115">las credenciales adecuadas de Hola se hace referencia en hello suscripción (archivo .publishsettings), que contiene una clave pública para el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a28c5-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="a28c5-116">archivo de suscripción de Hello puede contener credenciales de más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="a28c5-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="a28c5-117">Puede editar información de suscripción de Hola de hello **nueva/Editar suscripción** cuadro de diálogo, como se explica más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="a28c5-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="a28c5-118">Si desea toocreate un certificado usted mismo, puede hacer referencia a instrucciones toohello [crear y cargar un certificado de administración para Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) y, a continuación, cargar manualmente Hola certificado toohello [portal de Azure clásico ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a28c5-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="a28c5-119">Estas credenciales que Visual Studio requiere toomanage que no son servicios en la nube Hola mismas credenciales que están tooauthenticate requiere una solicitud en servicios de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a28c5-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="a28c5-120">Importación, configuración o edición de las credenciales de autenticación en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a28c5-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="a28c5-121">Puede importar, configurar o modificar las credenciales de autenticación en hello **nueva suscripción** cuadro de diálogo que aparece si lleva a cabo Hola después de acción:</span><span class="sxs-lookup"><span data-stu-id="a28c5-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="a28c5-122">En **Explorador de servidores**, abra menú contextual Hola Hola **Azure** nodo, elija **administrar y filtrar suscripciones...** , elija hello **certificados** ficha y siga uno de los procedimientos de hello:</span><span class="sxs-lookup"><span data-stu-id="a28c5-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="a28c5-123">Elija **importar** diálogo de tooopen Hola Importar suscripciones de Microsoft Azure donde podrá descargar archivo de las suscripciones de hello para hello actualmente cargado o suscripción, tooits de examinar la ubicación de descarga y, a continuación, importarlo para su uso en autenticación.</span><span class="sxs-lookup"><span data-stu-id="a28c5-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="a28c5-124">Elija **New** diálogo de nueva suscripción de hello tooopen donde puede configurar una nueva suscripción para su uso en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a28c5-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="a28c5-125">Elija **editar** (después de elegir su suscripción activa) diálogo de Editar suscripción hello tooopen donde puede editar una suscripción existente para su uso en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a28c5-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="a28c5-126">Hello siguiente procedimiento se da por supuesto que hello **nueva suscripción** cuadro de diálogo está abierto.</span><span class="sxs-lookup"><span data-stu-id="a28c5-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="a28c5-127">tooset credenciales de autenticación en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a28c5-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="a28c5-128">Hola **seleccionar un certificado existente** para lista de autenticación, seleccione un certificado.</span><span class="sxs-lookup"><span data-stu-id="a28c5-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="a28c5-129">Elija hello **ruta de acceso completa de copia hello** vínculo.</span><span class="sxs-lookup"><span data-stu-id="a28c5-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="a28c5-130">ruta de acceso de Hello para el certificado de hello (archivo .cer) es copiada toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="a28c5-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a28c5-131">toopublish su aplicación de Azure desde Visual Studio, debe cargar este certificado toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a28c5-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="a28c5-132">tooupload Hola certificado toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="a28c5-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="a28c5-133">Abra hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a28c5-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="a28c5-134">Si se le solicita, inicie sesión en el portal de toohello y, a continuación, navegue demasiado**configuración**, **certificados de administración**.</span><span class="sxs-lookup"><span data-stu-id="a28c5-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="a28c5-135">En el panel de certificados de administración de hello, elija **cargar**.</span><span class="sxs-lookup"><span data-stu-id="a28c5-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="a28c5-136">Seleccione la suscripción de Azure, pegue Hola ruta de acceso completa del archivo .cer de Hola que acaba de crear y elija **cargar**.</span><span class="sxs-lookup"><span data-stu-id="a28c5-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
