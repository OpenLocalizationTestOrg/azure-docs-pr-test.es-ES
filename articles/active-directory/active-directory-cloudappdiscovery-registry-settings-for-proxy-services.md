---
title: "Configuración del Registro de Cloud App Discovery para servicios de proxy | Microsoft Docs"
description: El objetivo de este tema es proporcionarle los pasos que debe llevar a cabo para establecer el puerto requerido en los equipos que ejecutan el agente de Cloud App Discovery.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="72485-103">Configuración del registro de Cloud App Discovery para los servicios de proxy</span><span class="sxs-lookup"><span data-stu-id="72485-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="72485-104">De forma predeterminada, el agente de Cloud App Discovery está configurado para usar solo los puertos 80 o 443.</span><span class="sxs-lookup"><span data-stu-id="72485-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="72485-105">Si piensa instalar Cloud App Discovery en un entorno con un servidor proxy que usa un puerto personalizado (que no sea el 80 ni el 443), deberá configurar los agentes para usar dicho puerto.</span><span class="sxs-lookup"><span data-stu-id="72485-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="72485-106">La configuración se basa en una clave del registro.</span><span class="sxs-lookup"><span data-stu-id="72485-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="72485-107">El objetivo de este tema es proporcionarle los pasos que debe llevar a cabo para establecer el puerto requerido en los equipos que ejecutan el agente de Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="72485-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="72485-108">**Para modificar el puerto que usa el equipo que ejecuta el agente de Cloud App Discovery, lleve a cabo los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="72485-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="72485-109">Inicie el editor del Registro.</span><span class="sxs-lookup"><span data-stu-id="72485-109">Start the registry editor.</span></span> <br> ![Ejecute](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="72485-111">Vaya a o cree la siguiente clave del registro:</span><span class="sxs-lookup"><span data-stu-id="72485-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="72485-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="72485-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="72485-113">Cree un nuevo valor de **cadenas múltiples** denominado **Puertos**.</span><span class="sxs-lookup"><span data-stu-id="72485-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="72485-114">![Nuevo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="72485-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="72485-115">Para abrir el cuadro de diálogo **Modificar cadenas múltiples** , haga doble clic en el valor Puertos.</span><span class="sxs-lookup"><span data-stu-id="72485-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="72485-116">En el cuadro de texto Datos de valor, escriba los siguientes valores y agregue todos los puertos personalizados que se usan en su organización: </span><span class="sxs-lookup"><span data-stu-id="72485-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="72485-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="72485-117">
   **80**</span></span> <br><span data-ttu-id="72485-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="72485-118">
   **8080**</span></span> <br><span data-ttu-id="72485-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="72485-119">
   **8118**</span></span> <br><span data-ttu-id="72485-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="72485-120">
   **8888**</span></span> <br><span data-ttu-id="72485-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="72485-121">
   **81**</span></span> <br><span data-ttu-id="72485-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="72485-122">
   **12080**</span></span> <br><span data-ttu-id="72485-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="72485-123">
**6999**</span></span> <br><span data-ttu-id="72485-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="72485-124">
**30606**</span></span> <br><span data-ttu-id="72485-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="72485-125">
**31595**</span></span> <br><span data-ttu-id="72485-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="72485-126">
**4080**</span></span> <br><span data-ttu-id="72485-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="72485-127">
**443**</span></span> <br><span data-ttu-id="72485-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="72485-128">
**1110**</span></span> <br><br><span data-ttu-id="72485-129">
![Modificar cadenas múltiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="72485-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="72485-130">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Modificar cadenas múltiples**.</span><span class="sxs-lookup"><span data-stu-id="72485-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="72485-131">**Recursos adicionales**</span><span class="sxs-lookup"><span data-stu-id="72485-131">**Additional Resources**</span></span>

* [<span data-ttu-id="72485-132">¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?</span><span class="sxs-lookup"><span data-stu-id="72485-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

