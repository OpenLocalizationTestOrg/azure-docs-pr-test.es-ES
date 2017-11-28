---
title: aaaConfigure SSL para un servicio en la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación. Estos ejemplos utilizan Hola portal de Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="bc693-104">Configuración de SSL para una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="bc693-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc693-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bc693-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="bc693-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="bc693-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="bc693-107">Cifrado de Secure Socket Layer (SSL) es el método de hello más frecuente de que protege los datos enviados a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="bc693-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="bc693-108">Esta tarea describe cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc693-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="bc693-109">procedimientos de Hello en esta tarea aplican tooAzure servicios en la nube; para servicios de aplicaciones, consulte [esto](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="bc693-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="bc693-110">Esta tarea utiliza una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="bc693-110">This task uses a production deployment.</span></span> <span data-ttu-id="bc693-111">Al final de Hola de este tema se proporciona información sobre el uso de una implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="bc693-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="bc693-112">Lea [esto](cloud-services-how-to-create-deploy-portal.md) primero si aún no ha creado un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bc693-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="bc693-113">Paso 1: Obtener un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bc693-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="bc693-114">tooconfigure SSL para una aplicación, primero debe tooget un certificado SSL firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito.</span><span class="sxs-lookup"><span data-stu-id="bc693-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="bc693-115">Si no ya tiene una, deberá tooobtain de una compañía que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="bc693-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="bc693-116">certificado de Hello debe cumplir Hola según los requisitos para los certificados SSL en Azure:</span><span class="sxs-lookup"><span data-stu-id="bc693-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="bc693-117">certificado de Hello debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="bc693-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="bc693-118">certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="bc693-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="bc693-119">Hello nombre de sujeto del certificado debe coincidir con servicio de nube de hello dominio utilizado tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="bc693-120">No se puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio de cloudapp.net Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="bc693-121">Debe adquirir una toouse de nombre de dominio personalizado al tener acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="bc693-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="bc693-122">Cuando solicite un certificado de una entidad de certificación, nombre de sujeto del certificado de hello debe coincidir con tooaccess de usa el nombre de dominio personalizado de Hola la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc693-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="bc693-123">Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="bc693-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="bc693-124">certificado de Hello debe usar un mínimo de cifrado de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="bc693-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="bc693-125">Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="bc693-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="bc693-126">Un certificado autofirmado no se autentica a través de una entidad de certificación y puede utilizar el dominio de cloudapp.net hello como dirección URL del sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="bc693-127">Por ejemplo, hello siguiente tarea usa un certificado autofirmado en qué hello es el nombre común (CN) usado en el certificado de hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="bc693-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="bc693-128">A continuación, debe incluir información sobre el certificado de hello en la definición de servicio y los archivos de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="bc693-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="bc693-129"><a name="modify"></a></span><span class="sxs-lookup"><span data-stu-id="bc693-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="bc693-130">Paso 2: Modificar archivos de definición y configuración del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="bc693-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="bc693-131">La aplicación debe ser el certificado de hello toouse configurado y se debe agregar un extremo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bc693-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="bc693-132">Como resultado, hello archivos de configuración y definición de servicio necesitan toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="bc693-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="bc693-133">En el entorno de desarrollo, abra el archivo de definición de servicio (CSDEF) de hello, agregue un **certificados** sección dentro de hello **WebRole** sección e incluya Hola después de obtener información acerca de la el certificado (y los certificados intermedios):</span><span class="sxs-lookup"><span data-stu-id="bc693-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="bc693-134">Hola **certificados** sección define el nombre de Hola de nuestro certificado, su ubicación y el nombre de Hola de almacén de Hola donde se encuentra.</span><span class="sxs-lookup"><span data-stu-id="bc693-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="bc693-135">Permisos (`permisionLevel` atributo) puede tooone de conjunto de hello después de valores:</span><span class="sxs-lookup"><span data-stu-id="bc693-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="bc693-136">Valor del permiso</span><span class="sxs-lookup"><span data-stu-id="bc693-136">Permission Value</span></span> | <span data-ttu-id="bc693-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc693-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bc693-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="bc693-138">limitedOrElevated</span></span> |<span data-ttu-id="bc693-139">**(Valor predeterminado)**  Todos los procesos de rol pueden tener acceso a la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="bc693-140">elevated</span><span class="sxs-lookup"><span data-stu-id="bc693-140">elevated</span></span> |<span data-ttu-id="bc693-141">Solo los procesos elevados pueden tener acceso a la clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="bc693-142">En el archivo de definición de servicio, agregue un **InputEndpoint** elemento dentro de hello **extremos** sección tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="bc693-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

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

3. <span data-ttu-id="bc693-143">En el archivo de definición de servicio, agregue un **enlace** elemento dentro de hello **sitios** sección.</span><span class="sxs-lookup"><span data-stu-id="bc693-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="bc693-144">Este elemento agrega un toomap de enlace HTTPS del sitio de punto de conexión tooyour:</span><span class="sxs-lookup"><span data-stu-id="bc693-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

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

   <span data-ttu-id="bc693-145">Archivo de definición de servicio toohello de cambios necesarios de hello todos se hayan completado; Sin embargo, todavía necesita información de certificado de hello tooadd al archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="bc693-146">En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue a **Certificados** el valor de su certificado.</span><span class="sxs-lookup"><span data-stu-id="bc693-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="bc693-147">Hello ejemplo de código siguiente proporciona detalles de hello **certificados** sección, excepto el valor de huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

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

<span data-ttu-id="bc693-148">(Este ejemplo se utiliza **sha1** para el algoritmo de huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="bc693-149">Especificar valor adecuado de hello para el algoritmo de huella digital del certificado).</span><span class="sxs-lookup"><span data-stu-id="bc693-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="bc693-150">Ahora que se han actualizado los archivos de configuración de servicio y la definición del servicio hello, su implementación para cargar tooAzure del paquete.</span><span class="sxs-lookup"><span data-stu-id="bc693-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="bc693-151">Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.</span><span class="sxs-lookup"><span data-stu-id="bc693-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="bc693-152">Paso 3: Cargar un certificado</span><span class="sxs-lookup"><span data-stu-id="bc693-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="bc693-153">Conectar toohello portal de Azure y...</span><span class="sxs-lookup"><span data-stu-id="bc693-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="bc693-154">Hola **todos los recursos** sección de hello Portal, seleccione su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bc693-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Publicación del servicio en la nube](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="bc693-156">Haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="bc693-156">Click **Certificates**.</span></span>

    ![Haga clic en el icono de certificados de Hola](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="bc693-158">Haga clic en **cargar** en parte superior de hello del área de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Haga clic en el elemento de menú de carga de Hola](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="bc693-160">Proporcionar hello **archivo**, **contraseña**, a continuación, haga clic en **cargar** final Hola del área de entrada de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="bc693-161">Paso 4: Conectar la instancia de rol toohello a través de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bc693-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="bc693-162">Ahora que la implementación está en funcionamiento en Azure, puede conectarse tooit mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bc693-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="bc693-163">Haga clic en hello **dirección URL del sitio** tooopen de explorador web de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Haga clic en la dirección URL del sitio de Hola](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="bc693-165">En el explorador web, modifique Hola vínculo toouse **https** en lugar de **http**y, a continuación, visite la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc693-166">Si está utilizando un certificado autofirmado, al examinar el extremo HTTPS tooan que esté asociada con el certificado autofirmado de hello verá un error de certificado en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="bc693-167">Mediante el uso de un certificado firmado por una entidad de certificación de confianza elimina este problema; Hola mientras tanto, puede omitir error Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="bc693-168">(Otra opción es el almacén de certificados de entidad de certificación de confianza del usuario de toohello de tooadd Hola certificado autofirmado).</span><span class="sxs-lookup"><span data-stu-id="bc693-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Vista previa del sitio](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="bc693-170">Si desea toouse SSL para una implementación de ensayo en lugar de una implementación de producción, primero deberá toodetermine Hola URL que se usa para la implementación de ensayo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="bc693-171">Una vez que se ha implementado el servicio en la nube, Hola URL toohello entorno de ensayo está determinado por hello **Id. de implementación** GUID en este formato:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="bc693-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="bc693-172">Crear un certificado con la dirección URL basada en GUID de hello comunes nombre (CN) toohello igual (por ejemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="bc693-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="bc693-173">Use hello tooadd portal Hola certificado tooyour provisionalmente servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bc693-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="bc693-174">A continuación, agregue Hola información tooyour CSDEF y CSCFG los archivos de certificado, volver a empaquetar la aplicación y actualizar el nuevo paquete de implementación de ensayo toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="bc693-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="bc693-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc693-175">Next steps</span></span>
* <span data-ttu-id="bc693-176">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc693-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="bc693-177">Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc693-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="bc693-178">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc693-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="bc693-179">[Administración del servicio en la nube](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc693-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
