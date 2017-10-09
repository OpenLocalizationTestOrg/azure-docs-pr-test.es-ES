---
title: aaaEnable cifrado de datos transparente en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** habilitar transparente datos cifrado **."
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
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="92507-103">Habilitación del Cifrado de datos transparente en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="92507-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="92507-104">Azure Security Center recomienda que habilite el Cifrado de datos transparente (TDE) en bases de datos SQL si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="92507-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="92507-105">TDE protege los datos y le ayuda a cumplir los requisitos de cumplimiento mediante el cifrado de la base de datos, copias de seguridad asociadas y archivos de registro de transacciones en reposo, sin necesidad de cambios tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="92507-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="92507-106">toolearn más vea [cifrado de datos transparente con base de datos de SQL Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="92507-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="92507-107">Esta recomendación aplica toohello solo; el servicio de SQL Azure no incluye SQL que se ejecutan en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="92507-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="92507-108">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="92507-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="92507-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="92507-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="92507-110">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="92507-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="92507-111">Hola **recomendaciones** hoja, seleccione **Habilitar cifrado de datos transparente**.</span><span class="sxs-lookup"><span data-stu-id="92507-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="92507-112">![Habilitar el cifrado de datos transparente][1]</span><span class="sxs-lookup"><span data-stu-id="92507-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="92507-113">Se abrirá hello **Habilitar cifrado de datos transparente en las bases de datos SQL** hoja.</span><span class="sxs-lookup"><span data-stu-id="92507-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="92507-114">Seleccione un tooenable de base de datos SQL TDE en.</span><span class="sxs-lookup"><span data-stu-id="92507-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="92507-115">![Seleccionar base de datos SQL tooenable TDE en][2]</span><span class="sxs-lookup"><span data-stu-id="92507-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="92507-116">En hello **cifrado de datos transparente** hoja, seleccione **ON** en cifrado de datos y seleccione **guardar** en la cinta de opciones superior Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="92507-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="92507-117">![Activación de TDE][3]</span><span class="sxs-lookup"><span data-stu-id="92507-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="92507-118">Una vez que TDE está habilitado en hello seleccionado base de datos SQL, hello **estado de cifrado** cambiará demasiado**Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="92507-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Estado de cifrado][4]

## <a name="see-also"></a><span data-ttu-id="92507-120">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="92507-120">See also</span></span>
<span data-ttu-id="92507-121">En este artículo se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Habilitar la cifrado de datos transparente".</span><span class="sxs-lookup"><span data-stu-id="92507-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="92507-122">toolearn más información acerca de SQL TDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="92507-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="92507-123">Cifrado de datos transparente con Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="92507-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="92507-124">Introducción al cifrado de datos transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="92507-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="92507-125">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="92507-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="92507-126">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="92507-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="92507-127">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="92507-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="92507-128">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="92507-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="92507-129">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="92507-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="92507-130">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="92507-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="92507-131">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="92507-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="92507-132">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="92507-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
