---
title: "Administración de roles en servicios en la nube de Azure con Visual Studio | Microsoft Docs"
description: "Obtenga información sobre cómo agregar y quitar roles en los servicios en la nube de Azure con Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="b0fdf-103">Administración de roles en servicios en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0fdf-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="b0fdf-104">Una vez creado el servicio en la nube de Azure, puede agregarle nuevos roles o quitarle roles existentes.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="b0fdf-105">También puede importar un proyecto existente y convertirlo en un rol.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="b0fdf-106">Por ejemplo, puede importar una aplicación web ASP.NET y designarla como rol web.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="b0fdf-107">Incorporación de un rol a un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="b0fdf-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="b0fdf-108">Los pasos siguientes le explican cómo agregar un rol web o un rol de trabajo a un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b0fdf-109">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b0fdf-110">En el **Explorador de soluciones**, expanda el nodo del proyecto</span><span class="sxs-lookup"><span data-stu-id="b0fdf-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="b0fdf-111">Haga clic con el botón derecho en el nodo **Roles** para ver el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="b0fdf-112">En el menú contextual, seleccione **Agregar** y, luego, seleccione un rol web o un rol de trabajo existente en la solución actual o cree un proyecto de rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="b0fdf-113">También puede seleccionar un proyecto adecuado, por ejemplo, un proyecto de aplicación web ASP.NET, y asociarlo a un proyecto de rol.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Opciones de menú para agregar un rol a un proyecto de servicio en la nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="b0fdf-115">Eliminación de un rol de un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="b0fdf-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="b0fdf-116">Los pasos siguientes le explican cómo quitar un rol web o un rol de trabajo de un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b0fdf-117">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="b0fdf-118">En el **Explorador de soluciones**, expanda el nodo del proyecto</span><span class="sxs-lookup"><span data-stu-id="b0fdf-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="b0fdf-119">Expanda el nodo **Roles**.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="b0fdf-120">Haga clic con el botón derecho en el nodo que desea quitar y, en el menú contextual, seleccione **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![Opciones de menú para agregar un rol a un servicio en la nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="b0fdf-122">Nueva incorporación de un rol a un proyecto de servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="b0fdf-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="b0fdf-123">Si quita un rol del proyecto de servicio en la nube pero posteriormente decide volver a agregarlo al proyecto, solo se agregarán la declaración del rol y los atributos básicos como, por ejemplo, los extremos y la información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="b0fdf-124">No se agrega ningún recurso o referencia adicional al archivo `ServiceDefinition.csdef` ni al archivo `ServiceConfiguration.cscfg`.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="b0fdf-125">Si quiere agregar esta información, tiene que volver a agregarla manualmente en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="b0fdf-126">Por ejemplo, es posible que quite un rol de servicio web y más adelante decida agregarlo de nuevo a la solución.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="b0fdf-127">Si lo hace, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-127">If you do this, an error occurs.</span></span> <span data-ttu-id="b0fdf-128">Para evitar este error, tiene que agregar de nuevo el elemento `<LocalResources>` que se muestra en el siguiente código XML al archivo `ServiceDefinition.csdef`.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="b0fdf-129">Use el nombre del rol de servicio web que volvió a agregar al proyecto como parte del nombre del atributo para el elemento **<LocalStorage>** .</span><span class="sxs-lookup"><span data-stu-id="b0fdf-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="b0fdf-130">En este ejemplo el nombre del rol de servicio web es **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="b0fdf-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="b0fdf-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0fdf-131">Next steps</span></span>
- [<span data-ttu-id="b0fdf-132">Configuración de los roles para un servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0fdf-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
