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
ms.openlocfilehash: 947ea3c9d789ecf5a754001aafcda6f8bcd41047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="07082-103">Habilitación de la sincronización de contraseñas con Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="07082-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="07082-104">En las tareas anteriores, habilitó Azure Active Directory Domain Services para su inquilino de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07082-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="07082-105">La siguiente tarea consiste en habilitar la sincronización de los hashes de credenciales necesarios para que la autenticación NT LAN Manager (NTLM) y Kerberos se sincronice con Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="07082-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="07082-106">Una vez configurada la sincronización de credenciales, los usuarios pueden iniciar sesión en el dominio administrado mediante sus credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="07082-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="07082-107">Los pasos necesarios son diferentes según se trate de cuentas de usuario solo de nube o de las cuentas de usuarios que se sincronizan desde el directorio local mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="07082-108">Si el inquilino de Azure AD tiene una combinación entre usuarios solo de nube y usuarios de la instalación local de AD, deberá realizar ambos pasos.</span><span class="sxs-lookup"><span data-stu-id="07082-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="07082-109">**Cuentas de usuario solo de nube**: [Sincronización de contraseñas de cuentas de usuario solo de nube con el dominio administrado](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="07082-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="07082-110">**Cuentas de usuario locales**: [Sincronización de contraseñas de cuentas de usuario sincronizadas desde la instancia local de AD con el dominio administrado](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="07082-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="07082-111">Tarea 5: habilitar la sincronización de contraseñas con el dominio administrado para las cuentas de usuario sincronizadas con la instancia local de AD</span><span class="sxs-lookup"><span data-stu-id="07082-111">Task 5: enable password synchronization to your managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="07082-112">Se establece un inquilino de Azure AD para sincronizar con el directorio local de su organización con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-112">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="07082-113">De forma predeterminada, Azure AD Connect no sincroniza los hashes de credenciales de NTLM y Kerberos con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07082-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD.</span></span> <span data-ttu-id="07082-114">Para usar Azure AD Domain Services, debe configurar Azure AD Connect para sincronizar los hashes de credenciales necesarios para la autenticación NTLM y Kerberos.</span><span class="sxs-lookup"><span data-stu-id="07082-114">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="07082-115">Los pasos siguientes permiten la sincronización de los hashes de credenciales necesarios del directorio local con el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07082-115">The following steps enable synchronization of the required credential hashes from your on-premises directory to your Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="07082-116">Si la organización tiene cuentas de usuario que están sincronizadas desde el directorio local, debe habilitar la sincronización de los hashes de NTLM y Kerberos para usar el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="07082-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order to use the managed domain.</span></span> <span data-ttu-id="07082-117">Una cuenta de usuario sincronizada es una cuenta que se creó en el directorio local y se ha sincronizado con el inquilino de Azure AD mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-117">A synced user account is an account that was created in your on-premises directory and is synchronized to your Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="07082-118">Instalación o actualización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="07082-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="07082-119">Instale la versión recomendada más reciente de Azure AD Connect en un equipo unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="07082-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="07082-120">Si tiene una instancia existente del programa de instalación de Azure AD Connect, debe actualizarla para usar la versión más reciente de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="07082-121">Con el fin de evitar errores y problemas conocidos que puedan estar ya corregidos, asegúrese de usar la versión más reciente de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="07082-122">**[Descarga de Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="07082-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="07082-123">Versión recomendada: **1.1.553.0**, publicada el 27 de junio de 2017.</span><span class="sxs-lookup"><span data-stu-id="07082-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="07082-124">Para permitir que las credenciales de contraseñas heredadas (necesarias para la autenticación de NTLM y Kerberos) se sincronicen con el inquilino de Azure AD, DEBE instalar la versión recomendada más reciente de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="07082-124">You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant.</span></span> <span data-ttu-id="07082-125">Esta funcionalidad no está disponible en versiones anteriores de Azure AD Connect o con la herramienta DirSync heredada.</span><span class="sxs-lookup"><span data-stu-id="07082-125">This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="07082-126">Puede encontrar las instrucciones de instalación de Azure AD Connect en el siguiente artículo: [Introducción a Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="07082-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="07082-127">Habilitación de la sincronización de valores hash de credenciales de NTLM y Kerberos con Azure AD</span><span class="sxs-lookup"><span data-stu-id="07082-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="07082-128">Ejecute el siguiente script de PowerShell en cada bosque de AD para forzar la sincronización completa de contraseñas y permitir que los hashes de credenciales de los usuarios locales se sincronicen con el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07082-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="07082-129">Este script permite que los hashes de credenciales necesarios para que la autenticación NTLM o Kerberos se sincronice con el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07082-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

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

<span data-ttu-id="07082-130">En función del tamaño de su directorio (número de usuarios o grupos, por ejemplo), la sincronización de los hashes de credenciales con Azure AD llevará tiempo.</span><span class="sxs-lookup"><span data-stu-id="07082-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="07082-131">Las contraseñas se podrán usar en el dominio administrado de los Servicios de dominio de Azure AD poco después de que los valores hash se hayan sincronizado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07082-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="07082-132">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="07082-132">Related Content</span></span>
* [<span data-ttu-id="07082-133">Habilitación de la sincronización de contraseñas con los Servicios de dominio de Azure AD para un directorio de Azure AD solo de nube</span><span class="sxs-lookup"><span data-stu-id="07082-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="07082-134">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="07082-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="07082-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain (Unión de una máquina virtual con Windows a un dominio administrado de Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="07082-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="07082-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain (Unión de una máquina virtual con Red Hat Enterprise Linux a un dominio administrado de Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="07082-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
