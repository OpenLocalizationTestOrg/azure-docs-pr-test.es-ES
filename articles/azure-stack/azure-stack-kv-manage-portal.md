---
title: "aaaManage el almacén de claves en la pila de Azure mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage el almacén de claves en la pila de Azure con PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a><span data-ttu-id="6413d-103">Administrar el almacén de claves en la pila de Azure mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="6413d-103">Manage Key Vault in Azure Stack using hello portal</span></span>

<span data-ttu-id="6413d-104">Puede administrar el almacén de claves en la pila de Azure mediante el portal de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-104">You can manage Key Vault in Azure Stack by using hello Azure Stack portal.</span></span> <span data-ttu-id="6413d-105">En este artículo le ayuda a obtener toocreate iniciada y administrar el almacén de claves en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6413d-105">This article helps you get started toocreate and manage Key Vault in Azure Stack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6413d-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6413d-106">Prerequisites</span></span>  

* <span data-ttu-id="6413d-107">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-107">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="6413d-108">Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-108">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="6413d-109">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6413d-109">Create a key vault</span></span> 

1. <span data-ttu-id="6413d-110">Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="6413d-110">Sign in toohello user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="6413d-111">En el panel de hello, haga clic en **nuevo > seguridad e identidad > almacén de claves**.</span><span class="sxs-lookup"><span data-stu-id="6413d-111">From hello dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![Pantalla de KV](media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="6413d-113">En hello **crear el almacén de claves** hoja, asignar un **nombre** para el almacén.</span><span class="sxs-lookup"><span data-stu-id="6413d-113">On hello **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="6413d-114">Nombre del almacén puede contener solo caracteres alfanuméricos, Hola carácter especial guiones (-), y no debe comenzar con un número.</span><span class="sxs-lookup"><span data-stu-id="6413d-114">Vault name can contain only alphanumeric characters, hello special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="6413d-115">Elija un **suscripción** de lista de Hola de suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="6413d-115">Choose a **Subscription** from hello list of available subscriptions.</span></span> <span data-ttu-id="6413d-116">Todas las suscripciones que ofrecen servicio de almacén de claves de Hola se muestran en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-116">All subscriptions that offer hello Key Vault service are displayed in hello drop-down.</span></span>  

5. <span data-ttu-id="6413d-117">Seleccione un **Grupo de recursos** existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="6413d-117">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="6413d-118">Seleccione hello **tarifa**.</span><span class="sxs-lookup"><span data-stu-id="6413d-118">Select hello **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="6413d-119">Los almacenes de claves de Azure Stack Development Kit admiten la SKU **Estándar** únicamente.</span><span class="sxs-lookup"><span data-stu-id="6413d-119">Key vaults in Azure Stack Development Kit support **Standard** SKU only.</span></span>

7. <span data-ttu-id="6413d-120">Elija **Directivas de acceso** existentes o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="6413d-120">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="6413d-121">Directiva de acceso permite toogrant permisos para un usuario, aplicación o una seguridad agrupar las operaciones de tooperform con este almacén.</span><span class="sxs-lookup"><span data-stu-id="6413d-121">Access policy allows you toogrant permissions for a user, application, or a security group tooperform operations with this vault.</span></span>  

8. <span data-ttu-id="6413d-122">Si lo desea, elija un **directiva de acceso avanzado** características de hello tooenable como el acceso a equipos de tooVirtual para la implementación, acceso tooResource Manager para la implementación de plantilla y acceso tooAzure cifrado del disco para el volumen cifrado.</span><span class="sxs-lookup"><span data-stu-id="6413d-122">Optionally, choose an **Advanced access policy** tooenable hello features like access tooVirtual Machines for deployment, access tooResource Manager for template deployment and access tooAzure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="6413d-123">Después de establecer la configuración de hello, haga clic en **Aceptar** y, a continuación, **crear**.</span><span class="sxs-lookup"><span data-stu-id="6413d-123">After configuring hello settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="6413d-124">Esto inicia la implementación de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-124">This starts hello key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="6413d-125">Administración de claves y secretos</span><span class="sxs-lookup"><span data-stu-id="6413d-125">Manage keys and secrets</span></span>

<span data-ttu-id="6413d-126">Después de crear un almacén, use Hola siguiendo los pasos toocreate y administración de claves y secretos en el almacén de Hola de.</span><span class="sxs-lookup"><span data-stu-id="6413d-126">After you create a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="6413d-127">Crear una clave</span><span class="sxs-lookup"><span data-stu-id="6413d-127">Create a key</span></span>

1. <span data-ttu-id="6413d-128">Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="6413d-128">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="6413d-129">En el panel de hello, haga clic en **todos los recursos** > almacén de claves de hello select que creó anteriormente > haga clic en hello **claves** icono.</span><span class="sxs-lookup"><span data-stu-id="6413d-129">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Keys** tile.</span></span>  

3. <span data-ttu-id="6413d-130">De hello **claves** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6413d-130">From hello **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="6413d-131">En hello **crear una clave** hoja, la lista de Hola de formulario de **opciones**, elija el método hello que desea toouse toocreate una clave.</span><span class="sxs-lookup"><span data-stu-id="6413d-131">On hello **Create a key** blade, form hello list of **Options**, choose hello method that you want toouse toocreate a key.</span></span> <span data-ttu-id="6413d-132">Puede **Generar** una nueva clave, **Cargar** una clave existente o **Restaurar copia de seguridad** de una clave.</span><span class="sxs-lookup"><span data-stu-id="6413d-132">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="6413d-133">Escriba un **Nombre** para la clave.</span><span class="sxs-lookup"><span data-stu-id="6413d-133">Enter a **Name** for your key.</span></span> <span data-ttu-id="6413d-134">nombre de clave de Hola solo puede contener caracteres alfanuméricos y guiones de carácter especial de hello (-).</span><span class="sxs-lookup"><span data-stu-id="6413d-134">hello key name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="6413d-135">Como alternativa, configure los valores de **Establecer la fecha de activación** y **Establecer fecha de expiración** para la clave.</span><span class="sxs-lookup"><span data-stu-id="6413d-135">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="6413d-136">Haga clic en **crear** implementación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="6413d-136">Click **Create** toostart hello deployment.</span></span>  

<span data-ttu-id="6413d-137">Después de que se crea correctamente la clave de hello, puede seleccionarlo de hello **claves** hoja y ver o modificar sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="6413d-137">After hello key is successfully created, you can select it from hello **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="6413d-138">sección de propiedades de Hello contiene Hola **identificador de clave de**, un URI que aplicaciones externas pueden tener acceso a esta clave.</span><span class="sxs-lookup"><span data-stu-id="6413d-138">hello properties section contains hello **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="6413d-139">operaciones de toolimit en esta clave, configurar opciones en **las operaciones permitidas**.</span><span class="sxs-lookup"><span data-stu-id="6413d-139">toolimit operations on this key, configure settings under **Permitted operations**.</span></span>

![URI de clave](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="6413d-141">Crear un secreto</span><span class="sxs-lookup"><span data-stu-id="6413d-141">Create a secret</span></span> 

1. <span data-ttu-id="6413d-142">Inicie sesión en el portal de usuarios de toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="6413d-142">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="6413d-143">En el panel de hello, haga clic en **todos los recursos** > almacén de claves de hello select que creó anteriormente > haga clic en hello **secretos** icono.</span><span class="sxs-lookup"><span data-stu-id="6413d-143">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Secrets** tile.</span></span>  

3. <span data-ttu-id="6413d-144">De hello **secretos** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6413d-144">From hello **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="6413d-145">En hello **crear un secreto** hoja, en lista de Hola de **las opciones de carga**, elija una opción que se desea toocreate un secreto.</span><span class="sxs-lookup"><span data-stu-id="6413d-145">On hello **Create a secret** blade, from hello list of **Upload options**, choose an option by which you want toocreate a secret.</span></span> <span data-ttu-id="6413d-146">Puede crear un secreto **manualmente** especificando un valor de secreto de Hola o cargue una **certificado** desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="6413d-146">You can create a secret **Manually** by entering a value for hello secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="6413d-147">Escriba un **nombre** para secreto Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-147">Enter a **Name** for hello secret.</span></span> <span data-ttu-id="6413d-148">nombre de secreto Hola puede contener solo caracteres alfanuméricos y guiones de carácter especial de hello (-).</span><span class="sxs-lookup"><span data-stu-id="6413d-148">hello secret name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="6413d-149">Si lo desea, especifique hello **tipo de contenido**y configurar los valores de **establecer fecha de activación** y **establecer fecha de expiración** valores de secreto Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-149">Optionally, specify hello **Content type**, and configure values for **Set activation date** and **Set expiration date** values for hello secret.</span></span>  

7. <span data-ttu-id="6413d-150">Haga clic en implementación de crear toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-150">Click Create toostart hello deployment.</span></span>  

<span data-ttu-id="6413d-151">Después de que el secreto de Hola se crea correctamente, puede seleccionarlo de hello **secretos** hoja y ver o modificar sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="6413d-151">After hello secret is successfully created, you can select it from hello **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="6413d-152">sección de propiedades de Hello contiene **identificador de secreto**, un URI que aplicaciones externas pueden tener acceso a este secreto.</span><span class="sxs-lookup"><span data-stu-id="6413d-152">hello properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![URI de secreto](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="6413d-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6413d-154">Next Steps</span></span>
* [<span data-ttu-id="6413d-155">Implementar una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6413d-155">Deploy a VM by retrieving hello password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="6413d-156">Implementar una VM con un certificado almacenado en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6413d-156">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     


