---
title: Azure Log Integration en Security Center | Microsoft Docs
description: "Obtenga información sobre cómo funcionan las alertas de Azure Security Center con la integración de registros."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 294a795746420233e961e67cceec4b0538e49ff6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-your-security-center-alerts-in-azure-log-integration"></a><span data-ttu-id="32f83-103">Cómo obtener alertas de Security Center en Azure Log Integration</span><span class="sxs-lookup"><span data-stu-id="32f83-103">How to get your Security Center alerts in Azure log integration</span></span>
<span data-ttu-id="32f83-104">En este artículo se proporcionan los pasos necesarios para habilitar el servicio de Azure Log Integration para extraer información de alertas de seguridad generadas por Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="32f83-104">This article provides the steps required to enable the Azure Log Integration service to pull Security Alert information generated by Azure Security Center.</span></span> <span data-ttu-id="32f83-105">Primero debe haber completado correctamente los pasos descritos en el artículo [Introducción](security-azure-log-integration-get-started.md) antes de realizar los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="32f83-105">You must have successfully completed the steps in the  [Get started](security-azure-log-integration-get-started.md) article before performing the steps in this article.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="32f83-106">Pasos detallados</span><span class="sxs-lookup"><span data-stu-id="32f83-106">Detailed steps</span></span>
<span data-ttu-id="32f83-107">Con los siguientes pasos creará la entidad de servicio de Azure Active Directory necesaria y asignará permisos de lectura de la entidad de servicio a la suscripción:</span><span class="sxs-lookup"><span data-stu-id="32f83-107">The following steps will create the required Azure Active Directory Service Principal and assign the Service Principle read permissions to the subscription:</span></span>
1. <span data-ttu-id="32f83-108">Abra el símbolo del sistema y vaya a **C:\Archivos de programa\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="32f83-108">Open the command prompt and navigate to **c:\Program Files\Microsoft Azure Log Integration**</span></span>
2. <span data-ttu-id="32f83-109">Ejecute el comando ``azlog createazureid``.</span><span class="sxs-lookup"><span data-stu-id="32f83-109">Run the command ``azlog createazureid``</span></span>

    <span data-ttu-id="32f83-110">Este comando solicita el inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="32f83-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="32f83-111">A continuación, el comando crea una [Entidad de servicio de Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) en los inquilinos de Azure AD que hospedan las suscripciones de Azure en las que el usuario inició sesión como administrador, coadministrador o propietario.</span><span class="sxs-lookup"><span data-stu-id="32f83-111">The command then creates an [Azure Active Directory Service Principal](../active-directory/develop/active-directory-application-objects.md) in the Azure AD Tenants that host the Azure subscriptions in which the logged in user is an Administrator, a Co-Administrator, or an Owner.</span></span> <span data-ttu-id="32f83-112">El comando producirá un error si el usuario ha iniciado sesión solo como usuario invitado en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32f83-112">The command will fail if the logged in user is only a Guest user in the Azure AD Tenant.</span></span> <span data-ttu-id="32f83-113">La autenticación en Azure se hace con Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="32f83-113">Authentication to Azure is done through Azure Active Directory (AD).</span></span> <span data-ttu-id="32f83-114">La creación de una entidad de servicio para la integración de registro de Azure creará la identidad de Azure AD a la que se otorgará acceso de lectura de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="32f83-114">Creating a service principal for Azlog Integration creates the Azure AD identity that will be given access to read from Azure subscriptions.</span></span>

2. <span data-ttu-id="32f83-115">Después ejecutará un comando que asigna acceso de lectura en la suscripción a la entidad de servicio creada en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="32f83-115">Next you will run a command that assigns reader access on the subscription to the service principal created in step 2.</span></span> <span data-ttu-id="32f83-116">Si no especifica un SubscriptionID, entonces el comando intenta asignar el rol de lector de la entidad de servicio a todas las suscripciones a las que tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="32f83-116">If you don’t specify a SubscriptionID, then the command will attempt to assign the service principal reader role to all subscriptions to which you have any access.</span></span> </br></br>
``azlog authorize <SubscriptionID>`` </br> <span data-ttu-id="32f83-117">por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32f83-117">for example</span></span> </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    <span data-ttu-id="32f83-118">Puede que vea advertencias si ejecuta el comando authorize inmediatamente después del comando createazureid.</span><span class="sxs-lookup"><span data-stu-id="32f83-118">You may see warnings if you run the authorize command immediately after the createazureid command.</span></span> <span data-ttu-id="32f83-119">Se produce cierta latencia entre el momento en que se crea la cuenta de Azure AD y el momento en que la cuenta está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="32f83-119">There is some latency between when the Azure AD account is created and when the account is available for use.</span></span> <span data-ttu-id="32f83-120">Si espera unos 60 segundos después de ejecutar el comando createazureid para ejecutar el comando authorize, no debería ver estas advertencias.</span><span class="sxs-lookup"><span data-stu-id="32f83-120">If you wait about 60 seconds after running the createazureid command to run the authorize command, then you should not see these warnings.</span></span>

4. <span data-ttu-id="32f83-121">Compruebe las carpetas siguientes para confirmar que contienen los archivos JSON del registro de auditoría:</span><span class="sxs-lookup"><span data-stu-id="32f83-121">Check the following folders to confirm that the Audit log JSON files are there:</span></span>
 * <span data-ttu-id="32f83-122">**c:\Users\azlog\AzureResourceManagerJson**</span><span class="sxs-lookup"><span data-stu-id="32f83-122">**c:\Users\azlog\AzureResourceManagerJson**</span></span>
 * <span data-ttu-id="32f83-123">**c:\Users\azlog\AzureResourceManagerJsonLD**</span><span class="sxs-lookup"><span data-stu-id="32f83-123">**c:\Users\azlog\AzureResourceManagerJsonLD**</span></span> </br></br>
5. <span data-ttu-id="32f83-124">Compruebe las carpetas siguientes para confirmar que contienen las alertas de Security Center:</span><span class="sxs-lookup"><span data-stu-id="32f83-124">Check the following folders to confirm that Security Center alerts exist in them:</span></span></br></br>
 * <span data-ttu-id="32f83-125">**c:\Users\azlog\AzureSecurityCenterJson**</span><span class="sxs-lookup"><span data-stu-id="32f83-125">**c:\Users\azlog\AzureSecurityCenterJson**</span></span>
 * <span data-ttu-id="32f83-126">**c:\Users\azlog\AzureSecurityCenterJsonLD**</span><span class="sxs-lookup"><span data-stu-id="32f83-126">**c:\Users\azlog\AzureSecurityCenterJsonLD**</span></span> </br></br>

<span data-ttu-id="32f83-127">Si experimenta problemas durante la instalación y la configuración, abra una [solicitud de soporte técnico](/azure-supportability/how-to-create-azure-support-request.md) y seleccione **Integración de registros** como el servicio para el que está solicitando soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="32f83-127">If you run into any issues during the installation and configuration, please open a [support request](/azure-supportability/how-to-create-azure-support-request.md), select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32f83-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32f83-128">Next steps</span></span>
<span data-ttu-id="32f83-129">Para más información sobre Azure Log Integration, vea los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="32f83-129">To learn more about Azure Log Integration, see the following documents:</span></span>

* <span data-ttu-id="32f83-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Integración de registros de Microsoft Azure para registros de Azure): Centro de descarga para obtener información, los requisitos del sistema y las instrucciones de instalación de la integración de registros de Azure.</span><span class="sxs-lookup"><span data-stu-id="32f83-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span></span>
* <span data-ttu-id="32f83-131">[Introduction to Azure log integration](security-azure-log-integration-overview.md) (Introducción a la integración de registro de Azure): este documento es una introducción del servicio de integración de registro de Azure, las principales funcionalidades y cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="32f83-131">[Introduction to Azure log integration](security-azure-log-integration-overview.md) – This document introduces you to Azure log integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="32f83-132">[Pasos de configuración para soluciones de asociados](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) : esta entrada de blog le muestra cómo configurar la integración de registros de Azure para que funcione con soluciones de asociados, como Splunk, HP ArcSight y IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="32f83-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how to configure Azure log integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="32f83-133">[Preguntas más frecuentes sobre la integración de registro de Azure (P+F)](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre la integración de registro de Azure.</span><span class="sxs-lookup"><span data-stu-id="32f83-133">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span></span>
* <span data-ttu-id="32f83-134">[Integración de las alertas de Security Center con la integración de registro de Azure (versión preliminar)](../security-center/security-center-integrating-alerts-with-log-integration.md). Este documento le explica cómo sincronizar las alertas de Security Center, además de los eventos de seguridad de máquina virtual recopilados por Diagnósticos de Azure y los registros de auditoría de Azure, con sus análisis de registros o una solución SIEM.</span><span class="sxs-lookup"><span data-stu-id="32f83-134">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure Audit Logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="32f83-135">[New features for Azure diagnostics and Azure Audit Logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) (Nuevas características de Diagnósticos de Azure y registros de auditoría de Azure): esta entrada de blog es una introducción a los registros de auditoría de Azure y a otras características que le ayudarán a obtener información sobre las operaciones de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32f83-135">[New features for Azure diagnostics and Azure Audit Logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – This blog post introduces you to Azure Audit Logs and other features that help you gain insights into the operations of your Azure resources.</span></span>