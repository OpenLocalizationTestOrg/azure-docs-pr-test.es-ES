---
title: "Integración de registro con los registros de auditoría de Azure Active Directory aaaAzure | Documentos de Microsoft"
description: "Saber cómo tooinstall Hola servicio de integración de registro de Azure e integrar los registros de registros de auditoría de Azure"
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="33eed-103">Integración de los registros de auditoría de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33eed-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="33eed-104">Los eventos de auditoría de Azure Active Directory (Azure AD) le ayudan a identificar las acciones con privilegios que se produjeron en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33eed-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="33eed-105">Puede ver Hola tipos de eventos que puede realizar un seguimiento mediante la revisión [eventos de informe de auditoría de Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="33eed-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33eed-106">Antes de intentar pasos hello en este artículo, debe revisar hello [Introducción](security-azure-log-integration-get-started.md) artículo y complete los pasos de Hola allí.</span><span class="sxs-lookup"><span data-stu-id="33eed-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="33eed-107">Registros de auditoría de Azure Active directory de pasos toointegrate</span><span class="sxs-lookup"><span data-stu-id="33eed-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="33eed-108">Abra el símbolo del sistema de Hola y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="33eed-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="33eed-109">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="33eed-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="33eed-110">Este comando solicita el inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="33eed-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="33eed-111">Hello comando, a continuación, crea un Azure Active Directory entidad de servicio en los inquilinos de hello Azure AD que hospedan Hola suscripciones de Azure en qué Hola ha iniciado la sesión de usuario es un administrador, un administrador o un propietario.</span><span class="sxs-lookup"><span data-stu-id="33eed-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="33eed-112">comando Hola se producirá un error si usuario registrado hello es solo un usuario invitado en el inquilino de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="33eed-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="33eed-113">TooAzure de autenticación se realiza a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33eed-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="33eed-114">Crear a una entidad de servicio para la integración de registro de Azure crea Hola identidad de Azure AD que se da acceso tooread de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="33eed-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="33eed-115">Comando de ejecución Hola siguiente tooprovide el identificador del inquilino.</span><span class="sxs-lookup"><span data-stu-id="33eed-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="33eed-116">Necesita a miembro de toobe del comando de hello inquilino admin rol toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="33eed-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="33eed-117">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33eed-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="33eed-118">Comprobar Hola después tooconfirm de carpetas que Hola archivos de JSON de registro de auditoría de Azure Active Directory se crea en ellas:</span><span class="sxs-lookup"><span data-stu-id="33eed-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="33eed-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="33eed-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="33eed-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="33eed-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="33eed-121">Hello vídeo siguiente muestra los pasos de hello tratados en este artículo:</span><span class="sxs-lookup"><span data-stu-id="33eed-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="33eed-122">Para obtener instrucciones específicas para incluir información de hello en archivos JSON de hello en el sistema de administración (SIEM) de eventos e información de seguridad, póngase en contacto con su proveedor SIEM.</span><span class="sxs-lookup"><span data-stu-id="33eed-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="33eed-123">Ayuda de la Comunidad está disponible a través de hello [foro de MSDN de integración de Azure registro](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="33eed-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="33eed-124">Este foro permite a los usuarios en hello Azure registro integración Comunidad toosupport entre sí con preguntas, respuestas, sugerencias y trucos.</span><span class="sxs-lookup"><span data-stu-id="33eed-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="33eed-125">Además, equipo de integración de Azure registro de hello supervisa este foro y ayuda a siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="33eed-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="33eed-126">También puede abrir una [solicitud de soporte técnico](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="33eed-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="33eed-127">Seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="33eed-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33eed-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33eed-128">Next steps</span></span>
<span data-ttu-id="33eed-129">toolearn más información acerca de la integración de registro de Azure, vea:</span><span class="sxs-lookup"><span data-stu-id="33eed-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="33eed-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324) (Microsoft Azure Log Integration para registros de Azure): Esta página del Centro de descarga proporciona información, los requisitos del sistema y las instrucciones de instalación de Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="33eed-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="33eed-131">[Introducción tooAzure registro integración](security-azure-log-integration-overview.md): este artículo explica tooAzure integración de registro, sus capacidades claves y su funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="33eed-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="33eed-132">[Pasos de configuración de socios comerciales](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): esta entrada de blog muestra cómo tooconfigure toowork de integración de registro de Azure con socios comerciales soluciones Splunk, HP ArcSight y IBM QRadar.</span><span class="sxs-lookup"><span data-stu-id="33eed-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="33eed-133">[Preguntas más frecuentes sobre Azure Log Integration](security-azure-log-integration-faq.md). Este artículo de preguntas más frecuentes responde a preguntas sobre Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="33eed-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="33eed-134">[Integración de las alertas del centro de seguridad con la integración de Azure registro](../security-center/security-center-integrating-alerts-with-log-integration.md): este artículo muestra cómo las alertas toosync centro de seguridad, junto con los eventos de seguridad de máquina virtual recopilados por diagnósticos de Azure y los registros de auditoría de Azure, con los análisis de registros o Solución SIEM.</span><span class="sxs-lookup"><span data-stu-id="33eed-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="33eed-135">[Registros de auditoría de nuevas características para diagnósticos de Azure y Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): esta entrada de blog presenta tooAzure los registros de auditoría y otras características que le ayudarán a obtienen información sobre las operaciones de Hola de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="33eed-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
