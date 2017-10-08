---
title: aaaManage Azure Analysis Services | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage un Analysis Services server en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="4ed3e-103">Administración de Analysis Services</span><span class="sxs-lookup"><span data-stu-id="4ed3e-103">Manage Analysis Services</span></span>
<span data-ttu-id="4ed3e-104">Una vez que ha creado un servidor de Analysis Services en Azure, puede haber algunas tareas de administración y administración necesita tooperform inmediatamente o algún tiempo inactivo road Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="4ed3e-105">Por ejemplo, ejecutar el procesamiento toohello de actualización de datos, controlar quién puede tener acceso a los modelos de hello en el servidor o supervisar el estado del servidor.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="4ed3e-106">Varias de estas tareas solo se pueden realizar en Azure Portal, otras en SQL Server Management Studio (SSMS) y otras se pueden realizar indistintamente en ambos.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="4ed3e-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4ed3e-107">Azure portal</span></span>
<span data-ttu-id="4ed3e-108">[Portal de Azure](http://portal.azure.com/) es donde puede crear y eliminar servidores, supervisar los recursos de servidor, cambiar el tamaño y administrar quién tiene acceso tooyour servidores.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="4ed3e-109">Si tiene problemas, también puede enviar una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-109">If you're having some problems, you can also submit a support request.</span></span>

![Obtención del nombre del servidor en Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="4ed3e-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="4ed3e-111">SQL Server Management Studio</span></span>
<span data-ttu-id="4ed3e-112">Conectar el servidor de tooyour en Azure es igual que conecta la instancia del servidor tooa en su propia organización.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="4ed3e-113">En SSMS, puede realizar muchas de hello mismo tareas como procesar los datos o crear una secuencia de comandos de procesamiento, administrar roles y usar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="4ed3e-115">Descarga e instalación de SSMS</span><span class="sxs-lookup"><span data-stu-id="4ed3e-115">Download and install SSMS</span></span>
<span data-ttu-id="4ed3e-116">tooget todos Hola características más recientes y experiencia más fluida de hello cuando se conecta el servidor de Analysis Services de Azure de tooyour, asegúrese de utiliza la versión más reciente de Hola de SSMS.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="4ed3e-117">[Descargue SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="4ed3e-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="4ed3e-118">tooconnect con SSMS</span><span class="sxs-lookup"><span data-stu-id="4ed3e-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="4ed3e-119">Cuando se usa SSMS, antes de conectar saludos del servidor tooyour primera vez, asegúrese de que el nombre de usuario se incluye en el grupo de administradores de servicios de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="4ed3e-120">más información, consulte toolearn [los administradores del servidor](#server-administrators) más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="4ed3e-121">Antes de conectar, necesita el nombre del servidor de tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="4ed3e-122">En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, el nombre del servidor de copia Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="4ed3e-124">En SSMS > **Explorador de objetos**, haga clic en **Conectar** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="4ed3e-125">Hola **conectar tooServer** cuadro de diálogo, pegar en nombre del servidor hello, a continuación, en **autenticación**, elija uno de los siguientes tipos de autenticación de hello:</span><span class="sxs-lookup"><span data-stu-id="4ed3e-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="4ed3e-126">**Autenticación de Windows** toouse sus credenciales de dominio ombre de usuario y la contraseña de Windows.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="4ed3e-127">**Autenticación de contraseña de Active Directory** toouse una cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="4ed3e-128">Por ejemplo, al establecer conexión desde un equipo unido que no es de dominio.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="4ed3e-129">**Autenticación Universal de Active Directory** toouse [la autenticación no interactiva o multifactor](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4ed3e-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Conectar en SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="4ed3e-131">Administradores del servidor y usuarios de la base de datos</span><span class="sxs-lookup"><span data-stu-id="4ed3e-131">Server administrators and database users</span></span>
<span data-ttu-id="4ed3e-132">En Azure Analysis Services hay dos tipos de usuarios: los administradores del servidor y los usuarios de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="4ed3e-133">Ambos tipos de usuarios deben estar en su instancia de Azure Active Directory y se deben especificar mediante la dirección de correo electrónico profesional o UPN.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="4ed3e-134">más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="4ed3e-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="4ed3e-135">Solución de problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="4ed3e-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="4ed3e-136">Cuando se conecta mediante SSMS, si experimenta problemas, puede que necesite caché de inicio de sesión de tooclear Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="4ed3e-137">Nada es toodisc almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="4ed3e-138">proceso de conexión de la caché de hello tooclear, cierre y reinicio Hola.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4ed3e-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ed3e-139">Next steps</span></span>
<span data-ttu-id="4ed3e-140">Si ya no ha implementado un nuevo servidor de modelo tabular tooyour, ahora es un buen momento.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="4ed3e-141">más información, consulte toolearn [implementar tooAzure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4ed3e-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="4ed3e-142">Si ha implementado un servidor de tooyour de modelo, le tooit tooconnect listo con un cliente o un explorador.</span><span class="sxs-lookup"><span data-stu-id="4ed3e-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="4ed3e-143">más información, consulte toolearn [obtener datos del servidor de Analysis Services de Azure](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4ed3e-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

