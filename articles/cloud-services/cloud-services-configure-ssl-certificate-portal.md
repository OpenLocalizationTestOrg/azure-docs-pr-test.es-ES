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
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configuración de SSL para una aplicación en Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [Portal de Azure clásico](cloud-services-configure-ssl-certificate.md)
>

Cifrado de Secure Socket Layer (SSL) es el método de hello más frecuente de que protege los datos enviados a través de hello internet. Esta tarea describe cómo toospecify un extremo HTTPS para un rol web y cómo tooupload SSL certificate toosecure la aplicación.

> [!NOTE]
> procedimientos de Hello en esta tarea aplican tooAzure servicios en la nube; para servicios de aplicaciones, consulte [esto](../app-service-web/web-sites-configure-ssl-certificate.md).
>

Esta tarea utiliza una implementación de producción. Al final de Hola de este tema se proporciona información sobre el uso de una implementación de ensayo.

Lea [esto](cloud-services-how-to-create-deploy-portal.md) primero si aún no ha creado un servicio en la nube.

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

<a name="modify"></a>

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

3. En el archivo de definición de servicio, agregue un **enlace** elemento dentro de hello **sitios** sección. Este elemento agrega un toomap de enlace HTTPS del sitio de punto de conexión tooyour:

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

   Archivo de definición de servicio toohello de cambios necesarios de hello todos se hayan completado; Sin embargo, todavía necesita información de certificado de hello tooadd al archivo de configuración de servicio de Hola.
4. En el archivo de configuración de servicio (CSCFG), ServiceConfiguration.Cloud.cscfg, agregue a **Certificados** el valor de su certificado. Hello ejemplo de código siguiente proporciona detalles de hello **certificados** sección, excepto el valor de huella digital de Hola.

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

(Este ejemplo se utiliza **sha1** para el algoritmo de huella digital de Hola. Especificar valor adecuado de hello para el algoritmo de huella digital del certificado).

Ahora que se han actualizado los archivos de configuración de servicio y la definición del servicio hello, su implementación para cargar tooAzure del paquete. Si va a usar **cspack**, no utilice la marca **/generateConfigurationFile**, puesto que así se sobrescribe la información del certificado que acaba de insertar.

## <a name="step-3-upload-a-certificate"></a>Paso 3: Cargar un certificado
Conectar toohello portal de Azure y...

1. Hola **todos los recursos** sección de hello Portal, seleccione su servicio en la nube.

    ![Publicación del servicio en la nube](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Haga clic en **Certificados**.

    ![Haga clic en el icono de certificados de Hola](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Haga clic en **cargar** en parte superior de hello del área de certificados de Hola.

    ![Haga clic en el elemento de menú de carga de Hola](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Proporcionar hello **archivo**, **contraseña**, a continuación, haga clic en **cargar** final Hola del área de entrada de datos de Hola.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Paso 4: Conectar la instancia de rol toohello a través de HTTPS
Ahora que la implementación está en funcionamiento en Azure, puede conectarse tooit mediante HTTPS.

1. Haga clic en hello **dirección URL del sitio** tooopen de explorador web de Hola.

   ![Haga clic en la dirección URL del sitio de Hola](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. En el explorador web, modifique Hola vínculo toouse **https** en lugar de **http**y, a continuación, visite la página de Hola.

   > [!NOTE]
   > Si está utilizando un certificado autofirmado, al examinar el extremo HTTPS tooan que esté asociada con el certificado autofirmado de hello verá un error de certificado en el Explorador de Hola. Mediante el uso de un certificado firmado por una entidad de certificación de confianza elimina este problema; Hola mientras tanto, puede omitir error Hola. (Otra opción es el almacén de certificados de entidad de certificación de confianza del usuario de toohello de tooadd Hola certificado autofirmado).
   >
   >

   ![Vista previa del sitio](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Si desea toouse SSL para una implementación de ensayo en lugar de una implementación de producción, primero deberá toodetermine Hola URL que se usa para la implementación de ensayo de Hola. Una vez que se ha implementado el servicio en la nube, Hola URL toohello entorno de ensayo está determinado por hello **Id. de implementación** GUID en este formato:`https://deployment-id.cloudapp.net/`  
   >
   > Crear un certificado con la dirección URL basada en GUID de hello comunes nombre (CN) toohello igual (por ejemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**). Use hello tooadd portal Hola certificado tooyour provisionalmente servicio en la nube. A continuación, agregue Hola información tooyour CSDEF y CSCFG los archivos de certificado, volver a empaquetar la aplicación y actualizar el nuevo paquete de implementación de ensayo toouse Hola.
   >

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).
* [Administración del servicio en la nube](cloud-services-how-to-manage-portal.md).
