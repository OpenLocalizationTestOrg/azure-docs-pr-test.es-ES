---
title: "Azure AD Connect: selección del tipo de instalación | Microsoft Docs"
description: "En este tema se explica cómo seleccionar el tipo de instalación que se usará para Azure AD Connect."
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="3b2dd-103">Selección del tipo de instalación que se usará para Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3b2dd-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="3b2dd-104">Azure AD Connect tiene dos tipos de instalación para la nueva instalación: rápida y personalizada.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="3b2dd-105">Este tema le ayudará a decidir qué opción utilizar durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="3b2dd-106">Express</span><span class="sxs-lookup"><span data-stu-id="3b2dd-106">Express</span></span>
<span data-ttu-id="3b2dd-107">La opción rápida es la más común y la utiliza el 90 % de todas las instalaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="3b2dd-108">Se diseñó para proporcionar una configuración que sirva para los escenarios más comunes de clientes.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="3b2dd-109">Se da por supuesto que:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-109">It assumes:</span></span>

- <span data-ttu-id="3b2dd-110">Tiene un único bosque de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="3b2dd-111">Tiene una cuenta de administrador de organización que usa para la instalación.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="3b2dd-112">Tiene menos de 100 000 objetos en Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="3b2dd-113">Obtendrá:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-113">You get:</span></span>

- <span data-ttu-id="3b2dd-114">[Sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md) desde entornos locales en Azure AD para inicios de sesión únicos.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="3b2dd-115">Una configuración que sincroniza a los [usuarios, grupos, contactos y equipos de Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="3b2dd-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="3b2dd-116">Sincronización de todos los objetos válidos en todos los dominios y todas las unidades organizativas.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="3b2dd-117">La [actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) está habilitada para asegurarse de que se utilice siempre la última versión disponible.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="3b2dd-118">Opciones en las que puede continuar utilizando la instalación rápida:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="3b2dd-119">Si no desea sincronizar todas las unidades organizativas, puede usar la instalación rápida y, en la última página, anule la selección de **Inicie el proceso de sincronización...***.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="3b2dd-120">Después, vuelva a ejecutar el Asistente para instalación y cambie las unidades organizativas en [Opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) y habilite la sincronización programada.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="3b2dd-121">Desea habilitar una de las características de Azure AD Premium, como la Escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="3b2dd-122">Utilice primero la instalación rápida para completar la instalación inicial.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="3b2dd-123">Después, vuelva a ejecutar el Asistente para instalación y cambie las [opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="3b2dd-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="3b2dd-124">Personalizado</span><span class="sxs-lookup"><span data-stu-id="3b2dd-124">Custom</span></span>
<span data-ttu-id="3b2dd-125">La ruta de acceso personalizada admite muchas más opciones que la instalación rápida.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="3b2dd-126">Se debe usar en todos los casos donde la configuración descrita en la sección anterior para la instalación rápida no es representativa para su organización.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="3b2dd-127">Se debe utilizar si:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-127">Use when:</span></span>

- <span data-ttu-id="3b2dd-128">No tiene acceso a una cuenta de administrador de empresa en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="3b2dd-129">Tiene más de un bosque o pretende sincronizar más de un bosque en el futuro.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="3b2dd-130">Tiene dominios en el bosque a los que no se puede acceder desde el servidor de Connect.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="3b2dd-131">Planea utilizar la federación o la autenticación de paso a través para el inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="3b2dd-132">Tiene más de 100 000 objetos y necesita utilizar una versión completa de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="3b2dd-133">Planea usar el filtrado basado en grupos y no solo el filtrado basado en dominios o en unidades organizativas.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="3b2dd-134">Actualización desde DirSync</span><span class="sxs-lookup"><span data-stu-id="3b2dd-134">Upgrade from DirSync</span></span>
<span data-ttu-id="3b2dd-135">Si actualmente utiliza DirSync, siga los pasos descritos en [Actualización desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) para actualizar la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="3b2dd-136">Hay dos opciones de actualización distintas:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="3b2dd-137">Actualización local para instalar Connect en el mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="3b2dd-138">Implementación paralela para instalar Connect en un servidor nuevo mientras el servidor existente de DirSync continúa operativo.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="3b2dd-139">Actualización desde Sincronización de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b2dd-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="3b2dd-140">Si actualmente utiliza Sincronización de Azure AD, puede seguir los [mismos pasos](active-directory-aadconnect-upgrade-previous-version.md) que cuando se actualiza desde una versión de Connect a otra más reciente.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="3b2dd-141">Hay dos opciones de actualización distintas:</span><span class="sxs-lookup"><span data-stu-id="3b2dd-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="3b2dd-142">Actualización local para instalar Connect en el mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="3b2dd-143">Migración oscilante para instalar Connect en un servidor nuevo mientras el servidor existente de Sincronización de Azure AD continúa operativo.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="3b2dd-144">Migración desde FIM2010 o MIM2016</span><span class="sxs-lookup"><span data-stu-id="3b2dd-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="3b2dd-145">Si actualmente utiliza Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con el conector de Azure AD, la única opción es una migración.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="3b2dd-146">Siga los pasos descritos en [migración oscilante](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="3b2dd-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="3b2dd-147">En los pasos, reemplace cualquier mención de Sincronización de Azure AD con FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b2dd-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b2dd-148">Next steps</span></span>
<span data-ttu-id="3b2dd-149">Dependiendo de la opción seleccionada, use la tabla de contenido a la izquierda para encontrar su artículo con los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="3b2dd-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
