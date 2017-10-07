---
title: "configuración de seguridad mezcla aaaSplit | Documentos de Microsoft"
description: "Configuración de certificados x409 para cifrado"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Configuración de seguridad de división y combinación
servicio de dividir y combinar de hello toouse, debe configurar correctamente la seguridad. Hola servicio forma parte de la característica de escalado flexible de Hola de base de datos de SQL de Microsoft Azure. Para obtener más información, vea el [Tutorial del servicio de división y combinación de Escalado elástico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Configuración de certificados
Los certificados se configuran de dos maneras. 

1. [Hola tooConfigure certificado SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure certificados de cliente](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>certificados tooobtain
Se pueden obtener certificados de entidades de certificación pública (CA) o de hello [servicio de certificados de Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Se trata de hello preferido métodos tooobtain certificados.

Si esas opciones no están disponibles, puede generar **certificados autofirmados**.

## <a name="tools-toogenerate-certificates"></a>Certificados de toogenerate de herramientas
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>herramientas de hello toorun
* Desde el Símbolo del sistema para desarrolladores de Visual Studio, consulte [Símbolo del sistema de Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Si está instalado, vaya a:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Obtener Hola WDK de [Windows 8.1: descargar kits y herramientas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certificado SSL de tooconfigure Hola
Un certificado SSL es necesario tooencrypt Hola comunicación y autenticar el servidor de Hola. Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:

### <a name="create-a-new-self-signed-certificate"></a>Creación de un nuevo certificado autofirmado
1. [Creación de un certificado autofirmado](#create-a-self-signed-certificate)
2. [Creación del archivo PFX para el certificado SSL autofirmado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Cargar el certificado SSL tooCloud servicio](#upload-ssl-certificate-to-cloud-service)
4. [Actualización del certificado SSL en el archivo de configuración de servicio](#update-ssl-certificate-in-service-configuration-file)
5. [Importación de la Entidad de certificación SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>almacenar de un certificado existente de certificado de hello toouse
1. [Exportación del certificado SSL desde el almacén de certificados](#export-ssl-certificate-from-certificate-store)
2. [Cargar el certificado SSL tooCloud servicio](#upload-ssl-certificate-to-cloud-service)
3. [Actualización del certificado SSL en el archivo de configuración de servicio](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse un certificado existente en un archivo PFX
1. [Cargar el certificado SSL tooCloud servicio](#upload-ssl-certificate-to-cloud-service)
2. [Actualización del certificado SSL en el archivo de configuración de servicio](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certificados de cliente tooconfigure
Se requieren certificados de cliente en orden tooauthenticate solicitudes toohello servicio. Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:

### <a name="turn-off-client-certificates"></a>Desactivación de los certificados de cliente
1. [Desactivación de la autenticación basada en certificado de cliente](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Emisión de nuevos certificados de cliente autofirmados
1. [Creación de una Entidad de certificación autofirmada](#create-a-self-signed-certification-authority)
2. [Cargar certificado de CA tooCloud servicio](#upload-ca-certificate-to-cloud-service)
3. [Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio](#update-ca-certificate-in-service-configuration-file)
4. [Emisión de certificados de cliente](#issue-client-certificates)
5. [Creación de archivos PFX para certificados de cliente](#create-pfx-files-for-client-certificates)
6. [Importación de certificados de cliente](#Import-Client-Certificate)
7. [Copia de las huellas digitales de certificados de cliente](#copy-client-certificate-thumbprints)
8. [Configurar a clientes permitido en hello archivo de configuración de servicio](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Uso de certificados de cliente existentes
1. [Find CA Public Key](#find-ca-public-key)
2. [Cargar certificado de CA tooCloud servicio](#Upload-CA-certificate-to-cloud-service)
3. [Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Copia de las huellas digitales de certificados de cliente](#Copy-Client-Certificate-Thumbprints)
5. [Configurar a clientes permitido en hello archivo de configuración de servicio](#configure-allowed-clients-in-the-service-configuration-file)
6. [Configuración de la comprobación de revocación de certificado de cliente](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Direcciones IP permitidas
Los puntos de conexión de servicio de acceso toohello pueden ser restringido toospecific intervalos de direcciones IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>cifrado de tooconfigure para la tienda de Hola
Un certificado es credenciales de hello tooencrypt requiere que se almacenan en el almacén de metadatos de Hola. Elegir el más apropiado de hello tres escenarios de Hola y ejecute todos sus pasos:

### <a name="use-a-new-self-signed-certificate"></a>Use un nuevo certificado autofirmado
1. [Creación de un certificado autofirmado](#create-a-self-signed-certificate)
2. [Crear archivo PFX para certificado de cifrado autofirmado](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Cargar certificado de cifrado tooCloud servicio](#upload-encryption-certificate-to-cloud-service)
4. [Actualización del certificado de cifrado en el archivo de configuración de servicio](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Usar un certificado existente del almacén de certificados de Hola
1. [Exportar el certificado de cifrado del almacén de certificados](#export-encryption-certificate-from-certificate-store)
2. [Cargar certificado de cifrado tooCloud servicio](#upload-encryption-certificate-to-cloud-service)
3. [Actualización del certificado de cifrado en el archivo de configuración de servicio](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Utilizar un certificado existente de un archivo PFX
1. [Cargar certificado de cifrado tooCloud servicio](#upload-encryption-certificate-to-cloud-service)
2. [Actualización del certificado de cifrado en el archivo de configuración de servicio](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>configuración predeterminada de Hola
configuración predeterminada de Hello deniega el punto de conexión de todos los acceso toohello HTTP. Se trata de hello recomendado, ya que los puntos de conexión de hello solicitudes toothese pueden incluir información confidencial, como credenciales de base de datos.
configuración predeterminada de Hello permite que el punto de conexión de todos los acceso toohello HTTPS. Esta configuración puede ser aún más restrictiva.

### <a name="changing-hello-configuration"></a>Cambiar la configuración de Hola
grupo de reglas de control de acceso que se aplican tooand extremo Hello se configura una Hola  **<EndpointAcls>**  sección Hola **archivo de configuración de servicio**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

las reglas de Hello en un grupo de control de acceso están configuradas en un <AccessControl name=""> sección del archivo de configuración de servicio de Hola. 

formato de Hola se explica en la documentación de listas de Control de acceso de red.
Por ejemplo, tooallow IP única en el punto de conexión de hello intervalo 100.100.0.0 too100.100.255.255 tooaccess Hola HTTPS, las reglas de hello sería similar al siguiente:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Prevención de la denegación de servicio
Hay dos mecanismos diferentes admiten toodetect y evitar los ataques de denegación de servicio:

* Restringir la cantidad de solicitudes simultáneas por host remoto (desactivado de manera predeterminada)
* Restringir la velocidad de acceso por host remoto (activado de manera predeterminada)

Estos se basan en características de hello ampliamente documentados en seguridad IP dinámica en IIS. Al cambiar esta configuración tenga cuidado de no Hola siguientes factores:

* comportamiento de Hola de dispositivos de traducción de direcciones de red sobre la información del host remoto de Hola y servidores proxy
* Se considera que cada recurso de tooany de solicitud en función de hello web (por ejemplo, cargar las secuencias de comandos, imágenes, etcetera)

## <a name="restricting-number-of-concurrent-accesses"></a>Restricción de la cantidad de acceso simultáneos
configuración de Hola que configura este comportamiento es:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Cambiar DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable esta protección.

## <a name="restricting-rate-of-access"></a>Restricción de la velocidad del acceso
configuración de Hola que configura este comportamiento es:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Configurar Hola respuesta tooa denegó la solicitud
Hello siguiente configura Hola respuesta tooa denegado la solicitud:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Consulte la documentación de toohello de seguridad IP dinámica en IIS para ver otros valores compatibles.

## <a name="operations-for-configuring-service-certificates"></a>Operaciones para configurar certificados de servicio
Este tema es solo para referencia. Siga los pasos de configuración de Hola que se describen en:

* Configurar un certificado SSL de Hola
* Configuración de certificados de cliente

## <a name="create-a-self-signed-certificate"></a>Creación de un certificado autofirmado
Ejecute:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n con la dirección URL del servicio de Hola. Caracteres comodín ("CN=*.cloudapp.net") y nombres alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") son compatibles.
* -e con fecha de expiración del certificado de hello crear una contraseña segura y especificarla cuando se le solicite.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Creación del archivo PFX para el certificado SSL autofirmado
Ejecute:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:

* Sí, exportar la clave privada de Hola
* Exportar todas las propiedades extendidas

## <a name="export-ssl-certificate-from-certificate-store"></a>Exportación del certificado SSL desde el almacén de certificados
* Busque el certificado
* Haga clic en Acciones -> Todas las tareas -> Exportar…
* Exporte el certificado a un archivo .PFX con estas opciones:
  * Sí, exportar la clave privada de Hola
  * Si es posible, incluir todos los certificados de ruta de certificación de Hola * exportar todas las propiedades extendidas

## <a name="upload-ssl-certificate-toocloud-service"></a>Cargar el servicio de toocloud de certificados SSL
Cargar el certificado con hello existente o generados. Archivo PFX con hello par de claves de SSL:

* Escribir contraseña de hello proteger la información de clave privada de Hola

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Actualización del certificado SSL en el archivo de configuración de servicio
Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Importación de la Entidad de certificación SSL
Siga estos pasos en todas las cuentas/máquina que se comunicarán con el servicio de Hola:

* Haga doble clic en Hola. Archivo .cer en el Explorador de Windows
* En el cuadro de diálogo de certificado de hello, haga clic en Instalar certificado...
* Importar certificado Hola que almacenar entidades de certificación raíz de confianza

## <a name="turn-off-client-certificate-based-authentication"></a>Desactivación de la autenticación basada en certificado de cliente
Se admite solo basada en certificado autenticación de cliente y deshabilitarlo permitirá a los puntos de conexión del servicio de toohello de acceso público, a menos que otros mecanismos están en vigor (por ejemplo, Microsoft Azure Virtual Network).

Cambiar estos toofalse de configuración de característica del servicio configuración archivo tooturn Hola de hello:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

A continuación, copie Hola misma huella digital que Hola SSL de certificados en la configuración del certificado de entidad emisora de certificados de hello:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Creación de una Entidad de certificación autofirmada
Ejecute hello siguiendo los pasos toocreate un tooact certificado autofirmado como una entidad de certificación:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize,

* -e con fecha de expiración de certificación de Hola

## <a name="find-ca-public-key"></a>Búsqueda de clave pública de Entidad de certificación
Todos los certificados de cliente se deben haber emitido por una entidad de certificación de confianza para el servicio de Hola. Buscar hello toohello clave pública entidad de certificación que emite certificados de cliente de Hola que van toobe utilizado para la autenticación en tooupload de orden se toohello servicio en la nube.

Si no hay ningún archivo de hello con clave pública de hello, exportarlo desde el almacén de certificados de hello:

* Busque el certificado
  * Busque un certificado de cliente emitido por Hola misma entidad de certificación
* Haga doble clic en el certificado de Hola.
* Seleccione la pestaña de la ruta de certificación de hello en el cuadro de diálogo de hello certificado.
* Haga doble clic en la entrada de la entidad emisora de certificados de hello en ruta de acceso de Hola.
* Tomar notas Hola de propiedades de certificado.
* Hola cerrar **certificado** cuadro de diálogo.
* Busque el certificado
  * Busque Hola CA se ha mencionado anteriormente.
* Haga clic en Acciones -> Todas las tareas -> Exportar…
* Exporte el certificado a un archivo .CER con estas opciones:
  * **No, no exportar la clave privada de Hola**
  * Si es posible, incluir todos los certificados de ruta de certificación de Hola.
  * Exportar todas las propiedades extendidas.

## <a name="upload-ca-certificate-toocloud-service"></a>Cargar el servicio de toocloud de certificados de entidad emisora de certificados
Cargar el certificado con hello existente o generados. Archivo CER con clave pública de hello entidad emisora de certificados.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Actualización de un certificado de Entidad de certificación en un archivo de configuración de servicio
Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Actualizar el valor de Hola de hello después de establecer con hello mismo huella digital:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Emisión de certificados de cliente
Cada servicio de hello tooaccess autorizados individuales debe tener un certificado de cliente emitido para his/hers exclusivo usar y debe elegir que posee tooprotect contraseña segura su clave privada. 

Hola pasos debe realizarse en Hola se generan y almacenan el mismo equipo donde hello certificado autofirmado de entidad emisora de certificados:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Personalización:

* -n con un identificador de cliente de toohello que se autenticarán con este certificado
* -e con fecha de expiración del certificado de Hola
* MyID.pvk y MyID.cer con nombres de archivo únicos para este certificado de cliente

Este comando le solicitará una contraseña toobe creado y, a continuación, usar una vez. Utilice una contraseña segura.

## <a name="create-pfx-files-for-client-certificates"></a>Creación de archivos PFX para certificados de cliente
Para cada certificado de cliente generado, ejecute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalización:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:

* Sí, exportar la clave privada de Hola
* Exportar todas las propiedades extendidas
* Hola toowhom individuales que se está emitiendo este certificado debe elegir la contraseña de la exportación de Hola

## <a name="import-client-certificate"></a>Importación de certificados de cliente
Cada usuario para el que se emitió un certificado de cliente debe importar el par de claves de hello en máquinas de Hola utilizará toocommunicate con el servicio de hello:

* Haga doble clic en Hola. Archivo PFX en el Explorador de Windows
* Importar certificado Hola Personal para almacenar con al menos esta opción:
  * Incluir todas las propiedades extendidas comprobadas

## <a name="copy-client-certificate-thumbprints"></a>Copia de las huellas digitales de certificados de cliente
Cada usuario para el que se emitió un certificado de cliente debe seguir estos pasos en la huella digital de orden tooobtain Hola de his/hers certificado que se agregará al archivo de configuración de servicio de toohello:

* Ejecute certmgr.exe
* Seleccione la ficha Personal Hola
* Haga doble clic en el certificado de cliente de hello toobe usado para la autenticación
* En hello certificado cuadro de diálogo que se abre, seleccione la ficha de detalles de Hola
* Asegúrese de que Mostrar esté mostrando Todo
* Campo de hello seleccione denominado huella digital en la lista de Hola
* Copiar valor de Hola de huella digital de Hola ** eliminar los caracteres Unicode no visibles delante del primer dígito de Hola ** eliminar todos los espacios

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Configurar a clientes de permitido en el archivo de configuración de servicio de Hola
Actualizar el valor de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con una lista separada por comas de huellas digitales de Hola Hola de certificados de cliente permitidos el acceso toohello servicio:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Configuración de la comprobación de revocación de certificado de cliente
configuración predeterminada de Hello no comprueba con hello entidad de certificación para el estado de revocación del certificado de cliente. tooturn en hello comprueba si Hola entidad de certificación que emitió los certificados de cliente hello es compatible con esas comprobaciones, cambie Hola siguientes configuración con uno de los valores de hello definidos en hello X509RevocationMode enumeración:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Crear archivo PFX para certificados de cifrado autofirmados
Para un certificado de cifrado, ejecute:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personalización:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Escriba la contraseña y, a continuación, exporte el certificado con estas opciones:

* Sí, exportar la clave privada de Hola
* Exportar todas las propiedades extendidas
* Necesitará Hola contraseña al cargar el servicio de nube de hello certificados toohello.

## <a name="export-encryption-certificate-from-certificate-store"></a>Exportar el certificado de cifrado del almacén de certificados
* Busque el certificado
* Haga clic en Acciones -> Todas las tareas -> Exportar…
* Exporte el certificado a un archivo .PFX con estas opciones: 
  * Sí, exportar la clave privada de Hola
  * Si es posible, incluir todos los certificados de ruta de certificación de Hola 
* Exportar todas las propiedades extendidas

## <a name="upload-encryption-certificate-toocloud-service"></a>Cargar el servicio de toocloud de certificados de cifrado
Cargar el certificado con hello existente o generados. Archivo PFX con el par de claves de cifrado de hello:

* Escribir contraseña de hello proteger la información de clave privada de Hola

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Actualización del certificado de cifrado en el archivo de configuración de servicio
Actualizar el valor de huella digital de Hola de hello después de la configuración en el archivo de configuración de servicio de hello con la huella digital de hello del servicio de nube de hello certificado cargado toohello:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Operaciones comunes de certificado
* Configurar un certificado SSL de Hola
* Configuración de certificados de cliente

## <a name="find-certificate"></a>Busque el certificado
Siga estos pasos:

1. Ejecute mmc.exe.
2. Archivo -> Agregar o quitar complemento…
3. Seleccione **Certificados**.
4. Haga clic en **Agregar**.
5. Elija la ubicación del almacén de certificados de Hola.
6. Haga clic en **Finalizar**
7. Haga clic en **Aceptar**.
8. Expanda **Certificados**.
9. Expanda el nodo del almacén de certificados de Hola.
10. Expandir nodo de hello certificado secundario.
11. Seleccione un certificado en la lista de Hola.

## <a name="export-certificate"></a>Exportación de certificado
Hola **Asistente para exportar certificados**:

1. Haga clic en **Siguiente**.
2. Seleccione **Sí**, a continuación, **clave privada de exportación hello**.
3. Haga clic en **Siguiente**.
4. Seleccione el formato de archivo de salida que desee Hola.
5. Compruebe las opciones de hello deseado.
6. Marque **Contraseña**.
7. Escriba una contraseña segura y confírmela.
8. Haga clic en **Siguiente**.
9. Escriba o busque un nombre de archivo donde toostore Hola certificado (utilice una. Extensión PFX).
10. Haga clic en **Siguiente**.
11. Haga clic en **Finalizar**
12. Haga clic en **Aceptar**.

## <a name="import-certificate"></a>Importación de certificado
En el Asistente para importar certificados hello:

1. Seleccione la ubicación del almacén de Hola.
   
   * Seleccione **usuario actual** si solo los procesos que se ejecutan en usuario actual tendrá acceso a servicio de Hola
   * Seleccione **equipo Local** si otros procesos en este equipo tendrá acceso a servicio de Hola
2. Haga clic en **Siguiente**.
3. Si importa desde un archivo, confirme la ruta de acceso de archivo Hola.
4. Si se importa un archivo .PFX:
   1. Escribir contraseña de hello protege la clave privada de Hola
   2. Seleccione las opciones de importación
5. Seleccionar certificados de "Ubicación" Hola después de la tienda
6. Haga clic en **Examinar**.
7. Seleccionar el almacén de hello deseado.
8. Haga clic en **Finalizar**
   
   * Si se ha elegido el almacén de la entidad de certificación raíz de confianza de hello, haga clic en **Sí**.
9. Haga clic en **Aceptar** en todas las ventanas de diálogo.

## <a name="upload-certificate"></a>Carga del certificado
Hola [Portal de Azure](https://portal.azure.com/)

1. Seleccione **Servicios en la nube**.
2. Seleccione servicio de nube de Hola.
3. En el menú superior de hello, haga clic en **certificados**.
4. En la barra de la parte inferior de hello, haga clic en **cargar**.
5. Seleccione el archivo de certificado de Hola.
6. Si es un. PFX archivo, escriba la contraseña de hello para la clave privada de Hola.
7. Una vez completado, copie huella digital del certificado Hola de nueva entrada de hello en lista de Hola.

## <a name="other-security-considerations"></a>Otras consideraciones de seguridad
configuración de SSL de Hello descrita en este documento cifrar la comunicación entre servicio hello y sus clientes cuando se usa el punto de conexión de hello HTTPS. Esto es importante, porque las credenciales para el acceso a la base de datos y posiblemente otra información confidencial están incluidos en la comunicación de Hola. Sin embargo, tenga en cuenta que el servicio de hello continúa estado interno, incluidas las credenciales, en sus tablas internas de la base de datos de SQL de Microsoft Azure de Hola que ha proporcionado para el almacenamiento de metadatos en su suscripción de Microsoft Azure. Esa base de datos se ha definido como parte de hello después de la configuración en el archivo de configuración de servicio (. Archivo CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Las credenciales almacenadas en esta base de datos están cifradas. Sin embargo, como práctica recomendada, asegúrese de que los roles web y de trabajo de las implementaciones de servicio se mantienen toodate y segura tienen acceso toohello metadatos hello y base de datos certificado usado para el cifrado y descifrado de credenciales almacenadas. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

