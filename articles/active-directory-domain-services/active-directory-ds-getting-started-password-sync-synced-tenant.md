---
title: "Active Directory Domain Services: habilitación de la sincronización de contraseñas | Microsoft Docs"
description: "Introducción a los Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="dcad9-103">Habilitar la sincronización de contraseña tooAzure los servicios de dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcad9-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="dcad9-104">En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dcad9-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="dcad9-105">tarea siguiente de Hello es tooenable sincronización de hashes de credenciales que requiere para tooAzure de autenticación de NT LAN Manager (NTLM) y Kerberos servicios de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="dcad9-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="dcad9-106">Una vez haya configurado la sincronización de credenciales, los usuarios pueden iniciar sesión toohello dominio administrado con sus credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="dcad9-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="dcad9-107">Hola pasos implicados son diferentes para cuentas de usuario de vs de cuentas de usuario solo en la nube que se sincronizan desde su directorio local mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dcad9-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="dcad9-108">Si su inquilino de Azure AD tiene una combinación de la nube solo los usuarios y los usuarios de sus instalaciones en AD, necesita tooperform ambos pasos.</span><span class="sxs-lookup"><span data-stu-id="dcad9-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="dcad9-109">**Las cuentas de usuario solo en la nube**: [sincronizar contraseñas para cuentas de usuario solo en la nube dominio administrado tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="dcad9-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="dcad9-110">**Las cuentas de usuario local**: [sincronizar contraseñas para cuentas de usuario que se ha sincronizado desde local AD tooyour administrado dominio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="dcad9-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="dcad9-111">Tarea 5: habilitar la sincronización de contraseña tooyour dominio administrado para cuentas de usuario se sincronizan con sus instalaciones en AD</span><span class="sxs-lookup"><span data-stu-id="dcad9-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="dcad9-112">Azure sincronizó un inquilino de AD se establece toosynchronize con el directorio local de su organización mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dcad9-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="dcad9-113">De forma predeterminada, Azure AD Connect no sincroniza NTLM y Kerberos tooAzure de hashes de credenciales AD.</span><span class="sxs-lookup"><span data-stu-id="dcad9-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="dcad9-114">toouse servicios de dominio de AD de Azure, deberá tooconfigure Azure AD Connect toosynchronize códigos hash de credenciales necesarios para la autenticación NTLM y Kerberos.</span><span class="sxs-lookup"><span data-stu-id="dcad9-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="dcad9-115">Hola pasos Habilitar sincronización de hashes de credenciales de hello necesaria del inquilino de Azure AD tooyour directorio local.</span><span class="sxs-lookup"><span data-stu-id="dcad9-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="dcad9-116">Si su organización tiene cuentas de usuario que se sincronizan desde su directorio local, debe habilitar la sincronización de hash de NTLM y Kerberos en el dominio administrado de orden toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="dcad9-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="dcad9-117">Una cuenta de usuario sincronizado es una cuenta que se creó en el directorio local y sincroniza a tooyour inquilino de Azure AD mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dcad9-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="dcad9-118">Instalación o actualización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="dcad9-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="dcad9-119">Instalar hello más reciente recomendada equipo unido a un lanzamiento de Azure AD Connect en un dominio.</span><span class="sxs-lookup"><span data-stu-id="dcad9-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="dcad9-120">Si tiene una instancia existente del programa de instalación de Azure AD Connect, necesita tooupdate, versión más reciente de hello toouse de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dcad9-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="dcad9-121">tooavoid conoce problemas o errores que pueden ya se han corregido, asegúrese de usar siempre la versión más reciente de Hola de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dcad9-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="dcad9-122">**[Descarga de Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="dcad9-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="dcad9-123">Versión recomendada: **1.1.553.0**, publicada el 27 de junio de 2017.</span><span class="sxs-lookup"><span data-stu-id="dcad9-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="dcad9-124">DEBE instalar hello más reciente recomienda versión de inquilino de Azure AD Connect tooenable Hola contraseña heredado credenciales (necesario para la autenticación NTLM y Kerberos) toosynchronize tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcad9-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="dcad9-125">Esta funcionalidad no está disponible en versiones anteriores de Azure AD Connect o con la herramienta de sincronización de directorios de hello heredado.</span><span class="sxs-lookup"><span data-stu-id="dcad9-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="dcad9-126">Instrucciones de instalación de Azure AD Connect están disponibles en los siguientes Hola artículo - [Introducción a Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="dcad9-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="dcad9-127">Habilitar la sincronización de NTLM y Kerberos tooAzure de hashes de credenciales AD</span><span class="sxs-lookup"><span data-stu-id="dcad9-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="dcad9-128">Ejecute hello siguiente script de PowerShell en cada bosque de AD, sincronización de contraseñas total tooforce y habilitar a inquilino de todos los usuarios locales credencial hashes toosync tooyour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcad9-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="dcad9-129">Esta secuencia de comandos permite hashes de credenciales de hello necesarios para el inquilino de tooyour sincronizada Azure AD de toobe de autenticación NTLM o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="dcad9-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="dcad9-130">Según el tamaño de hello del directorio (número de usuarios, grupos etc.), la sincronización de credenciales se aplica un algoritmo hash tooAzure AD lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="dcad9-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="dcad9-131">las contraseñas de Hola se podrán usar en el dominio administrado de los servicios de dominio de AD de Azure de hello poco después de que han sincronizado hashes de credenciales de hello tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="dcad9-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="dcad9-132">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="dcad9-132">Related Content</span></span>
* [<span data-ttu-id="dcad9-133">Habilitar la sincronización de contraseña tooAAD los servicios de dominio de un solo en la nube Azure directorio de AD</span><span class="sxs-lookup"><span data-stu-id="dcad9-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="dcad9-134">Administración de un dominio administrado con Servicios de dominio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcad9-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="dcad9-135">Unirse a un dominio administrado de Windows máquina virtual tooan servicios de dominio de AD de Azure</span><span class="sxs-lookup"><span data-stu-id="dcad9-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="dcad9-136">Unirse a un dominio administrado de Red Hat Enterprise Linux máquina virtual tooan servicios de dominio de AD de Azure</span><span class="sxs-lookup"><span data-stu-id="dcad9-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
