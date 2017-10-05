---
title: "Solución de problemas de Azure RBAC | Microsoft Docs"
description: Obtenga ayuda para los problemas o dudas que le surjan relativos a los recursos del control de acceso basado en roles.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="d4d57-103">Solución de problemas del control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="d4d57-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="d4d57-104">En este artículo se responden preguntas comunes sobre de los derechos de acceso específicos que se conceden con roles, para que sepa qué esperar cuando usa los roles de Azure Portal y pueda solucionar problemas de acceso.</span><span class="sxs-lookup"><span data-stu-id="d4d57-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="d4d57-105">Estos tres roles abarcan todos los tipos de recursos:</span><span class="sxs-lookup"><span data-stu-id="d4d57-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="d4d57-106">Propietario</span><span class="sxs-lookup"><span data-stu-id="d4d57-106">Owner</span></span>  
* <span data-ttu-id="d4d57-107">Colaborador</span><span class="sxs-lookup"><span data-stu-id="d4d57-107">Contributor</span></span>  
* <span data-ttu-id="d4d57-108">Lector</span><span class="sxs-lookup"><span data-stu-id="d4d57-108">Reader</span></span>  

<span data-ttu-id="d4d57-109">Los propietarios y los colaboradores tienen acceso total a la experiencia de administración, pero un colaborador no puede dar acceso a otros usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="d4d57-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="d4d57-110">Nos centraremos en el rol del lector, ya que tiene más aspectos que comentar.</span><span class="sxs-lookup"><span data-stu-id="d4d57-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="d4d57-111">Consulte el artículo de [introducción de Control de acceso basado en rol](role-based-access-control-configure.md) para obtener más información sobre cómo conceder acceso.</span><span class="sxs-lookup"><span data-stu-id="d4d57-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="d4d57-112">Cargas de trabajo del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d4d57-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="d4d57-113">Funcionalidades de acceso de escritura</span><span class="sxs-lookup"><span data-stu-id="d4d57-113">Write access capabilities</span></span>
<span data-ttu-id="d4d57-114">Si concede a un usuario acceso de solo lectura a una única aplicación web, se deshabilitan algunas características que no cabría esperar.</span><span class="sxs-lookup"><span data-stu-id="d4d57-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="d4d57-115">Las siguientes funcionalidades de administración requieren acceso de **escritura** a una aplicación web (bien como colaborador, bien como propietario) y no están disponibles en un escenario de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d4d57-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="d4d57-116">Comandos (p. ej., iniciar, parar, etc.)</span><span class="sxs-lookup"><span data-stu-id="d4d57-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="d4d57-117">Cambiar opciones, como la configuración general, opciones de escala, opciones de copia de seguridad y opciones de supervisión</span><span class="sxs-lookup"><span data-stu-id="d4d57-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="d4d57-118">Acceder a las credenciales de publicación y otros secretos, como opciones de aplicaciones y cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="d4d57-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="d4d57-119">Registros de streaming</span><span class="sxs-lookup"><span data-stu-id="d4d57-119">Streaming logs</span></span>
* <span data-ttu-id="d4d57-120">Configuración de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="d4d57-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="d4d57-121">Consola (símbolo del sistema)</span><span class="sxs-lookup"><span data-stu-id="d4d57-121">Console (command prompt)</span></span>
* <span data-ttu-id="d4d57-122">Implementaciones activas y recientes (para implementaciones git continuas locales)</span><span class="sxs-lookup"><span data-stu-id="d4d57-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="d4d57-123">Gasto estimado</span><span class="sxs-lookup"><span data-stu-id="d4d57-123">Estimated spend</span></span>
* <span data-ttu-id="d4d57-124">Pruebas web</span><span class="sxs-lookup"><span data-stu-id="d4d57-124">Web tests</span></span>
* <span data-ttu-id="d4d57-125">Red virtual (solo visible para un lector si un usuario con acceso de escritura ha configurado previamente una red virtual)</span><span class="sxs-lookup"><span data-stu-id="d4d57-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="d4d57-126">Si no puede acceder a ninguno de estos iconos, debe pedirle al administrador el acceso de colaborador a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d4d57-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="d4d57-127">Tratar con recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="d4d57-127">Dealing with related resources</span></span>
<span data-ttu-id="d4d57-128">Las aplicaciones web pueden resultar complicadas si entran en juego distintos recursos.</span><span class="sxs-lookup"><span data-stu-id="d4d57-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="d4d57-129">Este es un grupo de recursos típico con un par de sitios web:</span><span class="sxs-lookup"><span data-stu-id="d4d57-129">Here is a typical resource group with a couple websites:</span></span>

![Grupo de recursos de aplicación web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="d4d57-131">Como consecuencia, si le concede a alguien acceso solo a la aplicación web, muchas de las funcionalidades de la hoja del sitio web de Azure Portal están deshabilitadas.</span><span class="sxs-lookup"><span data-stu-id="d4d57-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="d4d57-132">Estos elementos requieren acceso de **escritura** al **plan de App Service** que corresponde a su sitio web:</span><span class="sxs-lookup"><span data-stu-id="d4d57-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="d4d57-133">Visualización del plan de tarifa de la aplicación web (gratis o estándar).</span><span class="sxs-lookup"><span data-stu-id="d4d57-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="d4d57-134">Configuración de escala (número de instancias, tamaño de la máquina virtual y configuración de escala automática).</span><span class="sxs-lookup"><span data-stu-id="d4d57-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="d4d57-135">Cuotas (almacenamiento, ancho de banda y CPU).</span><span class="sxs-lookup"><span data-stu-id="d4d57-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="d4d57-136">Estos elementos requieren acceso de **escritura** a todo el **grupo de recursos** que contiene su sitio web:</span><span class="sxs-lookup"><span data-stu-id="d4d57-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="d4d57-137">Enlaces y certificados SSL (los certificados SSL se pueden compartir entre sitios en el mismo grupo de recursos y la misma ubicación geográfica)</span><span class="sxs-lookup"><span data-stu-id="d4d57-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="d4d57-138">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="d4d57-138">Alert rules</span></span>  
* <span data-ttu-id="d4d57-139">Opciones de escala automática</span><span class="sxs-lookup"><span data-stu-id="d4d57-139">Autoscale settings</span></span>  
* <span data-ttu-id="d4d57-140">Componentes de Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4d57-140">Application insights components</span></span>  
* <span data-ttu-id="d4d57-141">Pruebas web</span><span class="sxs-lookup"><span data-stu-id="d4d57-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="d4d57-142">Cargas de trabajo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4d57-142">Virtual machine workloads</span></span>
<span data-ttu-id="d4d57-143">Al igual que con las aplicaciones web, algunas funciones de la hoja de máquina virtual requieren acceso de escritura a la máquina virtual o a otros recursos del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4d57-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="d4d57-144">Las máquinas virtuales están relacionadas con los nombres de dominio, las redes virtuales, las cuentas de almacenamiento y las reglas de alerta.</span><span class="sxs-lookup"><span data-stu-id="d4d57-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="d4d57-145">Estos elementos requieren acceso de **escritura** a la **máquina virtual**:</span><span class="sxs-lookup"><span data-stu-id="d4d57-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="d4d57-146">Extremos</span><span class="sxs-lookup"><span data-stu-id="d4d57-146">Endpoints</span></span>  
* <span data-ttu-id="d4d57-147">Direcciones IP</span><span class="sxs-lookup"><span data-stu-id="d4d57-147">IP addresses</span></span>  
* <span data-ttu-id="d4d57-148">Discos</span><span class="sxs-lookup"><span data-stu-id="d4d57-148">Disks</span></span>  
* <span data-ttu-id="d4d57-149">Extensiones</span><span class="sxs-lookup"><span data-stu-id="d4d57-149">Extensions</span></span>  

<span data-ttu-id="d4d57-150">Estos requieren acceso de **escritura** a la **máquina virtual** y al **grupo de recursos** (junto con el nombre de dominio) donde se encuentran:</span><span class="sxs-lookup"><span data-stu-id="d4d57-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="d4d57-151">El conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="d4d57-151">Availability set</span></span>  
* <span data-ttu-id="d4d57-152">El conjunto de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="d4d57-152">Load balanced set</span></span>  
* <span data-ttu-id="d4d57-153">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="d4d57-153">Alert rules</span></span>  

<span data-ttu-id="d4d57-154">Si no puede acceder a ninguno de estos iconos, debe pedirle al administrador el acceso de colaborador al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4d57-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="d4d57-155">Ver más</span><span class="sxs-lookup"><span data-stu-id="d4d57-155">See more</span></span>
* <span data-ttu-id="d4d57-156">[Control de acceso basado en roles de Azure](role-based-access-control-configure.md): inicio de RBAC en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d57-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="d4d57-157">[RBAC: Roles integrados](role-based-access-built-in-roles.md): obtenga información sobre los roles que se incluyen como estándar en RBAC.</span><span class="sxs-lookup"><span data-stu-id="d4d57-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="d4d57-158">[Roles personalizados en Azure RBAC](role-based-access-control-custom-roles.md): aprenda a crear roles personalizados para satisfacer sus necesidades de acceso.</span><span class="sxs-lookup"><span data-stu-id="d4d57-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="d4d57-159">[Creación de un informe de historial de cambios de acceso](role-based-access-control-access-change-history-report.md): realice un seguimiento del cambio de asignaciones de rol en el RBAC.</span><span class="sxs-lookup"><span data-stu-id="d4d57-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

