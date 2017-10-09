---
title: aaaProtect datos personales con controles de identidad y acceso de Azure | Documentos de Microsoft
description: Mediante el uso de Azure toohelp de controles de identidad y acceso a proteger sus datos personales
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="0726b-103">Azure Active Directory y Multi-Factor Authentication: protección de datos personales con controles de identidad y acceso</span><span class="sxs-lookup"><span data-stu-id="0726b-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="0726b-104">Este artículo proporciona información y procedimientos que puede usar datos personales tooprotect con los servicios y características de seguridad de autenticación de Azure Active Directory y varios factores.</span><span class="sxs-lookup"><span data-stu-id="0726b-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="0726b-105">Escenario</span><span class="sxs-lookup"><span data-stu-id="0726b-105">Scenario</span></span>

<span data-ttu-id="0726b-106">Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas.</span><span class="sxs-lookup"><span data-stu-id="0726b-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="0726b-107">toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="0726b-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="0726b-108">la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="0726b-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="0726b-109">Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global.</span><span class="sxs-lookup"><span data-stu-id="0726b-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="0726b-110">También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="0726b-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="0726b-111">línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.</span><span class="sxs-lookup"><span data-stu-id="0726b-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="0726b-112">Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes de la compañía de Hola ubicados en todo Hola a todos tienen acceso a recursos de empresa de toosome.</span><span class="sxs-lookup"><span data-stu-id="0726b-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="0726b-113">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="0726b-113">Problem statement</span></span>

<span data-ttu-id="0726b-114">empresa Hola debe proteger la privacidad de Hola de datos personales de los clientes y empleados frente a atacantes buscando toouse en riesgo identidades toogain acceso.</span><span class="sxs-lookup"><span data-stu-id="0726b-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="0726b-115">También deben asegurarse de que toopersonal de acceso a datos por los usuarios legítimos se restringe a solo aquellos que lo necesiten toodo sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="0726b-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="0726b-116">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="0726b-116">Company goal</span></span>

<span data-ttu-id="0726b-117">objetivo de la compañía de Hello es tooensure que tienen acceso a datos toopersonal esté estrictamente controlado.</span><span class="sxs-lookup"><span data-stu-id="0726b-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="0726b-118">Es fundamental que las identidades de los usuarios con acceso a los datos toopersonal protegerse con una autenticación segura.</span><span class="sxs-lookup"><span data-stu-id="0726b-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="0726b-119">Una directiva de [privilegios mínimos] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) se debe aplicar para que los usuarios legítimos tengan único nivel de Hola de acceso que necesitan y nada más.</span><span class="sxs-lookup"><span data-stu-id="0726b-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="0726b-120">Soluciones</span><span class="sxs-lookup"><span data-stu-id="0726b-120">Solutions</span></span>

<span data-ttu-id="0726b-121">Microsoft Azure proporciona herramientas de administración de identidades y accesos toohelp control de las empresas que tenga acceso tooresources que contienen datos personales.</span><span class="sxs-lookup"><span data-stu-id="0726b-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="0726b-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0726b-122">Azure Active Directory</span></span>

<span data-ttu-id="0726b-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) administra las identidades y controla el acceso tooAzure así como otros locales y otros recursos de nube, datos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0726b-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="0726b-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ayuda a número de administradores de Azure toominimize Hola de personas que tienen acceso toocertain información como datos personales.</span><span class="sxs-lookup"><span data-stu-id="0726b-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="0726b-125">Les permite toodiscover, restrinja y supervise las identidades con privilegios y sus acceso tooresources y tooassign temporal, Just (JIT) derechos administrativos tooeligible usuarios.</span><span class="sxs-lookup"><span data-stu-id="0726b-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="0726b-126">Asimismo, proporciona información sobre quién tiene privilegios administrativos de AAD.</span><span class="sxs-lookup"><span data-stu-id="0726b-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="0726b-127">las actividades de Hello implicadas el uso de AAD PIM incluyen:</span><span class="sxs-lookup"><span data-stu-id="0726b-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="0726b-128">Habilitación de Privileged Identity Management para el directorio</span><span class="sxs-lookup"><span data-stu-id="0726b-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="0726b-129">Usar importante información toosee del panel de administración de Privileged Identity Management de un vistazo</span><span class="sxs-lookup"><span data-stu-id="0726b-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="0726b-130">Administración de identidades de hello con privilegios (administradores) agregando o quitando el rol de administradores permanentes ni aptos tooeach</span><span class="sxs-lookup"><span data-stu-id="0726b-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="0726b-131">Configuración de activación de rol Hola</span><span class="sxs-lookup"><span data-stu-id="0726b-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="0726b-132">Activación de roles</span><span class="sxs-lookup"><span data-stu-id="0726b-132">Activating roles</span></span>

- <span data-ttu-id="0726b-133">Revisión de la actividad de un rol</span><span class="sxs-lookup"><span data-stu-id="0726b-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="0726b-134">¿Cómo se puede habilitar AAD PIM?</span><span class="sxs-lookup"><span data-stu-id="0726b-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="0726b-135">toostart usar PIM para su directorio, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0726b-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="0726b-136">Inicie sesión en toohello portal de Azure como administrador global de su directorio.</span><span class="sxs-lookup"><span data-stu-id="0726b-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="0726b-137">Si su organización tiene más de un directorio, seleccione el nombre de usuario en hello superior derecha del programa Hola a portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0726b-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="0726b-138">Seleccione el directorio de Hola donde use AD Privileged Identity Management de Azure.</span><span class="sxs-lookup"><span data-stu-id="0726b-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="0726b-139">Seleccione **más servicios** y usar hello **filtro** toosearch de cuadro de texto para Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="0726b-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="0726b-140">Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="0726b-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="0726b-141">Hola aplicación Privileged Identity Management se abre.</span><span class="sxs-lookup"><span data-stu-id="0726b-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="0726b-142">Una vez que se ha configurado AD Privileged Identity Management de Azure, consulte hoja de navegación de hello cada vez que abra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0726b-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="0726b-143">Para obtener más información e instrucciones sobre cómo empezar a trabajar con AAD PIM, consulte [Comenzar a usar Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0726b-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="0726b-144">Control de acceso basado en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="0726b-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="0726b-145">[Role-Based Access Control de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ayuda a administradores de Azure a administrar acceso a los recursos tooAzure habilitando Hola concesión de acceso basado en rol asignado del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0726b-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="0726b-146">Puede separar los derechos dentro de un equipo y solo Hola cantidad de acceso toousers, grupos y aplicaciones que necesitan tooperform sus trabajos de concesiones.</span><span class="sxs-lookup"><span data-stu-id="0726b-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="0726b-147">Se puede conceder acceso basado en roles toousers mediante Hola portal de Azure, Azure herramientas de línea de comandos o las API de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="0726b-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="0726b-148">Para obtener más información acerca de conceptos básicos de RBAC de Azure, consulte [empezar a trabajar con Control de acceso basado en roles en hello Portal de Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="0726b-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="0726b-149">¿Cómo se puede administrar RBAC de Azure con PowerShell?</span><span class="sxs-lookup"><span data-stu-id="0726b-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="0726b-150">Puede usar cmdlets de PowerShell toomanage RBAC de Azure, incluidos Hola después de las tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="0726b-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="0726b-151">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="0726b-151">List roles</span></span>

- <span data-ttu-id="0726b-152">Consulta de quién ha accedido</span><span class="sxs-lookup"><span data-stu-id="0726b-152">See who has access</span></span>

- <span data-ttu-id="0726b-153">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="0726b-153">Grant access</span></span>

- <span data-ttu-id="0726b-154">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="0726b-154">Remove access</span></span>

- <span data-ttu-id="0726b-155">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="0726b-155">Create a custom role</span></span>

- <span data-ttu-id="0726b-156">Acciones Get para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="0726b-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="0726b-157">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="0726b-157">Modify a custom role</span></span>

- <span data-ttu-id="0726b-158">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="0726b-158">Delete a custom role</span></span>

- <span data-ttu-id="0726b-159">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="0726b-159">List custom roles</span></span>

<span data-ttu-id="0726b-160">Para obtener instrucciones sobre cómo toomanage RBAC de Azure con PowerShell, vea [administrar Role-based Access con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="0726b-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="0726b-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0726b-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="0726b-162">[La autenticación multifactor Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) es una solución de comprobación de dos pasos que le ayuda a proteger acceso toodata y las aplicaciones, al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="0726b-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="0726b-163">Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).</span><span class="sxs-lookup"><span data-stu-id="0726b-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="0726b-164">toodeploy MFA en hello nube de Azure, necesita toofirst habilitarlo y, a continuación, activar la verificación en dos pasos para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0726b-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="0726b-165">¿Cómo habilito toouse Azure MFA?</span><span class="sxs-lookup"><span data-stu-id="0726b-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="0726b-166">Si los usuarios tienen licencias que incluyen la autenticación multifactor de Azure, no hay nada que necesite toodo tooturn en Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="0726b-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="0726b-167">De lo contrario, deberá toocreate un proveedor de autenticación multifactor en su directorio.</span><span class="sxs-lookup"><span data-stu-id="0726b-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="0726b-168">toodo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0726b-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="0726b-169">Seleccione **Active Directory** en hello Azure portal clásico (iniciado sesión como administrador).</span><span class="sxs-lookup"><span data-stu-id="0726b-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="0726b-170">Seleccione **Proveedores de Multi-Factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="0726b-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="0726b-171">Seleccione **Nuevo** y, a continuación, en **App Services,** seleccione **Proveedor de Multi-Factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="0726b-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="0726b-172">Seleccione **Creación rápida.**</span><span class="sxs-lookup"><span data-stu-id="0726b-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="0726b-173">Rellene el campo de nombre de Hola y seleccione un modelo de uso (por autenticación o por usuario habilitado).</span><span class="sxs-lookup"><span data-stu-id="0726b-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="0726b-174">Designar un directorio con qué hello está asociado el proveedor de MFA.</span><span class="sxs-lookup"><span data-stu-id="0726b-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="0726b-175">Haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="0726b-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="0726b-176">Para obtener más instrucciones sobre cómo toomanage el proveedor de autenticación multifactor, consulte [introducción con un proveedor de autenticación multifactor de Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="0726b-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="0726b-177">¿Cómo se puede activar la verificación en dos pasos para los usuarios?</span><span class="sxs-lookup"><span data-stu-id="0726b-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="0726b-178">Puede exigir la verificación en dos pasos para todos los inicios de sesión, o puede crear verificacion de toorequire de directivas de acceso condicional sólo cuando se dan condiciones específicas.</span><span class="sxs-lookup"><span data-stu-id="0726b-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="0726b-179">Habilitar MFA de Azure mediante el cambio de estado de usuario es el enfoque tradicional de Hola para exigir la verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="0726b-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="0726b-180">Todos los usuarios de Hola que habilitar tendrán Hola verificación en dos pasos de mismo requisito tooperform cada vez que inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="0726b-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="0726b-181">La habilitación de un usuario invalida las directivas de acceso condicional que pudieran afectar a dicho usuario.</span><span class="sxs-lookup"><span data-stu-id="0726b-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="0726b-182">Habilitar Azure MFA con una directiva de acceso condicional es un enfoque más flexible para exigir la verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="0726b-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="0726b-183">Puede crear directivas de acceso condicional que se aplican toogroups, así como los usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="0726b-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="0726b-184">Los grupos de alto riesgo pueden recibir más restricciones que los grupos de bajo riesgo o bien la verificación en dos pasos puede ser necesaria solo para aplicaciones de alto riesgo en la nube y omitida para las de bajo riesgo.</span><span class="sxs-lookup"><span data-stu-id="0726b-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="0726b-185">Sin embargo, el acceso condicional es una característica de pago de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0726b-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="0726b-186">Hola tooenable MFA cambiando el estado de usuario siguientes:</span><span class="sxs-lookup"><span data-stu-id="0726b-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="0726b-187">Inicie sesión en toohello portal de Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="0726b-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="0726b-188">Vaya demasiado**Azure Active Directory \> usuarios y grupos \> todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0726b-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="0726b-189">Seleccione **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="0726b-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="0726b-190">Buscar usuario de Hola que quiere tooenable de MFA de Azure.</span><span class="sxs-lookup"><span data-stu-id="0726b-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="0726b-191">Puede que necesite toochange Hola vista en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0726b-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="0726b-192">Compruebe Hola cuadro siguiente toohello del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="0726b-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="0726b-193">En hello derecha, bajo pasos rápidos, elija **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="0726b-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="0726b-194">Confirme la selección en la ventana emergente de Hola que se abre.</span><span class="sxs-lookup"><span data-stu-id="0726b-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="0726b-195">Los usuarios para los que se ha habilitado MFA le preguntará hello tooregister próxima vez que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0726b-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="0726b-196">tooenable MFA de Azure con una directiva de acceso condicional, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0726b-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="0726b-197">Inicie sesión en toohello portal de Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="0726b-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="0726b-198">Vaya demasiado**Azure Active Directory \> acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="0726b-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="0726b-199">Seleccione **Nueva directiva**.</span><span class="sxs-lookup"><span data-stu-id="0726b-199">Select **New policy**.</span></span>

4. <span data-ttu-id="0726b-200">En **Asignaciones**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0726b-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="0726b-201">Hola de uso **Include** y **excluir** pestañas toospecify qué usuarios y grupos serán administrada por directiva Hola.</span><span class="sxs-lookup"><span data-stu-id="0726b-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="0726b-202">En **Asignaciones**, seleccione **Aplicaciones en la nube.**</span><span class="sxs-lookup"><span data-stu-id="0726b-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="0726b-203">Elija demasiado**incluyen todas las aplicaciones de nube**.</span><span class="sxs-lookup"><span data-stu-id="0726b-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="0726b-204">En **Controles de acceso**, seleccione **Conceder**.</span><span class="sxs-lookup"><span data-stu-id="0726b-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="0726b-205">Seleccione **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="0726b-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="0726b-206">Activar **habilitar Directiva de** demasiado**en** y, a continuación, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0726b-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="0726b-207">Para obtener información sobre cómo tooset de configuración de MFA de Azure de tooconfigure las alertas de fraude, se crea una omisión por única vez, usar mensajes de voz personalizados, configurar el almacenamiento en caché, especificar direcciones IP de confianza, crear contraseñas de aplicación, habilitar la autenticación Multifactor para dispositivos que los usuarios de confianza y seleccione teniendo en cuenta métodos de comprobación, vea [configurar configuración de Azure Multi-factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="0726b-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0726b-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0726b-208">Next steps</span></span>

- [<span data-ttu-id="0726b-209">Protección del acceso con privilegios en Azure AD</span><span class="sxs-lookup"><span data-stu-id="0726b-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="0726b-210">Preguntas más frecuentes relacionadas con Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0726b-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="0726b-211">Solución de problemas del control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="0726b-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="0726b-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="0726b-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
