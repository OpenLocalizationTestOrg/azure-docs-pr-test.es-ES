---
title: "Introducción al cifrado aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las distintas opciones de cifrado en Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Información general del cifrado de Azure

Este artículo proporciona información general sobre cómo se usa el cifrado en Microsoft Azure. Se ocupa de las áreas principales de Hola de cifrado, como el cifrado en reposo, cifrado en tránsito y administración de claves con el almacén de claves. Cada sección incluye vínculos para obtener información más detallada.

## <a name="encryption-of-data-at-rest"></a>Cifrado de datos en reposo

Los datos en reposo incluyen información que se encuentra en el almacenamiento persistente en un medio físico, en cualquier formato digital. Esto incluye archivos en medios ópticos o magnéticos, datos archivados y copias de seguridad de datos. Microsoft Azure ofrece una variedad de toomeet de soluciones de almacenamiento de datos distintas necesidades, incluidos archivos, discos, blob y el almacenamiento de tabla. Microsoft también proporciona cifrado tooprotect [base de datos de SQL Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)y Azure Data Lake.

Cifrado de datos en reposo está disponible para los servicios a través de hello Azure Software como-servicio (SaaS), plataforma como-servicio (PaaS) y los modelos de nube de infraestructura como-servicio (IaaS). En este documento se resumen y proporciona recursos toohelp usar opciones de cifrado de Azure.

Para obtener más explicación de cómo se cifran los datos en reposo en Azure, consulte el documento Hola titulado [cifrado en el resto de datos de Azure](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Modelos de cifrado de Azure

Azure admite distintos modelos de cifrado, incluido el cifrado de servidor con claves administradas por el servicio, mediante claves administradas por el cliente en Azure Key Vault o mediante las claves administradas por el cliente en el hardware controlado por el cliente. Cifrado en el cliente permite toomanage y el almacén de claves local o en otra ubicación protegida.

### <a name="client-side-encryption"></a>cifrado de cliente

El cifrado de cliente se realiza fuera de Azure. El cifrado de cliente incluye:

- Datos cifrados por una aplicación que se ejecuta en el centro de datos del cliente de Hola o por una aplicación de servicio
- Datos que ya están cifrados cuando Azure los recibe.

Con el cifrado de cliente proveedor de servicios de nube de hello no tiene claves de cifrado de toohello de acceso y no puede descifrar estos datos. Mantener un control completo de las claves de Hola.

### <a name="server-side-encryption"></a>Cifrado del servidor

tres modelos de cifrado del lado servidor Hello ofrecen características de administración de claves diferentes, que se pueden elegir según sus requisitos.

- **Claves administradas del servicio** proporcionan una combinación de control y comodidad con una sobrecarga reducida

- **Claves administradas por el cliente** le permiten controlar claves de hello, incluidas Hola capacidad toobring sus propias claves (BYOK) o toogenerate nuevos.

- **Los servicios de administrar claves de ccustomer controlledhardware** permite toomanage claves en el repositorio de propietario que se encuentre fuera del control de Microsoft. Esto se denomina Hospedar su propia clave (HYOK). Sin embargo, la configuración es compleja y la mayoría de los servicios de Azure no son compatibles con este modelo.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Máquinas virtuales Windows y Linux pueden protegerse con [cifrado del disco de Azure](azure-security-disk-encryption.md), que utiliza hello [BitLocker de Windows](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) tecnología y Linux [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect discos del sistema operativo y discos de datos con el cifrado de volumen completo.

Las claves de cifrado y secretos se protegen en la suscripción de [Azure Key Vault](../key-vault/key-vault-whatis.md). Puede realizar una copia y restaurar cifradas máquinas virtuales que se cifran con la configuración de KEK hello mediante el servicio de copia de seguridad de Azure Hola.

### <a name="azure-storage-service-encryption"></a>Cifrado del servicio Azure Storage

Los datos en reposo en Azure Storage (tanto de blobs como de archivos) pueden cifrarse en escenarios de cliente y servidor.

[Cifrado del servicio de almacenamiento de Azure](../storage/storage-service-encryption.md) (SSE) puede cifrar automáticamente los datos antes de que se almacena y descifra automáticamente cuando lo recupera, realizar Hola procesar completamente transparente a los usuarios. Cifrado del servicio de almacenamiento usa 256 bits [el cifrado AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), que es uno de hello más fuertes cifrados en bloque disponibles y controla el cifrado, descifrado y administración de claves de forma transparente.

### <a name="client-side-encryption-of-azure-blobs"></a>Cifrado de cliente de blobs de Azure

El cifrado de cliente de blobs de Azure puede realizarse de maneras diferentes.

Puede usar Hola biblioteca de cliente de almacenamiento de Azure para datos tooencrypt del paquete de NuGet de .NET dentro de su toouploading anteriores de las aplicaciones de cliente se tooAzure almacenamiento.

toolearn más información sobre y descarga Hola biblioteca de cliente de almacenamiento de Azure para el paquete de NuGet. NET, vea documento Hola titulado [8.3.0 de almacenamiento de Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage)

Cuando se usa el cifrado de cliente con el almacén de claves de Azure, los datos se cifran con una única simétrica contenido cifrado de clave (CEK) generadas por el SDK del cliente de almacenamiento de Azure Hola. Hola CEK se cifra mediante una clave de cifrado de claves (KEK), que puede ser una clave simétrica o un par de claves asimétricas. Puede administrarla de forma local o almacenarla en Azure Key Vault. Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de tooAzure.

toolearn más acerca del cifrado de cliente con el almacén de claves de Azure y empezar a trabajar con cómo tooinstructions, vea el documento Hola titulado [Tutorial: cifrar y descifrar los blobs en almacenamiento de Azure de Microsoft con el almacén de claves de Azure](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Por último, también puede utilizar Hola biblioteca de cliente de almacenamiento de Azure para el cifrado de cliente de Java tooperform antes de cargar datos tooAzure almacenamiento y toodecrypt los datos Hola al descargar a toohello cliente. Esta biblioteca también admite la integración con [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) para la administración de las claves de la cuenta de almacenamiento.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Cifrado de datos en reposo con Azure SQL Database

[Azure SQL Database](../sql-database/sql-database-technical-overview.md) es un servicio de base de datos relacional de uso general de Microsoft Azure que admite estructuras como datos relacionales, JSON, espacial y XML. SQL Azure admite el cifrado de servidor a través de la característica de cifrado de datos transparente (TDE) de Hola y el cifrado de cliente a través de la característica Always Encrypted de Hola.

#### <a name="transparent-data-encryption"></a>Cifrado de datos transparente

[Cifrado de datos transparente TDE](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) es usado tooencrypt [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [base de datos de SQL Azure](../sql-database/sql-database-technical-overview.md), y [almacenamiento de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) archivos de datos en tiempo real, usar una clave de cifrado de base de datos (DEK), que se almacena en el registro de arranque de base de datos de Hola para disponibilidad durante la recuperación.

TDE protege los archivos de registro y datos con los algoritmos de cifrado AES y 3DES. El cifrado del archivo de base de datos de Hola se realiza a nivel de página de hello; páginas de Hello en una base de datos cifrada se cifran antes de que se escriben toodisk y se descifran cuando se leen en la memoria. TDE ahora está habilitado de forma predeterminada en las bases de datos SQL de Azure recién creadas.

#### <a name="always-encrypted"></a>Always Encrypted

Hola [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) característica en SQL Azure le permite tooencrypt los datos dentro de toostoring anteriores de las aplicaciones de cliente en la base de datos de SQL Azure y permite la delegación de tooenable de toothird de administración de base de datos local usuarios y mantener la separación entre aquellos que poseen y puede ver datos de Hola y aquellos que administrarlo pero no debería tener acceso tooit.

#### <a name="cellcolumn-level-encryption"></a>Cifrado de nivel de columna/celda

La base de datos de SQL Azure le permite tooapply columna de tooa de cifrado simétrico de datos mediante Transact-SQL. Esto se denomina [cifrado de nivel de columna o de cifrado de nivel de celda](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (CLE), porque se pueden utilizar columnas específicas de tooencrypt o incluso determinadas celdas de datos con distintas claves de cifrado. Esto proporciona una capacidad de cifrado más granular que TDE, que cifra los datos en páginas.

CLE tiene funciones integradas que puede usar datos de tooencrypt mediante claves simétricas o asimétricas, clave pública de Hola de un certificado o con una frase de contraseña con 3DES.

### <a name="cosmos-db-database-encryption"></a>Cifrado de base de datos Cosmos DB

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) es la base de datos multimodelo de distribución global de Microsoft. Datos de usuario almacenados en la base de datos de Cosmos en el almacenamiento no volátil (unidades de estado sólido) se cifran de forma predeterminada; No hay ningún tooturn controles, activado o desactivado. El cifrado en reposo se implementa mediante una serie de tecnologías de seguridad, como sistemas seguros de almacenamiento de claves, redes cifradas y API criptográficas. Microsoft administra las claves de cifrado y se alternan según las directivas internas de Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Cifrado en reposo en Azure Data Lake Store

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) es un repositorio de toda la empresa de todos los tipos de datos recopilados en una definición formal de único lugar tooany anterior de requisitos o esquema. Almacén de Azure Data Lake admite "en de forma predeterminada," cifrado transparente de los datos en reposo, que se configura durante la creación de hello de la cuenta. De forma predeterminada, almacén de Data Lake administra las claves de hello en su nombre, pero tienes Hola opción toomanage a usted mismo.

Se utilizan tres tipos de claves en cifrar y descifrar datos: Hola clave de cifrado maestra (MEK), la clave de cifrado de datos (DEK) y la clave de cifrado de bloque (BEK). Hola MEK es tooencrypt usado hello DEK, que se almacena en medios persistentes, y hello BEK se deriva de bloque de datos de Hola y de saludo DEK. Si está administrando sus propias claves, puede girar hello MEK.

## <a name="encryption-of-data-in-transit"></a>Cifrado de datos en tránsito

Azure ofrece varios mecanismos para mantener la privacidad de los datos cuando se mueven desde una ubicación tooanother.

### <a name="tlsssl-encryption-in-azure"></a>Cifrado TLS/SSL en Azure

Microsoft usa hello [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) del protocolo tooprotect datos cuando se transmiten entre los clientes y servicios de nube de Hola. Centros de datos de Microsoft negocian una conexión TLS con sistemas de cliente que se conectan tooAzure servicios. TLS proporciona una autenticación sólida, privacidad de mensajes e integridad (lo que permite la detección de la manipulación, interceptación y falsificación de mensajes), interoperabilidad, flexibilidad de algoritmo y facilidad de implementación y uso.

[Confidencialidad directa total](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) protege las conexiones entre los sistemas cliente de los clientes y los servicios en la nube de Microsoft mediante claves únicas. Las conexiones también usan longitudes de clave de cifrado RSA de 2048 bits. Esta combinación hace difícil para un usuario toointercept y acceso a datos en tránsito.

### <a name="azure-storage-transactions"></a>Transacciones de Azure Storage

Cuando se interactúa con el almacenamiento de Azure a través del portal de Azure de hello, todas las transacciones tienen lugar a través de HTTPS. También puede utilizar Hola API de REST de almacenamiento a través de HTTPS toointeract con el almacenamiento de Azure. Puede aplicar uso Hola de HTTPS al llamar a objetos de tooaccess de las API de REST de hello en cuentas de almacenamiento al permitir la transferencia segura necesaria para la cuenta de almacenamiento de Hola.

Firmas de acceso compartido ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), que puede ser usado toodelegate tener acceso a objetos de almacenamiento de tooAzure, incluya una opción toospecify ese Hola solo puede usar el protocolo HTTPS al utilizar firmas de acceso compartido. Esto garantiza que cualquier usuario enviar vínculos con tokens SAS utilice protocolo adecuado Hola.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) tooaccess usa recursos compartidos de archivos de Azure admite el cifrado, y está disponible en Windows Server 2012 R2, Windows 8, Windows 8.1 y Windows 10, lo que permite el acceso entre regiones e incluso acceder en el escritorio de Hola.

Cifrado en el cliente cifra los datos de hello antes de que envíe tooAzure almacenamiento, por lo que se cifra cuando transmite a través de red Hola.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Cifrado de SMB a través de redes virtuales de Azure 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) en máquinas virtuales de Azure que ejecuta Windows Server 2012 y versiones posteriores de proporciona Hola datos de capacidad toomake transferencias seguro mediante el cifrado de datos en tránsito a través de redes virtuales de Azure, los ataques tooprotect contra manipulaciones y escuchas. Los administradores pueden habilitar el cifrado SMB para todo el servidor hello, o simplemente algunos recursos compartidos.

De forma predeterminada, una vez que se activa cifrado SMB para un recurso compartido o el servidor, solo los clientes SMB 3 se permiten recursos compartidos de tooaccess Hola cifrado.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Cifrado en tránsito en Azure Virtual Machines

Datos en tránsito a y desde, entre máquinas virtuales de Azure que ejecutan Windows se cifran en un número de formas, según la naturaleza de Hola de conexión de Hola.

### <a name="rdp-sessions"></a>Sesiones RDP

Puede conectarse e iniciar en tooan una máquina virtual de Azure con hello [protocolo de escritorio remoto](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) desde un equipo cliente de Windows o desde un equipo Mac con un cliente RDP instalado. Datos en tránsito a través de red de hello en las sesiones RDP se pueden proteger mediante TLS.

También puede usar Escritorio remoto tooconnect tooa VM de Linux en Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Proteger el acceso a las máquinas virtuales de tooLinux mediante SSH

Puede usar [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux máquinas virtuales ejecutan en Azure para la administración remota. SSH es un protocolo de conexión cifrada que permite inicios de sesión seguros sobre conexiones no seguras. Es el protocolo de conexión predeterminado de Hola para máquinas virtuales de Linux hospedadas en Azure. Mediante el uso de claves de SSH para la autenticación, se elimina la necesidad de Hola para contraseñas toolog en. SSH utiliza un par de claves públicas/privadas (cifrado simétrico) para la autenticación.

## <a name="azure-vpn-encryption"></a>Cifrado de VPN de Azure

Puede conectarse tooAzure a través de una red privada virtual que crea privacidad tooprotect Hola túnel seguro de datos de Hola que se envían a través de red de Hola.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[La puerta de enlace VPN Azure](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) puede ser usado toosend cifra el tráfico entre la red virtual y su ubicación local a través de una conexión pública, o toosend entre redes virtuales.

La VPN de sitio a sitio usa [IPsec](https://en.wikipedia.org/wiki/IPsec) para el cifrado de transporte. Azure VPN Gateway utiliza un conjunto de propuestas predeterminadas. Puede configurar una directiva personalizada de IPsec/IKE de toouse de puertas de enlace de VPN de Azure con determinados algoritmos criptográficos y ventajas claves, en lugar de Hola conjuntos de directivas predeterminado de Azure.

### <a name="point-to-site-vpn"></a>VPN de punto a sitio

Point-to-Site VPN que los equipos cliente individual acceso tooan red Virtual de Azure. [Hola protocolo de túnel de sockets seguros](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) es el túnel VPN de hello toocreate utilizado y puede atravesar firewalls (túnel Hola aparece como una conexión HTTPS). Puede usar su propio CA raíz de PKI interna para la conectividad de punto a sitio.

Puede configurar una red para el tooa virtual de point-to-site VPN conexión con hello portal de Azure con autenticación de certificados o PowerShell.

toolearn más información acerca de point-to-site VPN conexiones tooAzure de redes virtuales, consulte: [configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificación: portal de Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) y

[Configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>VPN de sitio a sitio 

Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2). Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa.

Puede configurar una red para el tooa virtual de sitio a sitio VPN conexión con hello portal de Azure, PowerShell o hello Azure interfaz de línea de comandos (CLI).

Lea esto para obtener más información:

[Crear una conexión de sitio a sitio en hello portal de Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Creación de una conexión de sitio a sitio](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Cifrado en tránsito en Azure Data Lake

Los datos en tránsito (también conocidos como datos en movimiento) también se cifran siempre en Data Lake Store. Por otra parte media toopersistent de tooencrypting datos toostoring anterior, Hola datos están protegidos también siempre a través de HTTPS en tránsito. HTTPS es Hola único protocolo admitido para hello que REST de almacén de datos Lake interfaces.

toolearn más información acerca del cifrado de datos en tránsito en Azure Data Lake, consulte documento Hola titulado [cifrado de datos de almacén de Azure Data Lake.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Administración de claves con Azure Key Vault

Sin protección adecuada y la administración de claves de hello, cifrado quedo inutilizable. Almacén de claves de Azure es la solución recomendada de Microsoft para administrar y controlar las claves de tooencryption de acceso que se usa servicios en la nube. Las claves de tooaccess de permisos pueden asignarse tooservices o toousers a través de cuentas de Azure Active Directory.

Almacén de claves de Azure libera a las empresas de hello necesidad tooconfigure, aplicar la revisión y mantener los módulos de seguridad de Hardware (HSM) y el software de administración de claves. Con el almacén de claves de Azure, Microsoft nunca ve las claves y las aplicaciones no tienen acceso directo toothem; mantener el control. También puede importar o generar claves en HSM.

## <a name="next-steps"></a>Pasos siguientes

- [Información general de seguridad de Azure](security-get-started-overview.md)
- [Azure Network Security Overview (Información general sobre Azure Network Security)](security-network-overview.md)
- [Introducción a la seguridad de base de datos de Azure](azure-database-security-overview.md)
- [Información general de seguridad de Azure Virtual Machines](security-virtual-machines-overview.md)
- [Cifrado de datos en reposo](azure-security-encryption-atrest.md)
- [Procedimientos recomendados de seguridad de datos y cifrado](azure-security-data-encryption-best-practices.md)
