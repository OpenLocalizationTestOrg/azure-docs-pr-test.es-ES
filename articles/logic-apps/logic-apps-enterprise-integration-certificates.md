---
title: "certificados aaaUsing con paquete de integración empresarial | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse certificados con hello paquete de integración empresarial | Aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="daa68-103">Información sobre los certificados y Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="daa68-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="daa68-104">Información general</span><span class="sxs-lookup"><span data-stu-id="daa68-104">Overview</span></span>
<span data-ttu-id="daa68-105">Integración de Enterprise utiliza las comunicaciones de certificados toosecure B2B.</span><span class="sxs-lookup"><span data-stu-id="daa68-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="daa68-106">Puede emplear dos tipos de certificados en las aplicaciones de integración de empresas:</span><span class="sxs-lookup"><span data-stu-id="daa68-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="daa68-107">Certificados públicos, que deben comprarse a una entidad de certificación (CA).</span><span class="sxs-lookup"><span data-stu-id="daa68-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="daa68-108">Certificados privados, que puede emitir usted mismo.</span><span class="sxs-lookup"><span data-stu-id="daa68-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="daa68-109">A veces, estos certificados son autofirmados tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="daa68-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="daa68-110">¿Qué son los certificados?</span><span class="sxs-lookup"><span data-stu-id="daa68-110">What are certificates?</span></span>
<span data-ttu-id="daa68-111">Los certificados son documentos digitales que comprobar la identidad de Hola de participantes de hello en comunicaciones electrónicas y que proteger las comunicaciones electrónicas.</span><span class="sxs-lookup"><span data-stu-id="daa68-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="daa68-112">¿Por qué se utilizan los certificados?</span><span class="sxs-lookup"><span data-stu-id="daa68-112">Why use certificates?</span></span>
<span data-ttu-id="daa68-113">A veces, hay que conservar la confidencialidad de las comunicaciones B2B.</span><span class="sxs-lookup"><span data-stu-id="daa68-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="daa68-114">Integración de Enterprise utiliza certificados toosecure estas comunicaciones de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="daa68-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="daa68-115">Mediante el cifrado de contenido de Hola de mensajes</span><span class="sxs-lookup"><span data-stu-id="daa68-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="daa68-116">Firmando digitalmente los mensajes</span><span class="sxs-lookup"><span data-stu-id="daa68-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="daa68-117">Carga de un certificado público</span><span class="sxs-lookup"><span data-stu-id="daa68-117">Upload a public certificate</span></span>

<span data-ttu-id="daa68-118">toouse una *certificado público* en las aplicaciones lógicas con capacidades de B2B, primero necesita tooupload Hola certificado en su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="daa68-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="daa68-119">Después de cargar un certificado, está disponible toohelp proteger los mensajes B2B al definir sus propiedades en hello [contratos](logic-apps-enterprise-integration-agreements.md) creados por usted.</span><span class="sxs-lookup"><span data-stu-id="daa68-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="daa68-120">Presentamos Hola pasos detallados para cargar los certificados públicos en su cuenta de integración después de iniciar sesión en toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="daa68-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="daa68-121">Seleccione **más servicios** y escriba **integración** en el cuadro de búsqueda del filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="daa68-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="daa68-122">Seleccione **cuentas de integración** desde la lista de resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="daa68-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="daa68-123">![Seleccionar Examinar](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="daa68-124">Seleccione Hola integración cuenta toowhich desea tooadd Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="daa68-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Seleccione Hola integración cuenta toowhich desea tooadd Hola certificado](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="daa68-126">Seleccione hello **certificados** icono.</span><span class="sxs-lookup"><span data-stu-id="daa68-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="daa68-127">![Icono de hello seleccione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="daa68-128">Hola **certificados** hoja que se abre, seleccione hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="daa68-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="daa68-129">![Seleccione el botón de agregar Hola](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="daa68-130">Escriba un **nombre** para el certificado y hello, a continuación, seleccione el tipo de certificado como **público** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="daa68-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="daa68-131">Icono de carpeta de hello seleccione lado derecho de Hola de hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="daa68-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="daa68-132">Cuando se abre el selector de archivos de hello, busque y seleccione el archivo de certificado de Hola que quiere tooupload tooyour integración cuenta.</span><span class="sxs-lookup"><span data-stu-id="daa68-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="daa68-133">Seleccione el certificado de hello y, a continuación, seleccione **Aceptar** en el selector de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="daa68-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="daa68-134">Esto se valida y carga Hola certificados tooyour integración cuentas.</span><span class="sxs-lookup"><span data-stu-id="daa68-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="daa68-135">Por último, encenderlo hello **agregar certificado** hoja, seleccione hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="daa68-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="daa68-136">![Seleccione el botón Aceptar Hola](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="daa68-137">Seleccione hello **certificados** icono.</span><span class="sxs-lookup"><span data-stu-id="daa68-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="daa68-138">Debería ver Hola recién agregado el certificado.</span><span class="sxs-lookup"><span data-stu-id="daa68-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="daa68-139">![Vea el nuevo certificado de Hola](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="daa68-140">Carga de un certificado privado</span><span class="sxs-lookup"><span data-stu-id="daa68-140">Upload a private certificate</span></span>

<span data-ttu-id="daa68-141">toouse una *certificado privado* en las aplicaciones lógicas con capacidades de B2B, se puede cargar una cuenta de integración de certificado privado tooyour Hola realizar pasos</span><span class="sxs-lookup"><span data-stu-id="daa68-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="daa68-142">[Cargar su tooKey clave privada almacén](../key-vault/key-vault-get-started.md "Obtenga más información sobre el almacén de claves") y proporcionar un **nombre de clave**</span><span class="sxs-lookup"><span data-stu-id="daa68-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="daa68-143">Debe autorizar las operaciones de tooperform de las aplicaciones lógicas en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="daa68-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="daa68-144">Puede conceder a entidad de servicio de aplicaciones de la lógica de acceso toohello mediante Hola siguiente comando de PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="daa68-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="daa68-145">Una vez que haya realizado paso anterior de hello, agregue una cuenta de toointegration certificado privado.</span><span class="sxs-lookup"><span data-stu-id="daa68-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="daa68-146">A continuación se Hola pasos detallados para cargar los certificados privados en su cuenta de integración después de iniciar sesión en toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="daa68-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="daa68-147">Seleccionar cuenta de hello integración toowhich desea tooadd Hola certificado y seleccione hello **certificados** icono.</span><span class="sxs-lookup"><span data-stu-id="daa68-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="daa68-148">![Icono de hello seleccione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="daa68-149">Hola **certificados** hoja que se abre, seleccione hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="daa68-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="daa68-150">![Seleccione el botón de agregar Hola](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="daa68-151">Escriba un **nombre** para su certificado y el tipo de certificado de hello seleccione como **privada** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="daa68-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="daa68-152">Seleccione icono de carpeta de hello en hello derecha de hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="daa68-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="daa68-153">Cuando se abre el selector de archivos de hello, Buscar certificado público correspondiente Hola que quiere tooupload tooyour integración cuenta.</span><span class="sxs-lookup"><span data-stu-id="daa68-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="daa68-154">Al agregar un certificado privado es importante tooadd correspondiente pública certificados tooshow en [acuerdo AS2](logic-apps-enterprise-integration-as2.md) reciben y envían la configuración para firmar y cifrar los mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="daa68-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="daa68-155">Seleccione hello **grupo de recursos**, **el almacén de claves**, **nombre de clave** y seleccione hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="daa68-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="daa68-156">![Agregar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="daa68-157">Seleccione hello **certificados** icono.</span><span class="sxs-lookup"><span data-stu-id="daa68-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="daa68-158">Debería ver Hola recién agregado el certificado.</span><span class="sxs-lookup"><span data-stu-id="daa68-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="daa68-159">![Vea el nuevo certificado de Hola](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="daa68-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="daa68-160">Creación de un contrato B2B</span><span class="sxs-lookup"><span data-stu-id="daa68-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="daa68-161">Más información sobre Key Vault</span><span class="sxs-lookup"><span data-stu-id="daa68-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Información sobre el Almacén de claves")  

