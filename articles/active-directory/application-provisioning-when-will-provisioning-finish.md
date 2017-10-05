---
title: "Aprovisionamiento de usuarios a una aplicación de la Galería de Azure AD que tarda horas o más | Microsoft Docs"
description: "Cómo averiguar por qué el aprovisionamiento de la aplicación puede estar tardando más de lo previsto"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="a1417-103">Aprovisionamiento de usuarios a una aplicación de la Galería de Azure AD que tarda horas o más</span><span class="sxs-lookup"><span data-stu-id="a1417-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="a1417-104">Cuando se habilita por primera vez el aprovisionamiento automático de una aplicación, la sincronización inicial puede tardar desde 20 minutos hasta varias horas, según el tamaño del directorio de Azure AD y el número de usuarios en el ámbito de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a1417-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="a1417-105">Las sincronizaciones posteriores a la inicial serán más rápidas, ya que el servicio de aprovisionamiento almacena marcas de agua que representan el estado de ambos sistemas tras la sincronización inicial, lo cual mejora el rendimiento de las posteriores.</span><span class="sxs-lookup"><span data-stu-id="a1417-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="a1417-106">Cómo mejorar el rendimiento del aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="a1417-106">How to improve provisioning performance</span></span>

<span data-ttu-id="a1417-107">Si la sincronización inicial está tardando más de unas horas, puede hacer algo para mejorar el rendimiento:</span><span class="sxs-lookup"><span data-stu-id="a1417-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="a1417-108">**Filtros de ámbito del usuario.**</span><span class="sxs-lookup"><span data-stu-id="a1417-108">**User scoping filters.**</span></span> <span data-ttu-id="a1417-109">Los filtros de ámbito le permiten ajustar los datos que el servicio de aprovisionamiento de Azure AD extrae mediante el filtrado de usuarios basado en valores de atributo determinados.</span><span class="sxs-lookup"><span data-stu-id="a1417-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="a1417-110">Para más información sobre los filtros de ámbito, consulte [Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="a1417-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1417-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1417-111">Next steps</span></span>
[<span data-ttu-id="a1417-112">Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1417-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

