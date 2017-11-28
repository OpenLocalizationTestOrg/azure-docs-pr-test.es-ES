---
title: servicios con Visual Studio en la nube aaaManaging roles de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd y quitar roles de Azure servicios en la nube con Visual Studio."
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
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="1838f-103">Administración de roles en servicios en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1838f-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="1838f-104">Después de haber creado su servicio de nube de Azure, puede agregar nuevos tooit de roles o quitar roles.</span><span class="sxs-lookup"><span data-stu-id="1838f-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="1838f-105">También puede importar un proyecto existente y convertirlo tooa rol.</span><span class="sxs-lookup"><span data-stu-id="1838f-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="1838f-106">Por ejemplo, puede importar una aplicación web ASP.NET y designarla como rol web.</span><span class="sxs-lookup"><span data-stu-id="1838f-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="1838f-107">Agregar un tooan de rol Servicio de nube de Azure</span><span class="sxs-lookup"><span data-stu-id="1838f-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="1838f-108">Hola pasos le guiarán por agregar un proyecto web o trabajo rol tooan nube de Azure servicio en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1838f-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1838f-109">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1838f-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1838f-110">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="1838f-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="1838f-111">Menú contextual hello **Roles** menú contextual del nodo toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="1838f-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="1838f-112">En el menú contextual de hello, seleccione **agregar**, a continuación, seleccione un rol web existente o un rol de trabajo de la solución actual de Hola o crear un proyecto de rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1838f-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="1838f-113">También puede seleccionar un proyecto adecuado, por ejemplo, un proyecto de aplicación web ASP.NET, y asociarlo a un proyecto de rol.</span><span class="sxs-lookup"><span data-stu-id="1838f-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Opciones de menú tooadd un proyecto de servicio de rol tooan nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="1838f-115">Eliminación de un rol de un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="1838f-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="1838f-116">Hello siguientes pasos le guiarán quitar un rol web o de trabajo de un proyecto de servicio de nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1838f-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1838f-117">Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1838f-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1838f-118">En **el Explorador de soluciones**, expanda el nodo del proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="1838f-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="1838f-119">Expanda hello **Roles** nodo.</span><span class="sxs-lookup"><span data-stu-id="1838f-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="1838f-120">Menú contextual nodo de hello desea tooremove y, en el menú contextual de hello, seleccione **quitar**.</span><span class="sxs-lookup"><span data-stu-id="1838f-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Opciones de menú tooadd un tooan de rol Servicio de nube de Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="1838f-122">Volver a agregar un proyecto de servicio de rol tooan nube de Azure</span><span class="sxs-lookup"><span data-stu-id="1838f-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="1838f-123">Si quitar una función de su proyecto de servicio de nube, pero más adelante decide tooadd nuevo rol de hello toohello proyecto, solo declaración del rol de Hola y atributos básicos, como los puntos de conexión e información de diagnóstico, se agregan.</span><span class="sxs-lookup"><span data-stu-id="1838f-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="1838f-124">No hay recursos adicionales o referencias se agregan toohello `ServiceDefinition.csdef` archivo o toohello `ServiceConfiguration.cscfg` archivo.</span><span class="sxs-lookup"><span data-stu-id="1838f-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="1838f-125">Si desea tooadd esta información, necesita toomanually agregar a estos archivos.</span><span class="sxs-lookup"><span data-stu-id="1838f-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="1838f-126">Por ejemplo, puede quitar un rol de servicio web y después decidir tooadd hacer copia de este rol en la solución.</span><span class="sxs-lookup"><span data-stu-id="1838f-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="1838f-127">Si lo hace, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="1838f-127">If you do this, an error occurs.</span></span> <span data-ttu-id="1838f-128">tooprevent este error, tienes hello tooadd `<LocalResources>` elemento mostrado en hello después XML nuevamente en hello `ServiceDefinition.csdef` archivo.</span><span class="sxs-lookup"><span data-stu-id="1838f-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="1838f-129">Usar el nombre de rol de servicio web de Hola que agregó de nuevo en el proyecto de hello como parte del atributo de nombre de Hola para Hola Hola  **<LocalStorage>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="1838f-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="1838f-130">En este ejemplo, nombre de Hola Hola web del rol de servicio es **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="1838f-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1838f-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1838f-131">Next steps</span></span>
- [<span data-ttu-id="1838f-132">Configurar los Roles de Hola para un servicio de nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1838f-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
