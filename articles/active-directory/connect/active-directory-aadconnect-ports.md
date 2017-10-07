---
title: "La identidad híbrida requería puertos y protocolos - Azure | Microsoft Docs"
description: "Esta página es una página de referencia técnica para puertos que sean necesario toobe abierto para Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a><span data-ttu-id="f546d-103">La identidad híbrida requería puertos y protocolos</span><span class="sxs-lookup"><span data-stu-id="f546d-103">Hybrid Identity Required Ports and Protocols</span></span>
<span data-ttu-id="f546d-104">Hola después de documento es una referencia técnica en hello requerido puertos y protocolos para implementar una solución de identidad híbrida.</span><span class="sxs-lookup"><span data-stu-id="f546d-104">hello following document is a technical reference on hello required ports and protocols for implementing a hybrid identity solution.</span></span> <span data-ttu-id="f546d-105">Utilice Hola después de ilustración y consulte toohello de tabla correspondiente.</span><span class="sxs-lookup"><span data-stu-id="f546d-105">Use hello following illustration and refer toohello corresponding table.</span></span>

![Qué es Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a><span data-ttu-id="f546d-107">Tabla 1: Azure AD Connect y AD local</span><span class="sxs-lookup"><span data-stu-id="f546d-107">Table 1 - Azure AD Connect and On-premises AD</span></span>
<span data-ttu-id="f546d-108">Esta tabla describe Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect hello y AD local.</span><span class="sxs-lookup"><span data-stu-id="f546d-108">This table describes hello ports and protocols that are required for communication between hello Azure AD Connect server and on-premises AD.</span></span>

| <span data-ttu-id="f546d-109">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-109">Protocol</span></span> | <span data-ttu-id="f546d-110">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-110">Ports</span></span> | <span data-ttu-id="f546d-111">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-112">DNS</span><span class="sxs-lookup"><span data-stu-id="f546d-112">DNS</span></span> |<span data-ttu-id="f546d-113">53 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-113">53 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-114">Búsquedas de DNS en el bosque de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="f546d-114">DNS lookups on hello destination forest.</span></span> |
| <span data-ttu-id="f546d-115">Kerberos</span><span class="sxs-lookup"><span data-stu-id="f546d-115">Kerberos</span></span> |<span data-ttu-id="f546d-116">88 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-116">88 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-117">Bosque de AD toohello de autenticación de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f546d-117">Kerberos authentication toohello AD forest.</span></span> |
| <span data-ttu-id="f546d-118">MS-RPC</span><span class="sxs-lookup"><span data-stu-id="f546d-118">MS-RPC</span></span> |<span data-ttu-id="f546d-119">135 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-119">135 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-120">Se utiliza durante la configuración inicial del Asistente de Azure AD Connect de hello cuando enlaza toohello AD bosque de Hola y también durante la sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="f546d-120">Used during hello initial configuration of hello Azure AD Connect wizard when it binds toohello AD forest, and also during Password synchronization.</span></span> |
| <span data-ttu-id="f546d-121">LDAP</span><span class="sxs-lookup"><span data-stu-id="f546d-121">LDAP</span></span> |<span data-ttu-id="f546d-122">389 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-122">389 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-123">Se usa para la importación de datos de AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-123">Used for data import from AD.</span></span> <span data-ttu-id="f546d-124">Los datos se cifran con Kerberos Sign & Seal.</span><span class="sxs-lookup"><span data-stu-id="f546d-124">Data is encrypted with Kerberos Sign & Seal.</span></span> |
| <span data-ttu-id="f546d-125">RPC</span><span class="sxs-lookup"><span data-stu-id="f546d-125">RPC</span></span> | <span data-ttu-id="f546d-126">445 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-126">445 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-127">Utilizando una cuenta de equipo en el bosque de AD Hola de toocreate SSO sin problemas.</span><span class="sxs-lookup"><span data-stu-id="f546d-127">Used by Seamless SSO toocreate a computer account in hello AD forest.</span></span> |
| <span data-ttu-id="f546d-128">LDAP/SSL</span><span class="sxs-lookup"><span data-stu-id="f546d-128">LDAP/SSL</span></span> |<span data-ttu-id="f546d-129">636 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-129">636 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-130">Se usa para la importación de datos de AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-130">Used for data import from AD.</span></span> <span data-ttu-id="f546d-131">transferencia de datos de Hello estarán firmada y cifrada.</span><span class="sxs-lookup"><span data-stu-id="f546d-131">hello data transfer is signed and encrypted.</span></span> <span data-ttu-id="f546d-132">Solo se utiliza si está usando SSL.</span><span class="sxs-lookup"><span data-stu-id="f546d-132">Only used if you are using SSL.</span></span> |
| <span data-ttu-id="f546d-133">RPC</span><span class="sxs-lookup"><span data-stu-id="f546d-133">RPC</span></span> |<span data-ttu-id="f546d-134">49152- 65535 (Puerto RCP alto aleatorio)(TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-134">49152- 65535 (Random high RPC Port)(TCP/UDP)</span></span> |<span data-ttu-id="f546d-135">Se utiliza durante la configuración inicial de Hola de Azure AD Connect cuando enlaza toohello AD bosques y durante la sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="f546d-135">Used during hello initial configuration of Azure AD Connect when it binds toohello AD forests, and during Password synchronization.</span></span> <span data-ttu-id="f546d-136">Consulte [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) y [KB224196](https://support.microsoft.com/kb/224196) para más información.</span><span class="sxs-lookup"><span data-stu-id="f546d-136">See [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017), and [KB224196](https://support.microsoft.com/kb/224196) for more information.</span></span> |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a><span data-ttu-id="f546d-137">Tabla 2: Azure AD Connect y Azure AD</span><span class="sxs-lookup"><span data-stu-id="f546d-137">Table 2 - Azure AD Connect and Azure AD</span></span>
<span data-ttu-id="f546d-138">Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect hello y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-138">This table describes hello ports and protocols that are required for communication between hello Azure AD Connect server and Azure AD.</span></span>

| <span data-ttu-id="f546d-139">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-139">Protocol</span></span> | <span data-ttu-id="f546d-140">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-140">Ports</span></span> | <span data-ttu-id="f546d-141">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-142">HTTP</span><span class="sxs-lookup"><span data-stu-id="f546d-142">HTTP</span></span> |<span data-ttu-id="f546d-143">80 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-143">80 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-144">Usa certificados SSL de tooverify toodownload CRL (listas de revocación de certificados).</span><span class="sxs-lookup"><span data-stu-id="f546d-144">Used toodownload CRLs (Certificate Revocation Lists) tooverify SSL certificates.</span></span> |
| <span data-ttu-id="f546d-145">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-145">HTTPS</span></span> |<span data-ttu-id="f546d-146">443 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-146">443(TCP/UDP)</span></span> |<span data-ttu-id="f546d-147">Toosynchronize usado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-147">Used toosynchronize with Azure AD.</span></span> |

<span data-ttu-id="f546d-148">Para obtener una lista de direcciones URL e IP direcciones necesita tooopen en el firewall, vea [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span><span class="sxs-lookup"><span data-stu-id="f546d-148">For a list of URLs and IP addresses you need tooopen in your firewall, see [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span></span>

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a><span data-ttu-id="f546d-149">Tabla 3: Azure AD Connect y servidores de federación AD FS/WAP</span><span class="sxs-lookup"><span data-stu-id="f546d-149">Table 3 - Azure AD Connect and AD FS Federation Servers/WAP</span></span>
<span data-ttu-id="f546d-150">Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect de Hola y servidores de federación/WAP de AD FS.</span><span class="sxs-lookup"><span data-stu-id="f546d-150">This table describes hello ports and protocols that are required for communication between hello Azure AD Connect server and AD FS Federation/WAP servers.</span></span>  

| <span data-ttu-id="f546d-151">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-151">Protocol</span></span> | <span data-ttu-id="f546d-152">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-152">Ports</span></span> | <span data-ttu-id="f546d-153">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-153">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-154">HTTP</span><span class="sxs-lookup"><span data-stu-id="f546d-154">HTTP</span></span> |<span data-ttu-id="f546d-155">80 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-155">80 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-156">Usa certificados SSL de tooverify toodownload CRL (listas de revocación de certificados).</span><span class="sxs-lookup"><span data-stu-id="f546d-156">Used toodownload CRLs (Certificate Revocation Lists) tooverify SSL certificates.</span></span> |
| <span data-ttu-id="f546d-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-157">HTTPS</span></span> |<span data-ttu-id="f546d-158">443 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-158">443(TCP/UDP)</span></span> |<span data-ttu-id="f546d-159">Toosynchronize usado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-159">Used toosynchronize with Azure AD.</span></span> |
| <span data-ttu-id="f546d-160">WinRM</span><span class="sxs-lookup"><span data-stu-id="f546d-160">WinRM</span></span> |<span data-ttu-id="f546d-161">5985</span><span class="sxs-lookup"><span data-stu-id="f546d-161">5985</span></span> |<span data-ttu-id="f546d-162">Agente de escucha de WinRM</span><span class="sxs-lookup"><span data-stu-id="f546d-162">WinRM Listener</span></span> |

## <a name="table-4---wap-and-federation-servers"></a><span data-ttu-id="f546d-163">Tabla 4: Servidores de federación y WAP</span><span class="sxs-lookup"><span data-stu-id="f546d-163">Table 4 - WAP and Federation Servers</span></span>
<span data-ttu-id="f546d-164">Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre servidores de federación de Hola y los servidores WAP.</span><span class="sxs-lookup"><span data-stu-id="f546d-164">This table describes hello ports and protocols that are required for communication between hello Federation servers and WAP servers.</span></span>

| <span data-ttu-id="f546d-165">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-165">Protocol</span></span> | <span data-ttu-id="f546d-166">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-166">Ports</span></span> | <span data-ttu-id="f546d-167">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-167">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-168">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-168">HTTPS</span></span> |<span data-ttu-id="f546d-169">443 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-169">443(TCP/UDP)</span></span> |<span data-ttu-id="f546d-170">Se usa para autenticación.</span><span class="sxs-lookup"><span data-stu-id="f546d-170">Used for authentication.</span></span> |

## <a name="table-5---wap-and-users"></a><span data-ttu-id="f546d-171">Tabla 5 - WAP y usuarios</span><span class="sxs-lookup"><span data-stu-id="f546d-171">Table 5 - WAP and Users</span></span>
<span data-ttu-id="f546d-172">Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre los usuarios y los servidores WAP Hola.</span><span class="sxs-lookup"><span data-stu-id="f546d-172">This table describes hello ports and protocols that are required for communication between users and hello WAP servers.</span></span>

| <span data-ttu-id="f546d-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-173">Protocol</span></span> | <span data-ttu-id="f546d-174">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-174">Ports</span></span> | <span data-ttu-id="f546d-175">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-176">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-176">HTTPS</span></span> |<span data-ttu-id="f546d-177">443 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-177">443(TCP/UDP)</span></span> |<span data-ttu-id="f546d-178">Se usa para la autenticación de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f546d-178">Used for device authentication.</span></span> |
| <span data-ttu-id="f546d-179">TCP</span><span class="sxs-lookup"><span data-stu-id="f546d-179">TCP</span></span> |<span data-ttu-id="f546d-180">49443 (TCP)</span><span class="sxs-lookup"><span data-stu-id="f546d-180">49443 (TCP)</span></span> |<span data-ttu-id="f546d-181">Se usa para la autenticación de certificados.</span><span class="sxs-lookup"><span data-stu-id="f546d-181">Used for certificate authentication.</span></span> |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a><span data-ttu-id="f546d-182">Tabla 6a y 6b: autenticación de paso a través con inicio de sesión único (SSO) y sincronización de Hash de contraseña con inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="f546d-182">Table 6a & 6b - Pass-through Authentication with Single Sign On (SSO) and Password Hash Sync with Single Sign On (SSO)</span></span>
<span data-ttu-id="f546d-183">Hola las tablas siguientes describe Hola puertos y protocolos que son necesarios para la comunicación entre hello Azure AD Connect y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-183">hello following tables describes hello ports and protocols that are required for communication between hello Azure AD Connect and Azure AD.</span></span>

### <a name="table-6a---pass-through-authentication-with-sso"></a><span data-ttu-id="f546d-184">Tabla 6a: autenticación de paso a través con SSO</span><span class="sxs-lookup"><span data-stu-id="f546d-184">Table 6a - Pass-through Authentication with SSO</span></span>
|<span data-ttu-id="f546d-185">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-185">Protocol</span></span>|<span data-ttu-id="f546d-186">Número de puerto</span><span class="sxs-lookup"><span data-stu-id="f546d-186">Port Number</span></span>|<span data-ttu-id="f546d-187">Descripción</span><span class="sxs-lookup"><span data-stu-id="f546d-187">Description</span></span>
| --- | --- | ---
|<span data-ttu-id="f546d-188">HTTP</span><span class="sxs-lookup"><span data-stu-id="f546d-188">HTTP</span></span>|<span data-ttu-id="f546d-189">80</span><span class="sxs-lookup"><span data-stu-id="f546d-189">80</span></span>|<span data-ttu-id="f546d-190">Habilita el tráfico HTTP saliente para la validación de seguridad, como SSL.</span><span class="sxs-lookup"><span data-stu-id="f546d-190">Enable outbound HTTP traffic for security validation such as SSL.</span></span> <span data-ttu-id="f546d-191">También sea necesario para el conector de Hola de actualización automática capacidad toofunction correctamente.</span><span class="sxs-lookup"><span data-stu-id="f546d-191">Also needed for hello connector auto-update capability toofunction properly.</span></span>
|<span data-ttu-id="f546d-192">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-192">HTTPS</span></span>|<span data-ttu-id="f546d-193">443</span><span class="sxs-lookup"><span data-stu-id="f546d-193">443</span></span>| <span data-ttu-id="f546d-194">Habilitar el tráfico HTTPS saliente para operaciones como habilitar y deshabilitar la característica de hello, registrar conectores, descarga las actualizaciones de conector y controlar todas las solicitudes de inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="f546d-194">Enable outbound HTTPS traffic for operations such as enabling and disabling of hello feature, registering connectors, downloading connector updates, and handling all user sign-in requests.</span></span>

<span data-ttu-id="f546d-195">Además, Azure AD Connect debe toobe toomake capaz de direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f546d-195">In addition, Azure AD Connect needs toobe able toomake direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span></span>

### <a name="table-6b---password-hash-sync-with-sso"></a><span data-ttu-id="f546d-196">Tabla 6b: sincronización de Hash de contraseña con SSO</span><span class="sxs-lookup"><span data-stu-id="f546d-196">Table 6b - Password Hash Sync with SSO</span></span>

|<span data-ttu-id="f546d-197">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-197">Protocol</span></span>|<span data-ttu-id="f546d-198">Número de puerto</span><span class="sxs-lookup"><span data-stu-id="f546d-198">Port Number</span></span>|<span data-ttu-id="f546d-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="f546d-199">Description</span></span>
| --- | --- | ---
|<span data-ttu-id="f546d-200">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-200">HTTPS</span></span>|<span data-ttu-id="f546d-201">443</span><span class="sxs-lookup"><span data-stu-id="f546d-201">443</span></span>| <span data-ttu-id="f546d-202">Habilite el registro SSO (sólo es necesario para hello proceso de registro SSO).</span><span class="sxs-lookup"><span data-stu-id="f546d-202">Enable SSO registration (required only for hello SSO registration process).</span></span>

<span data-ttu-id="f546d-203">Además, Azure AD Connect debe toobe toomake capaz de direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f546d-203">In addition, Azure AD Connect needs toobe able toomake direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653).</span></span> <span data-ttu-id="f546d-204">Una vez más, esto solo es necesario para el proceso de registro de hello SSO.</span><span class="sxs-lookup"><span data-stu-id="f546d-204">Again, this is only required for hello SSO registration process.</span></span>

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a><span data-ttu-id="f546d-205">Tabla 7a y 7b: Agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD</span><span class="sxs-lookup"><span data-stu-id="f546d-205">Table 7a & 7b - Azure AD Connect Health agent for (AD FS/Sync) and Azure AD</span></span>
<span data-ttu-id="f546d-206">Hello en las tablas siguientes se describen los puntos de conexión de hello, puertos y protocolos que son necesarios para la comunicación entre agentes de mantenimiento de Azure AD Connect y Azure AD</span><span class="sxs-lookup"><span data-stu-id="f546d-206">hello following tables describe hello endpoints, ports, and protocols that are required for communication between Azure AD Connect Health agents and Azure AD</span></span>

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a><span data-ttu-id="f546d-207">Tabla 7a: Puertos y protocolos para el agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD</span><span class="sxs-lookup"><span data-stu-id="f546d-207">Table 7a - Ports and Protocols for Azure AD Connect Health agent for (AD FS/Sync) and Azure AD</span></span>
<span data-ttu-id="f546d-208">Esta tabla describen Hola siguiendo los puertos de salida y los protocolos que son necesarios para la comunicación entre agentes de hello Azure AD Connect Health y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f546d-208">This table describes hello following outbound ports and protocols that are required for communication between hello Azure AD Connect Health agents and Azure AD.</span></span>  

| <span data-ttu-id="f546d-209">Protocol</span><span class="sxs-lookup"><span data-stu-id="f546d-209">Protocol</span></span> | <span data-ttu-id="f546d-210">Puertos</span><span class="sxs-lookup"><span data-stu-id="f546d-210">Ports</span></span> | <span data-ttu-id="f546d-211">Description</span><span class="sxs-lookup"><span data-stu-id="f546d-211">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f546d-212">HTTPS</span><span class="sxs-lookup"><span data-stu-id="f546d-212">HTTPS</span></span> |<span data-ttu-id="f546d-213">443 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-213">443(TCP/UDP)</span></span> |<span data-ttu-id="f546d-214">Salida</span><span class="sxs-lookup"><span data-stu-id="f546d-214">Outbound</span></span> |
| <span data-ttu-id="f546d-215">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="f546d-215">Azure Service Bus</span></span> |<span data-ttu-id="f546d-216">5671 (TCP/UDP)</span><span class="sxs-lookup"><span data-stu-id="f546d-216">5671 (TCP/UDP)</span></span> |<span data-ttu-id="f546d-217">Salida</span><span class="sxs-lookup"><span data-stu-id="f546d-217">Outbound</span></span> |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a><span data-ttu-id="f546d-218">7b: Puntos de conexión para el agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD</span><span class="sxs-lookup"><span data-stu-id="f546d-218">7b - Endpoints for Azure AD Connect Health agent for (AD FS/Sync) and Azure AD</span></span>
<span data-ttu-id="f546d-219">Para obtener una lista de puntos de conexión, consulte [Hola sección de requisitos para el agente de hello Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="f546d-219">For a list of endpoints, see [hello Requirements section for hello Azure AD Connect Health agent](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).</span></span>
