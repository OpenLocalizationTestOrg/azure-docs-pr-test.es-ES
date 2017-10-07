---
title: "datos personales aaaProtect en tránsito con el cifrado en Azure | Documentos de Microsoft"
description: Mediante el cifrado en Azure tooprotect los datos personales
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Tecnologías de cifrado de Azure: protección de datos personales en tránsito con cifrado

En este artículo le ayudará a comprender y usar datos de toosecure de tecnologías de cifrado de Azure en tránsito. 

Privacidad de hello protección de datos personales que viajan a través de la red de hello es una parte esencial de una estrategia de seguridad varias capas de defensa en profundidad. El cifrado en tránsito es diseñada tooprevent si un atacante intercepta las transmisiones de ser capaz de datos de hello tooview o el uso.

## <a name="scenario"></a>Escenario

Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas. toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido 

la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola. Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global. También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones. línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.

Datos personales de los clientes se escribe en la base de datos de Hola de oficinas remotas de la compañía de Hola y de agentes de viaje situados alrededor de Hola a todos. Los documentos que contienen información del cliente se transfieren a través de almacenamiento de la red tooAzure Hola.

## <a name="problem-statement"></a>Declaración del problema

empresa Hola debe proteger la privacidad de Hola de los clientes y datos personales de los empleados mientras están en tránsito tooand desde servicios de Azure.

## <a name="company-goal"></a>Objetivo de la empresa

Hola tooensure de objetivo de empresa que se cifran los datos personales al desactivar el disco. Si las personas no autorizadas interceptan datos personales de hello desactivar el disco, debe ser en un formulario que se representará ilegible. La aplicación del cifrado debería ser fácil o totalmente transparente tanto para los usuarios como para los administradores.

## <a name="solutions"></a>Soluciones

Los servicios de Azure proporcionan varios toohelp herramientas y tecnologías de proteger los datos personales en tránsito.

### <a name="azure-storage"></a>Azure Storage

Datos que se almacenan en la nube de hello deben viajar desde el cliente hello, que puede estar ubicado físicamente en cualquier lugar de Hola a todos, toohello centro de datos de Azure. Cuando esos datos se recuperan los usuarios, pasa de nuevo, en hello dirección opuesta. Datos que están en tránsito a través de Hola Internet pública siempre está en riesgo de interceptación por los atacantes. Es privacidad de hello tooprotect importante de los datos personales mediante el uso de toosecure de cifrado de nivel de transporte tal como se mueve entre ubicaciones.

Hola protocolo HTTPS proporciona un canal de comunicaciones cifradas seguras a través de Internet de Hola. HTTPS debe ser objetos de tooaccess usado en el almacenamiento de Azure y al llamar a las API de REST. Exigir el uso del protocolo HTTPS de Hola al usar [firmas de acceso compartido](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) objetos de almacenamiento (SAS) toodelegate acceso tooAzure. Hay dos tipos de SAS: SAS de servicio y SAS de cuenta.

#### <a name="how-do-i-construct-a-service-sas"></a>¿Cómo se puede crear una SAS de servicio?

Un servicio SAS delegados acceso tooa recurso en solo uno de los servicios de almacenamiento de hello (servicio blob, cola, tabla o archivo). Hola tooconstruct una SAS de servicio siguientes:

1. Especificar Hola Signed campo de versión

2. Especificar Hola Signed recursos (Blob y archivo de servicio solo)

3. Especificar encabezados de respuesta de tooOverride de parámetros de consulta (servicio de Blob y archivo de servicio solo)

4. Especificar hello (solo servicio de tabla) el nombre de tabla

5. Especificar Hola directiva de acceso

6. Especificar Hola intervalo de validez de firma

8. Especifique los permisos

9. Especifique la dirección IP o el intervalo IP

10. Especificar Hola protocolo HTTP

11. Especifique los intervalos de acceso a la tabla

12. Especificar Hola identificador firmado

13. Especificar Hola firma

Para obtener instrucciones más detalladas, consulte [Creación de una SAS de servicio](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>¿Cómo se puede crear una SAS de cuenta?

Una SAS de cuenta delega tooresources de acceso en uno o varios de los servicios de almacenamiento de Hola. También puede delegar el acceso tooread, escritura y las operaciones de eliminación en contenedores de blobs, tablas, colas y recursos compartidos de archivos que no se permiten con un servicio de SAS. Construcción de una cuenta SA es toothat similar de una SAS de servicio. Para obtener instrucciones detalladas, consulte [Creación de una SAS de cuenta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>¿Cómo se puede aplicar HTTPS al llamar a API de REST?

tooenforce el uso de Hola de HTTPS al llamar a objetos de las API de REST tooaccess en cuentas de almacenamiento, puede habilitar la transferencia segura necesaria Hola cuenta de almacenamiento. 

1. Hola portal de Azure, seleccione **crear cuenta de almacenamiento**, o para una cuenta de almacenamiento existente, seleccione **configuración** y, a continuación, **configuración**.

2. En **Se requiere transferencia segura**, seleccione **Habilitado**.

![Creación de una cuenta de almacenamiento](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Para obtener más instrucciones, incluido cómo tooenable seguros transferir necesarios mediante programación, vea [requieren Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>¿Cómo se pueden cifrar datos en Azure File Storage?

tooencrypt datos en tránsito con [almacenamiento de archivos de Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), puede usar SMB 3.x con Windows 8, 8.1 y 10 y Windows Server 2012 R2 y Windows Server 2016. Cuando se usa el servicio de archivos de Azure de hello, se produce un error en cualquier conexión sin cifrado cuando "Proteger la transferencia requerida" está habilitada. Esto incluye escenarios con algunos tipos de hello cliente Linux SMB, SMB 2.1 y SMB 3.0 sin cifrado.

#### <a name="azure-client-side-encryption"></a>Cifrado de cliente de Azure

Otra opción para proteger datos personales mientras se transfieren entre una aplicación cliente y Azure Storage es [Cifrado de cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Hola datos se cifran antes de que se transfieren al almacenamiento de Azure y cuando se recuperan datos de Hola desde el almacenamiento de Azure, se descifran datos Hola tras su recepción en el lado del cliente de Hola.

### <a name="azure-site-to-site-vpn"></a>VPN de sitio a sitio de Azure

Un modo eficaz tooprotect personal los datos en tránsito entre una red corporativa o un usuario y Hola red virtual de Azure están toouse una [sitio a sitio](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) o [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) red privada Virtual (VPN). Una conexión VPN crea un túnel cifrado seguro a través de Internet de Hola.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>¿Cómo se puede crear una conexión VPN de sitio a sitio?

Una VPN de sitio a sitio conecta a varios usuarios en hello tooAzure de red corporativa. toocreate una conexión de sitio a sitio en el portal de Azure, Hola Hola siguientes:

1. Cree una red virtual.

2. Especifique un servidor DNS

3. Crear una subred de puerta de enlace de Hola.

4. Crear puerta de enlace VPN de Hola. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Crear puerta de enlace de red local de Hola.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Configure el dispositivo VPN.

7. Crear la conexión de VPN de Hola.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Compruebe la conexión de VPN de Hola.

Para obtener instrucciones detalladas sobre cómo conexión toocreate un sitio a sitio en hello Azure portal, vea [crear un sitio a sitio de conexión en hello Portal de Azure]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>¿Cómo se puede crear una conexión VPN de punto a sitio?

Una VPN de sitio a punto, crea una conexión segura en una red virtual de la tooa de equipos cliente individuales. Esto es útil cuando se desea tooconnect tooAzure desde una ubicación remota, como desde el centro principal o de un hotel o conferencia. toocreate una conexión punto a sitio en hello portal de Azure,

1. Cree una red virtual.

2. Agregue una subred de puerta de enlace.

3. Especifique un servidor DNS (opcional).

4. Cree una puerta de enlace de red virtual.

5. Genere certificados.

6. Agregar grupo de direcciones de cliente de Hola.

7. Cargar datos de certificado público del certificado de raíz de Hola.

8. Generar e instalar el paquete de configuración de cliente VPN de Hola.

9. Instale un certificado de cliente exportado.

10. Conectar tooAzure.

11. Compruebe la conexión.

Para obtener instrucciones detalladas, consulte [configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: Portal de Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Microsoft recomienda que siempre que usan los datos de tooexchange de protocolos SSL/TLS en diferentes ubicaciones. Las organizaciones que elija toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandes conjuntos de datos mediante un vínculo WAN de alta velocidad dedicado también puede cifrar los datos de hello en hello mediante TLS/SSL u otros protocolos para una mayor protección de nivel de aplicación.

### <a name="encryption-by-default"></a>Cifrado de forma predeterminada

Microsoft utiliza los datos de tooprotect de cifrado en tránsito entre los clientes y los servicios de nube de Azure. Si interactúa con el almacenamiento de Azure a través de hello Portal de Azure, todas las transacciones se producen a través de HTTPS.

[Seguridad de la capa de transporte](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) es el protocolo de Hola que los centros de datos de Microsoft intentará toonegotiate con sistemas de cliente que se conectan tooMicrosoft servicios en la nube. TLS proporciona una autenticación sólida, privacidad de mensajes e integridad (lo que permite la detección de la manipulación, interceptación y falsificación de mensajes), interoperabilidad, flexibilidad de algoritmo y facilidad de implementación y uso.

[Confidencialidad directa total](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) también se emplea para que cada conexión entre los sistemas cliente de los clientes y los servicios en la nube de Microsoft use claves únicas. Servicios en la nube tooMicrosoft conexiones también sacar partido de cifrado de 2048 bits RSA según longitudes de clave. Hola combinación de TLS, longitudes de clave de RSA 2048 bits, y PFS hace mucho más difícil para un usuario toointercept y acceso a datos que están en tránsito entre servicios de nube de Microsoft y los clientes.

Los datos en tránsito siempre se cifran en [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). Por otra parte media toopersistent de tooencrypting datos toostoring anterior, Hola datos están protegidos también siempre a través de HTTPS en tránsito. HTTPS es Hola único protocolo admitido para hello que REST de almacén de datos Lake interfaces.

## <a name="summary"></a>Resumen

empresa Hola puede lograr su objetivo de proteger la privacidad hello y datos personal de tales datos exigir HTTPS conexiones tooAzure almacenamiento, mediante firmas de acceso compartido y habilitar la transferencia segura necesaria hello en cuentas de almacenamiento. También puede proteger datos personales mediante conexiones SMB 3.0 e implementando cifrado de cliente. Hola a las conexiones VPN de sitio a sitio de red corporativa toohello red virtual de Azure y conexiones de point-to-site VPN de los usuarios individuales crean un túnel seguro a través del cual pueden viajar forma segura los datos personales. Prácticas de cifrado predeterminado de Microsoft protegerá aún más la privacidad de Hola de los datos personales.

## <a name="next-steps"></a>Pasos siguientes

- [Procedimientos recomendados de cifrado y seguridad de datos en Azure](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Planeamiento y diseño de VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [Preguntas más frecuentes sobre VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Compra y configuración de un certificado SSL para Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
