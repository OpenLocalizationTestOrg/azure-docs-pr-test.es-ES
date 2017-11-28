---
title: "direcciones de administración del entorno del servicio de aplicaciones de aaaAzure"
description: "Las direcciones de administración de listas de hello utilizan toocommand un entorno de servicio de aplicaciones"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="7f820-103">Direcciones de administración de App Service Environment</span><span class="sxs-lookup"><span data-stu-id="7f820-103">App Service Environment management addresses</span></span>

<span data-ttu-id="7f820-104">Hola Environment(ASE) de servicio de aplicación es una implementación de hello servicio de aplicaciones de Azure en una subred de la red Virtual de Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="7f820-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="7f820-105">Hola ASE debe ser accesible desde Hola servicio de aplicaciones de Azure para que éste puede administrarse.</span><span class="sxs-lookup"><span data-stu-id="7f820-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="7f820-106">Este tráfico de administración ASE atraviesa la red de hello controlado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="7f820-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="7f820-107">Se trata de servicio de aplicaciones de Azure administración servidores toohello VIP pública que está asociado a ASE Hola.</span><span class="sxs-lookup"><span data-stu-id="7f820-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="7f820-108">Para obtener detalles sobre Hola ASE redes dependencias leen [hello entorno del servicio de aplicaciones y consideraciones de red][networking].</span><span class="sxs-lookup"><span data-stu-id="7f820-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="7f820-109">Para obtener información general sobre Hola ASE puede empezar con [toohello Introducción entono][intro].</span><span class="sxs-lookup"><span data-stu-id="7f820-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="7f820-110">Este documento enumera las direcciones IP de origen de hello para el tráfico de administración toohello ASE.</span><span class="sxs-lookup"><span data-stu-id="7f820-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="7f820-111">Puede usar estos toolock de grupos de seguridad de red de direcciones toocreate hacia abajo el tráfico entrante o utilizarlos en tablas de rutas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7f820-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="7f820-112">toouse esta información debe toouse:</span><span class="sxs-lookup"><span data-stu-id="7f820-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="7f820-113">direcciones IP de Hola que se enumeran para todas las regiones</span><span class="sxs-lookup"><span data-stu-id="7f820-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="7f820-114">dicha región de toohello de coincidencia que su ASE se implementa en las direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f820-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="7f820-115">tráfico de administración de Hola entrantes procede estas direcciones IP tooports 454 y 455.</span><span class="sxs-lookup"><span data-stu-id="7f820-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="7f820-116">Region</span><span class="sxs-lookup"><span data-stu-id="7f820-116">Region</span></span> | <span data-ttu-id="7f820-117">Direcciones</span><span class="sxs-lookup"><span data-stu-id="7f820-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="7f820-118">Todas las regiones</span><span class="sxs-lookup"><span data-stu-id="7f820-118">All regions</span></span> | <span data-ttu-id="7f820-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="7f820-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="7f820-120">Centro y Sur de EE. UU. y Centro y norte de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7f820-120">South Central US & North Central US</span></span> | <span data-ttu-id="7f820-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="7f820-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="7f820-122">Sudeste de Australia y Este de Australia</span><span class="sxs-lookup"><span data-stu-id="7f820-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="7f820-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="7f820-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="7f820-124">Oeste de EE. UU. y Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7f820-124">US West & US East</span></span> | <span data-ttu-id="7f820-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="7f820-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="7f820-126">Europa Occidental y Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="7f820-126">West Europe & North Europe</span></span> | <span data-ttu-id="7f820-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="7f820-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="7f820-128">Centro occidental de EE.UU y Oeste de EE.UU. 2</span><span class="sxs-lookup"><span data-stu-id="7f820-128">West Central US & West US 2</span></span> | <span data-ttu-id="7f820-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="7f820-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="7f820-130">Centro de EE. UU. y Este de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="7f820-130">Central US & East US 2</span></span> | <span data-ttu-id="7f820-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="7f820-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="7f820-132">Este de Asia y Sudeste de Asia</span><span class="sxs-lookup"><span data-stu-id="7f820-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="7f820-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="7f820-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="7f820-134">Este de Japón y Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="7f820-134">Japan East & Japan West</span></span> | <span data-ttu-id="7f820-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="7f820-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="7f820-136">Centro de Canadá & Este de Canadá</span><span class="sxs-lookup"><span data-stu-id="7f820-136">Canada Central & Canada East</span></span> | <span data-ttu-id="7f820-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="7f820-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="7f820-138">Oeste del Reino Unido & Sur del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="7f820-138">UK West & UK South</span></span> | <span data-ttu-id="7f820-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="7f820-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="7f820-140">Corea del Sur y Corea Central</span><span class="sxs-lookup"><span data-stu-id="7f820-140">Korea South & Korea Central</span></span> | <span data-ttu-id="7f820-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="7f820-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="7f820-142">Sur de Brasil y Centro y Sur de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7f820-142">Brazil South & South Central US</span></span>| <span data-ttu-id="7f820-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="7f820-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="7f820-144">India central e India meridional</span><span class="sxs-lookup"><span data-stu-id="7f820-144">Central India & South India</span></span> | <span data-ttu-id="7f820-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="7f820-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="7f820-146">India occidental e India meridional</span><span class="sxs-lookup"><span data-stu-id="7f820-146">West India & South India</span></span> | <span data-ttu-id="7f820-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="7f820-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
