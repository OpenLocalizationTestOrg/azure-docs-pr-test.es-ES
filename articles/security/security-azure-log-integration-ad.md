---
title: "Azure Log Integration con registros de auditoría de Azure Active Directory | Microsoft Docs"
description: "Aquí aprenderá cómo instalar el servicio Azure Log Integration y cómo integrar los registros desde registros de auditoría de Azure"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="4b890-103">Integración de los registros de auditoría de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b890-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="4b890-104">Los eventos de auditoría de Azure Active Directory (Azure AD) le ayudan a identificar las acciones con privilegios que se produjeron en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b890-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="4b890-105">Puede ver los tipos de eventos de los que puede realizar un seguimiento mediante la revisión de [Eventos del informe de auditoría de Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="4b890-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4b890-106">Debe revisar el artículo [Introducción](security-azure-log-integration-get-started.md) y completar los pasos allí antes de intentar seguir los pasos descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4b890-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="4b890-107">Pasos para la integración de los registros de auditoría de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b890-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="4b890-108">Abra el símbolo del sistema y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="4b890-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="4b890-109">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="4b890-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="4b890-110">Este comando solicita el inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b890-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="4b890-111">A continuación, el comando crea una entidad de servicio de Azure Active Directory en los inquilinos de Azure AD que hospedan las suscripciones de Azure en las que el usuario inició sesión como administrador, coadministrador o propietario.</span><span class="sxs-lookup"><span data-stu-id="4b890-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="4b890-112">El comando producirá un error si el usuario ha iniciado sesión solo como usuario invitado en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b890-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="4b890-113">La autenticación en Azure se hace con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b890-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="4b890-114">La creación de una entidad de servicio para Azure Log Integration creará la identidad de Azure AD a la que se otorgará acceso de lectura de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b890-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="4b890-115">Ejecute el siguiente comando para proporcionar el identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="4b890-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="4b890-116">Debe ser miembro del rol de administrador de inquilinos para ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="4b890-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="4b890-117">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4b890-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="4b890-118">Compruebe las siguientes carpetas para confirmar que se han creado los archivos JSON de registro de auditoría de Azure Active Directory en las siguientes rutas:</span><span class="sxs-lookup"><span data-stu-id="4b890-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="4b890-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="4b890-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="4b890-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="4b890-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="4b890-121">En el siguiente vídeo se muestran los pasos que se describen en este artículo:</span><span class="sxs-lookup"><span data-stu-id="4b890-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="4b890-122">Para obtener instrucciones específicas sobre cómo llevar la información de los archivos JSON al sistema de información de seguridad y administración de eventos (SIEM), póngase en contacto con el proveedor SIEM.</span><span class="sxs-lookup"><span data-stu-id="4b890-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="4b890-123">Puede encontrar ayuda de la comunidad en [Foro MSDN de Azure Log Integration](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="4b890-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="4b890-124">Este foro permite a los usuarios de la comunidad de Azure Log Integration ayudarse unos a otros con preguntas, respuestas, consejos y sugerencias.</span><span class="sxs-lookup"><span data-stu-id="4b890-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="4b890-125">Además, el equipo de Azure Log Integration supervisa este foro y le ayudará siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="4b890-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="4b890-126">También puede abrir una [solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="4b890-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="4b890-127">Seleccione **Azure Log Integration** como el servicio para el que está solicitando el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4b890-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b890-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b890-128">Next steps</span></span>
<span data-ttu-id="4b890-129">Para más información sobre Azure Log Integration, consulte:</span><span class="sxs-lookup"><span data-stu-id="4b890-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="4b890-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Microsoft Azure Log Integration para registros de Azure): Esta página del Centro de descarga proporciona información, los requisitos del sistema y las instrucciones de instalación de Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="4b890-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="4b890-131">[Introduction to Azure log integration](security-azure-log-integration-overview.md) (Introducción a Azure Log Integration): este documento es una introducción de Azure Log Integration, sus principales funcionalidades y cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="4b890-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="4b890-132">[Pasos de configuración para soluciones de asociados](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta entrada de blog le muestra cómo configurar Azure Log Integration para que funcione con soluciones de asociados, como Splunk, HP ArcSight y IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="4b890-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="4b890-133">[Preguntas más frecuentes sobre Azure Log Integration](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="4b890-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="4b890-134">[Integración de las alertas de Security Center con Azure Log Integration (versión preliminar)](../security-center/security-center-integrating-alerts-with-log-integration.md). Este artículo le explica cómo sincronizar las alertas de Security Center, además de los eventos de seguridad de máquina virtual recopilados por Azure Diagnostics y los registros de auditoría de Azure, con sus análisis de registros o una solución SIEM.</span><span class="sxs-lookup"><span data-stu-id="4b890-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="4b890-135">[New features for Azure diagnostics and Azure Audit Logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) (Nuevas características de Azure Diagnostics y registros de auditoría de Azure): esta entrada de blog es una introducción a los registros de auditoría de Azure y a otras características que le ayudarán a obtener información sobre las operaciones de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b890-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
