---
title: "aaaLicensing Microsoft® Smooth Streaming Client Porting Kit"
description: "Obtenga información acerca de cómo toolicensing Hola Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="a06a6-103">Licencias de Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="a06a6-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="a06a6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a06a6-104">Overview</span></span>
<span data-ttu-id="a06a6-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** abreviado) es una implementación de cliente de Smooth Streaming que está optimizada toohelp incrustada los fabricantes de dispositivos, cable y operadores de telefonía móvil, proveedores de servicios de contenido, auricular fabricantes, proveedores de software independientes (ISV) y productos de toocreate de proveedores de soluciones y servicios para la transmisión por secuencias contenido de streaming adaptable en formato Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a06a6-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="a06a6-106">SSPK es una implementación independiente de dispositivo y plataforma de cliente de Smooth Streaming que puede portar por plataforma y Hola Licenciatario tooany dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a06a6-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="a06a6-107">Incluye a continuación es una arquitectura de alto nivel y cuadro de IIS Smooth Streaming Porting Kit es Hola Smooth Streaming Client implementación proporcionada por Microsoft e incluye toda la lógica de núcleo de hello para la reproducción de contenido de transmisión por secuencias suave.</span><span class="sxs-lookup"><span data-stu-id="a06a6-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="a06a6-108">A continuación, los asociados los portan para un dispositivo o plataforma específicos mediante la implementación de interfaces adecuadas.</span><span class="sxs-lookup"><span data-stu-id="a06a6-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="a06a6-110">Description</span><span class="sxs-lookup"><span data-stu-id="a06a6-110">Description</span></span>
<span data-ttu-id="a06a6-111">La licencia de SSPK tiene unos términos que ofrecen un valor empresarial excelente.</span><span class="sxs-lookup"><span data-stu-id="a06a6-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="a06a6-112">Licencia SSPK proporciona sector Hola con:</span><span class="sxs-lookup"><span data-stu-id="a06a6-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="a06a6-113">Código fuente de Smooth Streaming Porting Kit en C++</span><span class="sxs-lookup"><span data-stu-id="a06a6-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="a06a6-114">Implementa la funcionalidad Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="a06a6-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="a06a6-115">Agrega análisis de formato, heurística, lógica de almacenamiento en búfer, etc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="a06a6-116">API de aplicación del reproductor</span><span class="sxs-lookup"><span data-stu-id="a06a6-116">Player application APIs</span></span> 
  * <span data-ttu-id="a06a6-117">Interfaces de programación para la interacción con una aplicación de reproductor multimedia</span><span class="sxs-lookup"><span data-stu-id="a06a6-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="a06a6-118">Interfaz de capa de abstracción de plataforma (PAL)</span><span class="sxs-lookup"><span data-stu-id="a06a6-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="a06a6-119">interfaces de programación para la interacción con el sistema operativo de hello (subprocesos, sockets)</span><span class="sxs-lookup"><span data-stu-id="a06a6-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="a06a6-120">Interfaz de capa de abstracción de hardware (HAL)</span><span class="sxs-lookup"><span data-stu-id="a06a6-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="a06a6-121">Interfaces de programación para la interacción con el  descodificadores de A/V de hardware (descodificación, representación)</span><span class="sxs-lookup"><span data-stu-id="a06a6-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="a06a6-122">Interfaz de administración de derechos digitales (DRM)</span><span class="sxs-lookup"><span data-stu-id="a06a6-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="a06a6-123">interfaces de programación para administrar DRM a través de hello capa de abstracción de DRM (DAL)</span><span class="sxs-lookup"><span data-stu-id="a06a6-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="a06a6-124">Microsoft PlayReady Porting Kit se distribuye por separado, pero se integra mediante esta interfaz.</span><span class="sxs-lookup"><span data-stu-id="a06a6-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="a06a6-125">Para obtener más detalles acerca de las licencias de Microsoft PlayReady Device, haga clic en [aquí](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="a06a6-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="a06a6-126">Ejemplos de implementación</span><span class="sxs-lookup"><span data-stu-id="a06a6-126">Implementation samples</span></span> 
  * <span data-ttu-id="a06a6-127">Ejemplo de implementación de PAL para Linux</span><span class="sxs-lookup"><span data-stu-id="a06a6-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="a06a6-128">Ejemplo de implementación de HAL para Linux</span><span class="sxs-lookup"><span data-stu-id="a06a6-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="a06a6-129">Opciones de licencia</span><span class="sxs-lookup"><span data-stu-id="a06a6-129">Licensing Options</span></span>
<span data-ttu-id="a06a6-130">Microsoft Smooth Streaming Client Porting Kit se efectúa toolicensees disponible en dos contratos de licencia distintos: uno para el desarrollo de productos provisional de cliente de transmisión por secuencias suave y otro para la distribución de los usuarios de tooend de Smooth Streaming Client productos finales.</span><span class="sxs-lookup"><span data-stu-id="a06a6-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="a06a6-131">Para los fabricantes de conjunto de chips, integradores de sistema o software independiente (ISV) que requieren un traslado de código de origen kit toodevelop productos provisional, un Microsoft Smooth Streaming Client Porting Kit **licencia del producto provisional** debe ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="a06a6-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="a06a6-132">Para los fabricantes de dispositivos o ISV que necesiten derechos de distribución para que los usuarios de Smooth Streaming cliente Final productos tooend, Hola Microsoft Smooth Streaming Client Porting Kit **licencia del producto Final** debe ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="a06a6-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="a06a6-133">Licencia de producto provisional de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="a06a6-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="a06a6-134">Bajo esta licencia, Microsoft ofrece un Smooth Streaming Client Porting Kit y Hola toodevelop de derechos de propiedad intelectual necesarias y distribuir los propietarios de licencias de productos de versión preliminar de cliente de transmisión por secuencias suave tooother Smooth Streaming Client Porting Kit dispositivo que distribuir Smooth Streaming Client productos finales.</span><span class="sxs-lookup"><span data-stu-id="a06a6-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a06a6-135">Estructura de tarifas</span><span class="sxs-lookup"><span data-stu-id="a06a6-135">Fee structure</span></span>
<span data-ttu-id="a06a6-136">Una cuota de licencia única de 50.000 dólares estadounidenses proporciona acceso toohello Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="a06a6-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="a06a6-137">Licencia Microsoft Smooth Streaming Client Porting Kit Final Product</span><span class="sxs-lookup"><span data-stu-id="a06a6-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="a06a6-138">Bajo esta licencia, Microsoft ofrece necesarias tooreceive de derechos de propiedad intelectual Smooth Streaming Client provisional productos de otros propietarios de licencias de Smooth Streaming Client Porting Kit y toodistribute marca de empresa Smooth Streaming cliente Final Usuarios de productos tooend.</span><span class="sxs-lookup"><span data-stu-id="a06a6-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a06a6-139">Estructura de tarifas</span><span class="sxs-lookup"><span data-stu-id="a06a6-139">Fee structure</span></span>
<span data-ttu-id="a06a6-140">Hola Smooth Streaming cliente Final del producto se encuentra disponible en un modelo de pago de regalías como en:</span><span class="sxs-lookup"><span data-stu-id="a06a6-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="a06a6-141">0,10 USD por cada implementación de dispositivo enviada</span><span class="sxs-lookup"><span data-stu-id="a06a6-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="a06a6-142">pago de regalías Hola está limitado a 50.000 dólares cada año</span><span class="sxs-lookup"><span data-stu-id="a06a6-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="a06a6-143">Sin regalía para las primeras 10.000 implementaciones de dispositivo cada año</span><span class="sxs-lookup"><span data-stu-id="a06a6-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="a06a6-144">Procedimiento de licencias y acceso al SSPK</span><span class="sxs-lookup"><span data-stu-id="a06a6-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="a06a6-145">Envíe un mensaje de correo electrónico [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) para cualquier consulta sobre todas las licencias.</span><span class="sxs-lookup"><span data-stu-id="a06a6-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="a06a6-146">Hola [portal SSPK distribución](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) es accesible tooregistered licenciatarios provisional.</span><span class="sxs-lookup"><span data-stu-id="a06a6-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="a06a6-147">Los propietarios de licencias provisionales y SSPK Final pueden enviar preguntas técnicas demasiado[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a06a6-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="a06a6-148">Licencias con contrato de producto provisional de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="a06a6-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="a06a6-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="a06a6-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="a06a6-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a06a6-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a06a6-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a06a6-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a06a6-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a06a6-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-153">Alticast Corporation</span></span>
* <span data-ttu-id="a06a6-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a06a6-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a06a6-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-157">Cavium, Inc.</span></span>
* <span data-ttu-id="a06a6-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a06a6-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-159">Enseo, Inc.</span></span>
* <span data-ttu-id="a06a6-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a06a6-160">Fluendo S.A.</span></span>
* <span data-ttu-id="a06a6-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a06a6-162">Infomir GMBH</span></span>
* <span data-ttu-id="a06a6-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="a06a6-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="a06a6-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="a06a6-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="a06a6-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="a06a6-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-166">MediaTek Inc.</span></span>
* <span data-ttu-id="a06a6-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="a06a6-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="a06a6-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="a06a6-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="a06a6-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a06a6-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="a06a6-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a06a6-172">SoftAtHome</span></span>
* <span data-ttu-id="a06a6-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-173">Sony Corporation</span></span>
* <span data-ttu-id="a06a6-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="a06a6-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a06a6-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a06a6-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="a06a6-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="a06a6-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="a06a6-180">Licencias con contrato de producto final de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="a06a6-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="a06a6-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a06a6-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a06a6-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a06a6-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a06a6-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a06a6-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a06a6-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="a06a6-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a06a6-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="a06a6-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="a06a6-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="a06a6-189">VE TİC.</span></span> <span data-ttu-id="a06a6-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="a06a6-190">A.Ş</span></span>
* <span data-ttu-id="a06a6-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="a06a6-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="a06a6-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="a06a6-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="a06a6-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="a06a6-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a06a6-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-196">Enseo, Inc.</span></span>
* <span data-ttu-id="a06a6-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="a06a6-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a06a6-198">Fluendo S.A.</span></span>
* <span data-ttu-id="a06a6-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="a06a6-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="a06a6-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="a06a6-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="a06a6-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a06a6-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="a06a6-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a06a6-205">Infomir GMBH</span></span>
* <span data-ttu-id="a06a6-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-207">KDDI Corporation</span></span>
* <span data-ttu-id="a06a6-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="a06a6-209">Orange SA</span></span>
* <span data-ttu-id="a06a6-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="a06a6-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="a06a6-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="a06a6-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="a06a6-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="a06a6-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a06a6-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="a06a6-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a06a6-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="a06a6-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="a06a6-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="a06a6-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="a06a6-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="a06a6-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="a06a6-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="a06a6-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="a06a6-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a06a6-219">SoftAtHome</span></span>
* <span data-ttu-id="a06a6-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-220">Sony Corporation</span></span>
* <span data-ttu-id="a06a6-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="a06a6-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="a06a6-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="a06a6-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="a06a6-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="a06a6-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a06a6-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a06a6-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="a06a6-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="a06a6-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="a06a6-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="a06a6-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="a06a6-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-228">Wistron Corporation</span></span>
* <span data-ttu-id="a06a6-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a06a6-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="a06a6-230">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="a06a6-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a06a6-231">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a06a6-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

