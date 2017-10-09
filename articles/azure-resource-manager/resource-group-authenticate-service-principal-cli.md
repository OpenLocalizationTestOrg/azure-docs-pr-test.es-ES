---
title: "aaaCreate identidad de aplicación de Azure con CLI de Azure | Documentos de Microsoft"
description: "Describe cómo controlan toouse CLI de Azure toocreate una aplicación de Azure Active Directory y entidad de servicio y lo acceso tooresources a través del acceso basado en roles. Muestra cómo tooauthenticate aplicación con una contraseña o un certificado."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="eff35-104">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eff35-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="eff35-105">Cuando haya una aplicación o un script que necesita tooaccess recursos, puede configurar una identidad para la aplicación hello y autenticar la aplicación hello con sus propias credenciales.</span><span class="sxs-lookup"><span data-stu-id="eff35-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="eff35-106">Esta identidad se conoce como una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="eff35-106">This identity is known as a service principal.</span></span> <span data-ttu-id="eff35-107">Este enfoque le permite:</span><span class="sxs-lookup"><span data-stu-id="eff35-107">This approach enables you to:</span></span>

* <span data-ttu-id="eff35-108">Asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos.</span><span class="sxs-lookup"><span data-stu-id="eff35-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="eff35-109">Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="eff35-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="eff35-110">Usar un certificado para la autenticación al ejecutar un script desatendido.</span><span class="sxs-lookup"><span data-stu-id="eff35-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="eff35-111">Este artículo muestra cómo toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset seguridad un toorun de aplicación en sus propias credenciales y la identidad.</span><span class="sxs-lookup"><span data-stu-id="eff35-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="eff35-112">Instalar la versión más reciente de Hola de [Azure CLI 1.0](../cli-install-nodejs.md) toomake que su entorno coincide con los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="eff35-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="eff35-113">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="eff35-113">Required permissions</span></span>
<span data-ttu-id="eff35-114">toocomplete en este tema, debe tener permisos suficientes en Azure Active Directory y la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="eff35-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="eff35-115">En concreto, debe ser capaz de toocreate una aplicación en Azure Active Directory hello y asignar Hola servicio principal tooa rol.</span><span class="sxs-lookup"><span data-stu-id="eff35-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="eff35-116">Hola más fácil manera toocheck si su cuenta tiene los permisos adecuados es a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="eff35-117">Consulte [Comprobación de los permisos necesarios en el portal](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="eff35-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="eff35-118">Ahora, continuar tooa sección para cada uno [contraseña](#create-service-principal-with-password) o [certificado](#create-service-principal-with-certificate) autenticación.</span><span class="sxs-lookup"><span data-stu-id="eff35-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="eff35-119">Creación de entidad de servicio con contraseña</span><span class="sxs-lookup"><span data-stu-id="eff35-119">Create service principal with password</span></span>
<span data-ttu-id="eff35-120">En esta sección, realice Hola pasos toocreate Hola aplicación de AD con una contraseña y asignar la entidad de servicio de toohello de rol de lector de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="eff35-121">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="eff35-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="eff35-122">toocreate una identidad de aplicación proporcionan Hola nombre de aplicación hello y una contraseña, como se muestra en el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="eff35-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="eff35-123">se devuelve la nueva entidad de servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-123">hello new service principal is returned.</span></span> <span data-ttu-id="eff35-124">Hola Id. de objeto es necesario al conceder permisos.</span><span class="sxs-lookup"><span data-stu-id="eff35-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="eff35-125">guid de Hello aparece con hello nombres principales de servicio es necesario al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="eff35-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="eff35-126">Este guid es hello mismo valor que el identificador de la aplicación hello. En las aplicaciones de ejemplo de Hola, este valor es que se hace referencia tooas Hola `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="eff35-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="eff35-127">Conceder permisos de entidad de seguridad de servicio de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="eff35-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="eff35-128">En este ejemplo, agregar rol lector de hello servicio toohello principal, que concede permiso tooread todos los recursos de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="eff35-129">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="eff35-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="eff35-130">Para el parámetro objectid de hello, proporcionar Hola Id. de objeto que utilizó al crear la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eff35-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="eff35-131">Antes de ejecutar este comando, debe permitir un poco Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eff35-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="eff35-132">Si estos comandos se ejecutan manualmente, lo habitual es que haya transcurrido suficiente tiempo entre las tareas.</span><span class="sxs-lookup"><span data-stu-id="eff35-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="eff35-133">En una secuencia de comandos, debe agregar una toosleep paso entre los comandos de hello (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="eff35-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="eff35-134">Si ve que Hola de error que indica que principal no existe en el directorio de hello, vuelva a ejecutar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="eff35-135">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="eff35-135">That's it!</span></span> <span data-ttu-id="eff35-136">La aplicación de AD y la entidad de servicio ya están configuradas.</span><span class="sxs-lookup"><span data-stu-id="eff35-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="eff35-137">sección de Hello siguiente muestra cómo toolog con hello de credenciales a través de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="eff35-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="eff35-138">Si desea toouse credencial de hello en la aplicación de código, no es necesario toocontinue con este tema.</span><span class="sxs-lookup"><span data-stu-id="eff35-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="eff35-139">También puede avanzar toohello [aplicaciones de ejemplo](#sample-applications) para obtener ejemplos de inicio de sesión con el identificador de la aplicación y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="eff35-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="eff35-140">Proporcionar credenciales a través de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eff35-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="eff35-141">Ahora, debe toolog en como operaciones de tooperform aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="eff35-142">Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="eff35-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="eff35-143">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eff35-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="eff35-144">tooretrieve Hola Id. de inquilino de su suscripción autenticado actualmente, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="eff35-145">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="eff35-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="eff35-146">Si necesita Id. de inquilino de hello tooget de otra suscripción, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="eff35-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="eff35-147">Si necesita toouse de Id. de cliente de tooretrieve hello para iniciar sesión, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="eff35-148">Hola toouse de valor para el registro es guid Hola aparecen en los nombres principales de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="eff35-149">Inicie sesión como entidad de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="eff35-150">Le solicitará contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-150">You are prompted for hello password.</span></span> <span data-ttu-id="eff35-151">Proporcione la contraseña de Hola que especificó al crear la aplicación hello AD.</span><span class="sxs-lookup"><span data-stu-id="eff35-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="eff35-152">Ahora está autenticado como entidad de seguridad de servicio de Hola Hola principal de servicio que ha creado.</span><span class="sxs-lookup"><span data-stu-id="eff35-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="eff35-153">Como alternativa, puede invocar operaciones de REST de toolog de línea de comandos de hello en.</span><span class="sxs-lookup"><span data-stu-id="eff35-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="eff35-154">De respuesta de autenticación de hello, puede recuperar el token de acceso de Hola para su uso con otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="eff35-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="eff35-155">Para obtener un ejemplo de recuperación de token de acceso de hello mediante la invocación de operaciones REST, consulte [generar un Token de acceso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="eff35-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="eff35-156">Creación de entidad de servicio con certificado</span><span class="sxs-lookup"><span data-stu-id="eff35-156">Create service principal with certificate</span></span>
<span data-ttu-id="eff35-157">En esta sección, realice los pasos de hello para:</span><span class="sxs-lookup"><span data-stu-id="eff35-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="eff35-158">Creación de un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="eff35-158">create a self-signed certificate</span></span>
* <span data-ttu-id="eff35-159">crear Hola aplicación AD con certificado de Hola y entidad de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="eff35-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="eff35-160">asignar la entidad de servicio de toohello de rol de lector de Hola</span><span class="sxs-lookup"><span data-stu-id="eff35-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="eff35-161">toocomplete estos pasos, debe tener [OpenSSL](http://www.openssl.org/) instalado.</span><span class="sxs-lookup"><span data-stu-id="eff35-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="eff35-162">Creación de un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="eff35-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="eff35-163">Hola anterior paso crea dos archivos: privkey.pem y cert.pem.</span><span class="sxs-lookup"><span data-stu-id="eff35-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="eff35-164">Combinar las claves públicas y privadas de hello en un único archivo.</span><span class="sxs-lookup"><span data-stu-id="eff35-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="eff35-165">Abra hello **examplecert.pem** de archivos y busque secuencia larga de Hola de caracteres entre **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---**.</span><span class="sxs-lookup"><span data-stu-id="eff35-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="eff35-166">Copiar datos del certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-166">Copy hello certificate data.</span></span> <span data-ttu-id="eff35-167">Estos datos se pasan como un parámetro al crear Hola entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="eff35-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="eff35-168">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="eff35-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="eff35-169">entidad de servicio de toocreate hello, proporcione el nombre de Hola de aplicación hello y datos de certificados de hello, tal y como se muestra en el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="eff35-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="eff35-170">se devuelve la nueva entidad de servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-170">hello new service principal is returned.</span></span> <span data-ttu-id="eff35-171">Hola Id. de objeto es necesario al conceder permisos.</span><span class="sxs-lookup"><span data-stu-id="eff35-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="eff35-172">guid de Hello aparece con hello nombres principales de servicio es necesario al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="eff35-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="eff35-173">Este guid es hello mismo valor que el identificador de la aplicación hello. En las aplicaciones de ejemplo de Hola, este valor es que se hace referencia tooas Hola identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="eff35-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="eff35-174">Conceder permisos de entidad de seguridad de servicio de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="eff35-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="eff35-175">En este ejemplo, agregar rol lector de hello servicio toohello principal, que concede permiso tooread todos los recursos de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="eff35-176">Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="eff35-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="eff35-177">Para el parámetro objectid de hello, proporcionar Hola Id. de objeto que utilizó al crear la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eff35-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="eff35-178">Antes de ejecutar este comando, debe permitir un poco Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eff35-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="eff35-179">Si estos comandos se ejecutan manualmente, lo habitual es que haya transcurrido suficiente tiempo entre las tareas.</span><span class="sxs-lookup"><span data-stu-id="eff35-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="eff35-180">En una secuencia de comandos, debe agregar una toosleep paso entre los comandos de hello (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="eff35-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="eff35-181">Si ve que Hola de error que indica que principal no existe en el directorio de hello, vuelva a ejecutar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="eff35-182">Proporcionar un certificado a través de un script automatizado de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eff35-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="eff35-183">Ahora, debe toolog en como operaciones de tooperform aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="eff35-184">Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="eff35-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="eff35-185">Un inquilino es una instancia de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eff35-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="eff35-186">tooretrieve Hola Id. de inquilino de su suscripción autenticado actualmente, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="eff35-187">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="eff35-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="eff35-188">Si necesita Id. de inquilino de hello tooget de otra suscripción, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="eff35-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="eff35-189">tooretrieve Hola huella digital del certificado y quite los caracteres que no necesite, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="eff35-190">De este modo, se devuelve un valor de huella digital similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="eff35-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="eff35-191">Si necesita toouse de Id. de cliente de tooretrieve hello para iniciar sesión, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="eff35-192">Hola toouse de valor para el registro es guid Hola aparecen en los nombres principales de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="eff35-193">Inicie sesión como entidad de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eff35-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="eff35-194">Ahora está autenticado como entidad de servicio Hola para hello aplicación de Azure Active Directory que creó.</span><span class="sxs-lookup"><span data-stu-id="eff35-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="eff35-195">Cambio de credenciales</span><span class="sxs-lookup"><span data-stu-id="eff35-195">Change credentials</span></span>

<span data-ttu-id="eff35-196">toochange Hola credenciales para una aplicación de AD, ya sea debido a un riesgo de seguridad o una expiración de la credencial, use `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="eff35-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="eff35-197">toochange una contraseña, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="eff35-198">toochange un valor de certificado, use:</span><span class="sxs-lookup"><span data-stu-id="eff35-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="eff35-199">Depurar</span><span class="sxs-lookup"><span data-stu-id="eff35-199">Debug</span></span>

<span data-ttu-id="eff35-200">Puede encontrar Hola siguientes errores al crear a una entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="eff35-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="eff35-201">**"Authentication_Unauthorized"** o **"ninguna suscripción encontrado en el contexto de Hola".**</span><span class="sxs-lookup"><span data-stu-id="eff35-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="eff35-202">-Ve este error cuando la cuenta no tiene hello [los permisos necesarios](#required-permissions) en hello Azure Active Directory tooregister una aplicación.</span><span class="sxs-lookup"><span data-stu-id="eff35-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="eff35-203">Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador. Pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="eff35-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="eff35-204">Su cuenta **"no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito '/ subscriptions / {guid}'."**  -Verá este error cuando su cuenta no tiene suficiente tooassign permisos una identidad de tooan de rol.</span><span class="sxs-lookup"><span data-stu-id="eff35-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="eff35-205">Pida el tooadd de administrador de suscripción rol Administrador de acceso tooUser.</span><span class="sxs-lookup"><span data-stu-id="eff35-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="eff35-206">Aplicaciones de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eff35-206">Sample applications</span></span>
<span data-ttu-id="eff35-207">Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:</span><span class="sxs-lookup"><span data-stu-id="eff35-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="eff35-208">.NET</span><span class="sxs-lookup"><span data-stu-id="eff35-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="eff35-209">Java</span><span class="sxs-lookup"><span data-stu-id="eff35-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="eff35-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="eff35-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="eff35-211">Python</span><span class="sxs-lookup"><span data-stu-id="eff35-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="eff35-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="eff35-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="eff35-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eff35-213">Next steps</span></span>
* <span data-ttu-id="eff35-214">Para obtener instrucciones detalladas sobre cómo integrar una aplicación en Azure para administrar recursos, vea [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="eff35-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="eff35-215">tooget obtener más información sobre el uso de certificados y la CLI de Azure, vea [autenticación basada en certificados con entidades de seguridad de servicio de Azure desde la línea de comandos de Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="eff35-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="eff35-216">Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="eff35-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
