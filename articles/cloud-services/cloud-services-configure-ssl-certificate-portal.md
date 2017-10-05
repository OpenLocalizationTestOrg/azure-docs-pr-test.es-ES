---
title: "Configuración de SSL para un servicio en la nube | Microsoft Docs"
description: "Aprenda a especificar un punto de conexión HTTPS para un rol web y cómo cargar un certificado SSL para proteger su aplicación. Estos ejemplos usan el Portal de Azure."
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="34be8-104">Configuración de SSL para una aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="34be8-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34be8-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="34be8-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="34be8-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="34be8-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="34be8-107">El cifrado de Capa de sockets seguros (SSL) es el método más usado para proteger los datos que se envían por Internet.</span><span class="sxs-lookup"><span data-stu-id="34be8-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="34be8-108">Esta tarea común analiza cómo especificar un punto de conexión HTTPS para un rol web y cómo cargar un certificado SSL para proteger su aplicación.</span><span class="sxs-lookup"><span data-stu-id="34be8-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="34be8-109">Los procedimientos de esta tarea se aplican a Servicios en la nube de Azure; para Servicios de aplicaciones consulte [esto](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="34be8-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="34be8-110">Esta tarea utiliza una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="34be8-110">This task uses a production deployment.</span></span> <span data-ttu-id="34be8-111">Al final de este tema se proporciona información sobre el uso de una implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="34be8-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="34be8-112">Lea [esto](cloud-services-how-to-create-deploy-portal.md) primero si aún no ha creado un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="34be8-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="34be8-113">Paso 1: Obtener un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="34be8-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="34be8-114">Para configurar SSL para una aplicación, necesita primero obtener un certificado SSL que haya sido firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito.</span><span class="sxs-lookup"><span data-stu-id="34be8-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="34be8-115">Si todavía no tiene uno de estos certificados, deberá obtenerla mediante una compañía que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="34be8-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="34be8-116">El certificado debe cumplir los siguientes requisitos de certificados SSL en Azure:</span><span class="sxs-lookup"><span data-stu-id="34be8-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="34be8-117">El certificado debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="34be8-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="34be8-118">El certificado debe crearse para el intercambio de claves, que se puedan exportar a un archivo Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="34be8-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="34be8-119">El nombre de sujeto del certificado debe coincidir con el dominio usado para tener acceso al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="34be8-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="34be8-120">No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="34be8-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="34be8-121">Debe adquirir un nombre de dominio personalizado para usarlo cuando obtenga acceso a su servicio.</span><span class="sxs-lookup"><span data-stu-id="34be8-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="34be8-122">Cuando solicite un certificado de una entidad de certificación, el nombre de sujeto del certificado debe coincidir con el nombre de dominio personalizado que se usó para tener acceso a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="34be8-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="34be8-123">Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="34be8-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="34be8-124">Este certificado debe usar un cifrado de 2048 bits como mínimo.</span><span class="sxs-lookup"><span data-stu-id="34be8-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="34be8-125">Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="34be8-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="34be8-126">Un certificado autofirmado no está autenticado por una CA y puede usar el dominio cloudapp.net como la dirección URL del sitio web.</span><span class="sxs-lookup"><span data-stu-id="34be8-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="34be8-127">Por ejemplo, la tarea siguiente usa un certificado autofirmado en el que el nombre común (CN) usado en el certificado es **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="34be8-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="34be8-128">A continuación, debe incluir información sobre el certificado en su definición de servicio y los archivos de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="34be8-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="34be8-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="34be8-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="34be8-130">Paso 2: Modificar los archivos de definición y configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="34be8-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="34be8-131">Su aplicación debe estar configurada para usar el certificado y se debe agregar un punto de conexión HTTPS.</span><span class="sxs-lookup"><span data-stu-id="34be8-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="34be8-132">Como resultado, se deben actualizar la definición de servicio y los archivos de configuración del servicio.</span><span class="sxs-lookup"><span data-stu-id="34be8-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="34be8-133">En su entorno de desarrollo, abra el archivo de definición de servicio (CSDEF), agregue una sección **Certificates** dentro de la sección **WebRole** e incluya la siguiente información sobre el certificado (y los certificados intermedios):</span><span class="sxs-lookup"><span data-stu-id="34be8-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="34be8-134">La sección **Certificates** define el nombre de nuestro certificado, su ubicación y el nombre de la tienda donde se encuentra.</span><span class="sxs-lookup"><span data-stu-id="34be8-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="34be8-135">Se pueden establecer permisos (atributo `permisionLevel`) en uno de los siguientes casos:</span><span class="sxs-lookup"><span data-stu-id="34be8-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="34be8-136">Valor del permiso</span><span class="sxs-lookup"><span data-stu-id="34be8-136">Permission Value</span></span> | <span data-ttu-id="34be8-137">Descripción</span><span class="sxs-lookup"><span data-stu-id="34be8-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="34be8-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="34be8-138">limitedOrElevated</span></span> |<span data-ttu-id="34be8-139">**(Predeterminado)** todos los procesos de rol pueden tener acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="34be8-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="34be8-140">elevated</span><span class="sxs-lookup"><span data-stu-id="34be8-140">elevated</span></span> |<span data-ttu-id="34be8-141">Solo los procesos elevados pueden tener acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="34be8-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="34be8-142">En el archivo de definición de servicio, agregue un elemento **InputEndpoint** en la sección **Endpoints** para habilitar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="34be8-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="34be8-143">En el archivo de definición de servicio, agregue un elemento **Binding** en la sección **Sites**.</span><span class="sxs-lookup"><span data-stu-id="34be8-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="34be8-144">Esta sección agrega un enlace HTTPS para asignar el punto de conexión a su sitio:</span><span class="sxs-lookup"><span data-stu-id="34be8-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="34be8-145">Se han completado todos los cambios requeridos en el archivo de definición de servicio; pero, aún necesita agregar la información del certificado en el archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="34be8-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="34be8-146">En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue a **Certificados** el valor de su certificado.</span><span class="sxs-lookup"><span data-stu-id="34be8-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="34be8-147">El ejemplo de código siguiente proporciona detalles de la sección **Certificados**, excepto el valor de la huella digital.</span><span class="sxs-lookup"><span data-stu-id="34be8-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="34be8-148">(En este ejemplo se usa **sha1** como algoritmo de huella digital.</span><span class="sxs-lookup"><span data-stu-id="34be8-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="34be8-149">Especifique el valor adecuado para el algoritmo de huella digital de su certificado).</span><span class="sxs-lookup"><span data-stu-id="34be8-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="34be8-150">Ahora que se actualizaron los archivos de definición del servicio y configuración del servicio, prepare su implementación para cargarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="34be8-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="34be8-151">Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.</span><span class="sxs-lookup"><span data-stu-id="34be8-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="34be8-152">Paso 3: Cargar un certificado</span><span class="sxs-lookup"><span data-stu-id="34be8-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="34be8-153">Conéctese a Azure Portal y...</span><span class="sxs-lookup"><span data-stu-id="34be8-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="34be8-154">En la sección **Todos los recursos** del portal, seleccione su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="34be8-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Publicación del servicio en la nube](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="34be8-156">Haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="34be8-156">Click **Certificates**.</span></span>

    ![Haga clic en el icono de certificados](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="34be8-158">Haga clic en **Cargar** en la parte superior del área de certificados.</span><span class="sxs-lookup"><span data-stu-id="34be8-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Haga clic en el elemento de menú Cargar](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="34be8-160">Escriba los valores de **Archivo** y **Contraseña**, y haga clic en **Cargar** en la parte inferior del área de entrada de datos.</span><span class="sxs-lookup"><span data-stu-id="34be8-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="34be8-161">Paso 4: Conectarse a la instancia de rol con HTTPS</span><span class="sxs-lookup"><span data-stu-id="34be8-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="34be8-162">Ahora que su implementación está funcionando en Azure, puede conectarse a ella con HTTPS.</span><span class="sxs-lookup"><span data-stu-id="34be8-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="34be8-163">Haga clic en la **dirección URL del sitio** para abrir el explorador web.</span><span class="sxs-lookup"><span data-stu-id="34be8-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Haga clic en la dirección URL del sitio](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="34be8-165">En el explorador web, modifique el vínculo para usar **https** en lugar de **http** y, a continuación, visite la página.</span><span class="sxs-lookup"><span data-stu-id="34be8-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="34be8-166">Si va a usar un certificado autofirmado, cuando vaya a un punto de conexión HTTPS que está asociado al certificado autofirmado, aparecerá un error de certificado en el explorador.</span><span class="sxs-lookup"><span data-stu-id="34be8-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="34be8-167">El uso de un certificado firmado por una entidad de certificación de confianza elimina el problema; mientras tanto, puede ignorar el error.</span><span class="sxs-lookup"><span data-stu-id="34be8-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="34be8-168">(Otra opción es agregar el certificado autofirmado a la tienda de certificados de la entidad de certificación de confianza para el usuario).</span><span class="sxs-lookup"><span data-stu-id="34be8-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Vista previa del sitio](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="34be8-170">Si desea usar SSL para una implementación de ensayo en vez de una implementación de producción, tendrá que determinar primero la dirección URL que se usó para la implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="34be8-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="34be8-171">Una vez que se ha implementado el servicio en la nube, la dirección URL del entorno de ensayo viene determinada por el GUID del **identificador de implementación** en este formato: `https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="34be8-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="34be8-172">Cree un certificado con el nombre común (CN) igual a la dirección URL basada en GUID (por ejemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="34be8-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="34be8-173">Use el portal para agregar el certificado a su servicio en la nube de ensayo.</span><span class="sxs-lookup"><span data-stu-id="34be8-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="34be8-174">A continuación, agregue la información del certificado a los archivos CSDEF y CSCFG, vuelva a empaquetar la aplicación y actualice la implementación de ensayo para que use el nuevo paquete.</span><span class="sxs-lookup"><span data-stu-id="34be8-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="34be8-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34be8-175">Next steps</span></span>
* <span data-ttu-id="34be8-176">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34be8-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="34be8-177">Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34be8-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="34be8-178">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34be8-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="34be8-179">[Administración del servicio en la nube](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34be8-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
