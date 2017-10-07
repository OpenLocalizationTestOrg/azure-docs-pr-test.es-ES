---
title: "Guía de aaaTroubleshooting de transmisión por secuencias en directo | Documentos de Microsoft"
description: "Este tema ofrece sugerencias sobre cómo tootroubleshoot live problemas de transmisión por secuencias."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="f2e9a-103">Guía de solución de problemas para el streaming en vivo</span><span class="sxs-lookup"><span data-stu-id="f2e9a-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="f2e9a-104">Este tema ofrece sugerencias acerca de cómo tootroubleshoot algunas live streaming problemas.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="f2e9a-105">Problemas relacionados con codificadores tooon locales</span><span class="sxs-lookup"><span data-stu-id="f2e9a-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="f2e9a-106">Esta sección proporciona sugerencias sobre cómo codificadores locales tooon relacionados de tootroubleshoot problemas que están configuración toosend canales de secuencia tooAMS una velocidad de bits única que están habilitadas para la codificación en directo.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="f2e9a-107">Problema: Desearía toosee registros</span><span class="sxs-lookup"><span data-stu-id="f2e9a-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="f2e9a-108">**Posible problema**: no puede encontrar los registros del codificador que podrían ayudar en los problemas de depuración.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="f2e9a-109">**Telestream Wirecast**: normalmente encontrará los registros en C:\Users\{username}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="f2e9a-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="f2e9a-110">**Live elemental**: puede encontrar tiene toologs de vínculos en el portal de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="f2e9a-111">Haga clic en **Estadísticas** y luego en **Registros**.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="f2e9a-112">En hello **archivos de registro** página, verá una lista de registros para todos los Hola AcontecimientoEnDirecto elementos; seleccione Hola una coincidencia de la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="f2e9a-113">**Flash el Codificador multimedia de Live**: puede encontrar Hola **directorio de registro...**  desplazándose toohello **registro codificación** ficha.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="f2e9a-114">Problema: no hay ninguna opción para generar una secuencia progresiva</span><span class="sxs-lookup"><span data-stu-id="f2e9a-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="f2e9a-115">**Problema potencial**: automáticamente no deshacer el entrelazado de codificador de Hola que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="f2e9a-116">**Pasos para solucionar problemas**: buscar una opción entrelazada dentro de la interfaz del codificador Hola.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="f2e9a-117">Cuando se habilite la opción de eliminación de entrelazado, compruebe de nuevo la configuración de la salida progresiva.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="f2e9a-118">Problema: Se intentó varias configuraciones de salida de codificador y tooconnect todavía no se puede.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="f2e9a-119">**Posible problema**: el canal de codificación Azure no se restableció correctamente.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="f2e9a-120">**Pasos para solucionar problemas**: asegúrese de codificador de hello seguro ya no inserta tooAMS, detener y restablecer el canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="f2e9a-121">Una vez que se ejecuta de nuevo, intente conectarse su codificador con una nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="f2e9a-122">Si todavía no se soluciona el problema de hello, intente crear un nuevo canal completamente, en ocasiones, pueden dañarse los canales tras varios intentos fallidos.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="f2e9a-123">**Problema potencial**: Hola GOP configuración de tamaño o fotograma clave no es óptimas.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="f2e9a-124">**Pasos para solucionar problemas**: el intervalo de fotogramas clave o el tamaño de GOP recomendado es de 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="f2e9a-125">Algunos codificadores calculan esta configuración en el número de fotogramas, mientras que otros usan segundos.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="f2e9a-126">Por ejemplo: cuando se realizan envíos a 30fps, Hola tamaño GOP sería 60 marcos, que es equivalente too2 segundos.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="f2e9a-127">**Problema potencial**: puertos estén cerrados están bloqueando el flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="f2e9a-128">**Pasos para solucionar problemas**: transmisión por secuencias a través de RTMP, compruebe el firewall o tooconfirm de configuración de proxy que estén abiertos los puertos de salida 1935 y 1936.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="f2e9a-129">Cuando se use el streaming de RTP, confirme que el puerto saliente 2010 está abierto.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="f2e9a-130">Problema: Al configurar Hola codificador toostream con hello protocolo RTP, hay ningún lugar tooenter un nombre de host.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="f2e9a-131">**Problema potencial**: codificadores RTP muchas no permiten nombres de host y una dirección IP deberá toobe adquirido.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="f2e9a-132">**Pasos para solucionar problemas**: toofind Hola dirección IP, abra un símbolo del sistema en cualquier equipo.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="f2e9a-133">toodo esto en Windows, abra Hola selector de ejecución (WIN + R) y escriba "cmd" tooopen.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="f2e9a-134">Una vez abierto Hola símbolo del sistema, escriba "Ping [nombre de Host de AMS]".</span><span class="sxs-lookup"><span data-stu-id="f2e9a-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="f2e9a-135">nombre de host de Hello puede obtenerse mediante la omisión de número de puerto de Hola de hello URL de introducción de Azure, como se resalta en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="f2e9a-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="f2e9a-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="f2e9a-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="f2e9a-138">Si, después de seguir los pasos de solución de problemas de Hola que todavía no se puede transmitir correctamente, envíe una incidencia de soporte técnico mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e9a-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="f2e9a-139">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f2e9a-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f2e9a-140">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f2e9a-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

