---
title: "Credenciales de implementación del servicio de aplicación aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola credenciales de implementación de servicio de aplicaciones de Azure."
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
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="9b2a1-103">Configuración de credenciales de implementación para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9b2a1-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="9b2a1-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) admite dos tipos de credenciales para la [implementación de GIT local](app-service-deploy-local-git.md) y la [implementación FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="9b2a1-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="9b2a1-105">Estos son no Hola igual que sus credenciales de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="9b2a1-106">**Las credenciales de nivel de usuario**: un conjunto de credenciales de cuenta de Azure completo Hola.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="9b2a1-107">Puede ser usado toodeploy tooApp servicio para cualquier aplicación en una suscripción que Hola cuenta de Azure tiene permiso tooaccess.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="9b2a1-108">Se trata de conjunto de credenciales de hello predeterminado que se configura en **servicios de aplicaciones** > **&lt;app_name >** > **decredencialesdeimplementación**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="9b2a1-109">Esto también es Hola conjunto predeterminado que aparece en el portal de hello interfaz gráfica de usuario (como hello **Introducción** y **propiedades** de la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="9b2a1-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b2a1-110">Al delegar el acceso a los recursos a través de Control de acceso basado en roles (RBAC) o los permisos de Coadministrador tooAzure, cada usuario de Azure que recibe acceso tooan aplicación puede usar sus credenciales de nivel de usuario personales hasta que se revoca el acceso.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="9b2a1-111">Estas credenciales de implementación no deben compartirse con otros usuarios de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="9b2a1-112">**Credenciales de nivel de aplicación**: un conjunto de credenciales para cada aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="9b2a1-113">Puede ser usado toodeploy toothat solo aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="9b2a1-114">las credenciales de Hola para cada aplicación se genera automáticamente al crear la aplicación y se encuentra en la aplicación hello perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="9b2a1-115">No se puede configurar manualmente las credenciales de hello, pero puede restablecerlas para una aplicación en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b2a1-116">En orden toogive a alguien acceso credenciales toothese a través de Control de acceso de en función de roles (RBAC), deberá toomake ellos colaborador o superior en hello Web App.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="9b2a1-117">Los lectores no se permiten toopublish y, por tanto, no pueden tener acceso a esas credenciales.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="9b2a1-118"><a name="userscope"></a>Establecimiento y restablecimiento de credenciales de nivel de usuario</span><span class="sxs-lookup"><span data-stu-id="9b2a1-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="9b2a1-119">Puede configurar las credenciales de nivel de usuario en cualquier [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="9b2a1-120">Independientemente de qué aplicación configurar estas credenciales, aplica tooall aplicaciones y para todas las suscripciones de Azure de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="9b2a1-121">tooconfigure sus credenciales de nivel de usuario:</span><span class="sxs-lookup"><span data-stu-id="9b2a1-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="9b2a1-122">Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **las credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b2a1-123">En el portal de hello, debe tener al menos una aplicación antes de que se puede tener acceso a la hoja de credenciales de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="9b2a1-124">Sin embargo, con hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), puede configurar las credenciales de nivel de usuario sin una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="9b2a1-125">Configurar el nombre de usuario de Hola y la contraseña y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="9b2a1-126">Una vez haya configurado las credenciales de implementación, puede encontrar Hola *Git* nombre de usuario de implementación de la aplicación **Introducción**,</span><span class="sxs-lookup"><span data-stu-id="9b2a1-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="9b2a1-127">y el nombre de usuario de implementación de *FTP* en las **Propiedades** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="9b2a1-128">Azure no muestra la contraseña de la implementación de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="9b2a1-129">Si olvida la contraseña de hello, no podrá recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="9b2a1-130">Sin embargo, puede restablecer las credenciales siguiendo los pasos de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="9b2a1-131"><a name="appscope"></a>Obtención y restablecimiento de las credenciales de nivel de aplicación</span><span class="sxs-lookup"><span data-stu-id="9b2a1-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="9b2a1-132">Para cada aplicación de servicio de aplicaciones, sus credenciales de nivel de aplicación se almacenan en hello perfil de publicación de XML.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="9b2a1-133">credenciales de nivel de aplicación de Hola tooget:</span><span class="sxs-lookup"><span data-stu-id="9b2a1-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="9b2a1-134">Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="9b2a1-135">Haga clic en **... Más** > **Obtener perfil de publicación** para que comience la descarga de un archivo .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="9b2a1-136">Hola abierto. Archivo de configuración de publicación y encontrar Hola `<publishProfile>` etiqueta con hello atributo `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="9b2a1-137">A continuación, obtenga sus atributos `userName` y `password`.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="9b2a1-138">Estas son las credenciales de nivel de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="9b2a1-139">Credenciales de nivel de usuario toohello similar, nombre de usuario de implementación de hello FTP está en formato de Hola de `<app_name>\<username>`, y es el nombre de usuario de hello Git implementación `<username>` sin Hola anterior `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="9b2a1-140">credenciales de nivel de aplicación de Hola tooreset:</span><span class="sxs-lookup"><span data-stu-id="9b2a1-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="9b2a1-141">Hola [portal de Azure](https://portal.azure.com), haga clic en el servicio de aplicaciones >  **&lt;any_app >** > **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="9b2a1-142">Haga clic en **... Más** > **Restablecer perfil de publicación**.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="9b2a1-143">Haga clic en **Sí** tooconfirm Hola restablece.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="9b2a1-144">acción de restablecimiento de Hello invalida cualquier descargados anteriormente. Archivos de configuración de publicación.</span><span class="sxs-lookup"><span data-stu-id="9b2a1-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b2a1-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b2a1-145">Next steps</span></span>

<span data-ttu-id="9b2a1-146">Obtener información sobre cómo toouse estas credenciales toodeploy la aplicación de [Git local](app-service-deploy-local-git.md) o con [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="9b2a1-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
