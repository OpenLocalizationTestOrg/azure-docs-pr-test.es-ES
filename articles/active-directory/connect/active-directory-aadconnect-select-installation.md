---
title: "Azure AD Connect: selección del tipo de instalación | Microsoft Docs"
description: "Este tema le guía a través de la instalación de hello tooselect escriba toouse para Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="f8197-103">Seleccione qué toouse del tipo de instalación de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f8197-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="f8197-104">Azure AD Connect tiene dos tipos de instalación para la nueva instalación: rápida y personalizada.</span><span class="sxs-lookup"><span data-stu-id="f8197-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="f8197-105">Este tema le ayudará a toodecide qué opción toouse durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="f8197-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="f8197-106">Express</span><span class="sxs-lookup"><span data-stu-id="f8197-106">Express</span></span>
<span data-ttu-id="f8197-107">Express es la opción más común de Hola y se utiliza al 90% de todas las instalaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="f8197-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="f8197-108">Fue diseñado tooprovide una configuración que le sirva para escenarios de clientes más comunes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8197-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="f8197-109">Se da por supuesto que:</span><span class="sxs-lookup"><span data-stu-id="f8197-109">It assumes:</span></span>

- <span data-ttu-id="f8197-110">Tiene un único bosque de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="f8197-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="f8197-111">Tener una cuenta de administrador de empresa que puede usar para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8197-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="f8197-112">Tiene menos de 100 000 objetos en Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="f8197-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="f8197-113">Obtendrá:</span><span class="sxs-lookup"><span data-stu-id="f8197-113">You get:</span></span>

- <span data-ttu-id="f8197-114">[Sincronización de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) desde local tooAzure AD para inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8197-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="f8197-115">Una configuración que sincroniza a los [usuarios, grupos, contactos y equipos de Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="f8197-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="f8197-116">Sincronización de todos los objetos válidos en todos los dominios y todas las unidades organizativas.</span><span class="sxs-lookup"><span data-stu-id="f8197-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="f8197-117">[La actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) está habilitado toomake Asegúrese de que siempre utilice Hola última versión disponible.</span><span class="sxs-lookup"><span data-stu-id="f8197-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="f8197-118">Opciones en las que puede continuar utilizando la instalación rápida:</span><span class="sxs-lookup"><span data-stu-id="f8197-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="f8197-119">Si no desea toosynchronize todas las unidades organizativas, puede usar Express y en la última página de hello, anule la selección de **iniciar el proceso de sincronización de Hola...** *.</span><span class="sxs-lookup"><span data-stu-id="f8197-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="f8197-120">A continuación, vuelva a ejecutar el Asistente para la instalación de Hola y cambie las unidades organizativas de hello en [opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) y habilitar la sincronización programada.</span><span class="sxs-lookup"><span data-stu-id="f8197-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="f8197-121">Desea tooenable una de las características de hello en Azure AD Premium, como la escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="f8197-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="f8197-122">En primer lugar, vaya a través de la instalación inicial de tooget express Hola completada.</span><span class="sxs-lookup"><span data-stu-id="f8197-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="f8197-123">A continuación, vuelva a ejecutar el Asistente para la instalación de Hola y cambiar hello [opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="f8197-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="f8197-124">Personalizado</span><span class="sxs-lookup"><span data-stu-id="f8197-124">Custom</span></span>
<span data-ttu-id="f8197-125">ruta de acceso personalizada Hello permite muchas más opciones que la versión express.</span><span class="sxs-lookup"><span data-stu-id="f8197-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="f8197-126">Se debe usar en todos los casos donde la configuración de hello descrito en la sección anterior para express no es representativo de su organización.</span><span class="sxs-lookup"><span data-stu-id="f8197-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="f8197-127">Se debe utilizar si:</span><span class="sxs-lookup"><span data-stu-id="f8197-127">Use when:</span></span>

- <span data-ttu-id="f8197-128">No tiene cuenta de administrador de empresa de tooan de acceso en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f8197-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="f8197-129">Tiene más de un bosque o piensa toosynchronize más de un bosque en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="f8197-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="f8197-130">Tiene dominios en el bosque no es accesible desde el servidor de Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8197-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="f8197-131">Planear la federación toouse o la autenticación de paso a través para el inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="f8197-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="f8197-132">Tiene más de 100.000 objetos y necesita toouse una versión completa de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8197-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="f8197-133">Planee toouse basado en el grupo filtrado y no solo dominio o filtrado basado en la unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="f8197-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="f8197-134">Actualización desde DirSync</span><span class="sxs-lookup"><span data-stu-id="f8197-134">Upgrade from DirSync</span></span>
<span data-ttu-id="f8197-135">Si actualmente utilizas DirSync, a continuación, siga los pasos de hello en [actualizar desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="f8197-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="f8197-136">Hay dos opciones de actualización distintas:</span><span class="sxs-lookup"><span data-stu-id="f8197-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="f8197-137">Conectar tooinstall de actualización en contexto en hello mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="f8197-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="f8197-138">Paralelo implementación tooinstall Connect en un nuevo servidor mientras servidor de sincronización de directorios existente de hello es sigue funcionando.</span><span class="sxs-lookup"><span data-stu-id="f8197-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="f8197-139">Actualización desde Sincronización de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8197-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="f8197-140">Si actualmente utilizas Azure AD Sync, puede seguir hello [mismos pasos](active-directory-aadconnect-upgrade-previous-version.md) como al actualizar desde una versión tooa de conectar más reciente.</span><span class="sxs-lookup"><span data-stu-id="f8197-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="f8197-141">Hay dos opciones de actualización distintas:</span><span class="sxs-lookup"><span data-stu-id="f8197-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="f8197-142">Conectar tooinstall de actualización en contexto en hello mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="f8197-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="f8197-143">Migración swing tooinstall Connect en un servidor nuevo al servidor de sincronización de Azure AD existente hello es sigue funcionando.</span><span class="sxs-lookup"><span data-stu-id="f8197-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="f8197-144">Migración desde FIM2010 o MIM2016</span><span class="sxs-lookup"><span data-stu-id="f8197-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="f8197-145">Si actualmente utilizas Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con hello conector de Azure AD, la única opción es una migración.</span><span class="sxs-lookup"><span data-stu-id="f8197-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="f8197-146">Siga los pasos de hello descritos en [swing migración](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="f8197-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="f8197-147">En los pasos de hello, reemplace cualquier mención de Azure AD Sync con FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="f8197-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8197-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8197-148">Next steps</span></span>
<span data-ttu-id="f8197-149">Dependiendo de la opción de Hola que ha seleccionado toouse, utilice Hola tabla de contenido toohello izquierdo toofind el artículo con hello pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="f8197-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
