---
title: "Protección de datos personales con controles de identidad y acceso de Azure | Microsoft Docs"
description: Uso de controles de identidad y acceso de Azure para ayudar a proteger sus datos personales
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
ms.openlocfilehash: b43754efd207679dbe08710f44f56454a5fd20ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="04685-103">Azure Active Directory y Multi-Factor Authentication: protección de datos personales con controles de identidad y acceso</span><span class="sxs-lookup"><span data-stu-id="04685-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="04685-104">En este artículo se proporcionan información y procedimientos que puede usar para proteger datos personales mediante servicios y características de seguridad de Azure Active Directory y Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="04685-104">This article provides information and procedures you can use to protect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="04685-105">Escenario</span><span class="sxs-lookup"><span data-stu-id="04685-105">Scenario</span></span>

<span data-ttu-id="04685-106">Una gran empresa de cruceros, con sede en Estados Unidos, se encuentra en proceso de expansión de sus operaciones para ofrecer itinerarios en los mares Mediterráneo, Adriático y Báltico, así como en las Islas Británicas.</span><span class="sxs-lookup"><span data-stu-id="04685-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="04685-107">Para apoyar esos esfuerzos, ha adquirido varias líneas de cruceros más pequeñas establecidas en Italia, Alemania, Dinamarca y Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="04685-107">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="04685-108">La empresa usa Microsoft Azure para almacenar datos corporativos en la nube.</span><span class="sxs-lookup"><span data-stu-id="04685-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="04685-109">Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global.</span><span class="sxs-lookup"><span data-stu-id="04685-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="04685-110">También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="04685-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="04685-111">La línea de cruceros también conserva una gran base de datos de miembros del programa de recompensa y lealtad que incluye información personal para hacer un seguimiento de las relaciones con clientes actuales y antiguos.</span><span class="sxs-lookup"><span data-stu-id="04685-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="04685-112">Los empleados corporativos tienen acceso a la red de las oficinas remotas de la empresa, mientras que los agentes de viajes repartidos por todo el mundo tienen acceso a algunos recursos empresariales.</span><span class="sxs-lookup"><span data-stu-id="04685-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="04685-113">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="04685-113">Problem statement</span></span>

<span data-ttu-id="04685-114">La empresa debe proteger la privacidad de los datos personales de los clientes y los empleados frente a atacantes que pretenden usar identidades comprometidas para obtener acceso.</span><span class="sxs-lookup"><span data-stu-id="04685-114">The company must protect the privacy of customers’ and employees’ personal data from attackers seeking to use compromised identities to gain access.</span></span> <span data-ttu-id="04685-115">También debe garantizar que el acceso a datos personales por parte de usuarios legítimos quede restringido a solo aquellos que lo necesiten para realizar sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="04685-115">They also must ensure that access to personal data by legitimate users is restricted to only those who need it to do their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="04685-116">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="04685-116">Company goal</span></span>

<span data-ttu-id="04685-117">El objetivo de la empresa es garantizar que el acceso a los datos personales esté estrictamente controlado.</span><span class="sxs-lookup"><span data-stu-id="04685-117">The company’s goal is to ensure that access to personal data is strictly controlled.</span></span> <span data-ttu-id="04685-118">Es fundamental que las identidades de los usuarios con acceso a los datos personales estén protegidas mediante una autenticación sólida.</span><span class="sxs-lookup"><span data-stu-id="04685-118">It is essential that identities of users with access to personal data be protected by strong authentication.</span></span> <span data-ttu-id="04685-119">Una directiva de [privilegios mínimos] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) debe aplicarse para que los usuarios legítimos tengan solo el nivel de acceso que necesitan, no más.</span><span class="sxs-lookup"><span data-stu-id="04685-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only the level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="04685-120">Soluciones</span><span class="sxs-lookup"><span data-stu-id="04685-120">Solutions</span></span>

<span data-ttu-id="04685-121">Microsoft Azure proporciona herramientas de administración de identidad y acceso para ayudar a las empresas a controlar quién tiene acceso a recursos que contienen datos personales.</span><span class="sxs-lookup"><span data-stu-id="04685-121">Microsoft Azure provides identity and access management tools to help companies control who has access to resources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="04685-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04685-122">Azure Active Directory</span></span>

<span data-ttu-id="04685-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) administra identidades y controla el acceso a Azure, así como otros recursos locales y otros recursos de nube, datos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04685-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access to Azure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="04685-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ayuda a los administradores de Azure a minimizar el número de personas con acceso a información determinada como, por ejemplo, datos personales.</span><span class="sxs-lookup"><span data-stu-id="04685-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators to minimize the number of people who have access to certain information such as personal data.</span></span> <span data-ttu-id="04685-125">Les permite detectar, restringir y supervisar identidades con privilegios y su acceso a recursos. También les permite asignar derechos administrativos Just-In-Time (JIT) temporales a usuarios aptos.</span><span class="sxs-lookup"><span data-stu-id="04685-125">It enables them to discover, restrict, and monitor privileged identities and their access to resources, and to assign temporary, Just-In-Time (JIT) administrative rights to eligible users.</span></span> <span data-ttu-id="04685-126">Asimismo, proporciona información sobre quién tiene privilegios administrativos de AAD.</span><span class="sxs-lookup"><span data-stu-id="04685-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="04685-127">Entre las actividades implicadas en el uso de AAD PIM se incluyen:</span><span class="sxs-lookup"><span data-stu-id="04685-127">The activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="04685-128">Habilitación de Privileged Identity Management para el directorio</span><span class="sxs-lookup"><span data-stu-id="04685-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="04685-129">Uso del panel del administrador de Privileged Identity Management para ver información importante de un vistazo</span><span class="sxs-lookup"><span data-stu-id="04685-129">Using Privileged Identity Management admin dashboard to see important information at a glance</span></span>

- <span data-ttu-id="04685-130">Administración de las identidades con privilegios (administradores) agregando o quitando administradores permanentes o aptos en cada rol</span><span class="sxs-lookup"><span data-stu-id="04685-130">Managing the privileged identities (administrators) by adding or removing permanent or eligible administrators to each role</span></span>

- <span data-ttu-id="04685-131">Configuración de las opciones de activación de rol</span><span class="sxs-lookup"><span data-stu-id="04685-131">Configuring the role activation settings</span></span>

- <span data-ttu-id="04685-132">Activación de roles</span><span class="sxs-lookup"><span data-stu-id="04685-132">Activating roles</span></span>

- <span data-ttu-id="04685-133">Revisión de la actividad de un rol</span><span class="sxs-lookup"><span data-stu-id="04685-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="04685-134">¿Cómo se puede habilitar AAD PIM?</span><span class="sxs-lookup"><span data-stu-id="04685-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="04685-135">Para empezar a usar PIM para su directorio, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04685-135">To start using PIM for your directory, do the following:</span></span>

1. <span data-ttu-id="04685-136">Inicie sesión en Azure Portal como administrador global de su directorio.</span><span class="sxs-lookup"><span data-stu-id="04685-136">Sign in to the Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="04685-137">Si su organización tiene más de un directorio, seleccione su nombre de usuario en la esquina superior derecha del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04685-137">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="04685-138">Seleccione el directorio donde va a usar Privileged Identity Management de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04685-138">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="04685-139">Seleccione **Más servicios** y use el cuadro de texto **Filtro** para buscar Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="04685-139">Select **More services** and use the **Filter** textbox to search for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="04685-140">Active **Anclar al panel** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="04685-140">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="04685-141">Se abre la aplicación Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="04685-141">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="04685-142">Después de configurar Azure AD Privileged Identity Management, verá la hoja de navegación cada vez que abra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04685-142">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="04685-143">Para obtener más información e instrucciones sobre cómo empezar a trabajar con AAD PIM, consulte [Comenzar a usar Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="04685-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="04685-144">Control de acceso basado en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="04685-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="04685-145">[Control de acceso basado en rol de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ayuda a los administradores de Azure a administrar el acceso a recursos de Azure habilitando la concesión de acceso en función del rol asignado del usuario.</span><span class="sxs-lookup"><span data-stu-id="04685-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access to Azure resources by enabling the granting of access based on the user’s assigned role.</span></span> <span data-ttu-id="04685-146">Puede separar los deberes de un equipo y conceder a los usuarios, grupos y aplicaciones únicamente el acceso que necesiten para su trabajo.</span><span class="sxs-lookup"><span data-stu-id="04685-146">You can segregate duties within a team and grant only the amount of access to users, groups and applications that they need to perform their jobs.</span></span>

<span data-ttu-id="04685-147">El acceso basado en rol se puede conceder a los usuarios que utilicen el Portal de Azure, las herramientas de la línea de comandos de Azure o las API de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="04685-147">Role-based access can be granted to users using the Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="04685-148">Para obtener más información sobre los aspectos básicos de RBAC de Azure, consulte [Introducción al control de acceso basado en rol en Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="04685-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in the Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="04685-149">¿Cómo se puede administrar RBAC de Azure con PowerShell?</span><span class="sxs-lookup"><span data-stu-id="04685-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="04685-150">Puede usar cmdlets de PowerShell para administrar RBAC de Azure, incluidas las siguientes tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="04685-150">You can use PowerShell cmdlets to manage Azure RBAC, including the following management tasks:</span></span>

- <span data-ttu-id="04685-151">Lista de roles</span><span class="sxs-lookup"><span data-stu-id="04685-151">List roles</span></span>

- <span data-ttu-id="04685-152">Consulta de quién ha accedido</span><span class="sxs-lookup"><span data-stu-id="04685-152">See who has access</span></span>

- <span data-ttu-id="04685-153">Conceder acceso</span><span class="sxs-lookup"><span data-stu-id="04685-153">Grant access</span></span>

- <span data-ttu-id="04685-154">Quitar acceso</span><span class="sxs-lookup"><span data-stu-id="04685-154">Remove access</span></span>

- <span data-ttu-id="04685-155">Crear un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="04685-155">Create a custom role</span></span>

- <span data-ttu-id="04685-156">Acciones Get para un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="04685-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="04685-157">Modificación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="04685-157">Modify a custom role</span></span>

- <span data-ttu-id="04685-158">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="04685-158">Delete a custom role</span></span>

- <span data-ttu-id="04685-159">Lista de roles personalizados</span><span class="sxs-lookup"><span data-stu-id="04685-159">List custom roles</span></span>

<span data-ttu-id="04685-160">Para obtener instrucciones sobre cómo administrar RBAC de Azure con PowerShell, consulte [Administración del acceso basado en rol con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="04685-160">For instructions on how to manage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="04685-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="04685-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="04685-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) es una solución de verificación en dos pasos que ayuda a proteger el acceso a los datos y las aplicaciones, además de satisfacer la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="04685-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access to data and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="04685-163">Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).</span><span class="sxs-lookup"><span data-stu-id="04685-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="04685-164">Para implementar MFA en la nube de Azure, debe habilitarlo primero y, a continuación, activar la verificación en dos pasos para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="04685-164">To deploy MFA in the Azure cloud, you need to first enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-to-use-mfa"></a><span data-ttu-id="04685-165">¿Cómo se puede habilitar Azure para usar MFA?</span><span class="sxs-lookup"><span data-stu-id="04685-165">How do I enable Azure to use MFA?</span></span>

<span data-ttu-id="04685-166">Si los usuarios tienen licencias que incluyen Azure Multi-Factor Authentication, no hay nada que se pueda hacer para activar Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="04685-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="04685-167">Si no las tienen, necesita crear un Proveedor de Multi-Factor Authentication en su directorio.</span><span class="sxs-lookup"><span data-stu-id="04685-167">If not, you need to create a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="04685-168">Para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="04685-168">To do this, follow these steps:</span></span>

1. <span data-ttu-id="04685-169">Seleccione **Active Directory** en el Portal de Azure clásico (conectado como administrador).</span><span class="sxs-lookup"><span data-stu-id="04685-169">Select **Active Directory** in the Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="04685-170">Seleccione **Proveedores de Multi-Factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="04685-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="04685-171">Seleccione **Nuevo** y, a continuación, en **App Services,** seleccione **Proveedor de Multi-Factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="04685-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="04685-172">Seleccione **Creación rápida.**</span><span class="sxs-lookup"><span data-stu-id="04685-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="04685-173">Rellene el campo de nombre y seleccione un modelo de uso (por autenticación o por usuario habilitado).</span><span class="sxs-lookup"><span data-stu-id="04685-173">Fill in the name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="04685-174">Designe un directorio con el que se asocie el Proveedor de MFA.</span><span class="sxs-lookup"><span data-stu-id="04685-174">Designate a directory with which the MFA Provider is associated.</span></span>

7. <span data-ttu-id="04685-175">Haga clic en el botón **Crear** .</span><span class="sxs-lookup"><span data-stu-id="04685-175">Click the **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="04685-176">Para obtener más instrucciones sobre cómo administrar el Proveedor de Multi-Factor Authentication, consulte [Introducción al Proveedor de Azure Multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="04685-176">For more instructions on how to manage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="04685-177">¿Cómo se puede activar la verificación en dos pasos para los usuarios?</span><span class="sxs-lookup"><span data-stu-id="04685-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="04685-178">Puede exigir la verificación en dos pasos para todos los inicios de sesión o crear directivas de acceso condicional para exigir la verificación en dos pasos únicamente cuando se apliquen condiciones específicas.</span><span class="sxs-lookup"><span data-stu-id="04685-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="04685-179">Habilitar Azure MFA mediante el cambio de estado del usuario es el enfoque tradicional para exigir la verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="04685-179">Enabling Azure MFA by changing user states is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="04685-180">Todos los usuarios que habilite tendrán el mismo requisito para realizar la verificación en dos pasos cada vez que inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="04685-180">All the users that you enable will have the same requirement to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="04685-181">La habilitación de un usuario invalida las directivas de acceso condicional que pudieran afectar a dicho usuario.</span><span class="sxs-lookup"><span data-stu-id="04685-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="04685-182">Habilitar Azure MFA con una directiva de acceso condicional es un enfoque más flexible para exigir la verificación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="04685-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="04685-183">Puede crear directivas de acceso condicional que se aplican a grupos, así como a usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="04685-183">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="04685-184">Los grupos de alto riesgo pueden recibir más restricciones que los grupos de bajo riesgo o bien la verificación en dos pasos puede ser necesaria solo para aplicaciones de alto riesgo en la nube y omitida para las de bajo riesgo.</span><span class="sxs-lookup"><span data-stu-id="04685-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="04685-185">Sin embargo, el acceso condicional es una característica de pago de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="04685-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="04685-186">Para habilitar MFA cambiando el estado del usuario, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04685-186">To enable MFA by changing user state, do the following:</span></span>

1. <span data-ttu-id="04685-187">Inicie sesión en Azure Portal como administrador.</span><span class="sxs-lookup"><span data-stu-id="04685-187">Sign in to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="04685-188">Vaya a **Azure Active Directory \> Usuarios y grupos \> Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="04685-188">Go to **Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="04685-189">Seleccione **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="04685-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="04685-190">Busque el usuario que desea habilitar para Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="04685-190">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="04685-191">Puede que necesite cambiar la vista en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="04685-191">You may need to change the view at the top.</span></span>
5. <span data-ttu-id="04685-192">Active la casilla situada junto al nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="04685-192">Check the box next to the user’s name.</span></span>
6. <span data-ttu-id="04685-193">En el lado derecho, bajo pasos rápidos, elija **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="04685-193">On the right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="04685-194">Confirme la selección en la ventana emergente que se abre.</span><span class="sxs-lookup"><span data-stu-id="04685-194">Confirm your selection in the pop-up window that opens.</span></span>  <span data-ttu-id="04685-195">Se pedirá a los usuarios para los que se ha habilitado MFA que se registren la próxima vez que inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="04685-195">Users for whom MFA has been enabled will be asked to register the next time they sign in.</span></span>

<span data-ttu-id="04685-196">Para habilitar Azure MFA con una directiva de acceso condicional, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04685-196">To enable Azure MFA with a conditional access policy, do the following:</span></span>

1. <span data-ttu-id="04685-197">Inicie sesión en Azure Portal como administrador.</span><span class="sxs-lookup"><span data-stu-id="04685-197">Sign in to the Azure portal as an administrator.</span></span>

2. <span data-ttu-id="04685-198">Vaya a **Azure Active Directory \> Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="04685-198">Go to **Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="04685-199">Seleccione **Nueva directiva**.</span><span class="sxs-lookup"><span data-stu-id="04685-199">Select **New policy**.</span></span>

4. <span data-ttu-id="04685-200">En **Asignaciones**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="04685-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="04685-201">Use las pestañas **Incluir** y     **Excluir** para especificar qué usuarios y grupos se administrarán con la directiva.</span><span class="sxs-lookup"><span data-stu-id="04685-201">Use the **Include** and     **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>

5. <span data-ttu-id="04685-202">En **Asignaciones**, seleccione **Aplicaciones en la nube.**</span><span class="sxs-lookup"><span data-stu-id="04685-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="04685-203">Elija **incluir Todas las aplicaciones en la nube**.</span><span class="sxs-lookup"><span data-stu-id="04685-203">Choose to **include All cloud apps**.</span></span>
6.  <span data-ttu-id="04685-204">En **Controles de acceso**, seleccione **Conceder**.</span><span class="sxs-lookup"><span data-stu-id="04685-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="04685-205">Seleccione **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="04685-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="04685-206">Cambie **Habilitar directiva** a **Activar** y, a continuación, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="04685-206">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="04685-207">Para obtener información sobre cómo establecer la configuración de Azure MFA para instalar alertas de fraude, crear una omisión por única vez, usar mensajes de voz personalizados, configurar el almacenamiento en caché, especificar direcciones IP de confianza, crear contraseñas de aplicación, habilitar el recuerdo de MFA para dispositivos que cuentan con la confianza de los usuarios y seleccionar métodos de verificación, consulte [Configuración de Azure Multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="04685-207">For information on how to configure Azure MFA settings to set up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="04685-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04685-208">Next steps</span></span>

- [<span data-ttu-id="04685-209">Protección del acceso con privilegios en Azure AD</span><span class="sxs-lookup"><span data-stu-id="04685-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="04685-210">Preguntas más frecuentes relacionadas con Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="04685-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="04685-211">Solución de problemas del control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="04685-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="04685-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="04685-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
