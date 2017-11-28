---
title: "Configuraciones de registro de detección de aplicación para los servicios de Proxy aaaCloud | Documentos de Microsoft"
description: objetivo de Hola de este tema es tooprovide a Hola lo necesita puerto tooperform tooset Hola necesario Hola ejecutan el agente de Cloud App Discovery de Hola.
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="049f7-103">Configuración del registro de Cloud App Discovery para los servicios de proxy</span><span class="sxs-lookup"><span data-stu-id="049f7-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="049f7-104">De forma predeterminada, el agente de Cloud App Discovery de hello es toouse configurado solo Hola puertos 80 o 443.</span><span class="sxs-lookup"><span data-stu-id="049f7-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="049f7-105">Si piensa instalar Cloud App Discovery en un entorno con un servidor proxy que usa un puerto personalizado (ni 80 ni el 443), necesita tooconfigure su toouse agentes este puerto.</span><span class="sxs-lookup"><span data-stu-id="049f7-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="049f7-106">configuración de Hola se basa en una clave del registro.</span><span class="sxs-lookup"><span data-stu-id="049f7-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="049f7-107">objetivo de Hola de este tema es tooprovide a Hola lo necesita puerto tooperform tooset Hola necesario Hola ejecutan el agente de Cloud App Discovery de Hola.</span><span class="sxs-lookup"><span data-stu-id="049f7-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="049f7-108">**puerto de hello toomodify usado por equipo de Hola que se ejecuta el agente de Cloud App Discovery de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="049f7-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="049f7-109">Inicie el editor del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="049f7-109">Start hello registry editor.</span></span> <br> ![Ejecute](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="049f7-111">Navegue tooor crear Hola después de la clave del registro:</span><span class="sxs-lookup"><span data-stu-id="049f7-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="049f7-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="049f7-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="049f7-113">Cree un nuevo valor de **cadenas múltiples** denominado **Puertos**.</span><span class="sxs-lookup"><span data-stu-id="049f7-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="049f7-114">![Nuevo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="049f7-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="049f7-115">Hola tooopen **modificar cadenas múltiples** cuadro de diálogo, haga doble clic en el valor de puertos de Hola.</span><span class="sxs-lookup"><span data-stu-id="049f7-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="049f7-116">En el cuadro de texto de datos de valor de hello, escriba Hola después de valores y agregue todos los puertos personalizados que se usan en su organización:</span><span class="sxs-lookup"><span data-stu-id="049f7-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="049f7-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="049f7-117">
   **80**</span></span> <br><span data-ttu-id="049f7-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="049f7-118">
   **8080**</span></span> <br><span data-ttu-id="049f7-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="049f7-119">
   **8118**</span></span> <br><span data-ttu-id="049f7-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="049f7-120">
   **8888**</span></span> <br><span data-ttu-id="049f7-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="049f7-121">
   **81**</span></span> <br><span data-ttu-id="049f7-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="049f7-122">
   **12080**</span></span> <br><span data-ttu-id="049f7-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="049f7-123">
**6999**</span></span> <br><span data-ttu-id="049f7-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="049f7-124">
**30606**</span></span> <br><span data-ttu-id="049f7-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="049f7-125">
**31595**</span></span> <br><span data-ttu-id="049f7-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="049f7-126">
**4080**</span></span> <br><span data-ttu-id="049f7-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="049f7-127">
**443**</span></span> <br><span data-ttu-id="049f7-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="049f7-128">
**1110**</span></span> <br><br><span data-ttu-id="049f7-129">
![Modificar cadenas múltiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="049f7-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="049f7-130">Haga clic en **Aceptar** tooclose hello **modificar cadenas múltiples** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049f7-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="049f7-131">**Recursos adicionales**</span><span class="sxs-lookup"><span data-stu-id="049f7-131">**Additional Resources**</span></span>

* [<span data-ttu-id="049f7-132">¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?</span><span class="sxs-lookup"><span data-stu-id="049f7-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

