---
title: "aaaUsing sistema de administración de identidades entre dominios aprovisionar automáticamente a los usuarios y grupos de Azure Active Directory tooapplications | Documentos de Microsoft"
description: "Azure Active Directory pueda aprovisionar automáticamente a los usuarios y grupos tooany identidad o aplicación almacén que está representado por un servicio web con interfaz Hola definido en la especificación del protocolo SCIM Hola"
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
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="8281a-103">Usa el sistema para los usuarios de administración de identidades entre dominios tooautomatically aprovisionar y grupos de Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="8281a-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="8281a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8281a-104">Overview</span></span>
<span data-ttu-id="8281a-105">Azure Active Directory (Azure AD) pueden aprovisionar automáticamente a los usuarios y grupos tooany identidad o aplicación almacén que está representado por un servicio web con interfaz de hello definida en hello [System para entre dominios Identity Management (SCIM) 2.0 especificación del protocolo](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="8281a-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="8281a-106">Azure Active Directory puede enviar solicitudes toocreate, modificar o eliminar asignado servicio de web toohello usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="8281a-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="8281a-107">servicio web de Hello, a continuación, puede convertir las solicitudes en las operaciones en el almacén de identidades de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8281a-108">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8281a-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="8281a-109">![][0]
*Figura 1: Aprovisionamiento de almacén de identidades de Azure Active Directory tooan a través de un servicio web*</span><span class="sxs-lookup"><span data-stu-id="8281a-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="8281a-110">Esta capacidad se puede utilizar junto con capacidad de "traiga su propia aplicación" hello en Azure AD tooenable single sign-on y para las aplicaciones que proporcionan o representadas por un servicio web SCIM el aprovisionamiento automático de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8281a-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="8281a-111">Existen dos casos de uso de SCIM en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="8281a-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="8281a-112">**Aprovisionamiento de usuarios y grupos tooapplications que admiten SCIM** aplicaciones que admiten SCIM 2.0 y usar tokens de portador OAuth para la autenticación funciona con Azure AD sin necesidad de configuración.</span><span class="sxs-lookup"><span data-stu-id="8281a-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="8281a-113">**Crear su propia solución de aprovisionamiento de aplicaciones compatibles con otros aprovisionamiento basado en la API** para las aplicaciones no SCIM, puede crear un tootranslate de punto de conexión SCIM entre el punto de conexión de Azure AD SCIM hello y cualquier aplicación de Hola de API es compatible con para el aprovisionamiento de usuario.</span><span class="sxs-lookup"><span data-stu-id="8281a-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="8281a-114">toohelp desarrollar un punto de conexión SCIM, se proporcionan las bibliotecas de Common Language Infrastructure (CLI) junto con ejemplos de código que muestran cómo toodo proporcionan un punto de conexión SCIM y traducir los mensajes de SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="8281a-115">Aprovisionamiento de usuarios y grupos tooapplications que admiten SCIM</span><span class="sxs-lookup"><span data-stu-id="8281a-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="8281a-116">Azure AD puede ser configurado tooautomatically aprovisionar asignado a los usuarios y grupos tooapplications que implementan un [sistema de administración de identidades entre dominios 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) servicio web y acepta los tokens de portador de OAuth para la autenticación .</span><span class="sxs-lookup"><span data-stu-id="8281a-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="8281a-117">Dentro de la especificación de hello SCIM 2.0, las aplicaciones deben cumplir estos requisitos:</span><span class="sxs-lookup"><span data-stu-id="8281a-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="8281a-118">Admite la creación de usuarios o grupos, según la sección 3.3 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="8281a-119">Admite la modificación de los usuarios o grupos con las solicitudes de revisión según la sección 3.5.2 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="8281a-120">Admite la recuperación de un recurso conocido según la sección 3.4.1 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="8281a-121">Admite consultas de usuarios o grupos, de acuerdo con el punto 3.4.2 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="8281a-122">De forma predeterminada, los usuarios se consultan por externalId y los grupos por displayName.</span><span class="sxs-lookup"><span data-stu-id="8281a-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="8281a-123">Admite consultas de usuario con el identificador y Administrador de acuerdo con el punto 3.4.2 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="8281a-124">Permite consultar los grupos por Id. y miembro según la sección 3.4.2 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="8281a-125">Acepta los tokens de portador de OAuth para la autorización según la sección 2.1 de hello protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="8281a-126">Consulte a su proveedor de la aplicación o la documentación que se incluye con la aplicación para ver si existen declaraciones de compatibilidad con estos requisitos.</span><span class="sxs-lookup"><span data-stu-id="8281a-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="8281a-127">Introducción</span><span class="sxs-lookup"><span data-stu-id="8281a-127">Getting started</span></span>
<span data-ttu-id="8281a-128">Las aplicaciones que admiten el perfil SCIM Hola se describe en este artículo pueden ser conectado tooAzure Active Directory mediante la característica de "aplicación distinta de la Galería" hello en Galería de aplicaciones de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="8281a-129">Una vez conectado, Azure AD se ejecuta un proceso de sincronización cada 20 minutos donde consulta punto de conexión de la aplicación hello SCIM para asigna usuarios y grupos y crea o modifica ellos según toohello detalles de asignación.</span><span class="sxs-lookup"><span data-stu-id="8281a-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="8281a-130">**una aplicación que admita SCIM tooconnect:**</span><span class="sxs-lookup"><span data-stu-id="8281a-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="8281a-131">Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8281a-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="8281a-132">Examinar demasiado ** Azure Active Directory > aplicaciones empresariales y seleccione **nueva aplicación > todos los > aplicación no gallery**.</span><span class="sxs-lookup"><span data-stu-id="8281a-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="8281a-133">Escriba un nombre para la aplicación y haga clic en **agregar** icono toocreate un objeto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8281a-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="8281a-134">![][1]
  *Figura 2: galería de aplicaciones de Azure AD*</span><span class="sxs-lookup"><span data-stu-id="8281a-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="8281a-135">En la pantalla resultante de bienvenida, seleccione hello **Provisioning** pestaña en la columna izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="8281a-136">Hola **modo de aprovisionamiento** menú, seleccione **automática**.</span><span class="sxs-lookup"><span data-stu-id="8281a-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="8281a-137">![][2]
  *Figura 3: Configurar el aprovisionamiento en hello portal de Azure*</span><span class="sxs-lookup"><span data-stu-id="8281a-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="8281a-138">Hola **dirección URL del inquilino** , escriba la dirección URL de Hola de punto de conexión de la aplicación hello SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="8281a-139">Ejemplo: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="8281a-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="8281a-140">Si el punto de conexión de hello SCIM requiere un token de portador de OAuth de un emisor que no sea de Azure AD, Hola copia requeridos token de portador OAuth en hello opcional **secreto Token** campo.</span><span class="sxs-lookup"><span data-stu-id="8281a-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="8281a-141">Si este campo se deja en blanco, Azure AD incluye un token de portador OAuth emitido desde Azure AD con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="8281a-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="8281a-142">Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="8281a-143">Haga clic en hello **Probar conexión** botón toohave Azure Active Directory intento tooconnect toohello SCIM punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8281a-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="8281a-144">Si se produce un error en los intentos de hello, se muestra información de error.</span><span class="sxs-lookup"><span data-stu-id="8281a-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="8281a-145">Si Hola intentos tooconnect toohello aplicación se realiza correctamente, a continuación, haga clic en **guardar** credenciales de administrador de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="8281a-146">Hola **asignaciones** sección, hay dos conjuntos seleccionables de asignaciones de atributos: uno para objetos de usuario y otro para los objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="8281a-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="8281a-147">Seleccione cada uno atributos de Hola de tooreview que se sincronizan desde la aplicación de Azure Active Directory tooyour.</span><span class="sxs-lookup"><span data-stu-id="8281a-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="8281a-148">Hola atributos seleccionados como **coincidencia** propiedades son utilizados toomatch Hola usuarios y grupos en su aplicación para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="8281a-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="8281a-149">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="8281a-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8281a-150">Opcionalmente, puede deshabilitar la sincronización de objetos de grupo deshabilitando Hola "grupos" asignación.</span><span class="sxs-lookup"><span data-stu-id="8281a-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="8281a-151">En **configuración**, hello **ámbito** campo define qué usuarios y grupos están sincronizados.</span><span class="sxs-lookup"><span data-stu-id="8281a-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="8281a-152">Al seleccionar "Sincronización solo asigna usuarios y grupos" (recomendado) solo sincronizará los usuarios y grupos asignados en hello **usuarios y grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="8281a-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="8281a-153">Una vez completada la configuración, cambiar hello **estado de aprovisionamiento** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="8281a-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="8281a-154">Haga clic en **guardar** toostart Hola servicio de aprovisionamiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="8281a-155">Si sincronizar solo asigna usuarios y grupos (recomendados), ser seguro hello tooselect **usuarios y grupos** pestaña y asigne los usuarios de Hola o grupos que desea toosync.</span><span class="sxs-lookup"><span data-stu-id="8281a-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="8281a-156">Una vez que se inició la sincronización inicial de hello, puede usar hello **registros de auditoría** ficha toomonitor progreso, que muestra todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8281a-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="8281a-157">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8281a-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="8281a-158">la sincronización inicial Hola toma tooperform más que las sincronizaciones posteriores, que se producen aproximadamente cada 20 minutos mientras se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="8281a-159">Creación de una solución de aprovisionamiento propia para cualquier aplicación</span><span class="sxs-lookup"><span data-stu-id="8281a-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="8281a-160">Al crear un servicio web SCIM que interactúa con Azure Active Directory, puede habilitar el inicio de sesión único y el aprovisionamiento automático de usuarios para prácticamente cualquier aplicación que proporciona una API de aprovisionamiento de usuarios REST o SOAP.</span><span class="sxs-lookup"><span data-stu-id="8281a-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="8281a-161">Aquí le mostramos cómo funciona:</span><span class="sxs-lookup"><span data-stu-id="8281a-161">Here’s how it works:</span></span>

1. <span data-ttu-id="8281a-162">Azure AD proporciona una biblioteca de infraestructura de lenguaje común conocida como [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="8281a-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="8281a-163">Los desarrolladores e integradores de sistema pueden usar esta biblioteca toocreate e implementar un extremo de servicio web basado en SCIM capaz de conectar el almacén de identidades de la aplicación de Azure AD tooany.</span><span class="sxs-lookup"><span data-stu-id="8281a-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="8281a-164">Las asignaciones se implementan en hello web servicio toomap Hola usuario estandarizado toohello usuario de esquema y protocolo requerido por la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8281a-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="8281a-165">dirección URL del extremo Hola está registrado en Azure AD como parte de una aplicación personalizada en la Galería de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="8281a-166">Usuarios y grupos se asignan toothis aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="8281a-167">Tras la asignación, se colocan en una aplicación de destino de cola toobe sincronizado toohello.</span><span class="sxs-lookup"><span data-stu-id="8281a-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="8281a-168">proceso de sincronización de Hello control cola Hola se ejecuta cada 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="8281a-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="8281a-169">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="8281a-169">Code Samples</span></span>
<span data-ttu-id="8281a-170">toomake esto, procesar un conjunto de [ejemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) son siempre que cree un extremo del servicio web SCIM y demostrar el aprovisionamiento automático.</span><span class="sxs-lookup"><span data-stu-id="8281a-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="8281a-171">Uno de los ejemplos es de un proveedor que mantiene un archivo con filas de valores separados por comas que representan a usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="8281a-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="8281a-172">Hola otro es de un proveedor que funciona en el servicio de Amazon Web Services Identity and Access Management Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="8281a-173">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="8281a-173">**Prerequisites**</span></span>

* <span data-ttu-id="8281a-174">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8281a-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="8281a-175">SDK de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="8281a-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="8281a-176">Equipo de Windows que admita Hola ASP.NET framework 4.5 toobe utiliza como Hola extremo SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="8281a-177">Este equipo debe ser accesible desde la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="8281a-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="8281a-178">Una suscripción de Azure con una versión de prueba o con licencia de Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="8281a-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="8281a-179">ejemplo de Hola a Amazon AWS requiere bibliotecas de hello [AWS Toolkit para Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="8281a-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="8281a-180">Para obtener más información, vea Hola Léame archivo incluido con el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="8281a-181">Introducción</span><span class="sxs-lookup"><span data-stu-id="8281a-181">Getting Started</span></span>
<span data-ttu-id="8281a-182">tooimplement Hola de manera más fácil solicita un punto de conexión SCIM que puede aceptar el aprovisionamiento de Azure AD es toobuild e implementar el ejemplo de código de hello que genera el archivo de valores separados por comas (CSV) de hello los usuarios aprovisionados tooa.</span><span class="sxs-lookup"><span data-stu-id="8281a-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="8281a-183">**un punto de conexión de ejemplo SCIM toocreate:**</span><span class="sxs-lookup"><span data-stu-id="8281a-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="8281a-184">Descargar paquete de ejemplo de código de hello en [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="8281a-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="8281a-185">Descomprima el paquete de Hola y lo coloca en el equipo de Windows en una ubicación como C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="8281a-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="8281a-186">En esta carpeta, iniciar solución de FileProvisioningAgent de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8281a-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="8281a-187">Seleccione **Herramientas > Administrador de paquetes de biblioteca > Package Manager Console**y ejecute hello siguientes comandos para hello FileProvisioningAgent tooresolve Hola solución las referencias del proyecto:</span><span class="sxs-lookup"><span data-stu-id="8281a-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="8281a-188">Compile hello FileProvisioningAgent proyecto.</span><span class="sxs-lookup"><span data-stu-id="8281a-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="8281a-189">Iniciar la aplicación de línea de comandos de hello en Windows (como administrador) y usar hello **cd** comando toochange Hola directorio tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** carpeta.</span><span class="sxs-lookup"><span data-stu-id="8281a-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="8281a-190">Ejecute hello siguiente comando, sustituyendo < dirección ip > Hola IP dirección o nombre de dominio de la máquina de Windows hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="8281a-191">En Windows en **configuración de Windows > configuración de Internet y red**, seleccione hello **Firewall de Windows > Configuración avanzada**y crear un **Inbound Rule** que permite el acceso de entrada tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="8281a-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="8281a-192">Si la máquina de Windows hello está detrás de un enrutador, Hola enrutador necesidades toobe configurado tooperform traducción de acceso de red entre su puerto 9000 que está expuesto toohello internet y el puerto 9000 en la máquina de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8281a-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="8281a-193">Esto es necesario para Azure AD toobe puede tooaccess este punto de conexión en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="8281a-194">**extremo de SCIM del ejemplo de Hola tooregister en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8281a-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="8281a-195">Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8281a-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="8281a-196">Examinar demasiado ** Azure Active Directory > aplicaciones empresariales y seleccione **nueva aplicación > todos los > aplicación no gallery**.</span><span class="sxs-lookup"><span data-stu-id="8281a-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="8281a-197">Escriba un nombre para la aplicación y haga clic en **agregar** icono toocreate un objeto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8281a-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="8281a-198">objeto de aplicación Hola creado es la aplicación de destino de hello toorepresent previsto se va a aprovisionar tooand implementar punto de conexión de hello único de inicio de sesión del mismo y no solamente SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="8281a-199">En la pantalla resultante de bienvenida, seleccione hello **Provisioning** pestaña en la columna izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="8281a-200">Hola **modo de aprovisionamiento** menú, seleccione **automática**.</span><span class="sxs-lookup"><span data-stu-id="8281a-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="8281a-201">![][2]
  *Figura 4: Configurar el aprovisionamiento en hello portal de Azure*</span><span class="sxs-lookup"><span data-stu-id="8281a-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="8281a-202">Hola **dirección URL del inquilino** , escriba la dirección URL de hello expuesta a internet y el puerto de su punto de conexión SCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="8281a-203">Esto sería algo como http://testmachine.contoso.com:9000 o http://<ip-address>:9000/, donde < dirección ip > es Hola internet expone IP dirección.</span><span class="sxs-lookup"><span data-stu-id="8281a-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="8281a-204">Si el punto de conexión de hello SCIM requiere un token de portador de OAuth de un emisor que no sea de Azure AD, Hola copia requeridos token de portador OAuth en hello opcional **secreto Token** campo.</span><span class="sxs-lookup"><span data-stu-id="8281a-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="8281a-205">Si se deja este campo en blanco, Azure AD incluirá un token de portador OAuth emitido desde Azure AD con cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="8281a-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="8281a-206">Las aplicaciones que usan Azure AD como un proveedor de identidades pueden validar este token emitido por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="8281a-207">Haga clic en hello **Probar conexión** botón toohave Azure Active Directory intento tooconnect toohello SCIM punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8281a-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="8281a-208">Si se produce un error en los intentos de hello, se muestra información de error.</span><span class="sxs-lookup"><span data-stu-id="8281a-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="8281a-209">Si Hola intentos tooconnect toohello aplicación se realiza correctamente, a continuación, haga clic en **guardar** credenciales de administrador de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="8281a-210">Hola **asignaciones** sección, hay dos conjuntos seleccionables de asignaciones de atributos: uno para objetos de usuario y otro para los objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="8281a-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="8281a-211">Seleccione cada uno atributos de Hola de tooreview que se sincronizan desde la aplicación de Azure Active Directory tooyour.</span><span class="sxs-lookup"><span data-stu-id="8281a-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="8281a-212">Hola atributos seleccionados como **coincidencia** propiedades son utilizados toomatch Hola usuarios y grupos en su aplicación para las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="8281a-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="8281a-213">Seleccione toocommit de botón de hello guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="8281a-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="8281a-214">En **configuración**, hello **ámbito** campo define qué usuarios y grupos están sincronizados.</span><span class="sxs-lookup"><span data-stu-id="8281a-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="8281a-215">Al seleccionar "Sincronización solo asigna usuarios y grupos" (recomendado) solo sincronizará los usuarios y grupos asignados en hello **usuarios y grupos** ficha.</span><span class="sxs-lookup"><span data-stu-id="8281a-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="8281a-216">Una vez completada la configuración, cambiar hello **estado de aprovisionamiento** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="8281a-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="8281a-217">Haga clic en **guardar** toostart Hola servicio de aprovisionamiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="8281a-218">Si sincronizar solo asigna usuarios y grupos (recomendados), ser seguro hello tooselect **usuarios y grupos** pestaña y asigne los usuarios de Hola o grupos que desea toosync.</span><span class="sxs-lookup"><span data-stu-id="8281a-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="8281a-219">Una vez que se inició la sincronización inicial de hello, puede usar hello **registros de auditoría** ficha toomonitor progreso, que muestra todas las acciones realizadas por hello aprovisionamiento del servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8281a-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="8281a-220">Para obtener más información sobre cómo registra el aprovisionamiento de tooread hello Azure AD, consulte [informes sobre el aprovisionamiento de cuentas de usuario automática](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8281a-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="8281a-221">Hola último paso en la comprobación de ejemplo de Hola es tooopen hello TargetFile.csv archivo en la carpeta de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug de hello en el equipo de Windows.</span><span class="sxs-lookup"><span data-stu-id="8281a-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="8281a-222">Una vez que se ejecuta el proceso de aprovisionamiento de hello, este archivo muestra detalles de Hola de todo asignan y aprovisionan de usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="8281a-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="8281a-223">Bibliotecas de desarrollo</span><span class="sxs-lookup"><span data-stu-id="8281a-223">Development libraries</span></span>
<span data-ttu-id="8281a-224">toodevelop su propio servicio web que cumple la especificación de SCIM toohello, primero familiarizarse con hello después bibliotecas proporcionados por Microsoft toohelp acelerar el proceso de desarrollo de hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="8281a-225">Se ofrecen bibliotecas de Common Language Infrastructure (CLI) que se pueden usar con lenguajes basados en dicha infraestructura, como C#.</span><span class="sxs-lookup"><span data-stu-id="8281a-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="8281a-226">Una de esas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara una interfaz Microsoft.SystemForCrossDomainIdentityManagement.IProvider, que se muestra en hello siguientes ilustración: A los desarrolladores que utilizan bibliotecas de hello implementaría esa interfaz con una clase que se puede hacer referencia, de forma genérica, como un proveedor.</span><span class="sxs-lookup"><span data-stu-id="8281a-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="8281a-227">bibliotecas de Hello permiten Hola developer toodeploy un servicio web que cumple la especificación de SCIM toohello.</span><span class="sxs-lookup"><span data-stu-id="8281a-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="8281a-228">servicio web de Hola o se puede hospedar en Internet Information Services o cualquier ensamblado ejecutable de Common Language Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="8281a-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="8281a-229">Solicitud se traduce a los métodos del proveedor de llamadas toohello, que se programan hello toooperate de desarrollador en un almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="8281a-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="8281a-230">[Express route controladores](http://expressjs.com/guide/routing.html) están disponibles para analizar objetos de solicitud de node.js que representan llamadas (según se define en hello especificación SCIM), realizadas el servicio web de node.js de tooa.</span><span class="sxs-lookup"><span data-stu-id="8281a-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="8281a-231">Creación de un punto de conexión SCIM personalizado</span><span class="sxs-lookup"><span data-stu-id="8281a-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="8281a-232">Utilizando las bibliotecas CLI de hello, los desarrolladores que utilizan dichas bibliotecas pueden hospedar sus servicios en cualquier ensamblado de Common Language Infrastructure ejecutable, o en Internet Information Services.</span><span class="sxs-lookup"><span data-stu-id="8281a-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="8281a-233">Este es el código de ejemplo para hospedar un servicio dentro de un ensamblado ejecutable, en la dirección de hello http://localhost: 9000:</span><span class="sxs-lookup"><span data-stu-id="8281a-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

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

<span data-ttu-id="8281a-234">Este servicio debe tener un certificado HTTP dirección y el servidor de autenticación del programa Hola a qué entidad de certificación raíz es uno de los siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="8281a-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="8281a-235">CNNIC</span></span>
* <span data-ttu-id="8281a-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="8281a-236">Comodo</span></span>
* <span data-ttu-id="8281a-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="8281a-237">CyberTrust</span></span>
* <span data-ttu-id="8281a-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="8281a-238">DigiCert</span></span>
* <span data-ttu-id="8281a-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="8281a-239">GeoTrust</span></span>
* <span data-ttu-id="8281a-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="8281a-240">GlobalSign</span></span>
* <span data-ttu-id="8281a-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="8281a-241">Go Daddy</span></span>
* <span data-ttu-id="8281a-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="8281a-242">Verisign</span></span>
* <span data-ttu-id="8281a-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="8281a-243">WoSign</span></span>

<span data-ttu-id="8281a-244">Un certificado de autenticación de servidor puede ser puerto tooa enlazados en un host de Windows mediante la utilidad de shell de red de hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="8281a-245">En este caso, valor de Hola proporcionado para el argumento de certhash hello es huella digital de hello del certificado de hello, mientras el valor de hello proporcionado para el argumento de appid hello es un identificador único global arbitrario.</span><span class="sxs-lookup"><span data-stu-id="8281a-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="8281a-246">servicio de hello toohost dentro de Internet Information Services, un desarrollador crearía un ensamblado de biblioteca de código CLA con una clase denominada inicio en hello espacio de nombres predeterminado del ensamblado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="8281a-247">Este es un ejemplo de este tipo de clase:</span><span class="sxs-lookup"><span data-stu-id="8281a-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="8281a-248">Control de la autenticación de puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="8281a-248">Handling endpoint authentication</span></span>
<span data-ttu-id="8281a-249">Las solicitudes de Azure Active Directory incluyen un token de portador de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8281a-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="8281a-250">Cualquier solicitud de servicio receptor Hola debería autenticar el emisor de hello como Azure Active Directory en nombre del inquilino de Azure Active Directory de hello esperada para acceso toohello servicio web de Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="8281a-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="8281a-251">En el token de hello, emisor Hola se identifica mediante una notificación de iss, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="8281a-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="8281a-252">En este ejemplo, la dirección base de hello del valor de notificación de hello, https://sts.windows.net, identifica Azure Active Directory como Hola emisor, mientras el segmento de dirección relativa, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello es un identificador único de hello Azure Active Inquilino de directorio en nombre de qué Hola token haya sido emitido.</span><span class="sxs-lookup"><span data-stu-id="8281a-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="8281a-253">Si Hola token haya sido emitido para el acceso a servicio de web de Azure Active Directory Graph hello, a continuación, identificador de Hola de dicho servicio, 00000002-0000-0000-c000-000000000000, debe ser en valor de Hola de aud del token de hello reclamar.</span><span class="sxs-lookup"><span data-stu-id="8281a-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="8281a-254">Los desarrolladores que utilizan bibliotecas CLA Hola proporcionadas por Microsoft para la creación de un servicio SCIM pueden autenticar las solicitudes de Azure Active Directory con el paquete Microsoft.Owin.Security.ActiveDirectory de hello siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8281a-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="8281a-255">En un proveedor, implemente la propiedad de Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de hello haciendo que se devuelva un toobe de método que se llama cada vez que se ha iniciado el servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

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

2. <span data-ttu-id="8281a-256">Agregue Hola después código toothat método toohave cualquier tooany de solicitud de puntos de conexión del servicio de hello autenticado como que lleven un token emitido por Azure Active Directory en nombre de un inquilino especificado para acceso toohello servicio web de Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="8281a-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="8281a-257">Esquema de grupos y usuarios</span><span class="sxs-lookup"><span data-stu-id="8281a-257">User and group schema</span></span>
<span data-ttu-id="8281a-258">Azure Active Directory puede proporcionar dos tipos de servicios web de recursos tooSCIM.</span><span class="sxs-lookup"><span data-stu-id="8281a-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="8281a-259">Esos tipos de recursos son los usuarios y grupos.</span><span class="sxs-lookup"><span data-stu-id="8281a-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="8281a-260">Recursos de usuario se identifican por identificador de esquema de hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, que se incluye en esta especificación de protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="8281a-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="8281a-261">asignación predeterminada de Hola de atributos de Hola de usuarios en los atributos de Azure Active Directory toohello de recursos de urn: ietf:params:scim:schemas:extension:enterprise:2.0:User se proporciona en la tabla 1, a continuación.</span><span class="sxs-lookup"><span data-stu-id="8281a-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="8281a-262">Recursos del grupo se identifican por identificador de esquema de hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="8281a-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="8281a-263">Tabla 2, a continuación, la asignación de muestra hello predeterminada de atributos de Hola de grupos de atributos de Azure Active Directory toohello de recursos http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="8281a-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="8281a-264">Tabla 1: Asignación de atributos de usuario predeterminada</span><span class="sxs-lookup"><span data-stu-id="8281a-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="8281a-265">Usuario de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8281a-265">Azure Active Directory user</span></span> | <span data-ttu-id="8281a-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="8281a-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="8281a-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="8281a-267">IsSoftDeleted</span></span> |<span data-ttu-id="8281a-268">active</span><span class="sxs-lookup"><span data-stu-id="8281a-268">active</span></span> |
| <span data-ttu-id="8281a-269">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8281a-269">displayName</span></span> |<span data-ttu-id="8281a-270">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8281a-270">displayName</span></span> |
| <span data-ttu-id="8281a-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="8281a-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="8281a-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="8281a-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="8281a-273">givenName</span><span class="sxs-lookup"><span data-stu-id="8281a-273">givenName</span></span> |<span data-ttu-id="8281a-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="8281a-274">name.givenName</span></span> |
| <span data-ttu-id="8281a-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="8281a-275">jobTitle</span></span> |<span data-ttu-id="8281a-276">título</span><span class="sxs-lookup"><span data-stu-id="8281a-276">title</span></span> |
| <span data-ttu-id="8281a-277">mail</span><span class="sxs-lookup"><span data-stu-id="8281a-277">mail</span></span> |<span data-ttu-id="8281a-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="8281a-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="8281a-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="8281a-279">mailNickname</span></span> |<span data-ttu-id="8281a-280">externalId</span><span class="sxs-lookup"><span data-stu-id="8281a-280">externalId</span></span> |
| <span data-ttu-id="8281a-281">manager</span><span class="sxs-lookup"><span data-stu-id="8281a-281">manager</span></span> |<span data-ttu-id="8281a-282">manager</span><span class="sxs-lookup"><span data-stu-id="8281a-282">manager</span></span> |
| <span data-ttu-id="8281a-283">mobile</span><span class="sxs-lookup"><span data-stu-id="8281a-283">mobile</span></span> |<span data-ttu-id="8281a-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="8281a-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="8281a-285">objectId</span><span class="sxs-lookup"><span data-stu-id="8281a-285">objectId</span></span> |<span data-ttu-id="8281a-286">id</span><span class="sxs-lookup"><span data-stu-id="8281a-286">id</span></span> |
| <span data-ttu-id="8281a-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="8281a-287">postalCode</span></span> |<span data-ttu-id="8281a-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="8281a-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="8281a-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="8281a-289">proxy-Addresses</span></span> |<span data-ttu-id="8281a-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="8281a-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="8281a-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="8281a-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="8281a-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="8281a-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="8281a-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="8281a-293">streetAddress</span></span> |<span data-ttu-id="8281a-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="8281a-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="8281a-295">surname</span><span class="sxs-lookup"><span data-stu-id="8281a-295">surname</span></span> |<span data-ttu-id="8281a-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="8281a-296">name.familyName</span></span> |
| <span data-ttu-id="8281a-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="8281a-297">telephone-Number</span></span> |<span data-ttu-id="8281a-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="8281a-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="8281a-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="8281a-299">user-PrincipalName</span></span> |<span data-ttu-id="8281a-300">userName</span><span class="sxs-lookup"><span data-stu-id="8281a-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="8281a-301">Tabla 2: Asignación de atributos de grupo predeterminada</span><span class="sxs-lookup"><span data-stu-id="8281a-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="8281a-302">Grupo de Azure Active Directory </span><span class="sxs-lookup"><span data-stu-id="8281a-302">Azure Active Directory group</span></span> | <span data-ttu-id="8281a-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="8281a-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="8281a-304">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8281a-304">displayName</span></span> |<span data-ttu-id="8281a-305">externalId</span><span class="sxs-lookup"><span data-stu-id="8281a-305">externalId</span></span> |
| <span data-ttu-id="8281a-306">mail</span><span class="sxs-lookup"><span data-stu-id="8281a-306">mail</span></span> |<span data-ttu-id="8281a-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="8281a-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="8281a-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="8281a-308">mailNickname</span></span> |<span data-ttu-id="8281a-309">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8281a-309">displayName</span></span> |
| <span data-ttu-id="8281a-310">members</span><span class="sxs-lookup"><span data-stu-id="8281a-310">members</span></span> |<span data-ttu-id="8281a-311">members</span><span class="sxs-lookup"><span data-stu-id="8281a-311">members</span></span> |
| <span data-ttu-id="8281a-312">objectId</span><span class="sxs-lookup"><span data-stu-id="8281a-312">objectId</span></span> |<span data-ttu-id="8281a-313">id</span><span class="sxs-lookup"><span data-stu-id="8281a-313">id</span></span> |
| <span data-ttu-id="8281a-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="8281a-314">proxyAddresses</span></span> |<span data-ttu-id="8281a-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="8281a-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="8281a-316">Aprovisionamiento y cancelación del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="8281a-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="8281a-317">Hola después mensajes de saludo de la ilustración se muestra que Azure Active Directory envía tooa SCIM servicio toomanage Hola del ciclo de vida de un usuario en otro almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="8281a-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="8281a-318">diagrama de Hello también muestra cómo SCIM proporciona un servicio implementado mediante las bibliotecas CLI de Hola por Microsoft para crear que dichos servicios traducen esas solicitudes toohello llama a métodos de un proveedor.</span><span class="sxs-lookup"><span data-stu-id="8281a-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="8281a-319">![][4]
*Figura 5: secuencia de aprovisionamiento y cancelación de aprovisionamiento de usuarios*</span><span class="sxs-lookup"><span data-stu-id="8281a-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="8281a-320">Las consultas de Active Directory Azure Hola servicio para un usuario con un valor de atributo externalId que coincide con valor de atributo de hello mailNickname de un usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8281a-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="8281a-321">consulta de Hola se expresa como una solicitud de protocolo de transferencia de hipertexto (HTTP), como en este ejemplo, donde jyoung es un ejemplo de un mailNickname de un usuario en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="8281a-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="8281a-322">Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de consulta del proveedor del servicio de hello toohello de llamada.</span><span class="sxs-lookup"><span data-stu-id="8281a-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="8281a-323">Esta es la firma de Hola de ese método:</span><span class="sxs-lookup"><span data-stu-id="8281a-323">Here is hello signature of that method:</span></span> 
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
  <span data-ttu-id="8281a-324">Aquí es definición Hola de interfaz de Hola Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="8281a-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="8281a-325">Hola siguiendo el ejemplo de una consulta para un usuario con un valor especificado para el atributo de externalId hello, valores de argumentos de hello pasados toohello método de consulta son:</span><span class="sxs-lookup"><span data-stu-id="8281a-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="8281a-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="8281a-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="8281a-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="8281a-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="8281a-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="8281a-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="8281a-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="8281a-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="8281a-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="8281a-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="8281a-331">Si el servicio Hola respuesta tooa consulta toohello web para un usuario con un valor de atributo externalId que coincida con el valor de atributo mailNickname Hola de un usuario no devuelve ningún usuario, Azure Active Directory solicita que un usuario la prestación del servicio Hola correspondiente toohello uno en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8281a-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="8281a-332">Este es un ejemplo de dicha solicitud:</span><span class="sxs-lookup"><span data-stu-id="8281a-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="8281a-333">bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM traduciría esa solicitud en un toohello de llamada al método Create de proveedor del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="8281a-334">método Create de Hello tiene esta firma:</span><span class="sxs-lookup"><span data-stu-id="8281a-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="8281a-335">En un tooprovision de solicitud de un usuario, el valor de hello del argumento de recursos de hello es una instancia de hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="8281a-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="8281a-336">Clase Core2EnterpriseUser, definido en la biblioteca de Microsoft.SystemForCrossDomainIdentityManagement.Schemas Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="8281a-337">Si el usuario de hello solicitud tooprovision Hola se realiza correctamente, a continuación, hello implementación del método hello es tooreturn esperado de una instancia de hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="8281a-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="8281a-338">Core2EnterpriseUser (clase), con el valor de Hola de propiedad de identificador hello establece toohello identificador único del usuario recién suministradas Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="8281a-339">tooupdate un usuario conocido tooexist en un almacén de identidades representado por un SCIM, Azure Active Directory continúa solicitando el estado actual de Hola de ese usuario del servicio Hola con una solicitud, como:</span><span class="sxs-lookup"><span data-stu-id="8281a-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="8281a-340">En un servicio que se generan con bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de saludo se traduce en un método de recuperación del proveedor del servicio de hello toohello de llamada.</span><span class="sxs-lookup"><span data-stu-id="8281a-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="8281a-341">Esta es la firma Hola del método de recuperación de hello:</span><span class="sxs-lookup"><span data-stu-id="8281a-341">Here is hello signature of hello Retrieve method:</span></span> 
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
  <span data-ttu-id="8281a-342">En el ejemplo de Hola del estado actual del hello tooretrieve solicitud de un usuario, valores de hello de propiedades de hello del objeto de hello proporcionada como valor de Hola de argumento de hello parámetros son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8281a-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="8281a-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="8281a-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="8281a-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="8281a-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="8281a-345">Si un atributo de referencia es toobe actualizado, a continuación, Azure Active Directory consultas Hola servicio toodetermine haya o no hello valor actual del atributo de referencia de hello en el almacén de identidades de hello representado por servicio Hola ya coincide con valor de Hola de dicho atributo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8281a-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="8281a-346">Para los usuarios, Hola solo de qué hello es consultado el valor actual de esta manera es Hola manager atributo.</span><span class="sxs-lookup"><span data-stu-id="8281a-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="8281a-347">Este es un ejemplo de una solicitud toodetermine si el atributo de administrador de Hola de un objeto de usuario determinado tiene actualmente un determinado valor:</span><span class="sxs-lookup"><span data-stu-id="8281a-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="8281a-348">Hola valor del parámetro de consulta de atributos de hello, identificador, significa que si existe un objeto de usuario que satisface la expresión de hello proporcionada como valor de hello del parámetro de consulta de filtro de hello, entonces servicio hello es toorespond esperado con un urn: ietf:params:scim:schemas: recursos principales: 2.0:User o urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, incluido solo Hola valor de atributo de Id. de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="8281a-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="8281a-349">Hola valo hello **identificador** atributo se conoce toohello solicitante.</span><span class="sxs-lookup"><span data-stu-id="8281a-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="8281a-350">Se incluye en el valor de Hola Hola filtro del parámetro de consulta; Hola de pidiendo sirve realmente toorequest una representación mínima de un recurso que satisfacen la expresión de filtro de hello como una indicación de si dicho objeto existe.</span><span class="sxs-lookup"><span data-stu-id="8281a-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="8281a-351">Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de consulta del proveedor del servicio de hello toohello de llamada.</span><span class="sxs-lookup"><span data-stu-id="8281a-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="8281a-352">valor de Hola de propiedades de Hola de objeto de hello proporcionado como valor de hello del argumento de parámetros de hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8281a-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="8281a-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="8281a-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="8281a-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="8281a-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="8281a-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="8281a-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="8281a-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="8281a-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="8281a-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="8281a-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="8281a-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="8281a-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="8281a-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="8281a-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="8281a-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="8281a-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="8281a-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="8281a-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="8281a-362">En este caso, valor Hola de índice Hola x puede ser 0 y valor Hola de Hola y de índice puede ser 1, o valor Hola de x puede ser 1 y valor Hola de y puede ser 0, según el orden de Hola de las expresiones de Hola Hola filtro del parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="8281a-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="8281a-363">Este es un ejemplo de una solicitud de Azure Active Directory tooan SCIM servicio tooupdate un usuario:</span><span class="sxs-lookup"><span data-stu-id="8281a-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
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
  <span data-ttu-id="8281a-364">las bibliotecas de Microsoft Common Language Infrastructure de Hola para implementar servicios SCIM traduciría solicitud Hola un toohello de llamada al método Update del proveedor del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="8281a-365">Aquí es firma Hola de hello método de actualización:</span><span class="sxs-lookup"><span data-stu-id="8281a-365">Here is hello signature of hello Update method:</span></span> 
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
    <span data-ttu-id="8281a-366">En el ejemplo de Hola de un usuario de solicitud tooupdate, objeto de hello proporciona como valor de Hola de argumento de revisión de hello tiene estos valores de propiedad:</span><span class="sxs-lookup"><span data-stu-id="8281a-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="8281a-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="8281a-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="8281a-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="8281a-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="8281a-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="8281a-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="8281a-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="8281a-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="8281a-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="8281a-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="8281a-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="8281a-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="8281a-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="8281a-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="8281a-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="8281a-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="8281a-375">un usuario de un almacén de identidades de aprovisionar toode representado por un servicio SCIM, Azure AD envía una solicitud como:</span><span class="sxs-lookup"><span data-stu-id="8281a-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="8281a-376">Si el servicio de Hola se compiló mediante bibliotecas de Common Language Infrastructure Hola proporcionadas por Microsoft para implementar servicios SCIM, solicitud de Hola se traduce en un método de eliminación del proveedor del servicio de hello toohello de llamada.</span><span class="sxs-lookup"><span data-stu-id="8281a-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="8281a-377">Este método tiene esta firma:</span><span class="sxs-lookup"><span data-stu-id="8281a-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="8281a-378">objeto de Hello proporciona como valor de Hola de argumento de hello resourceIdentifier tiene estos valores de propiedad en el ejemplo de Hola de una solicitud toode aprovisionar un usuario:</span><span class="sxs-lookup"><span data-stu-id="8281a-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="8281a-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="8281a-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="8281a-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="8281a-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="8281a-381">Aprovisionamiento y cancelación del aprovisionamiento de grupos</span><span class="sxs-lookup"><span data-stu-id="8281a-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="8281a-382">Hola siguientes ilustración muestra hello mensajes que Azure AcD envía tooa SCIM servicio toomanage Hola del ciclo de vida de un grupo en otro almacén de identidades.</span><span class="sxs-lookup"><span data-stu-id="8281a-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="8281a-383">Los mensajes se diferencian de los mensajes de Hola pertenecen toousers de tres maneras:</span><span class="sxs-lookup"><span data-stu-id="8281a-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="8281a-384">esquema de Hola de un recurso de grupo se identifica como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="8281a-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="8281a-385">Solicitudes tooretrieve grupos estipulan ese atributo de miembros de hello es toobe excluido de cualquier recurso proporcionado en la solicitud de toohello de respuesta.</span><span class="sxs-lookup"><span data-stu-id="8281a-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="8281a-386">Las solicitudes toodetermine si un atributo de referencia tiene un valor determinado se trata de solicitudes sobre el atributo de miembros de Hola.</span><span class="sxs-lookup"><span data-stu-id="8281a-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="8281a-387">![][5]
*Figura 6: secuencia de aprovisionamiento y cancelación del aprovisionamiento de grupos*</span><span class="sxs-lookup"><span data-stu-id="8281a-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="8281a-388">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="8281a-388">Related articles</span></span>
* [<span data-ttu-id="8281a-389">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8281a-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8281a-390">Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS</span><span class="sxs-lookup"><span data-stu-id="8281a-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="8281a-391">Personalización de asignaciones de atributos para el aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="8281a-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="8281a-392">Escritura de expresiones para asignaciones de atributos</span><span class="sxs-lookup"><span data-stu-id="8281a-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="8281a-393">Filtros de ámbito para el aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="8281a-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="8281a-394">Notificaciones de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="8281a-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="8281a-395">Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS</span><span class="sxs-lookup"><span data-stu-id="8281a-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
