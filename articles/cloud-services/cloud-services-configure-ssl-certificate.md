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
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configuración de SSL para una aplicación en Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [Portal de Azure clásico](cloud-services-configure-ssl-certificate.md)
> 
> 

El cifrado de Capa de sockets seguros (SSL) es el método más usado para proteger los datos que se envían por Internet. Esta tarea común analiza cómo especificar un punto de conexión HTTPS para un rol web y cómo cargar un certificado SSL para proteger su aplicación.

> [!NOTE]
> Los procedimientos de esta tarea se aplican a Azure Cloud Services; para App Services consulte [este](../app-service-web/web-sites-configure-ssl-certificate.md) artículo.
> 
> 

Esta tarea utiliza una implementación de producción. Al final de este tema se proporciona información sobre el uso de una implementación de ensayo.

Lea [este](cloud-services-how-to-create-deploy.md) artículo primero si aún no ha creado un servicio en la nube.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Paso 1: Obtener un certificado SSL
Para configurar SSL para una aplicación, necesita primero obtener un certificado SSL que haya sido firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito. Si todavía no tiene uno de estos certificados, deberá obtenerla mediante una compañía que venda certificados SSL.

El certificado debe cumplir los siguientes requisitos de certificados SSL en Azure:

* El certificado debe contener una clave privada.
* El certificado debe crearse para el intercambio de claves, que se puedan exportar a un archivo Personal Information Exchange (.pfx).
* El nombre de sujeto del certificado debe coincidir con el dominio usado para tener acceso al servicio en la nube. No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio cloudapp.net. Debe adquirir un nombre de dominio personalizado para usarlo cuando obtenga acceso a su servicio. Cuando solicite un certificado de una entidad de certificación, el nombre de sujeto del certificado debe coincidir con el nombre de dominio personalizado que se usó para tener acceso a su aplicación. Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.
* Este certificado debe usar un cifrado de 2048 bits como mínimo.

Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado. Un certificado autofirmado no está autenticado por una CA y puede usar el dominio cloudapp.net como la dirección URL del sitio web. Por ejemplo, la tarea siguiente usa un certificado autofirmado en el que el nombre común (CN) usado en el certificado es **sslexample.cloudapp.net**.

A continuación, debe incluir información sobre el certificado en su definición de servicio y los archivos de configuración del servicio.

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a>Paso 2: modificar la definición del servicio y los archivos de configuración
Su aplicación debe estar configurada para usar el certificado y se debe agregar un punto de conexión HTTPS. Como resultado, se deben actualizar la definición de servicio y los archivos de configuración del servicio.

1. En su entorno de desarrollo, abra el archivo de definición de servicio (CSDEF), agregue una sección **Certificates** dentro de la sección **WebRole** e incluya la siguiente información sobre el certificado (y los certificados intermedios):
   
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
   
   La sección **Certificates** define el nombre de nuestro certificado, su ubicación y el nombre de la tienda donde se encuentra.
   
   Se pueden establecer permisos (atributo `permisionLevel`) en uno de los siguientes casos:
   
   | Valor del permiso | Descripción |
   | --- | --- |
   | limitedOrElevated |**(Predeterminado)** todos los procesos de rol pueden tener acceso a la clave privada. |
   | elevated |Solo los procesos elevados pueden tener acceso a la clave privada. |
2. En el archivo de definición de servicio, agregue un elemento **InputEndpoint** en la sección **Endpoints** para habilitar HTTPS:
   
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

3. En el archivo de definición de servicio, agregue un elemento **Binding** en la sección **Sites**. Esta sección agrega un enlace de HTTPS para asignar el punto de conexión a su sitio:
   
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
   
   Se han efectuado todos los cambios necesarios en el archivo de definición de servicio; sin embargo, todavía necesita agregar la información del certificado en el archivo de configuración del servicio.
4. En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue una sección **Certificates** en la sección **Role** y reemplace el valor de la huella digital de muestra que se indica a continuación por el de su certificado:
   
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

(El ejemplo anterior usa **sha1** para el algoritmo de huella digital. Especifique el valor adecuado para el algoritmo de huella digital de su certificado).

Ahora que se actualizaron los archivos de definición del servicio y configuración del servicio, prepare su implementación para cargarla en Azure. Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.

## <a name="step-3-upload-a-certificate"></a>Paso 3: Cargar un certificado
Su paquete de implementación se actualizó para usar el certificado y se agregó un punto de conexión HTTPS. Ahora podrá cargar el paquete y el certificado en Azure con el Portal de Azure clásico.

1. Inicie sesión en el [Portal de Azure clásico][Azure classic portal]. 
2. Haga clic en **Cloud Services** en el panel de navegación izquierdo.
3. Haga clic en el servicio en la nube deseado.
4. Haga clic en la pestaña **Certificados**.
   
    ![Haga clic en la pestaña Certificados](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Haga clic en el botón **Upload** .
   
    ![Cargar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Proporcione el **archivo**, la **contraseña** y, a continuación, haga clic en **Completar** (la marca de verificación).

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a>Paso 4: Conectarse a la instancia de rol con HTTPS
Ahora que su implementación está funcionando en Azure, puede conectarse a ella con HTTPS.

1. En el Portal de Azure clásico, seleccione su implementación y, a continuación, haga clic en el vínculo de **Dirección URL del sitio**.
   
   ![Determinar URL del sitio][2]
2. En el explorador web, modifique el vínculo para usar **https** en lugar de **http** y, a continuación, visite la página.
   
   > [!NOTE]
   > Si va a usar un certificado autofirmado, cuando vaya a un punto de conexión HTTPS que está asociado al certificado autofirmado, aparecerá un error de certificado en el explorador. El uso de un certificado firmado por una entidad de certificación de confianza elimina el problema; mientras tanto, puede ignorar el error. (Otra opción es agregar el certificado autofirmado a la tienda de certificados de la entidad de certificación de confianza para el usuario).
   > 
   > 
   
   ![Ejemplo de sitio web con SSL][3]

Si desea usar SSL para una implementación de ensayo en vez de una implementación de producción, tendrá que determinar primero la dirección URL que se usó para la implementación de ensayo. Implemente su servicio en la nube para el entorno de ensayo sin incluir un certificado ni ninguna información del certificado. Una vez implementado, puede determinar la dirección URL basada en el GUID, que se incluye en el campo **Dirección URL del sitio** del Portal de Azure clásico. Cree un certificado con el nombre común (CN) igual a la dirección URL basada en GUID (por ejemplo, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Use el Portal de Azure clásico para agregar el certificado a su servicio en la nube de ensayo. A continuación, agregue la información del certificado a los archivos CSDEF y CSCFG, vuelva a empaquetar la aplicación y actualice la implementación de ensayo para que use el nuevo paquete.

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).
* Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).
* [Administración del servicio en la nube](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
