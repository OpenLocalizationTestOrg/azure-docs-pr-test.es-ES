---
title: "aaaOverview de seguridad en el almacén de Data Lake | Documentos de Microsoft"
description: "Descripción de cómo Azure Data Lake Store es un almacén de macrodatos más seguro"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Seguridad en el Almacén de Azure Data Lake
Muchas empresas están aprovechándose del análisis de grandes cantidades de datos de negocio visión toohelp que ellos realizar decisiones de smart. Es posible que una organización tenga un entorno regulado y complejo, con un número cada vez mayor de distintos tipos de usuarios. Es esencial para una toomake enterprise seguro de que los datos empresariales fundamentales se almacenan de forma más segura, con el nivel correcto de Hola de acceso concedido a los usuarios de tooindividual. Se ha diseñado el almacén de Azure Data Lake toohelp cumplir estos requisitos de seguridad. En este artículo, obtenga información acerca de las capacidades de seguridad de hello Lake del almacén de datos, incluidos:

* Autenticación
* Autorización
* Aislamiento de red
* Protección de datos
* Auditoría

## <a name="authentication-and-identity-management"></a>Autenticación y administración de identidades
La autenticación es proceso Hola por el que se comprueba una identidad de usuario cuando el usuario Hola interactúa con el almacén de Data Lake o con cualquier servicio que se conecta tooData Lake almacén. Para la autenticación y administración de identidades, utiliza el almacén de Data Lake [Azure Active Directory](../active-directory/active-directory-whatis.md), una completa identidad y acceso en la nube solución de administración que simplifica la administración de Hola de usuarios y grupos.

Cada una de las suscripciones de Azure puede asociarse a una instancia de Azure Active Directory. Solo los usuarios y las identidades de servicio que se definen en el servicio de Azure Active Directory pueden tener acceso a su cuenta de almacén de Data Lake mediante Hola portal de Azure, herramientas de línea de comandos, o a través de aplicaciones cliente de que su organización compilaciones con hello datos de Azure Almacén Lake SDK. Las principales ventajas del uso de Azure Active Directory como un mecanismo de control de acceso centralizado son:

* Administración simplificada del ciclo de vida de las identidades. identidad Hola de un usuario o un servicio (una identidad principal de servicio) se pueden crear rápidamente y se ha revocado rápidamente basta con eliminar o deshabilitar la cuenta de hello en el directorio de Hola.
* Multi-factor authentication. [Multi-factor authentication](../multi-factor-authentication/multi-factor-authentication.md) proporciona un nivel de seguridad adicional para los inicios de sesión y las transacciones del usuario.
* Autenticación desde cualquier cliente mediante un protocolo estándar abierto, como OAuth u OpenID.
* Federación con los servicios de directorio de empresa y los proveedores de identidades en la nube.

## <a name="authorization-and-access-control"></a>Control de autorización y acceso
Después de que Azure Active Directory autentica un usuario para que hello usuario puede tener acceso a almacén de Azure Data Lake, controles de autorización de permisos de acceso a almacén de Data Lake. Almacén de Data Lake separa autorización para actividades relacionadas con la cuenta y relacionadas con datos en hello siguiente manera:

* [Control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md) (RBAC) proporcionado por Azure para la administración de cuentas
* POSIX ACL para tener acceso a datos en el almacén de Hola

### <a name="rbac-for-account-management"></a>RBAC para la administración de cuentas
Se definen cuatro roles básicos para Data Lake Store de forma predeterminada. roles de Hello permiten diferentes operaciones en una cuenta de almacén de Data Lake a través de hello portal de Azure, cmdlets de PowerShell y las API de REST. Hola propietario y roles de colaborador pueden realizar una serie de funciones de administración en la cuenta de hello. Puede asignar toousers de rol de lector de Hola que sólo interactúan con los datos.

![Roles RBAC](./media/data-lake-store-security-overview/rbac-roles.png "Roles RBAC")

Tenga en cuenta que, aunque se asignan roles de administración de cuentas, algunos roles de afectar al acceso toodata. Necesita toouse ACL toocontrol acceso toooperations que un usuario puede realizar en el sistema de archivos de Hola. Hello en la tabla siguiente muestra un resumen de derechos de administración y derechos de acceso a datos Hola roles predeterminados.

| Roles | Derechos de administración | Derechos de acceso a datos | Explicación |
| --- | --- | --- | --- |
| Ningún rol asignado |None |Regido por ACL |usuario de Hello no puede utilizar hello Azure portal o Azure PowerShell cmdlets toobrowse almacén de Data Lake. usuario de Hello puede usar únicamente las herramientas de línea de comandos. |
| Propietario |Todo |Todo |rol de propietario de Hello es un superusuario. Este rol puede administrar todo el contenido y tiene acceso completo toodata. |
| Lector |Solo lectura |Regido por ACL |rol de lector de Hello puede ver todos los elementos relacionados con la administración de la cuenta, como qué usuario está asignado el rol de toowhich. rol de lector de Hello no puede realizar ningún cambio. |
| Colaborador |Todos, excepto agregar y quitar roles |Regido por ACL |rol de colaborador de Hello puede gestionar algunos aspectos de una cuenta, como las implementaciones y la creación y administración de alertas. rol de colaborador de Hello no se puede agregar o quitar roles. |
| Administrador de acceso de usuario |Agregar y quitar roles |Regido por ACL |rol de administrador de acceso de usuario de Hello puede administrar tooaccounts de acceso de usuario. |

Para obtener instrucciones, consulte [asignar usuarios o grupos de seguridad de las cuentas de almacén de tooData Lake](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Uso de ACL para operaciones en sistemas de archivos
Data Lake Store es un sistema de archivos jerárquico como el sistema de archivos distribuido de Hadoop (HDFS) que admite [POSIX ACL](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Controla la lectura (r), escritura (w) y ejecutar (tooresources de permisos para el rol de propietario de hello, para el grupo de propietarios de Hola y a otros usuarios y grupos x). Hola datos Lake almacén Public Preview (versión actual de hello), ACL pueden habilitarse en la carpeta raíz de hello, en las subcarpetas y en archivos individuales. Para más información sobre cómo funcionan las ACL en el contexto de Data Lake Store, consulte [Control de acceso en Data Lake Store](data-lake-store-access-control.md).

Se recomienda definir las ACL para varios usuarios mediante [grupos de seguridad](../active-directory/active-directory-accessmanagement-manage-groups.md). Agregar grupo de seguridad de los usuarios tooa y, a continuación, asignar las ACL de Hola para un grupo de seguridad de toothat de archivo o carpeta. Esto resulta útil cuando desea tener acceso personalizado tooprovide, porque tooadding limitado un máximo de nueve entradas de acceso personalizados. Para obtener más información sobre cómo toobetter proteger los datos almacenados en el almacén de Data Lake mediante el uso de grupos de seguridad de Azure Active Directory, vea [asignar usuarios o grupos de seguridad como las ACL toohello sistema de archivos de almacén de Azure Data Lake](data-lake-store-secure-data.md#filepermissions).

![Lista de accesos estándar y personalizados](./media/data-lake-store-security-overview/adl.acl.2.png "Lista de accesos estándar y personalizados")

## <a name="network-isolation"></a>Aislamiento de red
Almacenan datos de almacén de Data Lake de uso toohelp control access tooyour Hola a nivel de red. Puede establecer firewalls y definir un intervalo de direcciones IP para los clientes de confianza. Con un intervalo de direcciones IP, solo los clientes que tienen una dirección IP dentro del intervalo definido de hello pueden conectarse tooData Lake almacén.

![Configuración del firewall y acceso a IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Configuración del firewall y dirección IP")

## <a name="data-protection"></a>Protección de datos
Azure Data Lake Store protege los datos durante todo su ciclo de vida. Para los datos en tránsito, almacén de Data Lake usa datos de toosecure del protocolo de seguridad de capa de transporte (TLS) de hello estándar del sector a través de red de Hola.

![Cifrado en Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Cifrado en Data Lake Store")

Almacén de Data Lake también proporciona cifrado para los datos que se almacenan en la cuenta de hello. Puede optar toohave los datos cifrados u optar por sin cifrado. Si decide no participar en para el cifrado, los datos almacenados en el almacén de Data Lake están toostoring anterior cifrado en medios persistentes. En tal caso, almacén de Data Lake automáticamente cifra datos anteriores toopersisting y descifra datos tooretrieval anteriores, por lo que el cliente sea completamente transparente toohello acceso a los datos de Hola. No hay ningún cambio en el código necesario en los datos de tooencrypt/decrypt del lado de cliente de Hola.

Administración de claves, el almacén de Data Lake proporciona dos modos para administrar las claves de cifrado maestra (MEKs), que son necesarias para descifrar los datos que se almacenan en el almacén de Data Lake Hola. Se puede permitir que almacén de Data Lake administra hello MEKs por usted, o elija la propiedad tooretain de MEKs Hola con su cuenta de almacén de claves de Azure. Debe especificar el modo de saludo de administración de claves mientras al crear una cuenta de almacén de Data Lake. Para obtener más información sobre cómo configuración relacionada con el cifrado de tooprovide, consulte [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Registros de auditoría y diagnóstico
Puede usar los registros de auditoría o diagnóstico en función de si desea consultar registros de actividades relacionadas con la administración o con los datos.

* Las actividades relacionadas con la administración de usar las API del Administrador de recursos de Azure y aparecen en hello portal de Azure a través de los registros de auditoría.
* Las actividades relacionadas con datos usar API de REST de WebHDFS y aparecen en hello portal de Azure a través de los registros de diagnóstico.

### <a name="auditing-logs"></a>Registros de auditoría
toocomply con las normas, una organización puede requerir los seguimientos de auditoría adecuada si necesita toodig en determinados incidentes. Data Lake Store integra la auditoría y la supervisión y registra todas las actividades de administración de cuentas.

Para las auditorías de administración de cuenta, ver y elegir las columnas de Hola que desea toolog. También puede exportar los registros de auditoría tooAzure almacenamiento.

![Registros de auditoría](./media/data-lake-store-security-overview/audit-logs.png "Registros de auditoría")

### <a name="diagnostic-logs"></a>Registros de diagnóstico
Puede establecer los seguimientos de auditoría de acceso a datos en hello portal de Azure (en configuración de diagnóstico) y crear una cuenta de almacenamiento de blobs de Azure donde se almacenan los registros de Hola.

![Registros de diagnóstico](./media/data-lake-store-security-overview/diagnostic-logs.png "Registros de diagnóstico")

Después de configurar opciones de diagnóstico, puede ver registros de hello en hello **registros de diagnóstico** ficha.

Para más información sobre cómo trabajar con registros de diagnóstico con Azure Data Lake Store, consulte [Acceso a los registros de diagnóstico de Azure Data Lake](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Resumen
Los clientes empresariales exigen una plataforma de nube de análisis de datos que sea segura y fácil toouse. Se ha diseñado el almacén de Azure Data Lake toohelp cumplir los siguientes requisitos a través de administración de identidades y la autenticación a través de la integración de Azure Active Directory, autorización basada en ACL, el aislamiento de red, el cifrado de datos en tránsito y en reposo (que entran en hello futuras) y la auditoría.

Si desea que las nuevas características de toosee de almacén de Data Lake, envíenos sus comentarios en hello [foro de UserVoice de almacén de datos Lake](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Otras referencias
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Introducción a Data Lake Store](data-lake-store-get-started-portal.md)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)

