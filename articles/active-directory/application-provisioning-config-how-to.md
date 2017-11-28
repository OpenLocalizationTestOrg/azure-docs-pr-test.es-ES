---
title: "Configuración del aprovisionamiento de usuarios en una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Cómo configurar rápidamente el aprovisionamiento y desaprovisionamiento completos de cuentas de usuario para aplicaciones que ya aparecen en la galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="0d36e-103">Configuración del aprovisionamiento de usuarios en una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d36e-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="0d36e-104">El *aprovisionamiento de cuentas de usuario* es el acto de crear, actualizar o deshabilitar registros de cuenta de usuario en el almacén de perfiles de usuario local de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="0d36e-105">La mayoría de las aplicaciones SaaS y en la nube almacenan el rol y los permisos de los usuarios en su propio almacén local de perfiles de usuario, y la presencia de tal registro de usuario en su almacén local es *necesaria* para que funcionen el inicio de sesión único y el acceso.</span><span class="sxs-lookup"><span data-stu-id="0d36e-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="0d36e-106">En Azure Portal, en la pestaña **Aprovisionamiento** del panel de navegación izquierdo para una aplicación empresarial, se muestran los modos de aprovisionamiento admitidos para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="0d36e-107">Puede ser uno de dos valores:</span><span class="sxs-lookup"><span data-stu-id="0d36e-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="0d36e-108">Configuración de una aplicación para el aprovisionamiento manual</span><span class="sxs-lookup"><span data-stu-id="0d36e-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="0d36e-109">El aprovisionamiento *manual* quiere decir que las cuentas de usuario se deben crear manualmente mediante los métodos proporcionados por esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="0d36e-110">Esto podría suponer iniciar sesión en un portal administrativo para esa aplicación y agregar usuarios mediante una interfaz de usuario basada en Web.</span><span class="sxs-lookup"><span data-stu-id="0d36e-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="0d36e-111">O bien, podría tener que cargar una hoja de cálculo con los detalles de las cuentas de usuario, mediante un mecanismo proporcionado por esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="0d36e-112">Consulte la documentación suministrada por la aplicación o póngase en contacto con su desarrollador para determinar qué mecanismos hay disponibles.</span><span class="sxs-lookup"><span data-stu-id="0d36e-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="0d36e-113">Si Manual es el único modo que se muestra para una aplicación determinada, significa que aún no se ha creado ningún conector de aprovisionamiento de Azure AD automático para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="0d36e-114">O bien, significa que la aplicación no es compatible con la API de administración de usuarios obligatoria sobre la que se crea un conector de aprovisionamiento automatizado.</span><span class="sxs-lookup"><span data-stu-id="0d36e-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="0d36e-115">Si desea solicitar soporte técnico para el aprovisionamiento automático con una aplicación determinada, puede rellenar una solicitud en <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="0d36e-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="0d36e-116">Configuración de una aplicación para el aprovisionamiento automático</span><span class="sxs-lookup"><span data-stu-id="0d36e-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="0d36e-117">*Automático* significa que se ha desarrollado un conector de aprovisionamiento de Azure AD para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="0d36e-118">Para más información sobre el servicio de aprovisionamiento de Azure AD y cómo funciona, consulte [Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="0d36e-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="0d36e-119">Para más información sobre cómo aprovisionar usuarios y grupos específicos en una aplicación, consulte [Administración del aprovisionamiento de cuentas de usuario para aplicaciones empresariales](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="0d36e-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="0d36e-120">Los pasos que son necesarios para habilitar y configurar el aprovisionamiento automático varían según la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="0d36e-121">Para empezar, debería buscar el tutorial de configuración específico para configurar el aprovisionamiento para su aplicación y seguir esos pasos para configurar la aplicación y Azure AD para crear la conexión de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="0d36e-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="0d36e-122">Puede encontrar tutoriales sobre aplicaciones en [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="0d36e-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="0d36e-123">Una cuestión importante que tener en cuenta al configurar el aprovisionamiento es revisar y configurar las asignaciones de atributos y los flujos de trabajo que definen qué propiedades de usuario (o de grupo) fluyen de Azure AD a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d36e-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="0d36e-124">Esto incluye la configuración de la "propiedad de coincidencia" que se usa para identificar de forma exclusiva y emparejar a usuarios y grupos entre ambos sistemas.</span><span class="sxs-lookup"><span data-stu-id="0d36e-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="0d36e-125">Para más información acerca de este proceso importante.</span><span class="sxs-lookup"><span data-stu-id="0d36e-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d36e-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d36e-126">Next steps</span></span>
[<span data-ttu-id="0d36e-127">Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios</span><span class="sxs-lookup"><span data-stu-id="0d36e-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

