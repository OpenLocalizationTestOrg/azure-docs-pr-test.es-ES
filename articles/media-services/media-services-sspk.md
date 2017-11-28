---
title: "Licencias de Microsoft® Smooth Streaming Client Porting Kit"
description: "Más información sobre cómo obtener licencias de Microsoft® Smooth Streaming Client Porting Kit."
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
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="f5e24-103">Licencias de Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="f5e24-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="f5e24-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f5e24-104">Overview</span></span>
<span data-ttu-id="f5e24-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** para abreviar) es una implementación del cliente de Smooth Streaming que está optimizada para ayudar a los fabricantes de dispositivos incrustados y los operadores de cable y dispositivos móviles, los proveedores de servicios de contenido, los fabricantes de auriculares, los fabricantes de software independientes (ISV) y los proveedores de soluciones para crear productos y servicios para contenido de streaming adaptable en formato de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="f5e24-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="f5e24-106">SSPK es una implementación independiente del dispositivo y la plataforma del cliente de Smooth Streaming que el licenciatario puede portar a cualquier dispositivo y plataforma.</span><span class="sxs-lookup"><span data-stu-id="f5e24-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="f5e24-107">A continuación se incluye una arquitectura de alto nivel y el IIS Smooth Streaming Porting Kit es la implementación de Smooth Streaming Client proporcionada por Microsoft e incluye toda la lógica básica para la reproducción del contenido de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="f5e24-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="f5e24-108">A continuación, los asociados los portan para un dispositivo o plataforma específicos mediante la implementación de interfaces adecuadas.</span><span class="sxs-lookup"><span data-stu-id="f5e24-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="f5e24-110">Description</span><span class="sxs-lookup"><span data-stu-id="f5e24-110">Description</span></span>
<span data-ttu-id="f5e24-111">La licencia de SSPK tiene unos términos que ofrecen un valor empresarial excelente.</span><span class="sxs-lookup"><span data-stu-id="f5e24-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="f5e24-112">La licencia SSPK proporciona al sector:</span><span class="sxs-lookup"><span data-stu-id="f5e24-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="f5e24-113">Código fuente de Smooth Streaming Porting Kit en C++</span><span class="sxs-lookup"><span data-stu-id="f5e24-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="f5e24-114">Implementa la funcionalidad Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="f5e24-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="f5e24-115">Agrega análisis de formato, heurística, lógica de almacenamiento en búfer, etc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="f5e24-116">API de aplicación del reproductor</span><span class="sxs-lookup"><span data-stu-id="f5e24-116">Player application APIs</span></span> 
  * <span data-ttu-id="f5e24-117">Interfaces de programación para la interacción con una aplicación de reproductor multimedia</span><span class="sxs-lookup"><span data-stu-id="f5e24-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="f5e24-118">Interfaz de capa de abstracción de plataforma (PAL)</span><span class="sxs-lookup"><span data-stu-id="f5e24-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="f5e24-119">Interfaces de programación para la interacción con el sistema operativo (subprocesos, sockets)</span><span class="sxs-lookup"><span data-stu-id="f5e24-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="f5e24-120">Interfaz de capa de abstracción de hardware (HAL)</span><span class="sxs-lookup"><span data-stu-id="f5e24-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="f5e24-121">Interfaces de programación para la interacción con el  descodificadores de A/V de hardware (descodificación, representación)</span><span class="sxs-lookup"><span data-stu-id="f5e24-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="f5e24-122">Interfaz de administración de derechos digitales (DRM)</span><span class="sxs-lookup"><span data-stu-id="f5e24-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="f5e24-123">Interfaces de programación para administrar DRM a través de la capa de abstracción de DRM (DAL)</span><span class="sxs-lookup"><span data-stu-id="f5e24-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="f5e24-124">Microsoft PlayReady Porting Kit se distribuye por separado, pero se integra mediante esta interfaz.</span><span class="sxs-lookup"><span data-stu-id="f5e24-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="f5e24-125">Para obtener más detalles acerca de las licencias de Microsoft PlayReady Device, haga clic en [aquí](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="f5e24-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="f5e24-126">Ejemplos de implementación</span><span class="sxs-lookup"><span data-stu-id="f5e24-126">Implementation samples</span></span> 
  * <span data-ttu-id="f5e24-127">Ejemplo de implementación de PAL para Linux</span><span class="sxs-lookup"><span data-stu-id="f5e24-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="f5e24-128">Ejemplo de implementación de HAL para Linux</span><span class="sxs-lookup"><span data-stu-id="f5e24-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="f5e24-129">Opciones de licencia</span><span class="sxs-lookup"><span data-stu-id="f5e24-129">Licensing Options</span></span>
<span data-ttu-id="f5e24-130">Microsoft Smooth Streaming Client Porting Kit está disponible para los licenciatarios con dos contratos de licencia distintos: uno para el desarrollo de productos provisional de Smooth Streaming Client Interim Products y otro para la distribución de Smooth Streaming Client Final Products a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="f5e24-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="f5e24-131">Para los fabricantes de conjuntos de chips, integradores de sistemas o fabricantes de software independientes (ISV) que requieren un kit de portabilidad de código fuente para desarrollar productos provisionales, debe ejecutarse una **licencia de productos provisionales** del Microsoft Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="f5e24-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="f5e24-132">Para los fabricantes de dispositivos o ISV que requieren derechos de distribución de Smooth Streaming Client Final Products a usuarios finales, debe ejecutarse una **licencia de productos finales** del Microsoft Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="f5e24-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="f5e24-133">Licencia de producto provisional de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="f5e24-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="f5e24-134">Con esta licencia, Microsoft ofrece un Smooth Streaming Client Porting Kit y los derechos de propiedad intelectual necesarios para desarrollar y distribuir Smooth Streaming Client Interim Products a otros licenciados de dispositivos del Smooth Streaming Client Porting Kit que distribuyan Smooth Streaming Client Final Products.</span><span class="sxs-lookup"><span data-stu-id="f5e24-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="f5e24-135">Estructura de tarifas</span><span class="sxs-lookup"><span data-stu-id="f5e24-135">Fee structure</span></span>
<span data-ttu-id="f5e24-136">Una cuota de licencia única de 50.000 USD proporciona acceso al Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="f5e24-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="f5e24-137">Licencia Microsoft Smooth Streaming Client Porting Kit Final Product</span><span class="sxs-lookup"><span data-stu-id="f5e24-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="f5e24-138">Con esta licencia, Microsoft ofrece todos los derechos de propiedad intelectual necesarios para recibir Smooth Streaming Client Interim Products de otros licenciados del Smooth Streaming Client Porting Kit y distribuir Smooth Streaming Client Final Products con marca de empresa a usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="f5e24-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="f5e24-139">Estructura de tarifas</span><span class="sxs-lookup"><span data-stu-id="f5e24-139">Fee structure</span></span>
<span data-ttu-id="f5e24-140">La licencia Smooth Streaming Client Final Product se ofrece en un modelo de regalías como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f5e24-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="f5e24-141">0,10 USD por cada implementación de dispositivo enviada</span><span class="sxs-lookup"><span data-stu-id="f5e24-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="f5e24-142">La regalía está limitada a 50.000 USD al año</span><span class="sxs-lookup"><span data-stu-id="f5e24-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="f5e24-143">Sin regalía para las primeras 10.000 implementaciones de dispositivo cada año</span><span class="sxs-lookup"><span data-stu-id="f5e24-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="f5e24-144">Procedimiento de licencias y acceso al SSPK</span><span class="sxs-lookup"><span data-stu-id="f5e24-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="f5e24-145">Envíe un mensaje de correo electrónico [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) para cualquier consulta sobre todas las licencias.</span><span class="sxs-lookup"><span data-stu-id="f5e24-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="f5e24-146">Los licenciatarios de productos provisionales pueden acceder al [portal de distribución del SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) .</span><span class="sxs-lookup"><span data-stu-id="f5e24-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="f5e24-147">Los licenciatarios de productos provisionales y finales del SSPK pueden enviar preguntas técnicas a [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f5e24-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="f5e24-148">Licencias con contrato de producto provisional de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="f5e24-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="f5e24-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="f5e24-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="f5e24-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="f5e24-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="f5e24-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f5e24-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="f5e24-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="f5e24-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-153">Alticast Corporation</span></span>
* <span data-ttu-id="f5e24-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="f5e24-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="f5e24-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-157">Cavium, Inc.</span></span>
* <span data-ttu-id="f5e24-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="f5e24-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-159">Enseo, Inc.</span></span>
* <span data-ttu-id="f5e24-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="f5e24-160">Fluendo S.A.</span></span>
* <span data-ttu-id="f5e24-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="f5e24-162">Infomir GMBH</span></span>
* <span data-ttu-id="f5e24-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="f5e24-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="f5e24-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="f5e24-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="f5e24-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="f5e24-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-166">MediaTek Inc.</span></span>
* <span data-ttu-id="f5e24-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="f5e24-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="f5e24-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="f5e24-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="f5e24-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="f5e24-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="f5e24-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="f5e24-172">SoftAtHome</span></span>
* <span data-ttu-id="f5e24-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-173">Sony Corporation</span></span>
* <span data-ttu-id="f5e24-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="f5e24-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="f5e24-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f5e24-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="f5e24-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="f5e24-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="f5e24-180">Licencias con contrato de producto final de Microsoft Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="f5e24-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="f5e24-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="f5e24-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="f5e24-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="f5e24-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="f5e24-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="f5e24-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="f5e24-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="f5e24-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="f5e24-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="f5e24-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="f5e24-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="f5e24-189">VE TİC.</span></span> <span data-ttu-id="f5e24-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="f5e24-190">A.Ş</span></span>
* <span data-ttu-id="f5e24-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="f5e24-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="f5e24-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="f5e24-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="f5e24-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="f5e24-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="f5e24-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-196">Enseo, Inc.</span></span>
* <span data-ttu-id="f5e24-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="f5e24-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="f5e24-198">Fluendo S.A.</span></span>
* <span data-ttu-id="f5e24-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="f5e24-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="f5e24-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="f5e24-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="f5e24-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="f5e24-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="f5e24-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="f5e24-205">Infomir GMBH</span></span>
* <span data-ttu-id="f5e24-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-207">KDDI Corporation</span></span>
* <span data-ttu-id="f5e24-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="f5e24-209">Orange SA</span></span>
* <span data-ttu-id="f5e24-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="f5e24-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="f5e24-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="f5e24-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="f5e24-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="f5e24-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="f5e24-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="f5e24-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="f5e24-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="f5e24-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="f5e24-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="f5e24-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="f5e24-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="f5e24-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="f5e24-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="f5e24-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="f5e24-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="f5e24-219">SoftAtHome</span></span>
* <span data-ttu-id="f5e24-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-220">Sony Corporation</span></span>
* <span data-ttu-id="f5e24-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="f5e24-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="f5e24-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="f5e24-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="f5e24-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="f5e24-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="f5e24-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="f5e24-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="f5e24-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="f5e24-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="f5e24-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="f5e24-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="f5e24-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-228">Wistron Corporation</span></span>
* <span data-ttu-id="f5e24-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="f5e24-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="f5e24-230">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="f5e24-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f5e24-231">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f5e24-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

