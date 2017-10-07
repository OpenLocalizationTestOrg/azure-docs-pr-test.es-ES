---
title: "¿aaaWhat es el almacén de claves de Azure? | Microsoft Docs"
description: "El Almacén de claves de Azure ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Mediante el uso de Almacén de claves de Azure, los clientes pueden cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .PFX y contraseñas) a través de claves que están protegidas por módulos de seguridad de hardware (HSM)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>¿Qué es el Almacén de claves de Azure?
Almacén de claves de Azure está disponible en la mayoría de las regiones. Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introducción
El Almacén de claves de Azure ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Mediante el uso de Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .PFX y contraseñas) a través del uso de claves que están protegidas por módulos de seguridad de hardware (HSM). Para tener mayor seguridad, puede importar o generar las claves en HSM. Si elige toodo, procesos de Microsoft de las claves en FIPS 140-2 nivel 2 HSM validados (hardware y firmware).  

El almacén de claves agiliza el proceso de administración de claves de Hola y permite toomaintain control de claves que tienen acceso y cifrar los datos. Los programadores pueden crear claves para desarrollo y pruebas en minutos y, a continuación, perfectamente migrarlos tooproduction claves. Los administradores de seguridad pueden conceder (y revocar) tookeys de permiso, según sea necesario.

Hola de uso después de la tabla toobetter comprender cómo el almacén de claves puede ayudar a las necesidades de hello toomeet de los programadores y administradores de seguridad.

| Rol | Declaración del problema | Resuelto por Almacén de claves de Azure |
| --- | --- | --- |
| Desarrollador para una aplicación de Azure |"Deseo toowrite una aplicación de Azure que utiliza claves de firma y cifrado, pero deseo estos toobe claves externas de mi aplicación para que sea adecuada para una aplicación que se distribuye geográficamente solución Hola. <br/><br/>También quiero estos toobe claves y secretos protegido, sin necesidad de código de hello toowrite yo mismo. También desea estas claves y secretos toobe fácil para mí toouse en mis aplicaciones, con un rendimiento óptimo." |√ Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.<br/><br/> √ Las claves se protegen mediante Azure, para lo que se usan algoritmos estándar del sector, longitudes de clave y módulos de seguridad de hardware (HSM).<br/><br/> √ Claves se procesan en HSM que residen en hello mismos centros de datos de Azure como las aplicaciones de Hola. Esto proporciona una mayor confiabilidad y reducir la latencia de si las claves de hello residen en una ubicación independiente, como local. |
| Desarrollador para software como servicio (SaaS): |"No desea responsabilidad de responsabilidad o potencial de Hola para claves de inquilino de Mis clientes y secretos. <br/><br/>Desea Hola clientes tooown y administrar sus claves de modo que puedo concentrarse en hacer ¿qué hacer mejor, que proporciona características de software de hello principales". |√ Los clientes pueden importar sus propias claves a Azure y administrarlas. Cuando una aplicación de SaaS necesita operaciones criptográficas tooperform mediante claves de sus clientes, el almacén de claves realiza estas operaciones en nombre de la aplicación hello. aplicación Hello no ve las claves de los clientes de Hola. |
| Responsable principal de la seguridad (CSO) |"Las quiero tooknow que nuestras aplicaciones cumplen con FIPS 140-2 nivel 2 HSM para administración de claves segura. <br/><br/>Desea toomake seguro de que mi organización en el control del ciclo de vida de clave de Hola y puede supervisar el uso de claves. <br/><br/>Y aunque se usan varios servicios de Azure y recursos, deseo que las claves de hello toomanage desde una sola ubicación en Azure." |√ Los HSM tienen la validación FIPS 140-2 de nivel 2.<br/><br/>√ Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.<br/><br/>√ Registro del uso de claves casi en tiempo real.<br/><br/>Almacén de hello √ proporciona una única interfaz, independientemente de cuántos almacenes tiene en Azure, qué regiones soporte técnico y usarlos en las aplicaciones. |

Cualquiera con una suscripción a Azure puede crear y usar instancias de Key Vault. Aunque Key Vault beneficia a los desarrolladores y los administradores de seguridad, el administrador de una organización que administra otros servicios de Azure, podría implementarlo y administrarlo. Por ejemplo, este administrador podría iniciar sesión con una suscripción de Azure, cree un almacén para la organización de hello en qué claves toostore y, a continuación, ser responsable de las tareas operativas, como:

* Crear o importar una clave o un secreto
* Revocar o eliminar una clave o un secreto
* Autorizar a los usuarios o aplicaciones tooaccess Hola almacén de claves, por lo que, a continuación, pueden administrar o usar sus claves y secretos
* Configurar el uso de claves (por ejemplo, para firmar o cifrar)
* Supervisar el uso de claves

Este administrador, a continuación, se proporcionan a los programadores con URI toocall desde sus aplicaciones y proporcionar a su administrador de seguridad de información de registro de uso de claves. 

   ![Información general del Almacén de claves de Azure][1]

Los desarrolladores también pueden administrar las claves de hello directamente, mediante las API. Para obtener más información, consulte [Hola Guía del desarrollador de almacén de claves](key-vault-developers-guide.md).

## <a name="next-steps"></a>Pasos siguientes
Para consultar un tutorial de introducción para que un administrador, vea [Introducción al Almacén de claves de Azure](key-vault-get-started.md).

Para obtener más información acerca del registro de uso para el Almacén de claves, consulte [Registro del Almacén de claves de Azure](key-vault-logging.md).

Para más información acerca del uso de claves y secretos con Azure Key Vault, Consulte [About Keys, Secrets, and Certificates](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx) (Acerca de claves, secretos y certificados).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
