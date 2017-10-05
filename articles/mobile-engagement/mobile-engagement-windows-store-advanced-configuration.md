---
title: "Configuración avanzada del SDK de Engagement para aplicaciones universales de Windows"
description: "Opciones de configuración para Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="cae57-103">Configuración avanzada del SDK de Engagement para aplicaciones universales de Windows</span><span class="sxs-lookup"><span data-stu-id="cae57-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cae57-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="cae57-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="cae57-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cae57-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="cae57-106">iOS</span><span class="sxs-lookup"><span data-stu-id="cae57-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="cae57-107">Android</span><span class="sxs-lookup"><span data-stu-id="cae57-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="cae57-108">Este procedimiento describe cómo configurar diversas opciones de configuración de aplicaciones de Android para Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cae57-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cae57-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cae57-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="cae57-110">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="cae57-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="cae57-111">Deshabilitar los informes automáticos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="cae57-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="cae57-112">Puede deshabilitar la característica de informes automáticos de bloqueo de Engagement.</span><span class="sxs-lookup"><span data-stu-id="cae57-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="cae57-113">Cuando se produzca una excepción no controlada, Engagement no hará nada.</span><span class="sxs-lookup"><span data-stu-id="cae57-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="cae57-114">Si deshabilita esta característica, tenga en cuenta que cuando se produzca un error no controlado en la aplicación, Engagement no enviará la información del bloqueo, **NI** tampoco cerrará la sesión ni los trabajos.</span><span class="sxs-lookup"><span data-stu-id="cae57-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="cae57-115">Para deshabilitar los informes automáticos de bloqueo, personalice la configuración según la manera en que la declaró:</span><span class="sxs-lookup"><span data-stu-id="cae57-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="cae57-116">Desde el archivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="cae57-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="cae57-117">Establezca el informe de bloqueo en `false` entre las etiquetas `<reportCrash>` y `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="cae57-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="cae57-118">Desde el objeto `EngagementConfiguration` en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="cae57-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="cae57-119">Establezca el informe de bloqueo mediante el objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="cae57-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="cae57-120">Deshabilitar los informes en tiempo real</span><span class="sxs-lookup"><span data-stu-id="cae57-120">Disable real time reporting</span></span>
<span data-ttu-id="cae57-121">De forma predeterminada, el servicio de Engagement informa los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="cae57-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="cae57-122">Si su aplicación notifica registros con mucha frecuencia, es mejor almacenar en búfer los registros y notificarlos todos a la vez de manera periódica.</span><span class="sxs-lookup"><span data-stu-id="cae57-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="cae57-123">Esto se denomina "modo de ráfaga".</span><span class="sxs-lookup"><span data-stu-id="cae57-123">This is called “burst mode”.</span></span>

<span data-ttu-id="cae57-124">Para ello, llame al método siguiente:</span><span class="sxs-lookup"><span data-stu-id="cae57-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="cae57-125">El argumento es un valor en **milisegundos**.</span><span class="sxs-lookup"><span data-stu-id="cae57-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="cae57-126">Cuando desee volver a activar el registro en tiempo real, llame al método sin ningún parámetro o con el valor 0.</span><span class="sxs-lookup"><span data-stu-id="cae57-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="cae57-127">El modo de ráfaga aumenta ligeramente la duración de la batería, pero afecta al monitor de Engagement: la duración de todas las sesiones y trabajos se redondeará al umbral de ráfaga (por lo tanto, es posible que las sesiones y los trabajos más cortos que el umbral de ráfaga no sean visibles).</span><span class="sxs-lookup"><span data-stu-id="cae57-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="cae57-128">Se recomienda usar un umbral de ráfaga inferior a 30 000 (30 segundos).</span><span class="sxs-lookup"><span data-stu-id="cae57-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="cae57-129">Los registros guardados se limitan a 300 elementos.</span><span class="sxs-lookup"><span data-stu-id="cae57-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="cae57-130">Si el envío es demasiado largo, puede perder algunos registros.</span><span class="sxs-lookup"><span data-stu-id="cae57-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="cae57-131">El umbral de ráfaga no puede configurarse en un periodo inferior a un segundo.</span><span class="sxs-lookup"><span data-stu-id="cae57-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="cae57-132">Si intenta hacerlo, el SDK mostrará un seguimiento con el error y se restablecerá automáticamente en el valor predeterminado, es decir, cero segundos.</span><span class="sxs-lookup"><span data-stu-id="cae57-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="cae57-133">Esto hará que el SDK informe de los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="cae57-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
