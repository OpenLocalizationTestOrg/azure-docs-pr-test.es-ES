---
title: aaaAzure Active Directory Graph API | Documentos de Microsoft
description: "Una guía de introducción y tutorial rápido para hello API Graph que permite mediante programación a tooAzure AD a través de extremos de la API de REST."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a><span data-ttu-id="e9b58-103">API Graph de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9b58-103">Azure Active Directory Graph API</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9b58-104">Se recomienda encarecidamente que utilice [Microsoft Graph](https://graph.microsoft.io/) en lugar de Azure AD Graph API tooaccess recursos de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9b58-104">We strongly recommend that you use [Microsoft Graph](https://graph.microsoft.io/) instead of Azure AD Graph API tooaccess Azure Active Directory resources.</span></span> <span data-ttu-id="e9b58-105">Nuestros esfuerzos de desarrollo ahora se centran en Microsoft Graph y no están previstas realizar mejoras adicionales para la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-105">Our development efforts are now concentrated on Microsoft Graph and no further enhancements are planned for Azure AD Graph API.</span></span> <span data-ttu-id="e9b58-106">Hay un número muy limitado de escenarios para los que Azure AD Graph API todavía podría ser adecuado; Para obtener más información, vea hello [Microsoft Graph o hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) entrada de blog en hello centro de desarrollo de Office.</span><span class="sxs-lookup"><span data-stu-id="e9b58-106">There are a very limited number of scenarios for which Azure AD Graph API might still be appropriate; for more information, see hello [Microsoft Graph or hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blog post in hello Office Dev Center.</span></span>
> 
> 

<span data-ttu-id="e9b58-107">Hola API Graph de Azure Active Directory proporciona acceso mediante programación tooAzure AD a través de extremos de API de REST.</span><span class="sxs-lookup"><span data-stu-id="e9b58-107">hello Azure Active Directory Graph API provides programmatic access tooAzure AD through REST API endpoints.</span></span> <span data-ttu-id="e9b58-108">Las aplicaciones pueden usar Hola API Graph tooperform crear, leer, actualizar y eliminar operaciones (CRUD) en objetos y datos de directorio.</span><span class="sxs-lookup"><span data-stu-id="e9b58-108">Applications can use hello Graph API tooperform create, read, update, and delete (CRUD) operations on directory data and objects.</span></span> <span data-ttu-id="e9b58-109">Por ejemplo, hello API Graph admite hello las siguientes operaciones comunes para un objeto de usuario:</span><span class="sxs-lookup"><span data-stu-id="e9b58-109">For example, hello Graph API supports hello following common operations for a user object:</span></span>

* <span data-ttu-id="e9b58-110">Crear un usuario nuevo en un directorio</span><span class="sxs-lookup"><span data-stu-id="e9b58-110">Create a new user in a directory</span></span>
* <span data-ttu-id="e9b58-111">Obtener las propiedades detalladas de un usuario, como sus grupos</span><span class="sxs-lookup"><span data-stu-id="e9b58-111">Get a user’s detailed properties, such as their groups</span></span>
* <span data-ttu-id="e9b58-112">Actualizar las propiedades de un usuario, como su ubicación y número de teléfono, o cambiar su contraseña</span><span class="sxs-lookup"><span data-stu-id="e9b58-112">Update a user’s properties, such as their location and phone number, or change their password</span></span>
* <span data-ttu-id="e9b58-113">Consultar la pertenencia a grupos de un usuario para el acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="e9b58-113">Check a user’s group membership for role-based access</span></span>
* <span data-ttu-id="e9b58-114">Deshabilitar la cuenta de un usuario o eliminarla por completo</span><span class="sxs-lookup"><span data-stu-id="e9b58-114">Disable a user’s account or delete it entirely</span></span>

<span data-ttu-id="e9b58-115">En los objetos de toouser de suma, puede realizar las mismas operaciones en otros objetos como los grupos y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e9b58-115">In addition toouser objects, you can perform similar operations on other objects such as groups and applications.</span></span> <span data-ttu-id="e9b58-116">toocall Hola API Graph en un directorio, la aplicación hello debe estar registrado con Azure AD y puede configura toohello de tooallow obtener acceso al directorio.</span><span class="sxs-lookup"><span data-stu-id="e9b58-116">toocall hello Graph API on a directory, hello application must be registered with Azure AD and be configured tooallow access toohello directory.</span></span> <span data-ttu-id="e9b58-117">Esto se logra normalmente a través de un flujo de consentimiento de usuario o administrador.</span><span class="sxs-lookup"><span data-stu-id="e9b58-117">This is normally achieved through a user or admin consent flow.</span></span>

<span data-ttu-id="e9b58-118">toobegin utilizando hello Azure Active Directory Graph API, vea hello [Guía de inicio rápido de API de Graph](active-directory-graph-api-quickstart.md), o vista hello [documentación de referencia de API Graph interactiva](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="e9b58-118">toobegin using hello Azure Active Directory Graph API, see hello [Graph API Quickstart Guide](active-directory-graph-api-quickstart.md), or view hello [interactive Graph API reference documentation](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span></span>

## <a name="features"></a><span data-ttu-id="e9b58-119">Características</span><span class="sxs-lookup"><span data-stu-id="e9b58-119">Features</span></span>
<span data-ttu-id="e9b58-120">Hola API Graph proporciona Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="e9b58-120">hello Graph API provides hello following features:</span></span>

* <span data-ttu-id="e9b58-121">**Los extremos de la API de REST**: Hola API Graph es un servicio RESTful compuesto de extremos que se tiene acceso mediante solicitudes HTTP estándares.</span><span class="sxs-lookup"><span data-stu-id="e9b58-121">**REST API Endpoints**: hello Graph API is a RESTful service comprised of endpoints that are accessed using standard HTTP requests.</span></span> <span data-ttu-id="e9b58-122">Hola API Graph admite tipos de contenido XML o Javascript Object Notation (JSON) para las solicitudes y respuestas.</span><span class="sxs-lookup"><span data-stu-id="e9b58-122">hello Graph API supports XML or Javascript Object Notation (JSON) content types for requests and responses.</span></span> <span data-ttu-id="e9b58-123">Para obtener más información, consulte [Referencia de la API Graph de REST de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="e9b58-123">For more information, see [Azure AD Graph REST API Reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span></span>
* <span data-ttu-id="e9b58-124">**Autenticación con Azure AD**: cada toohello de solicitud API Graph deben autenticarse mediante la anexión de un símbolo (token) para la Web de JSON (JWT) en el encabezado de autorización de saludo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="e9b58-124">**Authentication with Azure AD**: Every request toohello Graph API must be authenticated by appending a JSON Web Token (JWT) in hello Authorization header of hello request.</span></span> <span data-ttu-id="e9b58-125">Este token se adquiere realizando el extremo de token de un tooAzure de solicitud de AD y proporcionar las credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="e9b58-125">This token is acquired by making a request tooAzure AD’s token endpoint and providing valid credentials.</span></span> <span data-ttu-id="e9b58-126">Puede usar Hola flujo de credenciales de cliente de OAuth 2.0 o tooacquire de flujo de concesión de código de autorización de hello un gráfico de token toocall Hola.</span><span class="sxs-lookup"><span data-stu-id="e9b58-126">You can use hello OAuth 2.0 client credentials flow or hello authorization code grant flow tooacquire a token toocall hello Graph.</span></span> <span data-ttu-id="e9b58-127">Para obtener más información, vea [OAuth 2.0 en Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9b58-127">For more information, [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="e9b58-128">**Autorización basada en roles (RBAC)**: grupos de seguridad son usado tooperform RBAC en hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-128">**Role-Based Authorization (RBAC)**: Security groups are used tooperform RBAC in hello Graph API.</span></span> <span data-ttu-id="e9b58-129">Por ejemplo, si desea toodetermine si un usuario tiene acceso tooa determinado recurso, Hola aplicación puede llamar a hello [comprobar pertenencia a grupos (transitiva)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) operación, que devuelve true o false.</span><span class="sxs-lookup"><span data-stu-id="e9b58-129">For example, if you want toodetermine whether a user has access tooa specific resource, hello application can call hello [Check Group Membership (transitive)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) operation, which returns true or false.</span></span>
* <span data-ttu-id="e9b58-130">**Consulta diferencial**: si desea toocheck para cambios en un directorio entre dos períodos de tiempo sin necesidad de toomake frecuentan consultas toohello API Graph, puede realizar una solicitud de consulta diferencial.</span><span class="sxs-lookup"><span data-stu-id="e9b58-130">**Differential Query**: If you want toocheck for changes in a directory between two time periods without having toomake frequent queries toohello Graph API, you can make a differential query request.</span></span> <span data-ttu-id="e9b58-131">Este tipo de solicitud devolverá solo los cambios Hola realizados entre una solicitud de consulta diferencial anterior hello y solicitud de hello actual.</span><span class="sxs-lookup"><span data-stu-id="e9b58-131">This type of request will return only hello changes made between hello previous differential query request and hello current request.</span></span> <span data-ttu-id="e9b58-132">Para más información, vea [Consulta diferencial de la API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).</span><span class="sxs-lookup"><span data-stu-id="e9b58-132">For more information, see [Azure AD Graph API Differential Query](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).</span></span>
* <span data-ttu-id="e9b58-133">**Extensiones de directorio**: si está desarrollando una aplicación que necesite tooread o escribir propiedades únicas para los objetos de directorio, puede registrar y usar valores de extensión mediante Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-133">**Directory Extensions**: If you are developing an application that needs tooread or write unique properties for directory objects, you can register and use extension values by using hello Graph API.</span></span> <span data-ttu-id="e9b58-134">Por ejemplo, si la aplicación requiere una propiedad de identificador de Skype para cada usuario, puede registrar Hola nueva propiedad en el directorio de Hola y estará disponible en cada objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="e9b58-134">For example, if your application requires a Skype ID property for each user, you can register hello new property in hello directory and it will be available on every user object.</span></span> <span data-ttu-id="e9b58-135">Para obtener más información, consulte [Extensiones de esquema de directorio de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).</span><span class="sxs-lookup"><span data-stu-id="e9b58-135">For more information, see [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).</span></span>
* <span data-ttu-id="e9b58-136">**Protegida por ámbitos de permiso**: API de AAD Graph expone los ámbitos de permiso que permiten proteger/consentido acceder a los datos de tooAAD y admiten una variedad de tipos de aplicación de cliente, incluidos:</span><span class="sxs-lookup"><span data-stu-id="e9b58-136">**Secured by permission scopes**: AAD Graph API exposes permission scopes that enable secure/consented access tooAAD data, and support a variety of client app types, including:</span></span>
  
  * <span data-ttu-id="e9b58-137">aquellos con una interfaz de usuario que reciben delegado acceso a toodata a través de autorización desde Hola usuario con sesión iniciada (delegado)</span><span class="sxs-lookup"><span data-stu-id="e9b58-137">those with a user interface which are given delegated access toodata via authorization from hello signed-in user (delegated)</span></span>
  * <span data-ttu-id="e9b58-138">Aquellos que usan el control de acceso basado en roles definido por las aplicaciones, como clientes de servicio o demonio (roles de aplicación).</span><span class="sxs-lookup"><span data-stu-id="e9b58-138">those that use application-define role-based access control such as service/daemon clients (app roles)</span></span>
    
    <span data-ttu-id="e9b58-139">Los delegados y ámbitos de permiso de rol de aplicación representan un privilegio expuesto por hello API Graph y se pueden solicitar por aplicaciones cliente a través de los permisos de registro de aplicación [características en el portal de Azure hello](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9b58-139">Both delegated and app role permission scopes represent a privilege exposed by hello Graph API and can be requested by client applications through application registration permissions [features in hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e9b58-140">Los clientes pueden comprobar los ámbitos de permiso de hello concedido toothem mediante la inspección de notificación de ámbito ("scp") de hello recibido en el token de acceso de Hola para permisos delegados y Hola funciones ("") de notificación para permisos de rol de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9b58-140">Clients can verify hello permission scopes granted toothem by inspecting hello scope (“scp”) claim received in hello access token for delegated permissions and hello roles (“roles”) claim for app role permissions.</span></span> <span data-ttu-id="e9b58-141">Obtenga más información sobre los [ámbitos de permiso de API Graph de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).</span><span class="sxs-lookup"><span data-stu-id="e9b58-141">Learn more about [Azure AD Graph API Permission Scopes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).</span></span>

## <a name="scenarios"></a><span data-ttu-id="e9b58-142">Escenarios</span><span class="sxs-lookup"><span data-stu-id="e9b58-142">Scenarios</span></span>
<span data-ttu-id="e9b58-143">Hola API Graph permite muchos escenarios de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e9b58-143">hello Graph API enables many application scenarios.</span></span> <span data-ttu-id="e9b58-144">Hola los escenarios siguientes es hello más comunes:</span><span class="sxs-lookup"><span data-stu-id="e9b58-144">hello following scenarios are hello most common:</span></span>

* <span data-ttu-id="e9b58-145">**Aplicación de línea de negocio (un solo inquilino)**: en este escenario, un desarrollador empresarial trabaja para una organización que tiene una suscripción a Office 365.</span><span class="sxs-lookup"><span data-stu-id="e9b58-145">**Line of Business (Single Tenant) Application**: In this scenario, an enterprise developer works for an organization that has an Office 365 subscription.</span></span> <span data-ttu-id="e9b58-146">Hola desarrollador compila una aplicación web que interactúa con las tareas de tooperform de Azure AD como asignar una licencia tooa un usuario.</span><span class="sxs-lookup"><span data-stu-id="e9b58-146">hello developer is building a web application that interacts with Azure AD tooperform tasks such assigning a license tooa user.</span></span> <span data-ttu-id="e9b58-147">Esta tarea requiere acceso toohello API de Graph, por lo que el desarrollador de hello registra la aplicación de un solo inquilino de hello en Azure AD y configura permisos lectura / escritura para hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-147">This task requires access toohello Graph API, so hello developer registers hello single tenant application in Azure AD and configures read and write permissions for hello Graph API.</span></span> <span data-ttu-id="e9b58-148">Hola, a continuación, la aplicación es toouse configurado sus propias credenciales o los de hello tooacquire de inicio de sesión de usuario actualmente un token toocall Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-148">Then hello application is configured toouse either its own credentials or those of hello currently sign-in user tooacquire a token toocall hello Graph API.</span></span>
* <span data-ttu-id="e9b58-149">**Software como aplicación de servicio (multiempresa)**: en este escenario, un fabricante de software independiente (ISV) desarrolla una aplicación web multiempresa hospedada que ofrece características de administración de usuarios para otras organizaciones que usan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b58-149">**Software as a Service Application (Multi-Tenant)**: In this scenario, an independent software vendor (ISV) is developing hosted multi-tenant web application that provides user management features for other organizations that use Azure AD.</span></span> <span data-ttu-id="e9b58-150">Estas características requieren acceso toodirectory objetos, y así aplicación hello debe toocall Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9b58-150">These features require access toodirectory objects, and so hello application needs toocall hello Graph API.</span></span> <span data-ttu-id="e9b58-151">desarrollador de Hello registra la aplicación hello en Azure AD, configura toorequire lectura y permisos de escritura para hello API Graph y, a continuación, habilita el acceso externo para que otras organizaciones pueden permitir la aplicación de hello toouse en su directorio.</span><span class="sxs-lookup"><span data-stu-id="e9b58-151">hello developer registers hello application in Azure AD, configures it toorequire read and write permissions for hello Graph API, and then enables external access so that other organizations can consent toouse hello application in their directory.</span></span> <span data-ttu-id="e9b58-152">Cuando un usuario de otra organización autentica la aplicación de toohello para hello primera vez, aparecerá un cuadro de diálogo de consentimiento con permisos de Hola Hola aplicación está solicitando.</span><span class="sxs-lookup"><span data-stu-id="e9b58-152">When a user in another organization authenticates toohello application for hello first time, they are shown a consent dialog with hello permissions hello application is requesting.</span></span>  <span data-ttu-id="e9b58-153">Concesión de consentimiento, a continuación, proporcionará la aplicación hello solicita los permisos toohello API Graph en el directorio del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9b58-153">Granting consent will then give hello application those requested permissions toohello Graph API in hello user’s directory.</span></span> <span data-ttu-id="e9b58-154">Para obtener más información sobre el marco de consentimiento de hello, consulte [información general del marco de consentimiento de hello](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e9b58-154">For more information on hello consent framework, see [Overview of hello Consent Framework](active-directory-integrating-applications.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e9b58-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e9b58-155">See Also</span></span>
[<span data-ttu-id="e9b58-156">Inicio rápido para la API de Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="e9b58-156">Azure AD Graph API Quickstart Guide</span></span>](active-directory-graph-api-quickstart.md)

[<span data-ttu-id="e9b58-157">Documentación de AD Graph de REST</span><span class="sxs-lookup"><span data-stu-id="e9b58-157">AD Graph REST documentation</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[<span data-ttu-id="e9b58-158">Guía del desarrollador de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9b58-158">Azure Active Directory developer's guide</span></span>](active-directory-developers-guide.md)
