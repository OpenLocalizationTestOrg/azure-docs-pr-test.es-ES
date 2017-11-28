---
title: "Configuración de SSL en un servicio en la nube (clásico) | Microsoft Docs"
description: "Aprenda a especificar un punto de conexión HTTPS para un rol web y cómo cargar un certificado SSL para proteger su aplicación."
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="f118a-103">Configuración de SSL para una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="f118a-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f118a-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f118a-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="f118a-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="f118a-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="f118a-106">El cifrado de Capa de sockets seguros (SSL) es el método más usado para proteger los datos que se envían por Internet.</span><span class="sxs-lookup"><span data-stu-id="f118a-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="f118a-107">Esta tarea común analiza cómo especificar un punto de conexión HTTPS para un rol web y cómo cargar un certificado SSL para proteger su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f118a-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="f118a-108">Los procedimientos de esta tarea se aplican a Azure Cloud Services; para App Services consulte [este](../app-service-web/web-sites-configure-ssl-certificate.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f118a-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="f118a-109">Esta tarea utiliza una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="f118a-109">This task uses a production deployment.</span></span> <span data-ttu-id="f118a-110">Al final de este tema se proporciona información sobre el uso de una implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="f118a-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="f118a-111">Lea [este](cloud-services-how-to-create-deploy.md) artículo primero si aún no ha creado un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="f118a-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="f118a-112">Paso 1: Obtener un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="f118a-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="f118a-113">Para configurar SSL para una aplicación, necesita primero obtener un certificado SSL que haya sido firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito.</span><span class="sxs-lookup"><span data-stu-id="f118a-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="f118a-114">Si todavía no tiene uno de estos certificados, deberá obtenerla mediante una compañía que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="f118a-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="f118a-115">El certificado debe cumplir los siguientes requisitos de certificados SSL en Azure:</span><span class="sxs-lookup"><span data-stu-id="f118a-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="f118a-116">El certificado debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="f118a-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="f118a-117">El certificado debe crearse para el intercambio de claves, que se puedan exportar a un archivo Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="f118a-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="f118a-118">El nombre de sujeto del certificado debe coincidir con el dominio usado para tener acceso al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="f118a-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="f118a-119">No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f118a-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="f118a-120">Debe adquirir un nombre de dominio personalizado para usarlo cuando obtenga acceso a su servicio.</span><span class="sxs-lookup"><span data-stu-id="f118a-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="f118a-121">Cuando solicite un certificado de una entidad de certificación, el nombre de sujeto del certificado debe coincidir con el nombre de dominio personalizado que se usó para tener acceso a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f118a-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="f118a-122">Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f118a-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="f118a-123">Este certificado debe usar un cifrado de 2048 bits como mínimo.</span><span class="sxs-lookup"><span data-stu-id="f118a-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="f118a-124">Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="f118a-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="f118a-125">Un certificado autofirmado no está autenticado por una CA y puede usar el dominio cloudapp.net como la dirección URL del sitio web.</span><span class="sxs-lookup"><span data-stu-id="f118a-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="f118a-126">Por ejemplo, la tarea siguiente usa un certificado autofirmado en el que el nombre común (CN) usado en el certificado es **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="f118a-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="f118a-127">A continuación, debe incluir información sobre el certificado en su definición de servicio y los archivos de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="f118a-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="f118a-128">Paso 2: modificar la definición del servicio y los archivos de configuración</span><span class="sxs-lookup"><span data-stu-id="f118a-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="f118a-129">Su aplicación debe estar configurada para usar el certificado y se debe agregar un punto de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f118a-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="f118a-130">Como resultado, se deben actualizar la definición de servicio y los archivos de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="f118a-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="f118a-131">En su entorno de desarrollo, abra el archivo de definición de servicio (CSDEF), agregue una sección **Certificates** dentro de la sección **WebRole** e incluya la siguiente información sobre el certificado (y los certificados intermedios):</span><span class="sxs-lookup"><span data-stu-id="f118a-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="f118a-132">La sección **Certificates** define el nombre de nuestro certificado, su ubicación y el nombre de la tienda donde se encuentra.</span><span class="sxs-lookup"><span data-stu-id="f118a-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="f118a-133">Se pueden establecer permisos (atributo `permisionLevel`) en uno de los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="f118a-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="f118a-134">Valor del permiso</span><span class="sxs-lookup"><span data-stu-id="f118a-134">Permission Value</span></span> | <span data-ttu-id="f118a-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="f118a-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="f118a-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="f118a-136">limitedOrElevated</span></span> |<span data-ttu-id="f118a-137">**(Predeterminado)** todos los procesos de rol pueden tener acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="f118a-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="f118a-138">elevated</span><span class="sxs-lookup"><span data-stu-id="f118a-138">elevated</span></span> |<span data-ttu-id="f118a-139">Solo los procesos elevados pueden tener acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="f118a-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="f118a-140">En el archivo de definición de servicio, agregue un elemento **InputEndpoint** en la sección **Endpoints** para habilitar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="f118a-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="f118a-141">En el archivo de definición de servicio, agregue un elemento **Binding** en la sección **Sites**.</span><span class="sxs-lookup"><span data-stu-id="f118a-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="f118a-142">Esta sección agrega un enlace de HTTPS para asignar el punto de conexión a su sitio:</span><span class="sxs-lookup"><span data-stu-id="f118a-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="f118a-143">Se han efectuado todos los cambios necesarios en el archivo de definición de servicio; sin embargo, todavía necesita agregar la información del certificado en el archivo de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="f118a-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="f118a-144">En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue una sección **Certificates** en la sección **Role** y reemplace el valor de la huella digital de muestra que se indica a continuación por el de su certificado:</span><span class="sxs-lookup"><span data-stu-id="f118a-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="f118a-145">(El ejemplo anterior usa **sha1** para el algoritmo de huella digital.</span><span class="sxs-lookup"><span data-stu-id="f118a-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="f118a-146">Especifique el valor adecuado para el algoritmo de huella digital de su certificado).</span><span class="sxs-lookup"><span data-stu-id="f118a-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="f118a-147">Ahora que se actualizaron los archivos de definición del servicio y configuración del servicio, prepare su implementación para cargarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="f118a-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="f118a-148">Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.</span><span class="sxs-lookup"><span data-stu-id="f118a-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="f118a-149">Paso 3: Cargar un certificado</span><span class="sxs-lookup"><span data-stu-id="f118a-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="f118a-150">Su paquete de implementación se actualizó para usar el certificado y se agregó un punto de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f118a-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="f118a-151">Ahora podrá cargar el paquete y el certificado en Azure con el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="f118a-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="f118a-152">Inicie sesión en el [Portal de Azure clásico][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="f118a-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="f118a-153">Haga clic en **Cloud Services** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="f118a-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="f118a-154">Haga clic en el servicio en la nube deseado.</span><span class="sxs-lookup"><span data-stu-id="f118a-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="f118a-155">Haga clic en la pestaña **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="f118a-155">Click the **Certificates** tab.</span></span>
   
    ![Haga clic en la pestaña Certificados](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="f118a-157">Haga clic en el botón **Upload** .</span><span class="sxs-lookup"><span data-stu-id="f118a-157">Click the **Upload** button.</span></span>
   
    ![Cargar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="f118a-159">Proporcione el **archivo**, la **contraseña** y, a continuación, haga clic en **Completar** (la marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="f118a-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="f118a-160">Paso 4: Conectarse a la instancia de rol con HTTPS</span><span class="sxs-lookup"><span data-stu-id="f118a-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="f118a-161">Ahora que su implementación está funcionando en Azure, puede conectarse a ella con HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f118a-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="f118a-162">En el Portal de Azure clásico, seleccione su implementación y, a continuación, haga clic en el vínculo de **Dirección URL del sitio**.</span><span class="sxs-lookup"><span data-stu-id="f118a-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Determinar URL del sitio][2]
2. <span data-ttu-id="f118a-164">En el explorador web, modifique el vínculo para usar **https** en lugar de **http** y, a continuación, visite la página.</span><span class="sxs-lookup"><span data-stu-id="f118a-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f118a-165">Si va a usar un certificado autofirmado, cuando vaya a un punto de conexión HTTPS que está asociado al certificado autofirmado, aparecerá un error de certificado en el explorador.</span><span class="sxs-lookup"><span data-stu-id="f118a-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="f118a-166">El uso de un certificado firmado por una entidad de certificación de confianza elimina el problema; mientras tanto, puede ignorar el error.</span><span class="sxs-lookup"><span data-stu-id="f118a-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="f118a-167">(Otra opción es agregar el certificado autofirmado a la tienda de certificados de la entidad de certificación de confianza para el usuario).</span><span class="sxs-lookup"><span data-stu-id="f118a-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Ejemplo de sitio web con SSL][3]

<span data-ttu-id="f118a-169">Si desea usar SSL para una implementación de ensayo en vez de una implementación de producción, tendrá que determinar primero la dirección URL que se usó para la implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="f118a-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="f118a-170">Implemente su servicio en la nube para el entorno de ensayo sin incluir un certificado ni ninguna información del certificado.</span><span class="sxs-lookup"><span data-stu-id="f118a-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="f118a-171">Una vez implementado, puede determinar la dirección URL basada en el GUID, que se incluye en el campo **Dirección URL del sitio** del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="f118a-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="f118a-172">Cree un certificado con el nombre común (CN) igual a la dirección URL basada en GUID (por ejemplo, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="f118a-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="f118a-173">Use el Portal de Azure clásico para agregar el certificado a su servicio en la nube de ensayo.</span><span class="sxs-lookup"><span data-stu-id="f118a-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="f118a-174">A continuación, agregue la información del certificado a los archivos CSDEF y CSCFG, vuelva a empaquetar la aplicación y actualice la implementación de ensayo para que use el nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="f118a-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f118a-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f118a-175">Next steps</span></span>
* <span data-ttu-id="f118a-176">[Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f118a-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="f118a-177">Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f118a-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="f118a-178">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="f118a-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="f118a-179">[Administración del servicio en la nube](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="f118a-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
