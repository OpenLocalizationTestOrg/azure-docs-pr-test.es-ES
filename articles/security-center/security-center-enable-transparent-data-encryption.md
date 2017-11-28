---
title: "Habilitación del Cifrado de datos transparente en Azure Security Center | Microsoft Docs"
description: "En este documento, mostramos cómo implementar la recomendación **Habilitar el Cifrado de datos transparente** del Azure Security Center."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="16731-103">Habilitación del Cifrado de datos transparente en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="16731-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="16731-104">Azure Security Center recomienda que habilite el Cifrado de datos transparente (TDE) en bases de datos SQL si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="16731-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="16731-105">TDE protege los datos y le ayuda a cumplir con los requisitos normativos cifrando la base de datos, las copias de seguridad asociadas y los archivos de registro de transacciones en reposo sin requerir cambios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16731-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="16731-106">Para obtener más información, consulte [Cifrado de datos transparente con Base de datos SQL de Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="16731-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="16731-107">Esta recomendación se aplica solo al servicio de SQL de Azure; no incluye al servicio SQL que se ejecuta en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="16731-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="16731-108">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="16731-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="16731-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="16731-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="16731-110">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="16731-110">Implement the recommendation</span></span>
1. <span data-ttu-id="16731-111">En la hoja **Recomendaciones**, seleccione **Habilitar el cifrado de datos transparente**.</span><span class="sxs-lookup"><span data-stu-id="16731-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="16731-112">![Habilitar el cifrado de datos transparente][1]</span><span class="sxs-lookup"><span data-stu-id="16731-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="16731-113">De este modo, se abre la hoja **Habilitar el cifrado de datos transparente en bases de datos SQL** .</span><span class="sxs-lookup"><span data-stu-id="16731-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="16731-114">Seleccione una base de datos SQL en la que habilitar el TDE.</span><span class="sxs-lookup"><span data-stu-id="16731-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="16731-115">![Selección de la base de datos SQL en la que habilitar TDE][2]</span><span class="sxs-lookup"><span data-stu-id="16731-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="16731-116">En la hoja **Cifrado de datos transparente**, seleccione **Activar** en Cifrado de datos y seleccione **Guardar** en la cinta de opciones superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="16731-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="16731-117">![Activación de TDE][3]</span><span class="sxs-lookup"><span data-stu-id="16731-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="16731-118">Una vez que el TDE esté habilitado en la base de datos SQL seleccionada, el **Estado de cifrado** cambiará a **Cifrado**.</span><span class="sxs-lookup"><span data-stu-id="16731-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Estado de cifrado][4]

## <a name="see-also"></a><span data-ttu-id="16731-120">Consulte también</span><span class="sxs-lookup"><span data-stu-id="16731-120">See also</span></span>
<span data-ttu-id="16731-121">En este artículo mostramos cómo implementar la recomendación "Habilitar el cifrado de datos transparente" de Security Center.</span><span class="sxs-lookup"><span data-stu-id="16731-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="16731-122">Para obtener más información sobre TDE de SQL, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="16731-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="16731-123">Cifrado de datos transparente con Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="16731-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="16731-124">Introducción al cifrado de datos transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="16731-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="16731-125">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="16731-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="16731-126">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16731-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="16731-127">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16731-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="16731-128">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16731-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="16731-129">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="16731-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="16731-130">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="16731-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="16731-131">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="16731-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="16731-132">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="16731-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
