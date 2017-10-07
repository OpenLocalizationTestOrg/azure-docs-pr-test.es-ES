---
title: "Introducción de almacén de claves de pila aaaAzure | Documentos de Microsoft"
description: "Aprenda cómo el almacén de claves de Azure Stack administra claves y secretos"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a>Introducción tooKey almacén en la pila de Azure

## <a name="before-you-start"></a>Antes de comenzar
En este artículo se da por supuesto siguiente hello:

* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.  
* Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.  
* [PowerShell está configurado para su uso con Azure Stack](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a>Conceptos básicos de Key Vault
Key Vault en Azure Stack ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Con Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .pfx y contraseñas).

El almacén de claves agiliza el proceso de administración de claves de Hola y permite toomaintain control de claves que tienen acceso y cifrar los datos. Los programadores pueden crear claves para desarrollo y pruebas en minutos y, a continuación, perfectamente migrarlos tooproduction claves. Los administradores de seguridad pueden conceder (y revocar) tookeys de permiso, según sea necesario.

Cualquiera que tenga una suscripción a Azure Stack puede crear y usar los almacenes de claves. Aunque el almacén de claves se beneficia a los desarrolladores y administradores de seguridad, pueden implementarse y administrado por el Administrador de la nube de Hola que administra otros servicios de la pila de Azure para una organización. Por ejemplo, Administrador de la nube de hello puede iniciar sesión con una suscripción de la pila de Azure, cree un almacén para la organización de hello en qué claves toostore y, a continuación, ser responsable de estas tareas operativas:

* Crear o importar una clave o un secreto
* Revocar o eliminar una clave o un secreto
* Autorizar a los usuarios o aplicaciones tooaccess Hola almacén de claves, por lo que, a continuación, pueden administrar o usar sus claves y secretos
* Configurar el uso de claves (por ejemplo, para firmar o cifrar)

Administrador de la nube de Hello, a continuación, puede ofrecer a los desarrolladores con URI toocall desde sus aplicaciones y proporcionar un administrador de seguridad con la información del registro de uso de claves.

Los desarrolladores también pueden administrar las claves de hello directamente, mediante las API. Para obtener más información, consulte la Guía del desarrollador del almacén de claves de Hola.

## <a name="scenarios"></a>Escenarios
Hello tabla siguiente detallan algunos de los escenarios de hello en el almacén de claves puede ayudar a satisfacer las necesidades de Hola de desarrolladores y administradores de seguridad:

### <a name="developer-for-an-azure-stack-application"></a>Desarrollador para una aplicación de Azure Stack
**Problema**: deseo toowrite una aplicación para la pila de Azure que utiliza claves de firma y cifrado, pero desea que estos toobe externo de mi aplicación para que sea adecuada para una aplicación que se distribuye geográficamente solución Hola.

**Instrucción**: Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.

### <a name="developer-for-software-as-a-service-saas"></a>Desarrollador para software como servicio (SaaS)
**Problema:** no deseo responsabilidad de responsabilidad o potencial de hello Mi cliente las claves y secretos.

**Instrucción**: Los clientes pueden importar sus propias claves a Azure Stack y administrarlas. Desea tooown de los clientes y administrar sus claves de modo que puedo concentrarse en hacer ¿qué hacer mejor, que proporciona características de software de hello principales.

### <a name="chief-security-officer-cso"></a>Responsable principal de la seguridad (CSO)
**Problema:** desea toomake seguro de que mi organización en el control del ciclo de vida de clave de Hola y puede supervisar el uso de claves.

**Instrucción**: Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.  Cuando una aplicación necesita operaciones criptográficas tooperform mediante el uso de claves de los clientes, el almacén de claves se consigue en nombre de la aplicación hello. aplicación Hello no ve las claves de los clientes de Hola.  Aunque se usan varios servicios de la pila de Azure y recursos, deseo que las claves de hello toomanage desde una sola ubicación en la pila de Azure. almacén de Hello proporciona una única interfaz, independientemente de cuántos almacenes tiene en pila de Azure, qué regiones soporte técnico y usarlos en las aplicaciones.

## <a name="next-steps"></a>Pasos siguientes

* [Administrar el almacén de claves en la pila de Azure mediante el portal de Hola](azure-stack-kv-manage-portal.md)  
* [Administrar Key Vault en Azure Stack mediante PowerShell](azure-stack-kv-manage-powershell.md)
