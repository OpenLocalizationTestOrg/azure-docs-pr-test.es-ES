---
title: aaaTroubleshoot RBAC de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="4788a-103">Solución de problemas del control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="4788a-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="4788a-104">En este artículo de documento preguntas más frecuentes sobre los derechos de acceso específicos de Hola que se conceden con roles, para que sepa qué tooexpect cuando usan Hola roles Hola portal de Azure y se puede solucionar problemas de acceso.</span><span class="sxs-lookup"><span data-stu-id="4788a-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="4788a-105">Estos tres roles abarcan todos los tipos de recursos:</span><span class="sxs-lookup"><span data-stu-id="4788a-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="4788a-106">Propietario</span><span class="sxs-lookup"><span data-stu-id="4788a-106">Owner</span></span>  
* <span data-ttu-id="4788a-107">Colaborador</span><span class="sxs-lookup"><span data-stu-id="4788a-107">Contributor</span></span>  
* <span data-ttu-id="4788a-108">Lector</span><span class="sxs-lookup"><span data-stu-id="4788a-108">Reader</span></span>  

<span data-ttu-id="4788a-109">Los propietarios y colaboradores tienen acceso total toohello administración de experiencia, pero un colaborador no puede conceder acceso tooother usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="4788a-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="4788a-110">Puede ser un poco más interesante con rol de lector de hello, por lo es donde se pasará algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="4788a-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="4788a-111">Vea hello [artículo iniciada por get de Control de acceso basado en roles](role-based-access-control-configure.md) para obtener más información sobre cómo tener acceso toogrant.</span><span class="sxs-lookup"><span data-stu-id="4788a-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="4788a-112">Cargas de trabajo del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4788a-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="4788a-113">Funcionalidades de acceso de escritura</span><span class="sxs-lookup"><span data-stu-id="4788a-113">Write access capabilities</span></span>
<span data-ttu-id="4788a-114">Si se concede una acceso de solo lectura de usuario tooa web única aplicación, se deshabilitan algunas características que no cabría esperar.</span><span class="sxs-lookup"><span data-stu-id="4788a-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="4788a-115">Hola después de capacidades de administración requiere **escribir** acceder a la aplicación web de tooa (colaborador o propietario) y no están disponibles en cualquier escenario de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="4788a-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="4788a-116">Comandos (p. ej., iniciar, parar, etc.)</span><span class="sxs-lookup"><span data-stu-id="4788a-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="4788a-117">Cambiar opciones, como la configuración general, opciones de escala, opciones de copia de seguridad y opciones de supervisión</span><span class="sxs-lookup"><span data-stu-id="4788a-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="4788a-118">Acceder a las credenciales de publicación y otros secretos, como opciones de aplicaciones y cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="4788a-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="4788a-119">Registros de streaming</span><span class="sxs-lookup"><span data-stu-id="4788a-119">Streaming logs</span></span>
* <span data-ttu-id="4788a-120">Configuración de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4788a-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="4788a-121">Consola (símbolo del sistema)</span><span class="sxs-lookup"><span data-stu-id="4788a-121">Console (command prompt)</span></span>
* <span data-ttu-id="4788a-122">Implementaciones activas y recientes (para implementaciones git continuas locales)</span><span class="sxs-lookup"><span data-stu-id="4788a-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="4788a-123">Gasto estimado</span><span class="sxs-lookup"><span data-stu-id="4788a-123">Estimated spend</span></span>
* <span data-ttu-id="4788a-124">Pruebas web</span><span class="sxs-lookup"><span data-stu-id="4788a-124">Web tests</span></span>
* <span data-ttu-id="4788a-125">Red virtual (solo visible tooa lector si ya ha configurado una red virtual por un usuario con acceso de escritura).</span><span class="sxs-lookup"><span data-stu-id="4788a-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="4788a-126">Si no se puede obtener acceso a cualquiera de estos iconos, deberá tooask el administrador para la aplicación web de colaborador acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="4788a-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="4788a-127">Tratar con recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="4788a-127">Dealing with related resources</span></span>
<span data-ttu-id="4788a-128">Las aplicaciones Web se ve complicadas por presencia de Hola de solo unos pocos recursos diferentes que interacción.</span><span class="sxs-lookup"><span data-stu-id="4788a-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="4788a-129">Este es un grupo de recursos típico con un par de sitios web:</span><span class="sxs-lookup"><span data-stu-id="4788a-129">Here is a typical resource group with a couple websites:</span></span>

![Grupo de recursos de aplicación web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="4788a-131">Como resultado, si concede a alguien acceso toojust hello web app, gran parte de la funcionalidad de hello en la hoja de sitio Web de Hola Hola portal de Azure está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="4788a-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="4788a-132">Estos elementos requieren **escribir** acceso toohello **plan de servicio de aplicaciones** que corresponde el sitio Web de tooyour:</span><span class="sxs-lookup"><span data-stu-id="4788a-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="4788a-133">Aplicación web de Hola de visualización del plan de tarifa (gratuito o estándar)</span><span class="sxs-lookup"><span data-stu-id="4788a-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="4788a-134">Configuración de escala (número de instancias, tamaño de la máquina virtual y configuración de escala automática).</span><span class="sxs-lookup"><span data-stu-id="4788a-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="4788a-135">Cuotas (almacenamiento, ancho de banda y CPU).</span><span class="sxs-lookup"><span data-stu-id="4788a-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="4788a-136">Estos elementos requieren **escribir** toohello acceso todo **grupo de recursos** que contiene el sitio Web:</span><span class="sxs-lookup"><span data-stu-id="4788a-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="4788a-137">Certificados SSL y enlaces (certificados SSL pueden compartirse entre los sitios de hello mismo grupo de recursos y la ubicación geográfica)</span><span class="sxs-lookup"><span data-stu-id="4788a-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="4788a-138">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="4788a-138">Alert rules</span></span>  
* <span data-ttu-id="4788a-139">Opciones de escala automática</span><span class="sxs-lookup"><span data-stu-id="4788a-139">Autoscale settings</span></span>  
* <span data-ttu-id="4788a-140">Componentes de Application Insights</span><span class="sxs-lookup"><span data-stu-id="4788a-140">Application insights components</span></span>  
* <span data-ttu-id="4788a-141">Pruebas web</span><span class="sxs-lookup"><span data-stu-id="4788a-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="4788a-142">Cargas de trabajo de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4788a-142">Virtual machine workloads</span></span>
<span data-ttu-id="4788a-143">Mucho al igual que con las aplicaciones web, algunas características de hoja de la máquina virtual de hello requieren una máquina virtual de acceso de escritura toohello o tooother recursos en grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4788a-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="4788a-144">Máquinas virtuales son nombres tooDomain relacionados, redes virtuales, cuentas de almacenamiento y las reglas de alerta.</span><span class="sxs-lookup"><span data-stu-id="4788a-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="4788a-145">Estos elementos requieren **escribir** acceso toohello **Máquina Virtual**:</span><span class="sxs-lookup"><span data-stu-id="4788a-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="4788a-146">Puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="4788a-146">Endpoints</span></span>  
* <span data-ttu-id="4788a-147">Direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4788a-147">IP addresses</span></span>  
* <span data-ttu-id="4788a-148">Discos</span><span class="sxs-lookup"><span data-stu-id="4788a-148">Disks</span></span>  
* <span data-ttu-id="4788a-149">Extensiones</span><span class="sxs-lookup"><span data-stu-id="4788a-149">Extensions</span></span>  

<span data-ttu-id="4788a-150">Se requiere el **escribir** Hola de acceso tooboth **Máquina Virtual**, hello y **grupo de recursos** (junto con el nombre de dominio de Hola) que se encuentre en:</span><span class="sxs-lookup"><span data-stu-id="4788a-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="4788a-151">El conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="4788a-151">Availability set</span></span>  
* <span data-ttu-id="4788a-152">El conjunto de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="4788a-152">Load balanced set</span></span>  
* <span data-ttu-id="4788a-153">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="4788a-153">Alert rules</span></span>  

<span data-ttu-id="4788a-154">Si no se puede obtener acceso a cualquiera de estos iconos, pida al administrador para el grupo de recursos de toohello de acceso de colaborador.</span><span class="sxs-lookup"><span data-stu-id="4788a-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="4788a-155">Ver más</span><span class="sxs-lookup"><span data-stu-id="4788a-155">See more</span></span>
* <span data-ttu-id="4788a-156">[Control de acceso basado en roles](role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4788a-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="4788a-157">[Funciones integradas](role-based-access-built-in-roles.md): obtener detalles acerca de los roles de Hola que vienen en RBAC.</span><span class="sxs-lookup"><span data-stu-id="4788a-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="4788a-158">[Roles personalizados en Azure RBAC](role-based-access-control-custom-roles.md): Obtenga información acerca de cómo toocreate roles personalizados toofit sus necesidades de acceso.</span><span class="sxs-lookup"><span data-stu-id="4788a-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="4788a-159">[Creación de un informe del historial de cambios de acceso](role-based-access-control-access-change-history-report.md): seguimiento del cambio de asignaciones de roles en RBAC.</span><span class="sxs-lookup"><span data-stu-id="4788a-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

