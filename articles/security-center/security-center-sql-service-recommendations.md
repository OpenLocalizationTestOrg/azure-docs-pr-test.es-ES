---
title: "Protección de los datos y el servicio de SQL de Azure en Azure Security Center | Microsoft Docs"
description: "En este documento se explica cómo las recomendaciones de Azure Security Center ayudan a proteger el servicio SQL de Azure y los datos y a cumplir las directivas de seguridad."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="32963-103">Protección del servicio SQL de Azure en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="32963-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="32963-104">El Centro de seguridad de Azure analiza el estado de seguridad de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32963-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="32963-105">Cuando Security Center identifica posibles vulnerabilidades de seguridad, crea recomendaciones que lo guiarán por el proceso de configuración de los controles necesarios.</span><span class="sxs-lookup"><span data-stu-id="32963-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="32963-106">Las recomendaciones se aplican a los tipos de recursos de Azure: máquinas virtuales, redes, SQL y datos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="32963-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="32963-107">Este artículo aborda las recomendaciones sobre los datos y el servicio SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="32963-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="32963-108">Las recomendaciones se centran en la habilitación de la auditoría de servidores y bases de datos de SQL de Azure, el cifrado de bases de datos SQL Database y la habilitación del cifrado de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="32963-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="32963-109">Use la tabla siguiente para entender mejor las recomendaciones disponibles sobre los datos y el servicio SQL y lo que harán cada una de ellas si se aplican.</span><span class="sxs-lookup"><span data-stu-id="32963-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="32963-110">Recomendaciones de datos y servicio SQL disponibles</span><span class="sxs-lookup"><span data-stu-id="32963-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="32963-111">Recomendación</span><span class="sxs-lookup"><span data-stu-id="32963-111">Recommendation</span></span> | <span data-ttu-id="32963-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="32963-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="32963-113">Habilitar la auditoría y la detección de amenazas en los servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="32963-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="32963-114">Recomienda activar la auditoría y la detección de amenazas para los servidores de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="32963-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="32963-115">Habilitación de la auditoría y la detección de amenazas en bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="32963-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="32963-116">Recomienda activar la auditoría y la detección de amenazas para las bases de datos de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="32963-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="32963-117">Habilitar Cifrado de datos transparente en bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="32963-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="32963-118">Recomienda habilitar el cifrado de bases de datos SQL (solo el servicio SQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="32963-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="32963-119">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="32963-119">See also</span></span>
<span data-ttu-id="32963-120">Para obtener más información sobre las recomendaciones que se aplican a otros tipos de recursos de Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="32963-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="32963-121">Protección de las máquinas virtuales en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="32963-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="32963-122">Protección de las aplicaciones en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="32963-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="32963-123">Protección de las redes en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="32963-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="32963-124">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="32963-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="32963-125">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md) : aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32963-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="32963-126">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="32963-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="32963-127">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="32963-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
