---
title: "Uso de System for Cross-Domain Identity Management para aprovisionar automáticamente a los usuarios y grupos de Azure Active Directory para aplicaciones | Microsoft Docs"
description: "Azure Active Directory puede aprovisionar automáticamente los usuarios y grupos a cualquier aplicación o almacén de identidades proporcionado por un servicio web con la interfaz definida en la especificación del protocolo SCIM"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="768dc-103">Uso de System for Cross-Domain Identity Management para aprovisionar automáticamente a los usuarios y grupos de Azure Active Directory para aplicaciones</span><span class="sxs-lookup"><span data-stu-id="768dc-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="768dc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="768dc-104">Overview</span></span>
<span data-ttu-id="768dc-105">Azure Active Directory (Azure AD) puede aprovisionar automáticamente a usuarios y grupos de cualquier aplicación o almacén de identidades dirigidos por un servicio web con la interfaz definida en la [especificación del protocolo System for Cross-Domain Identity Management (SCIM) 2.0](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="768dc-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="768dc-106">Azure Active Directory puede enviar solicitudes para crear, modificar o eliminar los usuarios y grupos asignados al servicio web.</span><span class="sxs-lookup"><span data-stu-id="768dc-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="768dc-107">El servicio web puede convertir entonces esas solicitudes en operaciones en el almacén de identidades de destino.</span><span class="sxs-lookup"><span data-stu-id="768dc-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="768dc-108">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="768dc-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="768dc-109">![][0]
*Figura 1: aprovisionamiento de Azure Active Directory en un almacén de identidades a través de un servicio web*</span><span class="sxs-lookup"><span data-stu-id="768dc-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="768dc-110">Esta funcionalidad puede usarse junto con la de aportación de la propia aplicación en Azure AD para habilitar el inicio de sesión único y el aprovisionamiento automático de usuarios para aplicaciones que proporcionan un servicio web SCIM o que son dirigidas por uno de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="768dc-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="768dc-111">Existen dos casos de uso de SCIM en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="768dc-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="768dc-112">**Aprovisionamiento de usuarios y grupos para aplicaciones que admiten SCIM**: las aplicaciones compatibles con SCIM 2.0 y que usan un token de portador de OAuth para la autenticación funcionan con Azure AD sin tener que configurarse.</span><span class="sxs-lookup"><span data-stu-id="768dc-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="768dc-113">**Creación de una solución de aprovisionamiento propia para aplicaciones que admiten otro aprovisionamiento basado en API**: para las aplicaciones que no son SCIM, puede crear un punto de conexión SCIM para la traducción entre el punto de conexión SCIM de Azure AD y cualquier API que admita la aplicación para el aprovisionamiento de usuarios.</span><span class="sxs-lookup"><span data-stu-id="768dc-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="768dc-114">Para facilitar el desarrollo de un punto de conexión SCIM, proporcionamos las bibliotecas Common Language Infrastructure (CLI) junto con ejemplos de código que muestran cómo proporcionar un punto de conexión SCIM y traducir los mensajes SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="768dc-115">Aprovisionamiento de usuarios y grupos para aplicaciones que admiten SCIM</span><span class="sxs-lookup"><span data-stu-id="768dc-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="768dc-116">Azure AD puede configurarse para aprovisionar automáticamente a usuarios y grupos asignados a aplicaciones que implementan un servicio web [System for Cross-Domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) y que aceptan tokens de portador de OAuth para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="768dc-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="768dc-117">Dentro de la especificación SCIM 2.0, las aplicaciones deben cumplir estos requisitos:</span><span class="sxs-lookup"><span data-stu-id="768dc-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="768dc-118">Admitir la creación de usuarios o grupos, según la sección 3.3 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="768dc-119">Admitir la modificación de usuarios o grupos con solicitudes de revisión, según la sección 3.5.2 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="768dc-120">Admitir la recuperación de un recurso conocido, según la sección 3.4.1 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="768dc-121">Admitir la consulta de usuarios o grupos, según la sección 3.4.2 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="768dc-122">De forma predeterminada, los usuarios se consultan por externalId y los grupos por displayName.</span><span class="sxs-lookup"><span data-stu-id="768dc-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="768dc-123">Admitir la consulta de usuarios por Id. y administrador, según la sección 3.4.2 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="768dc-124">Admitir la consulta de grupos por Id. y miembro, según la sección 3.4.2 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="768dc-125">Aceptar los tokens de portador de OAuth para la autorización. según la sección 2.1 del protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="768dc-126">Consulte a su proveedor de la aplicación o la documentación que se incluye con la aplicación para ver si existen declaraciones de compatibilidad con estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="768dc-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="768dc-127">Introducción</span><span class="sxs-lookup"><span data-stu-id="768dc-127">Getting started</span></span>
<span data-ttu-id="768dc-128">Las aplicaciones que admiten el perfil SCIM descrito en este artículo se pueden conectar a Azure Active Directory mediante la característica "de aplicación situada fuera de la galería" de la galería de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="768dc-129">Una vez conectadas, Azure AD ejecuta un proceso de sincronización cada 20 minutos en el que consulta el punto de conexión SCIM de la aplicación para ver los usuarios y grupos asignados, y los crea o modifica según los detalles de asignación.</span><span class="sxs-lookup"><span data-stu-id="768dc-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="768dc-130">**Para conectar una aplicación que admite SCIM:**</span><span class="sxs-lookup"><span data-stu-id="768dc-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="768dc-131">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="768dc-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="768dc-132">Vaya a **Azure Active Directory > Aplicaciones empresariales y seleccione **Nueva aplicación > Todas > Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="768dc-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="768dc-133">Escriba un nombre para la aplicación y haga clic en el icono **Agregar** para crear un objeto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="768dc-134">![][1]
  *Figura 2: galería de aplicaciones de Azure AD*</span><span class="sxs-lookup"><span data-stu-id="768dc-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="768dc-135">En la pantalla resultante, seleccione la pestaña **Aprovisionamiento** en la columna izquierda.</span><span class="sxs-lookup"><span data-stu-id="768dc-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="768dc-136">En el menú **Modo de aprovisionamiento**, seleccione **Automático**.</span><span class="sxs-lookup"><span data-stu-id="768dc-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="768dc-137">![][2]
  *Figura 3: configuración del aprovisionamiento en Azure Portal*</span><span class="sxs-lookup"><span data-stu-id="768dc-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="768dc-138">En el campo **Dirección URL del inquilino**, escriba la dirección URL del punto de conexión SCIM de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="768dc-139">Ejemplo: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="768dc-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="768dc-140">Si el punto de conexión SCIM requiere un token de portador OAuth de un emisor que no sea Azure AD, copie el token de portador OAuth necesario en el campo **Token secreto**.</span><span class="sxs-lookup"><span data-stu-id="768dc-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="768dc-141">Si este campo se deja en blanco, Azure AD incluye un token de portador OAuth emitido desde Azure AD con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="768dc-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="768dc-142">Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="768dc-143">Haga clic en el botón **Probar conexión** para que Azure Active Directory intente conectarse al punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="768dc-144">Si se produce un error en los intentos, se muestra información de error.</span><span class="sxs-lookup"><span data-stu-id="768dc-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="768dc-145">Si se produce la conexión, a continuación, haga clic en **Guardar** para guardar las credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="768dc-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="768dc-146">En la sección **Asignaciones**, hay dos conjuntos seleccionables de asignaciones de atributos: uno para los objetos de usuario y otro para los objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="768dc-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="768dc-147">Seleccione cada uno de ellos para revisar los atributos que se sincronizan desde Azure Active Directory a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="768dc-148">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con los usuarios y grupos de la aplicación con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="768dc-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="768dc-149">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="768dc-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="768dc-150">Opcionalmente, puede deshabilitar la sincronización de objetos de grupo deshabilitando la asignación de "grupos".</span><span class="sxs-lookup"><span data-stu-id="768dc-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="768dc-151">En **Configuración**, el campo **Ámbito** define qué usuarios y grupos se sincronizan.</span><span class="sxs-lookup"><span data-stu-id="768dc-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="768dc-152">Al seleccionar "Sync only assigned users and groups" (Sincronizar solo los usuarios y grupos asignados) (recomendado) solo sincronizará los usuarios y grupos asignados en la pestaña **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="768dc-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="768dc-153">Una vez completada la configuración, cambie el **Estado de aprovisionamiento** a **On** (Activo).</span><span class="sxs-lookup"><span data-stu-id="768dc-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="768dc-154">Haga clic en **Guardar** para iniciar el servicio de aprovisionamiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="768dc-155">Al sincronizar solo los usuarios y grupos asignados (recomendado), no olvide seleccionar la pestaña **Usuarios y grupos** y asigne los usuarios o grupos que se van a sincronizar.</span><span class="sxs-lookup"><span data-stu-id="768dc-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="768dc-156">Una vez que haya iniciado la sincronización inicial, puede utilizar la pestaña **Registros de auditoría** para supervisar el progreso, con lo que se muestran todas las acciones realizadas por el servicio de aprovisionamiento en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="768dc-157">Para más información sobre cómo leer los registros de aprovisionamiento de Azure AD, consulte el tutorial de [Creación de informes sobre el aprovisionamiento automático de cuentas de usuario](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="768dc-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="768dc-158">La sincronización inicial tardará más tiempo en realizarse que las posteriores, que se producen aproximadamente cada 20 minutos si se está ejecutando el servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="768dc-159">Creación de una solución de aprovisionamiento propia para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="768dc-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="768dc-160">Al crear un servicio web SCIM que interactúa con Azure Active Directory, puede habilitar el inicio de sesión único y el aprovisionamiento automático de usuarios para prácticamente cualquier aplicación que proporciona una API de aprovisionamiento de usuarios REST o SOAP.</span><span class="sxs-lookup"><span data-stu-id="768dc-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="768dc-161">Aquí le mostramos cómo funciona:</span><span class="sxs-lookup"><span data-stu-id="768dc-161">Here’s how it works:</span></span>

1. <span data-ttu-id="768dc-162">Azure AD proporciona una biblioteca de infraestructura de lenguaje común conocida como [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="768dc-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="768dc-163">Los desarrolladores y los integradores de sistemas pueden usar esta biblioteca para crear e implementar un punto de conexión de servicio web basado en SCIM capaz de conectar Azure AD a cualquier almacén de identidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="768dc-164">Las asignaciones se implementan en el servicio web para asignar el esquema de usuario estándar al esquema de usuario y el protocolo requerido por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="768dc-165">La dirección URL del punto de conexión está registrada en Azure AD como parte de una aplicación personalizada en la galería de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="768dc-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="768dc-166">Se asignan usuarios y grupos a esta aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="768dc-167">Tras la asignación, se colocan en una cola para sincronizarse con la aplicación de destino.</span><span class="sxs-lookup"><span data-stu-id="768dc-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="768dc-168">El proceso de sincronización que controla la cola se ejecuta cada 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="768dc-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="768dc-169">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="768dc-169">Code Samples</span></span>
<span data-ttu-id="768dc-170">Para facilitar este proceso, se proporciona un conjunto de [ejemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) que crean un punto de conexión de servicio web SCIM y demuestran el aprovisionamiento automático.</span><span class="sxs-lookup"><span data-stu-id="768dc-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="768dc-171">Uno de los ejemplos es de un proveedor que mantiene un archivo con filas de valores separados por comas que representan a usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="768dc-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="768dc-172">El otro es de un proveedor que funciona en el servicio de identidad y administración de acceso de Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="768dc-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="768dc-173">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="768dc-173">**Prerequisites**</span></span>

* <span data-ttu-id="768dc-174">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="768dc-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="768dc-175">SDK de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="768dc-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="768dc-176">Equipo de Windows que admite el ASP.NET framework 4.5 que se usará como punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="768dc-177">Este equipo debe ser accesible desde la nube</span><span class="sxs-lookup"><span data-stu-id="768dc-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="768dc-178">Una suscripción de Azure con una versión de prueba o con licencia de Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="768dc-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="768dc-179">El ejemplo de Amazon AWS requiere bibliotecas de [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="768dc-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="768dc-180">Para más información, consulte el archivo Léame incluido con el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="768dc-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="768dc-181">Introducción</span><span class="sxs-lookup"><span data-stu-id="768dc-181">Getting Started</span></span>
<span data-ttu-id="768dc-182">Es la manera más fácil de implementar un punto de conexión SCIM que puede aceptar las solicitudes de aprovisionamiento de Azure AD para compilar e implementar el ejemplo de código que genera los usuarios aprovisionados en un archivo de valores separados por comas (CSV).</span><span class="sxs-lookup"><span data-stu-id="768dc-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="768dc-183">**Para crear un punto de conexión SCIM de ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="768dc-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="768dc-184">Descargue el paquete de ejemplo de código en [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="768dc-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="768dc-185">Descomprima el paquete y colóquelo en un equipo con Windows, en una ubicación como C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="768dc-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="768dc-186">En esta carpeta, abra la solución FileProvisioningAgent en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="768dc-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="768dc-187">Seleccione **Herramientas > Administrador de paquetes de la biblioteca > Consola del administrador de paquetes** y ejecute los siguientes comandos para que el proyecto FileProvisioningAgent resuelva las referencias de la solución:</span><span class="sxs-lookup"><span data-stu-id="768dc-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="768dc-188">Genere el proyecto FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="768dc-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="768dc-189">Inicie la aplicación Símbolo del sistema de Windows (como administrador) y use el comando **cd** para cambiar el directorio a la carpeta **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**.</span><span class="sxs-lookup"><span data-stu-id="768dc-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="768dc-190">Ejecute el comando siguiente y reemplace <ip-address> por la dirección IP o el nombre de dominio de la máquina Windows:</span><span class="sxs-lookup"><span data-stu-id="768dc-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="768dc-191">En Windows, en **Configuración de Windows > Configuración de Internet y red**, seleccione **Firewall de Windows > Configuración avanzada** y cree una **regla de entrada** que permita el acceso de entrada al puerto 9000.</span><span class="sxs-lookup"><span data-stu-id="768dc-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="768dc-192">Si el equipo Windows está detrás de un enrutador, este debe configurarse para realizar la traducción de acceso de red entre su puerto 9000 que está expuesto a Internet y el puerto 9000 en el equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="768dc-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="768dc-193">Esto es necesario para que Azure AD pueda tener acceso a este punto de conexión en la nube.</span><span class="sxs-lookup"><span data-stu-id="768dc-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="768dc-194">**Para registrar el punto de conexión SCIM de ejemplo en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="768dc-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="768dc-195">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="768dc-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="768dc-196">Vaya a **Azure Active Directory > Aplicaciones empresariales y seleccione **Nueva aplicación > Todas > Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="768dc-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="768dc-197">Escriba un nombre para la aplicación y haga clic en el icono **Agregar** para crear un objeto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="768dc-198">El objeto de la aplicación creado está diseñado para representar la aplicación de destino a la que va a aprovisionar y para la que va a implementar el inicio de sesión único, no solo el punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="768dc-199">En la pantalla resultante, seleccione la pestaña **Aprovisionamiento** en la columna izquierda.</span><span class="sxs-lookup"><span data-stu-id="768dc-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="768dc-200">En el menú **Modo de aprovisionamiento**, seleccione **Automático**.</span><span class="sxs-lookup"><span data-stu-id="768dc-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="768dc-201">![][2]
  *Figura 4: configuración del aprovisionamiento en Azure Portal*</span><span class="sxs-lookup"><span data-stu-id="768dc-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="768dc-202">En el campo **URL de inquilino**, escriba la dirección URL expuesta a Internet y el puerto del punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="768dc-203">Sería algo como http://testmachine.contoso.com:9000 o http://<ip-address>:9000/, donde <ip-address> es la dirección IP expuesta a Internet.</span><span class="sxs-lookup"><span data-stu-id="768dc-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="768dc-204">Si el punto de conexión SCIM requiere un token de portador OAuth de un emisor que no sea Azure AD, copie el token de portador OAuth necesario en el campo **Token secreto**.</span><span class="sxs-lookup"><span data-stu-id="768dc-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="768dc-205">Si se deja este campo en blanco, Azure AD incluirá un token de portador OAuth emitido desde Azure AD con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="768dc-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="768dc-206">Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="768dc-207">Haga clic en el botón **Probar conexión** para que Azure Active Directory intente conectarse al punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="768dc-208">Si se produce un error en los intentos, se muestra información de error.</span><span class="sxs-lookup"><span data-stu-id="768dc-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="768dc-209">Si se produce la conexión, a continuación, haga clic en **Guardar** para guardar las credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="768dc-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="768dc-210">En la sección **Asignaciones**, hay dos conjuntos seleccionables de asignaciones de atributos: uno para los objetos de usuario y otro para los objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="768dc-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="768dc-211">Seleccione cada uno de ellos para revisar los atributos que se sincronizan desde Azure Active Directory a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="768dc-212">Los atributos seleccionados como propiedades de **Coincidencia** se usan para buscar coincidencias con los usuarios y grupos de la aplicación con el objetivo de realizar operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="768dc-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="768dc-213">Seleccione el botón Guardar para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="768dc-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="768dc-214">En **Configuración**, el campo **Ámbito** define qué usuarios y grupos se sincronizan.</span><span class="sxs-lookup"><span data-stu-id="768dc-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="768dc-215">Al seleccionar "Sync only assigned users and groups" (Sincronizar solo los usuarios y grupos asignados) (recomendado) solo sincronizará los usuarios y grupos asignados en la pestaña **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="768dc-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="768dc-216">Una vez completada la configuración, cambie el **Estado de aprovisionamiento** a **On** (Activo).</span><span class="sxs-lookup"><span data-stu-id="768dc-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="768dc-217">Haga clic en **Guardar** para iniciar el servicio de aprovisionamiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="768dc-218">Al sincronizar solo los usuarios y grupos asignados (recomendado), no olvide seleccionar la pestaña **Usuarios y grupos** y asigne los usuarios o grupos que se van a sincronizar.</span><span class="sxs-lookup"><span data-stu-id="768dc-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="768dc-219">Una vez que haya iniciado la sincronización inicial, puede utilizar la pestaña **Registros de auditoría** para supervisar el progreso, con lo que se muestran todas las acciones realizadas por el servicio de aprovisionamiento en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="768dc-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="768dc-220">Para más información sobre cómo leer los registros de aprovisionamiento de Azure AD, consulte el tutorial de [Creación de informes sobre el aprovisionamiento automático de cuentas de usuario](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="768dc-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="768dc-221">El último paso en la comprobación del ejemplo es abrir el archivo TargetFile.csv en la carpeta \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug en el equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="768dc-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="768dc-222">Una vez que se ejecuta el proceso de aprovisionamiento, este archivo muestra los detalles de todos los usuarios y grupos asignados y aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="768dc-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="768dc-223">Bibliotecas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="768dc-223">Development libraries</span></span>
<span data-ttu-id="768dc-224">Para desarrollar su propio servicio web que cumpla la especificación SCIM, familiarícese primero con las siguientes bibliotecas proporcionadas por Microsoft para ayudar a acelerar el proceso de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="768dc-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="768dc-225">Se ofrecen bibliotecas de Common Language Infrastructure (CLI) que se pueden usar con lenguajes basados en dicha infraestructura, como C#.</span><span class="sxs-lookup"><span data-stu-id="768dc-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="768dc-226">Una de esas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara una interfaz Microsoft.SystemForCrossDomainIdentityManagement.IProvider, que se muestra en la ilustración siguiente: un desarrollador que utiliza las bibliotecas implementaría esa interfaz con una clase a la que se puede hacer referencia, de forma genérica, como un proveedor.</span><span class="sxs-lookup"><span data-stu-id="768dc-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="768dc-227">Las bibliotecas permiten al programador implementar un servicio web que se ajusta a la especificación SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="768dc-228">El servicio web se puede hospedar en Internet Information Services o en cualquier ensamblado ejecutable de Common Language Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="768dc-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="768dc-229">La solicitud se traduce en llamadas a los métodos del proveedor, que pueden ser programadas por el desarrollador para operar en un almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="768dc-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="768dc-230">Los [controladores de ruta Express](http://expressjs.com/guide/routing.html) están disponibles para analizar los objetos de solicitud de node.js que representan llamadas (tal y como se define en la especificación SCIM), realizadas a un servicio web de node.js.</span><span class="sxs-lookup"><span data-stu-id="768dc-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="768dc-231">Creación de un punto de conexión SCIM personalizado</span><span class="sxs-lookup"><span data-stu-id="768dc-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="768dc-232">Mediante las bibliotecas CLI, los desarrolladores que usan dichas bibliotecas pueden hospedar sus servicios en cualquier ensamblado ejecutable de Common Language Infrastructure, o bien en Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="768dc-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="768dc-233">Este es el código de ejemplo para hospedar un servicio dentro de un ensamblado ejecutable, en la dirección http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="768dc-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="768dc-234">Este servicio debe tener una dirección HTTP y un certificado de autenticación de servidor para el que la entidad de certificación raíz sea una de las siguientes:</span><span class="sxs-lookup"><span data-stu-id="768dc-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="768dc-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="768dc-235">CNNIC</span></span>
* <span data-ttu-id="768dc-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="768dc-236">Comodo</span></span>
* <span data-ttu-id="768dc-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="768dc-237">CyberTrust</span></span>
* <span data-ttu-id="768dc-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="768dc-238">DigiCert</span></span>
* <span data-ttu-id="768dc-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="768dc-239">GeoTrust</span></span>
* <span data-ttu-id="768dc-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="768dc-240">GlobalSign</span></span>
* <span data-ttu-id="768dc-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="768dc-241">Go Daddy</span></span>
* <span data-ttu-id="768dc-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="768dc-242">Verisign</span></span>
* <span data-ttu-id="768dc-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="768dc-243">WoSign</span></span>

<span data-ttu-id="768dc-244">Un certificado de autenticación de servidor puede enlazarse a un puerto en un host de Windows mediante la utilidad de shell de red siguiente:</span><span class="sxs-lookup"><span data-stu-id="768dc-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="768dc-245">En este caso, el valor proporcionado para el argumento certhash es la huella digital del certificado, mientras que el valor proporcionado para el argumento appid es un identificador único global arbitrario.</span><span class="sxs-lookup"><span data-stu-id="768dc-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="768dc-246">Para hospedar el servicio en Internet Information Services, un desarrollador crearía un ensamblado de biblioteca de código CLI con una clase denominada Inicio en el espacio de nombres predeterminado del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="768dc-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="768dc-247">Este es un ejemplo de este tipo de clase:</span><span class="sxs-lookup"><span data-stu-id="768dc-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="768dc-248">Control de la autenticación de puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="768dc-248">Handling endpoint authentication</span></span>
<span data-ttu-id="768dc-249">Las solicitudes de Azure Active Directory incluyen un token de portador de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="768dc-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="768dc-250">Cualquier servicio que reciba la solicitud debe autenticar al emisor como Azure Active Directory en nombre del inquilino de Azure Active Directory esperado, para el acceso al servicio web Graph de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="768dc-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="768dc-251">En el token, el emisor se identifica mediante una notificación ISS, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="768dc-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="768dc-252">En este ejemplo, la dirección base del valor de notificación, https://sts.windows.net, identifica Azure Active Directory como el emisor, mientras que el segmento de dirección relativa, cbb1a5ac f33b 45fa 9bf5 f37db0fed422, es un identificador único del inquilino de Azure Active Directory en cuyo nombre se ha emitido el token.</span><span class="sxs-lookup"><span data-stu-id="768dc-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="768dc-253">Si el token se emitió para acceder al servicio web Graph de Azure Active Directory, el identificador de dicho servicio, 00000002-0000-0000-c000-000000000000, debe estar en el valor de notificación aud del token.</span><span class="sxs-lookup"><span data-stu-id="768dc-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="768dc-254">Los desarrolladores que usan las bibliotecas de CLI proporcionadas por Microsoft para crear un servicio SCIM pueden autenticar las solicitudes de Azure Active Directory mediante el paquete Microsoft.Owin.Security.ActiveDirectory siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="768dc-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="768dc-255">En un proveedor, implemente la propiedad Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior; para ello, haga que devuelva un método al que llamar cuando se inicia el servicio:</span><span class="sxs-lookup"><span data-stu-id="768dc-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="768dc-256">Agregue el siguiente código a dicho método para que cualquier solicitud a cualquiera de los puntos de conexión del servicio se autentique como si tuviera un token emitido por Azure Active Directory en nombre de un inquilino especificado, para acceder al servicio web Graph de Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="768dc-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="768dc-257">Esquema de grupos y usuarios</span><span class="sxs-lookup"><span data-stu-id="768dc-257">User and group schema</span></span>
<span data-ttu-id="768dc-258">Azure Active Directory puede aprovisionar dos tipos de recursos a los servicios web SCIM.</span><span class="sxs-lookup"><span data-stu-id="768dc-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="768dc-259">Esos tipos de recursos son los usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="768dc-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="768dc-260">Los recursos de usuario se identifican mediante el identificador de esquema, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, que se incluye en esta especificación del protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="768dc-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="768dc-261">La asignación predeterminada de los atributos de los usuarios en Azure Active Directory a los atributos de los recursos de urn: ietf:params:scim:schemas:extension:enterprise:2.0:User se proporciona en la tabla 1, a continuación.</span><span class="sxs-lookup"><span data-stu-id="768dc-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="768dc-262">Los recursos del grupo se identifican mediante el identificador del esquema, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="768dc-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="768dc-263">En la Tabla 2 se muestra la asignación predeterminada de los atributos de los grupos en Azure Active Directory para los atributos de los recursos de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="768dc-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="768dc-264">Tabla 1: Asignación de atributos de usuario predeterminada</span><span class="sxs-lookup"><span data-stu-id="768dc-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="768dc-265">Usuario de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="768dc-265">Azure Active Directory user</span></span> | <span data-ttu-id="768dc-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="768dc-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="768dc-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="768dc-267">IsSoftDeleted</span></span> |<span data-ttu-id="768dc-268">active</span><span class="sxs-lookup"><span data-stu-id="768dc-268">active</span></span> |
| <span data-ttu-id="768dc-269">DisplayName</span><span class="sxs-lookup"><span data-stu-id="768dc-269">displayName</span></span> |<span data-ttu-id="768dc-270">DisplayName</span><span class="sxs-lookup"><span data-stu-id="768dc-270">displayName</span></span> |
| <span data-ttu-id="768dc-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="768dc-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="768dc-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="768dc-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="768dc-273">givenName</span><span class="sxs-lookup"><span data-stu-id="768dc-273">givenName</span></span> |<span data-ttu-id="768dc-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="768dc-274">name.givenName</span></span> |
| <span data-ttu-id="768dc-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="768dc-275">jobTitle</span></span> |<span data-ttu-id="768dc-276">título</span><span class="sxs-lookup"><span data-stu-id="768dc-276">title</span></span> |
| <span data-ttu-id="768dc-277">mail</span><span class="sxs-lookup"><span data-stu-id="768dc-277">mail</span></span> |<span data-ttu-id="768dc-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="768dc-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="768dc-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="768dc-279">mailNickname</span></span> |<span data-ttu-id="768dc-280">externalId</span><span class="sxs-lookup"><span data-stu-id="768dc-280">externalId</span></span> |
| <span data-ttu-id="768dc-281">manager</span><span class="sxs-lookup"><span data-stu-id="768dc-281">manager</span></span> |<span data-ttu-id="768dc-282">manager</span><span class="sxs-lookup"><span data-stu-id="768dc-282">manager</span></span> |
| <span data-ttu-id="768dc-283">mobile</span><span class="sxs-lookup"><span data-stu-id="768dc-283">mobile</span></span> |<span data-ttu-id="768dc-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="768dc-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="768dc-285">objectId</span><span class="sxs-lookup"><span data-stu-id="768dc-285">objectId</span></span> |<span data-ttu-id="768dc-286">id</span><span class="sxs-lookup"><span data-stu-id="768dc-286">id</span></span> |
| <span data-ttu-id="768dc-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="768dc-287">postalCode</span></span> |<span data-ttu-id="768dc-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="768dc-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="768dc-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="768dc-289">proxy-Addresses</span></span> |<span data-ttu-id="768dc-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="768dc-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="768dc-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="768dc-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="768dc-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="768dc-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="768dc-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="768dc-293">streetAddress</span></span> |<span data-ttu-id="768dc-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="768dc-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="768dc-295">surname</span><span class="sxs-lookup"><span data-stu-id="768dc-295">surname</span></span> |<span data-ttu-id="768dc-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="768dc-296">name.familyName</span></span> |
| <span data-ttu-id="768dc-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="768dc-297">telephone-Number</span></span> |<span data-ttu-id="768dc-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="768dc-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="768dc-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="768dc-299">user-PrincipalName</span></span> |<span data-ttu-id="768dc-300">userName</span><span class="sxs-lookup"><span data-stu-id="768dc-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="768dc-301">Tabla 2: Asignación de atributos de grupo predeterminada</span><span class="sxs-lookup"><span data-stu-id="768dc-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="768dc-302">Grupo de Azure Active Directory </span><span class="sxs-lookup"><span data-stu-id="768dc-302">Azure Active Directory group</span></span> | <span data-ttu-id="768dc-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="768dc-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="768dc-304">DisplayName</span><span class="sxs-lookup"><span data-stu-id="768dc-304">displayName</span></span> |<span data-ttu-id="768dc-305">externalId</span><span class="sxs-lookup"><span data-stu-id="768dc-305">externalId</span></span> |
| <span data-ttu-id="768dc-306">mail</span><span class="sxs-lookup"><span data-stu-id="768dc-306">mail</span></span> |<span data-ttu-id="768dc-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="768dc-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="768dc-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="768dc-308">mailNickname</span></span> |<span data-ttu-id="768dc-309">DisplayName</span><span class="sxs-lookup"><span data-stu-id="768dc-309">displayName</span></span> |
| <span data-ttu-id="768dc-310">members</span><span class="sxs-lookup"><span data-stu-id="768dc-310">members</span></span> |<span data-ttu-id="768dc-311">members</span><span class="sxs-lookup"><span data-stu-id="768dc-311">members</span></span> |
| <span data-ttu-id="768dc-312">objectId</span><span class="sxs-lookup"><span data-stu-id="768dc-312">objectId</span></span> |<span data-ttu-id="768dc-313">id</span><span class="sxs-lookup"><span data-stu-id="768dc-313">id</span></span> |
| <span data-ttu-id="768dc-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="768dc-314">proxyAddresses</span></span> |<span data-ttu-id="768dc-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="768dc-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="768dc-316">Aprovisionamiento y cancelación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="768dc-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="768dc-317">La siguiente ilustración muestra los mensajes que Azure Active Directory enviará a un servicio SCIM para administrar el ciclo de vida de un usuario en otro almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="768dc-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="768dc-318">El diagrama también muestra cómo un servicio SCIM implementado mediante las bibliotecas CLI proporcionadas por Microsoft para la creación de dichos servicios traducirá esas solicitudes a llamadas a los métodos de un proveedor.</span><span class="sxs-lookup"><span data-stu-id="768dc-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="768dc-319">![][4]
*Figura 5: secuencia de aprovisionamiento y cancelación de aprovisionamiento de usuarios*</span><span class="sxs-lookup"><span data-stu-id="768dc-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="768dc-320">Azure Active Directory consulta el servicio para un usuario con un valor de atributo externalId que coincida con el valor de atributo mailNickname de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="768dc-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="768dc-321">La consulta se expresa como una solicitud de Protocolo de transferencia de hipertexto (HTTP) como la de este ejemplo, donde jyoung es un ejemplo de un mailNickname de un usuario en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="768dc-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="768dc-322">Si el servicio se creó mediante las bibliotecas de Common Language Infrastructure proporcionadas por Microsoft para implementar servicios SCIM, la solicitud se traduce en una llamada al método Query del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="768dc-323">Esta es la firma de ese método:</span><span class="sxs-lookup"><span data-stu-id="768dc-323">Here is the signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="768dc-324">Esta es la definición de la interfaz de Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="768dc-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="768dc-325">En el ejemplo anterior de una consulta para un usuario con un valor especificado para el atributo externalId, los valores de los argumentos pasados al método Query serán los siguientes:</span><span class="sxs-lookup"><span data-stu-id="768dc-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="768dc-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="768dc-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="768dc-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="768dc-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="768dc-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="768dc-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="768dc-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="768dc-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="768dc-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="768dc-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="768dc-331">Si la respuesta a una consulta al servicio web relativa a un usuario con un valor de atributo externalId que coincide con el valor de atributo mailNickname de un usuario no devuelve ningún usuario, Azure Active Directory solicita al servicio que aprovisione un usuario correspondiente al de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="768dc-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="768dc-332">Este es un ejemplo de dicha solicitud:</span><span class="sxs-lookup"><span data-stu-id="768dc-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="768dc-333">Las bibliotecas de Common Language Infrastructure proporcionadas por Microsoft para implementar servicios SCIM traduciría esa solicitud a una llamada al método Create del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="768dc-334">El método Create tiene esta firma:</span><span class="sxs-lookup"><span data-stu-id="768dc-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="768dc-335">En el caso de una solicitud de aprovisionamiento de un usuario, el valor del argumento del recurso es una instancia de Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="768dc-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="768dc-336">Clase Core2EnterpriseUser, definida en la biblioteca Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="768dc-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="768dc-337">Si la solicitud para aprovisionar el usuario se realiza correctamente, la implementación del método debería devolver una instancia de Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="768dc-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="768dc-338">Clase Core2EnterpriseUser, con el valor de la propiedad Identifier establecido en el identificador único del usuario recién aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="768dc-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="768dc-339">Para actualizar un usuario que se sabe que existe en un almacén de identidades dirigido por un SCIM, Azure Active Directory solicita el estado actual de dicho usuario desde el servicio con una solicitud como esta:</span><span class="sxs-lookup"><span data-stu-id="768dc-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="768dc-340">En un servicio creado mediante las bibliotecas Common Language Infrastructure proporcionadas por Microsoft para implementar servicios SCIM, la solicitud se traduce a una llamada al método Retrieve del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="768dc-341">Esta es la firma del método Retrieve:</span><span class="sxs-lookup"><span data-stu-id="768dc-341">Here is the signature of the Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="768dc-342">En el ejemplo anterior de una solicitud para recuperar el estado actual de un usuario, los valores de las propiedades del objeto proporcionados como el valor del argumento parameters son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="768dc-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="768dc-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="768dc-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="768dc-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="768dc-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="768dc-345">Si se va a actualizar un atributo de referencia, Azure Active Directory consulta el servicio para determinar si el valor actual del atributo de referencia en el almacén de identidades dirigido por el servicio ya coincide con el valor de dicho atributo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="768dc-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="768dc-346">Para los usuarios, el único atributo del que se va a consultar el valor actual de esta manera es el atributo manager.</span><span class="sxs-lookup"><span data-stu-id="768dc-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="768dc-347">Este es un ejemplo de una solicitud para determinar si el atributo de administrador de un determinado objeto de usuario tiene actualmente un determinado valor:</span><span class="sxs-lookup"><span data-stu-id="768dc-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="768dc-348">El valor del parámetro de consulta de atributos, id, significa que si existe un objeto de usuario que cumple la expresión especificada como el valor del parámetro de consulta filter, se espera que el servicio responda con un recurso urn:ietf:params:scim:schemas:core:2.0:User o urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, incluido solo el valor del atributo id de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="768dc-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="768dc-349">El solicitante conoce el valor del atributo **id**.</span><span class="sxs-lookup"><span data-stu-id="768dc-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="768dc-350">Se incluye en el valor del parámetro de consulta filter; el propósito de solicitarlo en realidad es solicitar una representación mínima de un recurso que cumpla la expresión de filtro como una indicación de si existe o no tal objeto.</span><span class="sxs-lookup"><span data-stu-id="768dc-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="768dc-351">Si el servicio se creó mediante las bibliotecas de Common Language Infrastructure proporcionadas por Microsoft para implementar servicios SCIM, la solicitud se traduce en una llamada al método Query del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="768dc-352">El valor de las propiedades del objeto proporcionado como el valor del argumento parameters es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="768dc-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="768dc-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="768dc-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="768dc-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="768dc-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="768dc-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="768dc-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="768dc-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="768dc-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="768dc-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="768dc-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="768dc-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="768dc-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="768dc-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="768dc-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="768dc-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="768dc-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="768dc-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="768dc-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="768dc-362">En este caso, el valor del índice x puede ser 0 y el valor del índice y puede ser 1, o bien el valor de x puede ser 1 y el valor de y puede ser 0, en función del orden de las expresiones del parámetro de consulta filter.</span><span class="sxs-lookup"><span data-stu-id="768dc-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="768dc-363">A continuación se proporciona un ejemplo de una solicitud de Azure Active Directory a un servicio SCIM para actualizar un usuario:</span><span class="sxs-lookup"><span data-stu-id="768dc-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="768dc-364">Las bibliotecas de Microsoft Common Language Infrastructure para implementar servicios SCIM traducirían la solicitud de una llamada al método Update del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="768dc-365">Esta es la signatura del método Update:</span><span class="sxs-lookup"><span data-stu-id="768dc-365">Here is the signature of the Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="768dc-366">En el ejemplo de una solicitud para actualizar un usuario, el objeto proporcionado como el valor del argumento patch tiene estos valores de propiedad:</span><span class="sxs-lookup"><span data-stu-id="768dc-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="768dc-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="768dc-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="768dc-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="768dc-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="768dc-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="768dc-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="768dc-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="768dc-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="768dc-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="768dc-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="768dc-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="768dc-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="768dc-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="768dc-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="768dc-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="768dc-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="768dc-375">Para cancelar el aprovisionamiento de un usuario de un almacén de identidades dirigido por un servicio SCIM, Azure AD envía una solicitud como esta:</span><span class="sxs-lookup"><span data-stu-id="768dc-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="768dc-376">Si el servicio se creó mediante las bibliotecas Common Language Infrastructure proporcionadas por Microsoft para implementar servicios SCIM, la solicitud se traduce a una llamada al método Delete del proveedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="768dc-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="768dc-377">Este método tiene esta firma:</span><span class="sxs-lookup"><span data-stu-id="768dc-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="768dc-378">El objeto proporcionado como el valor del argumento resourceIdentifier tiene tendrá estos valores de propiedad en el ejemplo anterior de una solicitud de cancelación del aprovisionamiento de un usuario:</span><span class="sxs-lookup"><span data-stu-id="768dc-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="768dc-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="768dc-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="768dc-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="768dc-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="768dc-381">Aprovisionamiento y cancelación del aprovisionamiento de grupos</span><span class="sxs-lookup"><span data-stu-id="768dc-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="768dc-382">La siguiente ilustración muestra los mensajes que Azure AD envía a un servicio SCIM para administrar el ciclo de vida de un grupo en otro almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="768dc-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="768dc-383">Esos mensajes se diferencian de los mensajes que pertenecen a los usuarios de tres maneras:</span><span class="sxs-lookup"><span data-stu-id="768dc-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="768dc-384">El esquema de un recurso de grupo se identifica como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="768dc-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="768dc-385">Las solicitudes para recuperar grupos estipulan que el atributo members se excluya de cualquier recurso proporcionado en respuesta a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="768dc-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="768dc-386">Las solicitudes para determinar si un atributo de referencia tiene un valor determinado son solicitudes sobre el atributo members.</span><span class="sxs-lookup"><span data-stu-id="768dc-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="768dc-387">![][5]
*Figura 6: secuencia de aprovisionamiento y cancelación del aprovisionamiento de grupos*</span><span class="sxs-lookup"><span data-stu-id="768dc-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="768dc-388">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="768dc-388">Related articles</span></span>
* [<span data-ttu-id="768dc-389">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="768dc-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="768dc-390">Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="768dc-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="768dc-391">Personalización de asignaciones de atributos para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="768dc-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="768dc-392">Escritura de expresiones para asignaciones de atributos</span><span class="sxs-lookup"><span data-stu-id="768dc-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="768dc-393">Filtros de ámbito para el aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="768dc-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="768dc-394">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="768dc-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="768dc-395">Lista de tutoriales sobre cómo integrar aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="768dc-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
