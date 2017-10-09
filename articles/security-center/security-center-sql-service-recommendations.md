---
title: aaaProtecting SQL Azure servicio y los datos en el centro de seguridad de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="27324-103">Protección del servicio SQL de Azure en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27324-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="27324-104">Centro de seguridad de Azure analiza el estado de seguridad de Hola de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="27324-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="27324-105">Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea las recomendaciones que le guiarán a lo largo de proceso de Hola de configuración de controles de Hola que sea necesitado.</span><span class="sxs-lookup"><span data-stu-id="27324-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="27324-106">Las recomendaciones aplican tipos de recursos de tooAzure: máquinas virtuales (VM), redes, aplicaciones y datos y SQL.</span><span class="sxs-lookup"><span data-stu-id="27324-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="27324-107">Este artículo tratan las recomendaciones que se aplican los datos y el servicio SQL de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="27324-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="27324-108">Las recomendaciones se centran en la habilitación de la auditoría de servidores y bases de datos de SQL de Azure, el cifrado de bases de datos SQL Database y la habilitación del cifrado de su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="27324-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="27324-109">Uso de tabla de Hola a continuación como un toohelp de referencia comprende recomendaciones de SQL disponibles servicio y los datos de Hola y lo que hace cada uno de ellos si se aplica.</span><span class="sxs-lookup"><span data-stu-id="27324-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="27324-110">Recomendaciones de datos y servicio SQL disponibles</span><span class="sxs-lookup"><span data-stu-id="27324-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="27324-111">Recomendación</span><span class="sxs-lookup"><span data-stu-id="27324-111">Recommendation</span></span> | <span data-ttu-id="27324-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="27324-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="27324-113">Habilitar la auditoría y la detección de amenazas en los servidores SQL Server</span><span class="sxs-lookup"><span data-stu-id="27324-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="27324-114">Recomienda activar la auditoría y la detección de amenazas para los servidores de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="27324-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="27324-115">Habilitación de la auditoría y la detección de amenazas en bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="27324-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="27324-116">Recomienda activar la auditoría y la detección de amenazas para las bases de datos de Azure SQL (solo en el servicio Azure SQL; no incluye la instancia SQL que se ejecuta en sus máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="27324-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="27324-117">Habilitar Cifrado de datos transparente en bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="27324-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="27324-118">Recomienda habilitar el cifrado de bases de datos SQL (solo el servicio SQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="27324-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="27324-119">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="27324-119">See also</span></span>
<span data-ttu-id="27324-120">toolearn más información acerca de las recomendaciones que se aplican tooother tipos de recursos de Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="27324-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="27324-121">Protección de las máquinas virtuales en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27324-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="27324-122">Protección de las aplicaciones en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27324-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="27324-123">Protección de las redes en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27324-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="27324-124">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="27324-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="27324-125">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="27324-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="27324-126">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="27324-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="27324-127">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="27324-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
