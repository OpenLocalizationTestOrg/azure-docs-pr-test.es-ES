---
title: "Configuración de LDAP seguro (LDAPS) en Azure AD Domain Services | Microsoft Docs"
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1ec3a-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="1ec3a-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="1ec3a-104">Este artículo muestra cómo puede habilitar el protocolo ligero de acceso a directorios seguro (LDAPS) para el dominio administrado con Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="1ec3a-105">LDAP seguro también se denomina "protocolo ligero de acceso a directorios (LDAP) en la Capa de sockets seguros (SSL)/Seguridad de la capa de transporte (TLS)".</span><span class="sxs-lookup"><span data-stu-id="1ec3a-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ec3a-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1ec3a-106">Before you begin</span></span>
<span data-ttu-id="1ec3a-107">Para realizar las tareas enumeradas en este artículo, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1ec3a-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="1ec3a-108">Una **suscripción de Azure**válida.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="1ec3a-109">Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="1ec3a-110">**Servicios de dominio de Azure AD** deben estar habilitado en el directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="1ec3a-111">Si no lo ha hecho, siga todas las tareas descritas en [Servicios de dominio de Azure AD (vista previa): introducción](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ec3a-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="1ec3a-112">Un **certificado que se usará para habilitar LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="1ec3a-113">**Recomendado**: obtenga un certificado de una entidad de certificación pública de confianza.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="1ec3a-114">Esta opción de configuración es más segura.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="1ec3a-115">Si lo prefiere, puede elegir [crear un certificado autofirmado](#task-1---obtain-a-certificate-for-secure-ldap) , tal y como se muestra más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="1ec3a-116">Requisitos para el certificado LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="1ec3a-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="1ec3a-117">Antes de habilitar LDAP seguro, adquiera un certificado válido de acuerdo con las instrucciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="1ec3a-118">Encontrará errores si intenta habilitar LDAP seguro para el dominio administrado con un certificado no válido o incorrecto.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="1ec3a-119">**Emisor de confianza**: el certificado debe ser emitido por una autoridad de confianza para los equipos que se conectan al dominio administrado mediante LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="1ec3a-120">Esta entidad puede ser una entidad de certificación pública de confianza para estos equipos.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="1ec3a-121">**Duración** : el certificado debe ser válido al menos para los próximos 3-6 meses.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="1ec3a-122">El acceso LDAP seguro a su dominio administrado se interrumpe cuando expira el certificado.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="1ec3a-123">**Nombre del firmante** : el nombre del firmante del certificado debe ser un comodín para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="1ec3a-124">Por ejemplo, si el dominio se denomina "contoso100.com", el nombre del firmante del certificado debe ser "*.contoso100.com".</span><span class="sxs-lookup"><span data-stu-id="1ec3a-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="1ec3a-125">Establezca el nombre DNS (nombre alternativo del firmante) en este nombre con caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="1ec3a-126">**Uso de la clave** : el certificado debe configurarse para los usos siguientes: firmas digitales y cifrado de claves.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="1ec3a-127">**Propósito del certificado** : el certificado debe ser válido para la autenticación del servidor SSL.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="1ec3a-128">**Entidades de certificación empresariales:** Azure AD Domain Services no admite el uso de certificados de LDAP seguros emitidos por la entidad de certificación empresarial de su organización.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="1ec3a-129">Esta restricción se debe a que el servicio no confía en la entidad de certificación empresarial como una entidad de certificación raíz.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="1ec3a-130">Tarea 1: Obtener un certificado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="1ec3a-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="1ec3a-131">La primera tarea implica la obtención de un certificado que se utilizará para el acceso LDAP seguro al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="1ec3a-132">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="1ec3a-132">You have two options:</span></span>

* <span data-ttu-id="1ec3a-133">Obtención de un certificado de una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="1ec3a-134">La entidad puede ser una entidad de certificación pública.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="1ec3a-135">Creación de un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="1ec3a-136">Opción A (recomendada): obtención de un certificado LDAP seguro desde una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="1ec3a-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="1ec3a-137">Si su organización obtiene los certificados de una entidad de certificación pública, debe obtener de esta el certificado LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="1ec3a-138">Al solicitar un certificado, asegúrese de cumplir todos los requisitos descritos en [Requisitos para el certificado LDAP seguro](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="1ec3a-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="1ec3a-139">Los equipos cliente que necesitan conectarse al dominio administrado mediante LDAP seguro deben confiar en el emisor del certificado de LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="1ec3a-140">Opción B: creación de un certificado autofirmado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="1ec3a-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="1ec3a-141">Si prevé que no usará un certificado de una entidad de certificación pública, puede crear un certificado autofirmado para LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="1ec3a-142">**Creación de un certificado autofirmado con PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1ec3a-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="1ec3a-143">En el equipo de Windows, abra una nueva ventana de PowerShell como **Administrador** y escriba los comandos siguientes para crear un nuevo certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="1ec3a-144">En el ejemplo anterior, reemplace "*.contoso100.com" por el nombre de dominio DNS de su dominio administrado. Por ejemplo, si ha creado un dominio administrado denominado "contoso100.onmicrosoft.com", reemplace "*.contoso100.com" en el script anterior con "*.contoso100.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="1ec3a-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selección de un directorio de Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="1ec3a-146">El certificado autofirmado recién creado se colocará en el almacén de certificados del equipo local.</span><span class="sxs-lookup"><span data-stu-id="1ec3a-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="1ec3a-147">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1ec3a-147">Next step</span></span>
[<span data-ttu-id="1ec3a-148">Tarea 2: Exportar el certificado LDAP seguro a un archivo .PFX</span><span class="sxs-lookup"><span data-stu-id="1ec3a-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
