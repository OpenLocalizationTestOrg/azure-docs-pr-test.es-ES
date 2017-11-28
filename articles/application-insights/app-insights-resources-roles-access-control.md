---
title: aaaResources, roles y control de acceso en Azure Application Insights | Documentos de Microsoft
description: "Propietarios, colaboradores y lectores de las perspectivas de su organización."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="d5264-103">Recursos, roles y control de acceso en Application Insights</span><span class="sxs-lookup"><span data-stu-id="d5264-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="d5264-104">Puede controlar quién ha leído y actualizar tooyour acceder a los datos en Azure [Application Insights][start], mediante el uso de [control de acceso basado en roles en Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5264-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5264-105">Asignar acceso toousers Hola **grupo de recursos o suscripción** toowhich pertenece el recurso de aplicación - no está en el propio recurso Hola.</span><span class="sxs-lookup"><span data-stu-id="d5264-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="d5264-106">Asignar Hola **colaborador de componente de Application Insights** rol.</span><span class="sxs-lookup"><span data-stu-id="d5264-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="d5264-107">Esto garantiza uniforme control de acceso tooweb pruebas y las alertas junto con el recurso de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5264-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="d5264-108">[Más información](#access).</span><span class="sxs-lookup"><span data-stu-id="d5264-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="d5264-109">Recursos, grupos y suscripciones</span><span class="sxs-lookup"><span data-stu-id="d5264-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="d5264-110">En primer lugar, vamos a ver algunas definiciones:</span><span class="sxs-lookup"><span data-stu-id="d5264-110">First, some definitions:</span></span>

* <span data-ttu-id="d5264-111">**Recurso** : una instancia de un servicio de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d5264-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="d5264-112">El recurso de Application Insights recopila, analiza y muestra los datos de telemetría de hello enviados desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5264-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="d5264-113">Otros tipos de recursos de Azure son aplicaciones web, bases de datos y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d5264-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="d5264-114">toosee sus recursos, abra hello [Portal de Azure][portal], inicie sesión y haga clic en todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d5264-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="d5264-115">toofind un recurso, tipo de parte de su nombre en el campo de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5264-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Enumeración de los recursos de Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="d5264-117">[**Grupo de recursos** ] [ group] -tooone grupo pertenece de cada recurso.</span><span class="sxs-lookup"><span data-stu-id="d5264-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="d5264-118">Un grupo es una práctica manera toomanage relacionados con recursos, especialmente para el control de acceso.</span><span class="sxs-lookup"><span data-stu-id="d5264-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="d5264-119">Por ejemplo, en un recurso de grupo podría poner una aplicación Web, una aplicación de Application Insights recursos toomonitor hello y una tookeep de recursos de almacenamiento exporta datos.</span><span class="sxs-lookup"><span data-stu-id="d5264-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Elija Examinar, Grupos de recursos, y luego elija un grupo.](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="d5264-121">[**Suscripción** ](https://manage.windowsazure.com) -toouse Application Insights u otros recursos de Azure, inicie sesión en tooan suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5264-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="d5264-122">Cada grupo de recursos pertenece tooone suscripción de Azure, donde puede seleccionar el paquete de precios y, si es una suscripción de la organización, elegir los miembros de Hola y sus permisos de acceso.</span><span class="sxs-lookup"><span data-stu-id="d5264-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="d5264-123">[**Cuenta de Microsoft** ] [ account] -Hola nombre de usuario y la contraseña que usa toosign en tooMicrosoft Azure suscripciones, XBox Live, Outlook.com y otros servicios de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5264-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="d5264-124"><a name="access"></a>Controlar el acceso en el grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="d5264-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="d5264-125">Es importante toounderstand que en recursos de toohello de suma que creó para la aplicación, hay también separar recursos ocultos para las alertas y las pruebas web.</span><span class="sxs-lookup"><span data-stu-id="d5264-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="d5264-126">Únicamente son toohello adjunto mismo [grupo de recursos](#resource-group) que la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5264-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="d5264-127">También podría haber colocado ahí otros servicios de Azure, como sitios web o almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d5264-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Recursos en Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="d5264-129">toocontrol tener acceso a recursos de toothese, por tanto, se recomienda:</span><span class="sxs-lookup"><span data-stu-id="d5264-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="d5264-130">Controlar el acceso en hello **grupo de recursos o suscripción** nivel.</span><span class="sxs-lookup"><span data-stu-id="d5264-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="d5264-131">Asignar Hola **colaborador de componente de aplicación visión** toousers de rol.</span><span class="sxs-lookup"><span data-stu-id="d5264-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="d5264-132">Esto les permite tooedit las pruebas web, alertas y recursos de Application Insights, sin proporcionar acceso tooany otros servicios de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5264-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="d5264-133">tooprovide acceso tooanother usuario</span><span class="sxs-lookup"><span data-stu-id="d5264-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="d5264-134">Debe tener la suscripción de toohello de derechos de propietario o grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5264-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="d5264-135">Hola usuario debe tener un [Account Microsoft][account], u obtener acceso a tootheir [Account Microsoft profesional](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d5264-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="d5264-136">Puede proporcionar acceso tooindividuals y también los grupos de toouser definidos en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5264-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="d5264-137">Navegar por el grupo de recursos de toohello</span><span class="sxs-lookup"><span data-stu-id="d5264-137">Navigate toohello resource group</span></span>
<span data-ttu-id="d5264-138">Agregar usuario de hello no existe.</span><span class="sxs-lookup"><span data-stu-id="d5264-138">Add hello user there.</span></span>

![En la hoja de recursos de la aplicación, abra Essentials, abrir el grupo de recursos de Hola y seleccionar Configuración/usuarios.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="d5264-141">O bien, puede ascender a otro nivel y agregar Hola usuario toohello suscripción.</span><span class="sxs-lookup"><span data-stu-id="d5264-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="d5264-142">Seleccione un rol.</span><span class="sxs-lookup"><span data-stu-id="d5264-142">Select a role</span></span>
![Seleccione un rol de usuario nuevo de Hola](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="d5264-144">Rol</span><span class="sxs-lookup"><span data-stu-id="d5264-144">Role</span></span> | <span data-ttu-id="d5264-145">En el grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="d5264-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="d5264-146">Propietario</span><span class="sxs-lookup"><span data-stu-id="d5264-146">Owner</span></span> |<span data-ttu-id="d5264-147">Puede cambiar cualquier cosa, incluido el acceso de usuario.</span><span class="sxs-lookup"><span data-stu-id="d5264-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="d5264-148">Colaborador</span><span class="sxs-lookup"><span data-stu-id="d5264-148">Contributor</span></span> |<span data-ttu-id="d5264-149">Puede editar cualquier cosa, incluidos todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d5264-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="d5264-150">colaborador de componentes de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d5264-150">Application Insights Component contributor</span></span> |<span data-ttu-id="d5264-151">Puede editar alertas, pruebas web y recursos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d5264-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="d5264-152">Lector</span><span class="sxs-lookup"><span data-stu-id="d5264-152">Reader</span></span> |<span data-ttu-id="d5264-153">Puede ver, pero no puede cambiar nada.</span><span class="sxs-lookup"><span data-stu-id="d5264-153">Can view but not change anything</span></span> |

<span data-ttu-id="d5264-154">La "edición" incluye la creación, la eliminación y la actualización:</span><span class="sxs-lookup"><span data-stu-id="d5264-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="d5264-155">Recursos</span><span class="sxs-lookup"><span data-stu-id="d5264-155">Resources</span></span>
* <span data-ttu-id="d5264-156">Pruebas web</span><span class="sxs-lookup"><span data-stu-id="d5264-156">Web tests</span></span>
* <span data-ttu-id="d5264-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="d5264-157">Alerts</span></span>
* <span data-ttu-id="d5264-158">Exportación continua</span><span class="sxs-lookup"><span data-stu-id="d5264-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="d5264-159">Seleccione usuario Hola</span><span class="sxs-lookup"><span data-stu-id="d5264-159">Select hello user</span></span>

<span data-ttu-id="d5264-160">Si el usuario Hola que desea no está en el directorio de hello, puede invitar a cualquier persona con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5264-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="d5264-161">(Si se usan servicios como Outlook.com, OneDrive, Windows Phone o XBox Live, se tiene una cuenta Microsoft).</span><span class="sxs-lookup"><span data-stu-id="d5264-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="d5264-162">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="d5264-162">Related content</span></span>

* [<span data-ttu-id="d5264-163">Control de acceso basado en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="d5264-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
