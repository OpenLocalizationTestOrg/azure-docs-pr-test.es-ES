---
title: "instalar aaaProblem Hola conector del agente de Proxy de aplicación | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot emite podría Hola de cara al instalar agente conector del Proxy de aplicación"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="a3a7e-103">Problema al instalar el conector del agente de Proxy de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="a3a7e-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="a3a7e-104">Conector del Proxy de aplicación de AAD de Microsoft es un componente de dominio interno que usa conectividad de las conexiones salientes tooestablish Hola de dominio interno de la toohello del punto de conexión disponible de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="a3a7e-105">Áreas problemáticas generales con la instalación del conector</span><span class="sxs-lookup"><span data-stu-id="a3a7e-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="a3a7e-106">Cuando se produce un error en la instalación de Hola de un conector, causa Hola suele ser uno de hello siguientes áreas:</span><span class="sxs-lookup"><span data-stu-id="a3a7e-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="a3a7e-107">**Conectividad** – toocomplete una instalación correcta, Hola nuevo conector necesidades tooregister y establecer propiedades de confianza en el futuro.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="a3a7e-108">Esto se realiza mediante la conexión toohello servicio Proxy de aplicación de AAD en la nube.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="a3a7e-109">**Establecimiento de confianza** – nuevo conector de hello crea un certificado autofirmado y registra el servicio en la nube toohello.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="a3a7e-110">**Autenticación de Hola, administrador** : durante la instalación, Hola usuario debe proporcionar credenciales de administrador de instalación del conector toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="a3a7e-111">Compruebe el servicio de Proxy de aplicación de nube de toohello de conectividad y página Login de Microsoft</span><span class="sxs-lookup"><span data-stu-id="a3a7e-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="a3a7e-112">**Objetivo:** comprobar puede conectar esa máquina de conector Hola extremo de registro de Proxy de aplicación AAD de toohello, así como la página de inicio de sesión de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="a3a7e-113">Abrir un toohello de explorador y vaya después de la página web: <https://aadap-portcheck.connectorporttest.msappproxy.net> y compruebe que tooCentral de conectividad de hello EE. UU. y funciona UU centros de datos con los puertos 9090 y 9091.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="a3a7e-114">Si cualquiera de estos puertos no se realiza correctamente (no tiene una marca de verificación verde), compruebe que Hola Firewall o proxy de back-end tiene \*. msappproxy.net con puertos 9090 y 9091 definida correctamente.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="a3a7e-115">Abra un explorador (pestaña independiente) y vaya toohello después de la página web: <https://login.microsoftonline.com>, asegúrese de que puede iniciar sesión toothat página.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="a3a7e-116">Comprobación de que los componentes de máquina y back-end admitan el certificado de confianza del proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="a3a7e-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="a3a7e-117">**Objetivo:** Compruebe que la máquina de conector de hello, el proxy de back-end y el firewall pueden admitir certificado Hola creado por el conector de Hola de confianza en el futuro.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="a3a7e-118">Conector de Hello intenta toocreate un certificado SHA512 que es compatible con TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="a3a7e-119">Si la máquina de Hola o proxy y firewall de back-end de hello no admite TLS 1.2, instalación de hello producirá un error.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="a3a7e-120">**problema de Hola tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="a3a7e-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="a3a7e-121">Compruebe la máquina de hello es compatible con TLS 1.2: las versiones de todas las ventanas posteriores a 2012 R2 deben admitir TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="a3a7e-122">Si el equipo del conector es de una versión de 2012 R2 o anterior, asegúrese de que ese Hola KB/s siguientes están instalados en el equipo de hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="a3a7e-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="a3a7e-123">Póngase en contacto con su administrador de red y pídale que tooverify que Hola back-end proxy y firewall no bloquean SHA512 para el tráfico saliente.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="a3a7e-124">Compruebe administrador es tooinstall usado Hola conector</span><span class="sxs-lookup"><span data-stu-id="a3a7e-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="a3a7e-125">**Objetivo:** compruebe ese usuario Hola que trate de conector de hello tooinstall es un administrador con las credenciales correctas.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="a3a7e-126">Actualmente, el usuario de hello debe ser un administrador global de hello toosucceed de instalación.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="a3a7e-127">**las credenciales de hello tooverify son correctas:**</span><span class="sxs-lookup"><span data-stu-id="a3a7e-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="a3a7e-128">Conectar demasiado<https://login.microsoftonline.com> y uso Hola mismas credenciales.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="a3a7e-129">Asegúrese de que el inicio de sesión de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-129">Make sure hello login is successful.</span></span> <span data-ttu-id="a3a7e-130">Puede comprobar el rol de usuario de hello yendo demasiado**Azure Active Directory**  - &gt; **usuarios y grupos**  - &gt; **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="a3a7e-131">Seleccione su cuenta de usuario, a continuación, "Directory Role" en el menú resultante Hola.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="a3a7e-132">Compruebe que ese rol seleccionado hello es "Administrador Global".</span><span class="sxs-lookup"><span data-stu-id="a3a7e-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="a3a7e-133">Si es que no se puede tooaccess cualquiera de hello páginas a lo largo de estos pasos, no es un administrador global.</span><span class="sxs-lookup"><span data-stu-id="a3a7e-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3a7e-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3a7e-134">Next steps</span></span>
[<span data-ttu-id="a3a7e-135">Descripción de los conectores del Proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3a7e-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
