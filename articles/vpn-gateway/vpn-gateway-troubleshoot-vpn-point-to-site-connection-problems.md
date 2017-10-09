---
title: "problemas de conexión de aaaTroubleshoot point-to-site Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot problemas de conexión de punto a sitio."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Solución de problemas: conexión de punto a sitio de Azure

En este artículo se enumeran problemas comunes de conexión de punto a sitio que puede experimentar. También se tratan las posibles causas de estos problemas y sus soluciones.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Error de cliente de VPN: no se encontró un certificado

### <a name="symptom"></a>Síntoma

Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:

**No se encuentra un certificado que se puede usar con este protocolo de autenticación extendido. (Error 798)**

### <a name="cause"></a>Causa

Este problema se produce si no está presente en el certificado de cliente hello **certificados - actual\Personal\Certificados**.

### <a name="solution"></a>Solución

Asegúrese de que ese certificado de cliente de Hola se instala en hello ubicación Hola o almacén de certificados (Certmgr.msc) siguiente:
 
**Certificados - Usuario actual\Personal\Certificados**

Para obtener más información acerca de cómo tooinstall Hola certificado de cliente, consulte [generar y exportar certificados para las conexiones point-to-site](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Cuando se importa el certificado de cliente de hello, no seleccione hello **Habilitar protección segura de clave privada** opción.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Error del cliente VPN: se ha recibido el mensaje de saludo con formato incorrecto o inesperado

### <a name="symptom"></a>Síntoma

Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:

**mensaje de Hola recibido fue inesperado o con formato incorrecto. (Error 0x80090326)**

### <a name="cause"></a>Causa

Este problema se produce si la clave pública del certificado de raíz hello no se cargará en la puerta de enlace de VPN de Azure de Hola. También puede producirse si la clave de hello está dañado o caducado.

### <a name="solution"></a>Solución

tooresolve este problema, comprobar el estado de Hola de raíz de hello certificados en hello Azure toosee portal si se ha revocado. Si no se revoque, intente reupload y un certificado de raíz de toodelete Hola. Para más información, vea [Crear certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Error de cliente de VPN: una cadena de certificados se ha procesado pero ha finalizado 

### <a name="symptom"></a>Síntoma 

Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:

**Una cadena de certificados ha procesado pero termina en un certificado raíz que no es de confianza para proveedor de confianza de Hola.**

### <a name="solution"></a>Solución

1. Asegúrese de que ese Hola siguientes certificados están en la ubicación correcta de hello:

    | Certificate | La ubicación |
    | ------------- | ------------- |
    | AzureClient.pfx  | Usuario actual\Personal\Certificados |
    | Azuregateway-*GUID*.cloudapp.net  | Usuario actual\Entidades de certificación raíz de confianza|
    | AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer    | Equipo local\Entidades de certificación raíz de confianza|

2. Si los certificados de hello ya están en la ubicación de hello, intente toodelete certificados de Hola y vuelva a instalarlos. Hola  **azuregateway -*GUID*. cloudapp.net** certificado está en el paquete de configuración de cliente VPN de Hola que descargó desde Hola portal de Azure. Puede usar archivadores tooextract Hola archivos del paquete de saludo.

## <a name="file-download-error-target-uri-is-not-specified"></a>Error en la descarga del archivo. No se ha especificado el URI de destino

### <a name="symptom"></a>Síntoma

Recepción Hola mensaje de error siguiente:

**Error en la descarga del archivo. No se ha especificado el URI de destino.**

### <a name="cause"></a>Causa 

Este problema se produce debido a un tipo de puerta de enlace incorrecto. 

### <a name="solution"></a>Solución

debe ser el tipo de puerta de enlace VPN de Hola **VPN**, y debe ser Hola tipo VPN **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Error de cliente de VPN: error de script personalizado de VPN de Azure 

### <a name="symptom"></a>Síntoma

Cuando intente tooconnect tooan red virtual de Azure mediante el uso de cliente VPN de hello, recibirá Hola mensaje de error siguiente:

**Secuencia de comandos personalizada (enrutamiento de la tabla tooupdate) no se pudo. (Error 8007026f)**

### <a name="cause"></a>Causa

Este problema puede producirse si está tratando de conexión de VPN de sitio a punto de hello tooopen mediante un acceso directo.

### <a name="solution"></a>Solución 

Abra el paquete VPN de hello directamente en lugar de abrirlo en acceso directo de Hola.

## <a name="cannot-install-hello-vpn-client"></a>No se puede instalar el cliente VPN de Hola

### <a name="cause"></a>Causa 

Un certificado adicional es necesario tootrust puerta de enlace VPN de hello para la red virtual. certificado de Hola se incluye en el paquete de configuración de cliente VPN de Hola que se genera a partir de hello portal de Azure.

### <a name="solution"></a>Solución

Extraer el paquete de configuración de cliente VPN de Hola y busque el archivo .cer de Hola. Hola tooinstall certificados, siga estos pasos:

1. Abra mmc.exe.
2. Agregar hello **certificados** complemento.
3. Seleccione hello **equipo** de la cuenta de equipo local Hola.
4. Menú contextual hello **entidades de certificación raíz de confianza** nodo. Haga clic en **All-Task** > **importación**y examinar toohello CER ha extraído del paquete de configuración de cliente VPN de Hola.
5. Reinicie el equipo de Hola. 
6. Pruebe el cliente VPN de hello tooinstall.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Error de portal de Azure: error de puerta de enlace VPN toosave Hola y Hola datos no son válidos

### <a name="symptom"></a>Síntoma

Al probar cambios de hello toosave para puerta de enlace VPN de Hola Hola portal de Azure, recibirá Hola mensaje de error siguiente:

**Puerta de enlace de red virtual de error toosave &lt;* nombre de puerta de enlace*&gt;. Los datos del certificado &lt;*identificador de certificado*&gt; no son válidos.**

### <a name="cause"></a>Causa 

Este problema puede producirse si Hola raíz certificado clave pública que ha cargado contiene un carácter no válido, como un espacio.

### <a name="solution"></a>Solución

Asegúrese de que los datos de hello en el certificado de hello no contienen caracteres no válidos, como los saltos de línea (retorno de carro). valor de Hello completo debe ser una línea larga. Hola después de texto es un ejemplo de certificado de hello:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Error de portal de Azure: error de puerta de enlace VPN toosave Hola y Hola nombre de recurso no es válido

### <a name="symptom"></a>Síntoma

Al probar cambios de hello toosave para puerta de enlace VPN de Hola Hola portal de Azure, recibirá Hola mensaje de error siguiente: 

**Puerta de enlace de red virtual de error toosave &lt;* nombre de puerta de enlace*&gt;. Nombre del recurso &lt; *nombre del certificado intentas tooupload* &gt; es válida **.

### <a name="cause"></a>Causa

Este problema se produce porque el nombre hello del certificado de hello contiene un carácter no válido, como un espacio. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Error de Azure Portal: error de descarga de archivo de paquete de VPN 503

### <a name="symptom"></a>Síntoma

Al probar el paquete de configuración de cliente VPN de toodownload hello, recibirá Hola mensaje de error siguiente:

**Error al archivo de hello toodownload. Detalles del error: error 503. Hola servidor está ocupado.**
 
### <a name="solution"></a>Solución

Este error puede deberse a un problema de red temporal. Paquete de VPN de hello toodownload vuelva a intentar tras unos minutos.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Actualización de puerta de enlace VPN de Azure: P2S todos los clientes son tooconnect no se puede

### <a name="cause"></a>Causa

Si el certificado de hello es más del 50 por ciento a través de su duración, se deshaga certificado Hola.

### <a name="solution"></a>Solución

tooresolve este problema, cree y redistribuir los clientes VPN de toohello de nuevos certificados. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Demasiados clientes de VPN conectados a la vez

Para cada puerta de enlace VPN, el número máximo de Hola de conexiones permitidas es 128. Puede ver el número total de Hola de clientes conectados en hello portal de Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Point-to-site VPN incorrectamente agrega una ruta para una tabla de rutas toohello 10.0.0.0/8

### <a name="symptom"></a>Síntoma

Al marcar la conexión VPN en el cliente de point-to-site Hola Hola, cliente VPN de Hola debe agregar una ruta hacia Hola red virtual de Azure. servicio auxiliar IP de Hello debe agregar una ruta para subred Hola Hola de clientes de VPN. 

Hola intervalo de cliente VPN pertenece tooa subred más pequeño de 10.0.0.0/8, como 10.0.12.0/24. En lugar de una ruta para 10.0.12.0/24, se agrega una ruta para 10.0.0.0/8 con una prioridad más alta. 

Esta ruta incorrecta interrumpe la conectividad con otras redes locales que es posible que pertenezca tooanother subred dentro de intervalo de 10.0.0.0/8 hello, como 10.50.0.0/24, que no tienen una ruta específica definida. 

### <a name="cause"></a>Causa

Este comportamiento es así por diseño para los clientes Windows. Si el cliente de hello usa el protocolo PPP IPCP de hello, que obtiene dirección IP de hello para la interfaz de túnel de hello del servidor de hello (Hola puerta de enlace VPN en este caso). Sin embargo, debido a una limitación en el protocolo de Hola, cliente hello no tiene máscara de subred de Hola. Porque no hay ningún otro tooget de manera, cliente hello intenta tooguess máscara de subred de hello en función de la clase hello de dirección IP de la interfaz de túnel de Hola. 

Por lo tanto, se agrega una ruta en función de hello después de asignación estática: 

Si la dirección pertenece A tooclass--> Aplicar prefijo/8

Si la dirección pertenece tooclass--> B aplicar /16

Si la dirección pertenece tooclass C--> aplicar /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>El cliente de VPN no puede acceder a recursos compartidos de archivos de red

### <a name="symptom"></a>Síntoma

cliente VPN de Hola ha conectado toohello red virtual de Azure. Sin embargo, el cliente de hello no puede tener acceso a recursos compartidos de red.

### <a name="cause"></a>Causa

Hola protocolo SMB se utiliza para el acceso de recurso compartido de archivos. Cuando se inicia la conexión de Hola, cliente VPN de hello agrega credenciales de la sesión de Hola y Hola produzcan. Una vez establecida la conexión de Hola, cliente de Hola se ve obligado a credenciales almacenadas en caché toouse hello para la autenticación Kerberos. Este proceso inicia consultas toohello Key Distribution Center (un controlador de dominio) tooget un token. Porque Hola cliente se conecta desde Hola Internet, no sea controlador de dominio pueda tooreach Hola. Por lo tanto, cliente hello no puede conmutar por error de Kerberos tooNTLM. 

Hola solo tiempo ese cliente Hola se recibirá un mensaje para una credencial es cuando tiene un certificado válido (con SAN = UPN) emitido por hello toowhich de dominio se ha unido. cliente de Hello también debe estar conectada físicamente toohello red de dominio. En este caso, el cliente de Hola intenta certificado de hello toouse y llega toohello controlador de dominio. A continuación, Hola Key Distribution Center devuelve un error de "KDC_ERR_C_PRINCIPAL_UNKNOWN". cliente de Hello es forzada toofail sobre tooNTLM. 

### <a name="solution"></a>Solución

toowork sobre el problema de hello, deshabilitar Hola almacenamiento en caché de credenciales de dominio de la siguiente subclave del registro de hello: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>No se puede encontrar la conexión de hello point-to-site VPN en Windows después de reinstalar el cliente VPN de Hola

### <a name="symptom"></a>Síntoma

Quitar la conexión de hello point-to-site VPN y, a continuación, vuelva a instalar el cliente VPN de Hola. En esta situación, Hola conexión VPN no está configurado correctamente. No ve la conexión de VPN de Hola Hola **las conexiones de red** configuración de Windows.

### <a name="solution"></a>Solución

problema de hello tooresolve, delete Hola antiguo VPN cliente archivos de configuración de **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, y, a continuación, vuelva a ejecutar el instalador del cliente VPN Hola.
