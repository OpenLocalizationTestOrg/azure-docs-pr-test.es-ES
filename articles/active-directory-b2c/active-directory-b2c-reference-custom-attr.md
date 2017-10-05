---
title: 'Azure Active Directory B2C: atributos personalizados | Microsoft Docs'
description: "Uso de atributos personalizados en Azure Active Directory B2C para recopilar información sobre sus consumidores"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="0c26a-103">Azure Active Directory B2C: uso de atributos personalizados para recopilar información sobre los consumidores</span><span class="sxs-lookup"><span data-stu-id="0c26a-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="0c26a-104">El directorio de Azure Active Directory (Azure AD) B2C incluye un conjunto integrado de información (atributos): Nombre propio, Apellido, Ciudad, Código postal y otros atributos.</span><span class="sxs-lookup"><span data-stu-id="0c26a-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="0c26a-105">Sin embargo, todas las aplicaciones orientadas al consumidor tienen requisitos únicos en lo relativo a qué atributos recopilan de los consumidores.</span><span class="sxs-lookup"><span data-stu-id="0c26a-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="0c26a-106">Con Azure AD B2C, puede ampliar el conjunto de atributos que se almacenan en cada cuenta de cliente.</span><span class="sxs-lookup"><span data-stu-id="0c26a-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="0c26a-107">Puede crear atributos personalizados en el [Portal de Azure](https://portal.azure.com/) y usarlos en las directivas de registro, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0c26a-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="0c26a-108">También puede leer y escribir estos atributos mediante la [API de Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0c26a-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c26a-109">Los atributos personalizados usan las [Extensiones de esquema de directorio de la API de Azure AD Graph](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c26a-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="0c26a-110">Creación de un atributo personalizado</span><span class="sxs-lookup"><span data-stu-id="0c26a-110">Create a custom attribute</span></span>
1. <span data-ttu-id="0c26a-111">[Siga estos pasos para ir a la hoja de características de B2C en el Portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="0c26a-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="0c26a-112">Haga clic en **Atributos de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="0c26a-113">Haga clic en **+Agregar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0c26a-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0c26a-114">Proporcione un **Nombre** para el atributo personalizado (por ejemplo, "ShoeSize") y, opcionalmente, una **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="0c26a-115">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0c26a-116">Actualmente solo está disponible el **Tipo de datos** "String".</span><span class="sxs-lookup"><span data-stu-id="0c26a-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="0c26a-117">El atributo personalizado ahora está disponible en la lista de **Atributos de usuario**, y puede usarlo en las directivas de registro.</span><span class="sxs-lookup"><span data-stu-id="0c26a-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="0c26a-118">Uso de un atributo personalizado en la directiva de registro</span><span class="sxs-lookup"><span data-stu-id="0c26a-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="0c26a-119">[Siga estos pasos para ir a la hoja de características de B2C en el Portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="0c26a-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="0c26a-120">Haga clic en **Directivas de registro**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="0c26a-121">Haga clic en la directiva de registro (por ejemplo, "B2C_1_SiUp") para abrirla.</span><span class="sxs-lookup"><span data-stu-id="0c26a-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="0c26a-122">Haga clic en **Editar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0c26a-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="0c26a-123">Haga clic en **Atributos de registro** y seleccione el atributo personalizado (por ejemplo, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="0c26a-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="0c26a-124">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-124">Click **OK**.</span></span>
5. <span data-ttu-id="0c26a-125">Haga clic en **Notificaciones de aplicación** y seleccione el atributo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0c26a-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="0c26a-126">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-126">Click **OK**.</span></span>
6. <span data-ttu-id="0c26a-127">Haga clic en **Guardar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0c26a-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="0c26a-128">Puede usar la característica "Ejecutar ahora" en la directiva para comprobar la experiencia del consumidor.</span><span class="sxs-lookup"><span data-stu-id="0c26a-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="0c26a-129">Ahora debe ver "ShoeSize" en la lista de atributos que se recopilan durante el registro del consumidor y en el token enviado de vuelta a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0c26a-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="0c26a-130">Notas</span><span class="sxs-lookup"><span data-stu-id="0c26a-130">Notes</span></span>
* <span data-ttu-id="0c26a-131">Junto con las directivas de registro, los atributos personalizados también se pueden utilizar en las directivas de registro o inicio de sesión y en las directivas de edición del perfil.</span><span class="sxs-lookup"><span data-stu-id="0c26a-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="0c26a-132">Hay un límite conocido de atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="0c26a-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="0c26a-133">Solo se crea la primera vez que se utiliza en cualquier directiva y no cuando se agrega a la lista de **atributos de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0c26a-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

