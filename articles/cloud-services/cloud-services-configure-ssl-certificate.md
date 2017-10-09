---
title: "aaaConfigure SSL para un servicio de nube (clásico) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="52cc6-103">Configuración de SSL para una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="52cc6-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52cc6-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="52cc6-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="52cc6-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="52cc6-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="52cc6-106">Cifrado de Secure Socket Layer (SSL) es el método de hello más frecuente de que protege los datos enviados a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="52cc6-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="52cc6-107">Esta tarea describe cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52cc6-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="52cc6-108">procedimientos de Hello en esta tarea aplican tooAzure servicios en la nube; para servicios de aplicaciones, consulte [esto](../app-service-web/web-sites-configure-ssl-certificate.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="52cc6-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="52cc6-109">Esta tarea utiliza una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="52cc6-109">This task uses a production deployment.</span></span> <span data-ttu-id="52cc6-110">Al final de Hola de este tema se proporciona información sobre el uso de una implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="52cc6-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="52cc6-111">Lea [este](cloud-services-how-to-create-deploy.md) artículo primero si aún no ha creado un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="52cc6-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="52cc6-112">Paso 1: Obtener un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="52cc6-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="52cc6-113">tooconfigure SSL para una aplicación, primero debe tooget un certificado SSL firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito.</span><span class="sxs-lookup"><span data-stu-id="52cc6-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="52cc6-114">Si no ya tiene una, deberá tooobtain de una compañía que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="52cc6-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="52cc6-115">certificado de Hello debe cumplir Hola según los requisitos para los certificados SSL en Azure:</span><span class="sxs-lookup"><span data-stu-id="52cc6-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="52cc6-116">certificado de Hello debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="52cc6-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="52cc6-117">certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="52cc6-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="52cc6-118">Hello nombre de sujeto del certificado debe coincidir con servicio de nube de hello dominio utilizado tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="52cc6-119">No se puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio de cloudapp.net Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="52cc6-120">Debe adquirir una toouse de nombre de dominio personalizado al tener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="52cc6-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="52cc6-121">Cuando solicite un certificado de una entidad de certificación, nombre de sujeto del certificado de hello debe coincidir con tooaccess de usa el nombre de dominio personalizado de Hola la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52cc6-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="52cc6-122">Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="52cc6-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="52cc6-123">certificado de Hello debe usar un mínimo de cifrado de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="52cc6-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="52cc6-124">Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="52cc6-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="52cc6-125">Un certificado autofirmado no se autentica a través de una entidad de certificación y puede utilizar el dominio de cloudapp.net hello como dirección URL del sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="52cc6-126">Por ejemplo, hello siguiente tarea usa un certificado autofirmado en qué hello es el nombre común (CN) usado en el certificado de hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="52cc6-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="52cc6-127">A continuación, debe incluir información sobre el certificado de hello en la definición de servicio y los archivos de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="52cc6-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="52cc6-128">Paso 2: Modificar archivos de definición y configuración del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="52cc6-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="52cc6-129">La aplicación debe ser el certificado de hello toouse configurado y se debe agregar un extremo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="52cc6-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="52cc6-130">Como resultado, hello archivos de configuración y definición de servicio necesitan toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="52cc6-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="52cc6-131">En el entorno de desarrollo, abra el archivo de definición de servicio (CSDEF) de hello, agregue un **certificados** sección dentro de hello **WebRole** sección e incluya Hola después de obtener información acerca de la el certificado (y los certificados intermedios):</span><span class="sxs-lookup"><span data-stu-id="52cc6-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="52cc6-132">Hola **certificados** sección define el nombre de Hola de nuestro certificado, su ubicación y el nombre de Hola de almacén de Hola donde se encuentra.</span><span class="sxs-lookup"><span data-stu-id="52cc6-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="52cc6-133">Permisos (`permisionLevel` atributo) puede tooone de conjunto de hello después de valores:</span><span class="sxs-lookup"><span data-stu-id="52cc6-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="52cc6-134">Valor del permiso</span><span class="sxs-lookup"><span data-stu-id="52cc6-134">Permission Value</span></span> | <span data-ttu-id="52cc6-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="52cc6-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="52cc6-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="52cc6-136">limitedOrElevated</span></span> |<span data-ttu-id="52cc6-137">**(Valor predeterminado)**  Todos los procesos de rol pueden tener acceso a la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="52cc6-138">elevated</span><span class="sxs-lookup"><span data-stu-id="52cc6-138">elevated</span></span> |<span data-ttu-id="52cc6-139">Solo los procesos elevados pueden tener acceso a la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="52cc6-140">En el archivo de definición de servicio, agregue un **InputEndpoint** elemento dentro de hello **extremos** sección tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="52cc6-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="52cc6-141">En el archivo de definición de servicio, agregue un **enlace** elemento dentro de hello **sitios** sección.</span><span class="sxs-lookup"><span data-stu-id="52cc6-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="52cc6-142">En esta sección se agrega un toomap de enlace HTTPS del sitio de punto de conexión tooyour:</span><span class="sxs-lookup"><span data-stu-id="52cc6-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
    ```xml   
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="52cc6-143">Archivo de definición de servicio toohello de cambios necesarios de hello todos se hayan completado, pero necesitará tooadd Hola certificado información al archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="52cc6-144">En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue un **certificados** sección dentro de hello **rol** sección, reemplazando el valor de huella digital de ejemplo de Hola se muestra a continuación con el certificado de:</span><span class="sxs-lookup"><span data-stu-id="52cc6-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
    ```xml   
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="52cc6-145">(Hola anterior en el ejemplo se utiliza **sha1** para el algoritmo de huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="52cc6-146">Especificar valor adecuado de hello para el algoritmo de huella digital del certificado).</span><span class="sxs-lookup"><span data-stu-id="52cc6-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="52cc6-147">Ahora que se han actualizado los archivos de configuración de servicio y la definición del servicio hello, su implementación para cargar tooAzure del paquete.</span><span class="sxs-lookup"><span data-stu-id="52cc6-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="52cc6-148">Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.</span><span class="sxs-lookup"><span data-stu-id="52cc6-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="52cc6-149">Paso 3: Cargar un certificado</span><span class="sxs-lookup"><span data-stu-id="52cc6-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="52cc6-150">El paquete de implementación se ha actualizado toouse certificado de Hola y se ha agregado un extremo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="52cc6-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="52cc6-151">Ahora puede cargar tooAzure de paquete y certificado de hello con hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="52cc6-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="52cc6-152">Inicie sesión en toohello [portal de Azure clásico][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="52cc6-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="52cc6-153">Haga clic en **servicios en la nube** en el panel de navegación del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="52cc6-154">Haga clic en el servicio de nube de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="52cc6-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="52cc6-155">Haga clic en hello **certificados** ficha.</span><span class="sxs-lookup"><span data-stu-id="52cc6-155">Click hello **Certificates** tab.</span></span>
   
    ![Haga clic en la pestaña de certificados de Hola](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="52cc6-157">Haga clic en hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="52cc6-157">Click hello **Upload** button.</span></span>
   
    ![Cargar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="52cc6-159">Proporcionar hello **archivo**, **contraseña**, a continuación, haga clic en **completar** (Hola marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="52cc6-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="52cc6-160">Paso 4: Conectar la instancia de rol toohello a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="52cc6-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="52cc6-161">Ahora que la implementación está en funcionamiento en Azure, puede conectarse tooit mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="52cc6-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="52cc6-162">En Hola portal de Azure clásico, seleccione la implementación y luego haga clic en el vínculo de hello en **dirección URL del sitio**.</span><span class="sxs-lookup"><span data-stu-id="52cc6-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Determinar URL del sitio][2]
2. <span data-ttu-id="52cc6-164">En el explorador web, modifique Hola vínculo toouse **https** en lugar de **http**y, a continuación, visite la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52cc6-165">Si está utilizando un certificado autofirmado, al examinar el extremo HTTPS tooan que esté asociada con el certificado autofirmado de hello verá un error de certificado en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="52cc6-166">Mediante el uso de un certificado firmado por una entidad de certificación de confianza elimina este problema; Hola mientras tanto, puede omitir error Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="52cc6-167">(Otra opción es el almacén de certificados de entidad de certificación de confianza del usuario de toohello de tooadd Hola certificado autofirmado).</span><span class="sxs-lookup"><span data-stu-id="52cc6-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Ejemplo de sitio web con SSL][3]

<span data-ttu-id="52cc6-169">Si desea toouse SSL para una implementación de ensayo en lugar de una implementación de producción, primero debe toodetermine Hola URL que se usa para la implementación de ensayo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="52cc6-170">Implementar el entorno de ensayo de toohello de servicio en la nube sin necesidad de incluir un certificado o cualquier información de certificado.</span><span class="sxs-lookup"><span data-stu-id="52cc6-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="52cc6-171">Una vez implementado, puede determinar Hola GUID basado en direcciones URL, que se enumera en hello portal de Azure clásico **dirección URL del sitio** campo.</span><span class="sxs-lookup"><span data-stu-id="52cc6-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="52cc6-172">Crear un certificado con la dirección URL basada en GUID de hello comunes nombre (CN) toohello igual (por ejemplo, **32818777 6e77 4ced a8fc 57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="52cc6-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="52cc6-173">Use hello Azure tooadd portal clásico Hola certificado tooyour provisionalmente servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="52cc6-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="52cc6-174">A continuación, agregue Hola información tooyour CSDEF y CSCFG los archivos de certificado, volver a empaquetar la aplicación y actualizar el nuevo paquete de implementación de ensayo toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="52cc6-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52cc6-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52cc6-175">Next steps</span></span>
* <span data-ttu-id="52cc6-176">[Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="52cc6-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="52cc6-177">Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="52cc6-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="52cc6-178">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="52cc6-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="52cc6-179">[Administración del servicio en la nube](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="52cc6-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
