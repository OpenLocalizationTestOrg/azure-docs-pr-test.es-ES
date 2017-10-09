---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="86010-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="86010-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="86010-104">Este artículo muestra cómo puede habilitar el protocolo ligero de acceso a directorios seguro (LDAPS) para el dominio administrado con Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86010-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="86010-105">LDAP seguro también se denomina "protocolo ligero de acceso a directorios (LDAP) en la Capa de sockets seguros (SSL)/Seguridad de la capa de transporte (TLS)".</span><span class="sxs-lookup"><span data-stu-id="86010-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86010-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="86010-106">Before you begin</span></span>
<span data-ttu-id="86010-107">tareas de hello tooperform enumeradas en este artículo, necesita:</span><span class="sxs-lookup"><span data-stu-id="86010-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="86010-108">Una **suscripción de Azure**válida.</span><span class="sxs-lookup"><span data-stu-id="86010-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="86010-109">Un **directorio de Azure AD** : sincronizado con un directorio local o solo en la nube.</span><span class="sxs-lookup"><span data-stu-id="86010-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="86010-110">**Servicios de dominio de Azure AD** debe estar habilitada para directorio de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86010-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="86010-111">Si lo ha hecho, siga todas las tareas de hello descritas en hello [Guía de introducción](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="86010-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="86010-112">A **tooenable de toobe usa certificado LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="86010-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="86010-113">**Recomendado**: obtenga un certificado de una entidad de certificación pública de confianza.</span><span class="sxs-lookup"><span data-stu-id="86010-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="86010-114">Esta opción de configuración es más segura.</span><span class="sxs-lookup"><span data-stu-id="86010-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="86010-115">Como alternativa, también puede elegir demasiado[crear un certificado autofirmado](#task-1---obtain-a-certificate-for-secure-ldap) tal como se muestra más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="86010-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="86010-116">Requisitos de certificado LDAP seguro Hola</span><span class="sxs-lookup"><span data-stu-id="86010-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="86010-117">Adquirir un certificado válido por hello siguiendo las directrices, antes de habilitar LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="86010-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="86010-118">Que se produzcan errores si intenta tooenable LDAP seguro para el dominio administrado con un certificado incorrecto o no es válido.</span><span class="sxs-lookup"><span data-stu-id="86010-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="86010-119">**Emisor de confianza** -certificado Hola debe ser emitido por una entidad de confianza para los equipos que se conectan toohello dominio administrado mediante LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="86010-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="86010-120">Esta entidad puede ser una entidad de certificación pública de confianza para estos equipos.</span><span class="sxs-lookup"><span data-stu-id="86010-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="86010-121">**Duración** -Hola certificado debe ser válido para al menos hello en los próximos 3 a 6 meses.</span><span class="sxs-lookup"><span data-stu-id="86010-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="86010-122">LDAP acceso tooyour administrado dominio seguro se interrumpe cuando expira el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="86010-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="86010-123">**Nombre de sujeto** -nombre de sujeto Hola certificado Hola debe ser un carácter comodín para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="86010-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="86010-124">Por ejemplo, si el dominio se denomina 'contoso100.com', nombre de sujeto del certificado de hello debe ser ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="86010-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="86010-125">Hola DNS nombre (nombre alternativo del sujeto) toothis comodín nombre del conjunto.</span><span class="sxs-lookup"><span data-stu-id="86010-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="86010-126">**Uso de la clave** - Hola certificado debe configurarse para hello después usa - firmas digitales y cifrado de clave.</span><span class="sxs-lookup"><span data-stu-id="86010-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="86010-127">**Propósito de certificado** -Hola certificado debe ser válido para la autenticación de servidor SSL.</span><span class="sxs-lookup"><span data-stu-id="86010-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="86010-128">**Entidades de certificación empresariales:** Azure AD Domain Services no admite el uso de certificados de LDAP seguros emitidos por la entidad de certificación empresarial de su organización.</span><span class="sxs-lookup"><span data-stu-id="86010-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="86010-129">Esta restricción es porque el servicio de hello no confía en la entidad emisora de certificados como una entidad de certificación raíz de empresa.</span><span class="sxs-lookup"><span data-stu-id="86010-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="86010-130">Tarea 1: Obtener un certificado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="86010-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="86010-131">primera tarea de Hello implica obtener un certificado utilizado para LDAP acceso toohello administrado dominio seguro.</span><span class="sxs-lookup"><span data-stu-id="86010-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="86010-132">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="86010-132">You have two options:</span></span>

* <span data-ttu-id="86010-133">Obtención de un certificado de una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="86010-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="86010-134">entidad de Hello puede ser una entidad de certificación pública.</span><span class="sxs-lookup"><span data-stu-id="86010-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="86010-135">Creación de un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="86010-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="86010-136">Opción A (recomendada): obtención de un certificado LDAP seguro desde una entidad de certificación</span><span class="sxs-lookup"><span data-stu-id="86010-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="86010-137">Si su organización obtiene los certificados de una entidad de certificación pública, deberá tooobtain Hola seguro LDAP de los certificados de esa entidad de certificación pública.</span><span class="sxs-lookup"><span data-stu-id="86010-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="86010-138">Al solicitar un certificado, asegúrese de cumplir todos los requisitos de hello, que se describen en [requisitos de certificado LDAP seguro hello](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="86010-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="86010-139">Los equipos cliente que necesitan tooconnect toohello dominio administrado mediante LDAP seguro deben confiar a emisor Hola de certificado LDAP seguro Hola.</span><span class="sxs-lookup"><span data-stu-id="86010-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="86010-140">Opción B: creación de un certificado autofirmado para LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="86010-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="86010-141">Si no prevé toouse un certificado de una entidad de certificación pública, puede elegir toocreate un certificado autofirmado para LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="86010-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="86010-142">**Creación de un certificado autofirmado con PowerShell**</span><span class="sxs-lookup"><span data-stu-id="86010-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="86010-143">En el equipo de Windows, abra una nueva ventana de PowerShell como **administrador** y Hola de tipo siga los comandos, toocreate un nuevo certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="86010-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="86010-144">En el anterior ejemplo de Hola, reemplace '*. contoso100.com' con el nombre de dominio DNS de hello del dominio administrado. Por ejemplo, si ha creado un dominio administrado denominado 'contoso100.onmicrosoft.com', reemplace '*. contoso100.com' Hola por encima de la secuencia de comandos con ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="86010-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selección de un directorio de Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="86010-146">certificado autofirmado de Hello recién creado se coloca en el almacén de certificados del equipo local de Hola.</span><span class="sxs-lookup"><span data-stu-id="86010-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="86010-147">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="86010-147">Next step</span></span>
[<span data-ttu-id="86010-148">Tarea 2: exportar hello tooa de certificado LDAP seguro. Archivo PFX</span><span class="sxs-lookup"><span data-stu-id="86010-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
