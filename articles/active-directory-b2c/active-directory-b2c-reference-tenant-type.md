---
title: 'Azure Active Directory B2C: Disponibilidad en regiones y residencia de datos | Microsoft Docs'
description: Un tema en tipos de Hola de inquilinos de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="46142-103">Azure Active Directory B2C: Disponibilidad en regiones y residencia de datos</span><span class="sxs-lookup"><span data-stu-id="46142-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="46142-104">Disponibilidad de la región y residencia de datos son dos conceptos muy diferentes que aplican tooAzure AD B2C de manera diferente del resto de Hola de Azure.</span><span class="sxs-lookup"><span data-stu-id="46142-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="46142-105">En este artículo se explican las diferencias de hello entre estos dos conceptos y comparar cómo se aplica tooAzure frente a Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="46142-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="46142-106">Resumen</span><span class="sxs-lookup"><span data-stu-id="46142-106">Summary</span></span>
<span data-ttu-id="46142-107">B2C de Azure AD es **suelen estar disponibles en todo el mundo** con la opción de Hola para **residencia de datos en Estados Unidos o en Europa**.</span><span class="sxs-lookup"><span data-stu-id="46142-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="46142-108">Conceptos</span><span class="sxs-lookup"><span data-stu-id="46142-108">Concepts</span></span>
* <span data-ttu-id="46142-109">**Disponibilidad de la región** hace referencia toowhere un servicio está disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="46142-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="46142-110">**Residencia datos** hace referencia se almacenan los datos de usuario de toowhere.</span><span class="sxs-lookup"><span data-stu-id="46142-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="46142-111">Disponibilidad en regiones</span><span class="sxs-lookup"><span data-stu-id="46142-111">Region availability</span></span>
<span data-ttu-id="46142-112">B2C de Azure AD está disponible en todo el mundo a través de hello nube pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="46142-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="46142-113">Esto difiere del modelo de hello mayoría de los demás seguimiento de los servicios de Azure que acoplar disponibilidad con residencia de datos.</span><span class="sxs-lookup"><span data-stu-id="46142-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="46142-114">Puede ver ejemplos de esto en ambos Azure [productos disponibles por región](https://azure.microsoft.com/regions/services/) hello y página [Calculadora de precios B2C de Active Directory](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="46142-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="46142-115">Residencia de datos</span><span class="sxs-lookup"><span data-stu-id="46142-115">Data residency</span></span>
<span data-ttu-id="46142-116">Azure AD B2C almacena los datos de usuarios en Estados Unidos o Europa.</span><span class="sxs-lookup"><span data-stu-id="46142-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="46142-117">La residencia de datos se determina en función del país o región seleccionado al [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46142-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Captura de pantalla de un inquilino de versión preliminar](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="46142-119">Datos que se encuentran en Estados Unidos de Hola para hello después de países o regiones:</span><span class="sxs-lookup"><span data-stu-id="46142-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="46142-120">Estados Unidos, Canadá, Costa Rica, República Dominicana, El Salvador, Guatemala, México, Panamá, Puerto Rico y Trinidad y Tobago</span><span class="sxs-lookup"><span data-stu-id="46142-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="46142-121">Los datos residen en Europa para hello después de países o regiones:</span><span class="sxs-lookup"><span data-stu-id="46142-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="46142-122">Alemania, Arabia Saudí, Argelia, Austria, Azerbaiyán, Bahréin, Bélgica, Bielorrusia, Bulgaria, Croacia, Chipre, Dinamarca, Egipto, Emiratos Árabes Unidos Eslovaquia, Eslovenia, España, Estonia, Finlandia, Francia, Grecia, Hungría, Irlanda, Islandia, Israel, Italia, Jordania, Kazajistán, Kenia, Kuwait, Letonia, Líbano, Liechtenstein, Lituania, Luxemburgo, Macedonia, Malta, Marruecos, Montenegro, Nigeria, Noruega, Omán, Países Bajos, Pakistán, Polonia, Portugal, Qatar, Reino Unido, República Checa, Rumanía, Rusia, Serbia, Sudáfrica, Suecia, Suiza, Túnez, Turquía y Ucrania.</span><span class="sxs-lookup"><span data-stu-id="46142-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="46142-123">Hola restantes países o regiones están en curso de Hola de añadidos toohello lista.</span><span class="sxs-lookup"><span data-stu-id="46142-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="46142-124">Por ahora, todavía puede usar Azure AD B2C escogiendo Hola países o regiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="46142-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="46142-125">Afganistán, Argentina, Australia, Brasil, Chile, Colombia, Corea, Ecuador, Filipinas, India, Indonesia, Iraq, Japón, Malasia, Nueva Zelanda, Paraguay, Perú, RAE de Hong Kong, Singapur, Sri Lanka, Taiwán, Tailandia, Uruguay y Venezuela.</span><span class="sxs-lookup"><span data-stu-id="46142-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="46142-126">Inquilino de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="46142-126">Preview tenant</span></span>
<span data-ttu-id="46142-127">Si había creado un inquilino de B2C durante el período de versión preliminar de Azure AD B2C, es probable que en **Tipo de inquilino** aparezca **Inquilino de vista previa**.</span><span class="sxs-lookup"><span data-stu-id="46142-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="46142-128">Si éste es el caso de hello, debe usar al inquilino solo para fines de pruebas y desarrollo y no para las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="46142-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46142-129">No hay ninguna ruta de acceso de migración desde una versión preliminar del inquilino de B2C inquilino tooa producción escala B2C.</span><span class="sxs-lookup"><span data-stu-id="46142-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="46142-130">Tenga en cuenta que existen problemas conocidos cuando se elimina un inquilino de vista previa B2C y volver a crear una escala de producción B2C inquilino tenga Hola el mismo nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="46142-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="46142-131">Deberá toocreate un inquilino de B2C producción escala con un nombre de dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="46142-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Captura de pantalla de un inquilino de versión preliminar](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
