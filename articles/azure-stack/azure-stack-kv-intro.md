---
title: "Introducción al almacén de claves de Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: dc8b5cb299da74c88aa5ae82636dc345ddd45a2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a>Introducción a Key Vault en Azure Stack

## <a name="before-you-start"></a>Antes de comenzar
En este artículo se da por hecho lo siguiente:

* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves.  
* Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault.  
* [PowerShell está configurado para su uso con Azure Stack](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a>Conceptos básicos de Key Vault
Key Vault en Azure Stack ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Con Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .pfx y contraseñas).

Almacén de claves agiliza el proceso de administración de claves y le permite mantener el control de claves que obtienen acceso a sus datos y los cifran. Los desarrolladores pueden crear claves para desarrollo y prueba en minutos y, a continuación, migrarlas sin problemas a claves de producción. Los administradores de seguridad pueden conceder (y revocar) permisos a las claves según sea necesario.

Cualquiera que tenga una suscripción a Azure Stack puede crear y usar los almacenes de claves. Aunque el almacén de claves se beneficia a los desarrolladores y administradores de seguridad, pueden implementarse y administrado por el Administrador de la nube que administra otros servicios de la pila de Azure para una organización. Por ejemplo, el Administrador de la nube puede iniciar sesión con una suscripción de la pila de Azure, cree un almacén para la organización en la que se va a almacenar las claves y, a continuación, ser responsable de estas tareas operativas:

* Crear o importar una clave o un secreto
* Revocar o eliminar una clave o un secreto
* Autorizar usuarios o aplicaciones para acceder al almacén de claves para que puedan administrar o usar sus claves y secretos
* Configurar el uso de claves (por ejemplo, para firmar o cifrar)

El Administrador de la nube, a continuación, puede proporcionar a los programadores con identificadores URI para llamar desde sus aplicaciones y proporcionar un administrador de seguridad con la información del registro de uso de la clave.

Los desarrolladores también pueden administrar las claves directamente mediante API. Para más información, consulte la guía para desarrolladores de Key Vault.

## <a name="scenarios"></a>Escenarios
La tabla siguiente muestra algunos de los escenarios en los que Key Vault puede ayudar a satisfacer las necesidades de los desarrolladores y de los administradores de seguridad:

### <a name="developer-for-an-azure-stack-application"></a>Desarrollador para una aplicación de Azure Stack
**Problema**: Quiero escribir una aplicación para Azure Stack que use claves para la firma y el cifrado, pero quiero que dichas claves no estén en la propia aplicación, con el fin de que la solución sea adecuada para una aplicación que se distribuya geográficamente.

**Instrucción**: Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.

### <a name="developer-for-software-as-a-service-saas"></a>Desarrollador para software como servicio (SaaS)
**Problema**: No quiero asumir la responsabilidad, ni tampoco la posible responsabilidad legal, de las claves y los secretos de mis clientes.

**Instrucción**: Los clientes pueden importar sus propias claves a Azure Stack y administrarlas. Quiero que los clientes sean propietarios y administren sus claves de modo que pueda concentrarme en mi trabajo, que es proporcionar las características de software principales.

### <a name="chief-security-officer-cso"></a>Responsable principal de la seguridad (CSO)
**Problema**: Deseo asegurarme de que mi organización tiene el control del ciclo de vida de las claves y puedo supervisar el uso de las mismas.

**Instrucción**: Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.  Cuando una aplicación necesita realizar operaciones criptográficas utilizando las claves de los clientes, Key Vault lo hace en nombre de la aplicación. La aplicación no ve las claves de los clientes.  Aunque usamos varios servicios y recursos de Azure Stack, quiero administrar las claves desde una ubicación única en Azure Stack. El almacén proporciona una sola interfaz, independientemente del número de almacenes que tenga en Azure Stack, las regiones que admitan y las aplicaciones que los usen.

## <a name="next-steps"></a>Pasos siguientes

* [Administrar Key Vault en Azure Stack mediante el portal](azure-stack-kv-manage-portal.md)  
* [Administrar Key Vault en Azure Stack mediante PowerShell](azure-stack-kv-manage-powershell.md)
