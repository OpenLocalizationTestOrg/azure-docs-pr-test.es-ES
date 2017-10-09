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
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configuración de SSL para una aplicación en Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [Portal de Azure clásico](cloud-services-configure-ssl-certificate.md)
> 
> 

Cifrado de Secure Socket Layer (SSL) es el método de hello más frecuente de que protege los datos enviados a través de hello internet. Esta tarea describe cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación.

> [!NOTE]
> procedimientos de Hello en esta tarea aplican tooAzure servicios en la nube; para servicios de aplicaciones, consulte [esto](../app-service-web/web-sites-configure-ssl-certificate.md) artículo.
> 
> 

Esta tarea utiliza una implementación de producción. Al final de Hola de este tema se proporciona información sobre el uso de una implementación de ensayo.

Lea [este](cloud-services-how-to-create-deploy.md) artículo primero si aún no ha creado un servicio en la nube.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Paso 1: Obtener un certificado SSL
tooconfigure SSL para una aplicación, primero debe tooget un certificado SSL firmado por una entidad de certificación (CA), un tercero de confianza que emite certificados para este propósito. Si no ya tiene una, deberá tooobtain de una compañía que venda certificados SSL.

certificado de Hello debe cumplir Hola según los requisitos para los certificados SSL en Azure:

* certificado de Hello debe contener una clave privada.
* certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).
* Hello nombre de sujeto del certificado debe coincidir con servicio de nube de hello dominio utilizado tooaccess Hola. No se puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio de cloudapp.net Hola. Debe adquirir una toouse de nombre de dominio personalizado al tener acceso al servicio. Cuando solicite un certificado de una entidad de certificación, nombre de sujeto del certificado de hello debe coincidir con tooaccess de usa el nombre de dominio personalizado de Hola la aplicación. Por ejemplo, si su nombre de dominio personalizado es **contoso.com**, debe solicitar un certificado a su entidad de certificación para ***.contoso.com** o **www.contoso.com**.
* certificado de Hello debe usar un mínimo de cifrado de 2048 bits.

Para propósitos de prueba, puede [crear](cloud-services-certs-create.md) y usar un certificado autofirmado. Un certificado autofirmado no se autentica a través de una entidad de certificación y puede utilizar el dominio de cloudapp.net hello como dirección URL del sitio Web de Hola. Por ejemplo, hello siguiente tarea usa un certificado autofirmado en qué hello es el nombre común (CN) usado en el certificado de hello **sslexample.cloudapp.net**.

A continuación, debe incluir información sobre el certificado de hello en la definición de servicio y los archivos de configuración de servicio.

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Paso 2: Modificar archivos de definición y configuración del servicio de Hola
La aplicación debe ser el certificado de hello toouse configurado y se debe agregar un extremo HTTPS. Como resultado, hello archivos de configuración y definición de servicio necesitan toobe actualizado.

1. En el entorno de desarrollo, abra el archivo de definición de servicio (CSDEF) de hello, agregue un **certificados** sección dentro de hello **WebRole** sección e incluya Hola después de obtener información acerca de la el certificado (y los certificados intermedios):
   
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
   
   Hola **certificados** sección define el nombre de Hola de nuestro certificado, su ubicación y el nombre de Hola de almacén de Hola donde se encuentra.
   
   Permisos (`permisionLevel` atributo) puede tooone de conjunto de hello después de valores:
   
   | Valor del permiso | Descripción |
   | --- | --- |
   | limitedOrElevated |**(Valor predeterminado)**  Todos los procesos de rol pueden tener acceso a la clave privada de Hola. |
   | elevated |Solo los procesos elevados pueden tener acceso a la clave privada de Hola. |
2. En el archivo de definición de servicio, agregue un **InputEndpoint** elemento dentro de hello **extremos** sección tooenable HTTPS:
   
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

3. En el archivo de definición de servicio, agregue un **enlace** elemento dentro de hello **sitios** sección. En esta sección se agrega un toomap de enlace HTTPS del sitio de punto de conexión tooyour:
   
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
   
   Archivo de definición de servicio toohello de cambios necesarios de hello todos se hayan completado, pero necesitará tooadd Hola certificado información al archivo de configuración de servicio de Hola.
4. En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue un **certificados** sección dentro de hello **rol** sección, reemplazando el valor de huella digital de ejemplo de Hola se muestra a continuación con el certificado de:
   
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

(Hola anterior en el ejemplo se utiliza **sha1** para el algoritmo de huella digital de Hola. Especificar valor adecuado de hello para el algoritmo de huella digital del certificado).

Ahora que se han actualizado los archivos de configuración de servicio y la definición del servicio hello, su implementación para cargar tooAzure del paquete. Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.

## <a name="step-3-upload-a-certificate"></a>Paso 3: Cargar un certificado
El paquete de implementación se ha actualizado toouse certificado de Hola y se ha agregado un extremo HTTPS. Ahora puede cargar tooAzure de paquete y certificado de hello con hello portal de Azure clásico.

1. Inicie sesión en toohello [portal de Azure clásico][Azure classic portal]. 
2. Haga clic en **servicios en la nube** en el panel de navegación del lado izquierdo de Hola.
3. Haga clic en el servicio de nube de hello deseado.
4. Haga clic en hello **certificados** ficha.
   
    ![Haga clic en la pestaña de certificados de Hola](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Haga clic en hello **cargar** botón.
   
    ![Cargar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Proporcionar hello **archivo**, **contraseña**, a continuación, haga clic en **completar** (Hola marca de verificación).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Paso 4: Conectar la instancia de rol toohello a través de HTTPS
Ahora que la implementación está en funcionamiento en Azure, puede conectarse tooit mediante HTTPS.

1. En Hola portal de Azure clásico, seleccione la implementación y luego haga clic en el vínculo de hello en **dirección URL del sitio**.
   
   ![Determinar URL del sitio][2]
2. En el explorador web, modifique Hola vínculo toouse **https** en lugar de **http**y, a continuación, visite la página de Hola.
   
   > [!NOTE]
   > Si está utilizando un certificado autofirmado, al examinar el extremo HTTPS tooan que esté asociada con el certificado autofirmado de hello verá un error de certificado en el Explorador de Hola. Mediante el uso de un certificado firmado por una entidad de certificación de confianza elimina este problema; Hola mientras tanto, puede omitir error Hola. (Otra opción es el almacén de certificados de entidad de certificación de confianza del usuario de toohello de tooadd Hola certificado autofirmado).
   > 
   > 
   
   ![Ejemplo de sitio web con SSL][3]

Si desea toouse SSL para una implementación de ensayo en lugar de una implementación de producción, primero debe toodetermine Hola URL que se usa para la implementación de ensayo de Hola. Implementar el entorno de ensayo de toohello de servicio en la nube sin necesidad de incluir un certificado o cualquier información de certificado. Una vez implementado, puede determinar Hola GUID basado en direcciones URL, que se enumera en hello portal de Azure clásico **dirección URL del sitio** campo. Crear un certificado con la dirección URL basada en GUID de hello comunes nombre (CN) toohello igual (por ejemplo, **32818777 6e77 4ced a8fc 57609d404462.cloudapp.net**). Use hello Azure tooadd portal clásico Hola certificado tooyour provisionalmente servicio en la nube. A continuación, agregue Hola información tooyour CSDEF y CSCFG los archivos de certificado, volver a empaquetar la aplicación y actualizar el nuevo paquete de implementación de ensayo toouse Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).
* [Administración del servicio en la nube](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
