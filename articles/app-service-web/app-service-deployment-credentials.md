---
title: "Credenciales de implementación de Azure App Service | Microsoft Docs"
description: "Aprenda a usar las credenciales de implementación de Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="83a10-103">Configuración de credenciales de implementación para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="83a10-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="83a10-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) admite dos tipos de credenciales para la [implementación de GIT local](app-service-deploy-local-git.md) y la [implementación FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="83a10-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="83a10-105">Estas credenciales no son las mismas que las de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83a10-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="83a10-106">**Credenciales de nivel de usuario**: un conjunto de credenciales para toda la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="83a10-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="83a10-107">Se puede utilizar para implementar App Service en cualquier aplicación o suscripción para la que la cuenta de Azure tenga permiso de acceso.</span><span class="sxs-lookup"><span data-stu-id="83a10-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="83a10-108">Este es el conjunto de credenciales predeterminado que se configura en **App Services** > **&lt;nombre_aplicación>** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="83a10-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="83a10-109">Este es también el conjunto predeterminado que aparece en la interfaz gráfica de usuario del portal (como la **Información general** y las **Propiedades** de la [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="83a10-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="83a10-110">Al delegar el acceso a recursos de Azure a través del control de acceso basado en rol (RBAC) o de permisos de coadministrador, cada usuario de Azure que recibe acceso a una aplicación puede usar sus credenciales de nivel de usuario personales hasta que se revoca el acceso.</span><span class="sxs-lookup"><span data-stu-id="83a10-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="83a10-111">Estas credenciales de implementación no deben compartirse con otros usuarios de Azure.</span><span class="sxs-lookup"><span data-stu-id="83a10-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="83a10-112">**Credenciales de nivel de aplicación**: un conjunto de credenciales para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="83a10-113">Se puede utilizar para implementar únicamente en esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="83a10-114">Las credenciales para cada aplicación se generan automáticamente al crear la aplicación y se encuentran en el perfil de publicación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="83a10-115">Las credenciales no se pueden configurar manualmente, pero se pueden restablecer para una aplicación en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="83a10-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="83a10-116">Para dar a alguien acceso a estas credenciales a través de Control de acceso basado en roles (RBAC), es preciso convertirlo en colaborador, o cualquier rol superior, en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="83a10-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="83a10-117">A los lectores no se les permite publicar, por lo que no pueden acceder a dichas credenciales.</span><span class="sxs-lookup"><span data-stu-id="83a10-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="83a10-118"><a name="userscope"></a>Establecimiento y restablecimiento de credenciales de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="83a10-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="83a10-119">Puede configurar las credenciales de nivel de usuario en cualquier [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="83a10-120">Independientemente de en qué aplicación configure estas credenciales, son válidas para todas las aplicaciones y para todas las suscripciones de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="83a10-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="83a10-121">Para configurar las credenciales de nivel de usuario:</span><span class="sxs-lookup"><span data-stu-id="83a10-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="83a10-122">En [Azure Portal](https://portal.azure.com), haga clic en App Service > **&lt;cualquier_aplicación >** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="83a10-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="83a10-123">En el portal, debe tener al menos una aplicación para tener acceso a la hoja de credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="83a10-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="83a10-124">Sin embargo, con la [CLI de Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), puede configurar las credenciales de nivel de usuario sin tener ninguna aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="83a10-125">Configure el nombre de usuario y la contraseña y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83a10-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="83a10-126">Una vez que haya configurado las credenciales de implementación, puede encontrar el nombre de usuario de implementación de *Git* en la **Información general** de la aplicación</span><span class="sxs-lookup"><span data-stu-id="83a10-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="83a10-127">y el nombre de usuario de implementación de *FTP* en las **Propiedades** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="83a10-128">Azure no muestra la contraseña de la implementación de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="83a10-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="83a10-129">Si olvida la contraseña, no podrá recuperarla.</span><span class="sxs-lookup"><span data-stu-id="83a10-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="83a10-130">Sin embargo, podrá restablecer las credenciales siguiendo los pasos descritos en esta sección.</span><span class="sxs-lookup"><span data-stu-id="83a10-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="83a10-131"><a name="appscope"></a>Obtención y restablecimiento de las credenciales de nivel de aplicación</span><span class="sxs-lookup"><span data-stu-id="83a10-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="83a10-132">Para cada aplicación de App Service, sus credenciales de nivel de aplicación se almacenan en el perfil de publicación XML.</span><span class="sxs-lookup"><span data-stu-id="83a10-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="83a10-133">Para obtener las credenciales de nivel de aplicación:</span><span class="sxs-lookup"><span data-stu-id="83a10-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="83a10-134">En [Azure Portal](https://portal.azure.com), haga clic en App Service > **&lt;cualquier_aplicación >** > **Información general**.</span><span class="sxs-lookup"><span data-stu-id="83a10-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="83a10-135">Haga clic en **... Más** > **Obtener perfil de publicación** para que comience la descarga de un archivo .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="83a10-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="83a10-136">Abra el archivo .PublishSettings y busque la etiqueta `<publishProfile>` con el atributo `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="83a10-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="83a10-137">A continuación, obtenga sus atributos `userName` y `password`.</span><span class="sxs-lookup"><span data-stu-id="83a10-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="83a10-138">Estas son las credenciales de nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="83a10-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="83a10-139">De manera similar a las credenciales de nivel de usuario, el nombre de usuario de implementación FTP se encuentra en el formato de `<app_name>\<username>`, y el nombre de usuario de implementación de GIT es simplemente `<username>` sin la parte `<app_name>\` del principio.</span><span class="sxs-lookup"><span data-stu-id="83a10-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="83a10-140">Para restablecer las credenciales de nivel de aplicación:</span><span class="sxs-lookup"><span data-stu-id="83a10-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="83a10-141">En [Azure Portal](https://portal.azure.com), haga clic en App Service > **&lt;cualquier_aplicación >** > **Información general**.</span><span class="sxs-lookup"><span data-stu-id="83a10-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="83a10-142">Haga clic en **... Más** > **Restablecer perfil de publicación**.</span><span class="sxs-lookup"><span data-stu-id="83a10-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="83a10-143">Haga clic en **SÍ** para confirmar el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="83a10-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="83a10-144">La acción de restablecimiento invalida cualquier archivo .PublishSettings anteriormente descargado.</span><span class="sxs-lookup"><span data-stu-id="83a10-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83a10-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="83a10-145">Next steps</span></span>

<span data-ttu-id="83a10-146">Obtenga información sobre cómo usar estas credenciales para implementar la aplicación desde [GIT local](app-service-deploy-local-git.md) o con [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="83a10-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
