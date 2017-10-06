---
title: "aaaUser aprovisionar la aplicación de la Galería de Azure AD tooan es tomar horas o más | Documentos de Microsoft"
description: "Cómo toofind out ¿por qué aprovisionar la aplicación de tooyour puede esté tardando más de lo esperado"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="470ec-103">Aplicación de la Galería de Azure AD tooan de aprovisionamiento de usuarios es tomar horas o más</span><span class="sxs-lookup"><span data-stu-id="470ec-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="470ec-104">Cuando habilita por primera vez el aprovisionamiento automático de una aplicación, la sincronización inicial Hola puede tardar de horas, tooseveral 20 minutos, según el tamaño de hello del directorio de Azure AD de Hola y número de Hola de usuarios en el ámbito de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="470ec-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="470ec-105">Las sincronizaciones posteriores después de la sincronización inicial de hello ser más rápidas, como las marcas de agua que representan el estado de Hola de ambos sistemas después de la sincronización inicial hello, mejorar el rendimiento de las sincronizaciones posteriores de almacenes de hello aprovisionamiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="470ec-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="470ec-106">¿Cómo tooimprove aprovisionamiento de rendimiento</span><span class="sxs-lookup"><span data-stu-id="470ec-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="470ec-107">Si la sincronización inicial Hola está tardando más de unas pocas horas, es único lo que puede hacer tooimprove rendimiento:</span><span class="sxs-lookup"><span data-stu-id="470ec-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="470ec-108">**Filtros de ámbito del usuario.**</span><span class="sxs-lookup"><span data-stu-id="470ec-108">**User scoping filters.**</span></span> <span data-ttu-id="470ec-109">Filtros de ámbito permiten toofine ajustar datos de Hola Hola aprovisionamiento extrae de servicio de Azure AD mediante el filtrado de usuarios basados en valores de atributo determinados.</span><span class="sxs-lookup"><span data-stu-id="470ec-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="470ec-110">Para más información sobre los filtros de ámbito, consulte [Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="470ec-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="470ec-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="470ec-111">Next steps</span></span>
[<span data-ttu-id="470ec-112">Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="470ec-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

