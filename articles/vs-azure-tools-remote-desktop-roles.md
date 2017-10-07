---
title: aaaUsing escritorio remoto con los Roles de Azure | Documentos de Microsoft
description: Uso de Escritorio de remoto con los roles de Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="1329b-103">Uso de Escritorio de remoto con los roles de Azure</span><span class="sxs-lookup"><span data-stu-id="1329b-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="1329b-104">Mediante el uso de hello Azure SDK y los servicios de escritorio remoto, puede tener acceso a las funciones de Azure y máquinas virtuales que se hospedan en Azure.</span><span class="sxs-lookup"><span data-stu-id="1329b-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="1329b-105">En Visual Studio, puede configurar Servicios de Escritorio remoto desde un proyecto de servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="1329b-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="1329b-106">tooenable de servicios de escritorio remoto, debe crear un proyecto totalmente funcional que contiene uno o más roles y, a continuación, publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1329b-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1329b-107">Debe tener acceso a un rol de Azure para solucionar problemas o desarrollo solamente.</span><span class="sxs-lookup"><span data-stu-id="1329b-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="1329b-108">Hola propósito de cada máquina virtual es un rol concreto en la aplicación de Azure, no toorun toorun otras aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="1329b-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="1329b-109">Si desea toouse toohost Azure una máquina virtual que puede utilizar para cualquier propósito, vea obtener acceso a máquinas virtuales de Azure del explorador de servidores.</span><span class="sxs-lookup"><span data-stu-id="1329b-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="1329b-110">tooenable y usar Escritorio remoto para un rol de Azure</span><span class="sxs-lookup"><span data-stu-id="1329b-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="1329b-111">En el Explorador de soluciones, abra el menú contextual de hello para el proyecto de servicio de nube y, a continuación, elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="1329b-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="1329b-112">Hola **publicar aplicación de Azure** aparece el Asistente para.</span><span class="sxs-lookup"><span data-stu-id="1329b-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Publicar el comando para un proyecto de servicio en la nube](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="1329b-114">En la parte inferior de Hola de **configuración de publicación de Microsoft Azure** página del Asistente de hello, seleccione hello **habilitar Escritorio remoto** para todos los roles de casilla.</span><span class="sxs-lookup"><span data-stu-id="1329b-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="1329b-115">Hola **configuración de escritorio remoto** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1329b-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="1329b-116">Final de Hola de hello **configuración de escritorio remoto** diálogo cuadro, elija hello **más opciones** botón.</span><span class="sxs-lookup"><span data-stu-id="1329b-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="1329b-117">Esto muestra un cuadro de lista desplegable que le permite crear o seleccionar un certificado para que puede cifrar la información de credenciales al conectarse a través de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="1329b-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="1329b-118">En la lista desplegable de hello, elija  **&lt;crear >**, o elija uno ya existente de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="1329b-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="1329b-119">Si selecciona un certificado existente, pase Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="1329b-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1329b-120">certificados de Hola que necesita para una conexión a escritorio remota son distintos de los certificados de Hola que se usan para otras operaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="1329b-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="1329b-121">certificado de acceso remoto de Hello debe tener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="1329b-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="1329b-122">Hola **Create Certificate** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1329b-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="1329b-123">Proporcione un nombre descriptivo para el nuevo certificado de Hola y, a continuación, elija Hola **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="1329b-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="1329b-124">Hola nuevo certificado aparece en cuadro de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1329b-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="1329b-125">Hola **configuración de escritorio remoto** diálogo cuadro, proporcione un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="1329b-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="1329b-126">No se puede usar una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="1329b-126">You can’t use an existing account.</span></span> <span data-ttu-id="1329b-127">No especifique Administrador como nombre de usuario de hello para la nueva cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="1329b-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="1329b-128">Si la contraseña de hello no cumple los requisitos de complejidad de hello, aparecerá un icono rojo siguiente cuadro de texto de contraseña toohello.</span><span class="sxs-lookup"><span data-stu-id="1329b-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="1329b-129">Hola contraseña debe contener letras mayúsculas, letras minúsculas y números o símbolos.</span><span class="sxs-lookup"><span data-stu-id="1329b-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="1329b-130">Elija una fecha en que expirará la cuenta de hello y después se bloquearán las conexiones a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="1329b-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="1329b-131">Cuando se haya proporcionado todos Hola información necesaria, elija hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="1329b-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="1329b-132">Varias opciones de configuración que habilite los servicios de acceso remoto se agregan los archivos .cscfg y .csdef toohello.</span><span class="sxs-lookup"><span data-stu-id="1329b-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="1329b-133">Hola **configuración de publicación de Microsoft Azure** asistente, elija hello **Aceptar** botón cuando esté listo toopublish su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="1329b-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="1329b-134">Si no está listo toopublish, elija hello **cancelar** botón.</span><span class="sxs-lookup"><span data-stu-id="1329b-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="1329b-135">Opciones de configuración de Hola se guardan y podrá publicar su servicio en la nube más adelante.</span><span class="sxs-lookup"><span data-stu-id="1329b-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="1329b-136">Conectar tooan rol de Azure mediante Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="1329b-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="1329b-137">Después de publicar el servicio de nube en Azure, puede usar toolog del explorador de servidores en máquinas virtuales de Hola que hospeda Azure.</span><span class="sxs-lookup"><span data-stu-id="1329b-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="1329b-138">En el Explorador de servidores, expanda hello **Azure** nodo y a continuación, expanda el nodo de Hola para un servicio de nube y uno de su toodisplay una lista de instancias de roles.</span><span class="sxs-lookup"><span data-stu-id="1329b-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="1329b-139">Abra el acceso directo de Hola para un nodo de la instancia y, a continuación, elija **conectar usando Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="1329b-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Conexión a través del escritorio remoto](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="1329b-141">Escriba el nombre de usuario de Hola y la contraseña que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1329b-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="1329b-142">Ahora está registrado en la sesión remota.</span><span class="sxs-lookup"><span data-stu-id="1329b-142">You are now logged into your remote session.</span></span>

