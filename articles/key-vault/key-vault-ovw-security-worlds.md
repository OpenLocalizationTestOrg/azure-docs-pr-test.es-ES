---
ms.assetid: 
title: "espacios de seguridad del almacén de claves de aaaAzure | Documentos de Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Espacios de seguridad y límites geográficos de Azure Key Vault

Azure Key Vault es un servicio multiinquilino y usa un grupo de módulos de seguridad de hardware (HSM) en cada ubicación de Azure. 

Todos los HSM en Azure ubicaciones de hello mismo recurso compartido de la región geográfica Hola mismo límite criptográfico (mundo de seguridad de Thales). Por ejemplo, UU y oeste de EE. UU. compartir Hola a todos de seguridad mismo porque pertenecen ubicación geográfica de toohello Estados Unidos. De forma similar, todas las ubicaciones de Azure en el recurso compartido de Japón Hola mundo de la misma seguridad y todas las ubicaciones de Azure en Australia, India y así sucesivamente. 

## <a name="backup-and-restore-behavior"></a>Tareas de copia de seguridad y restauración

Una copia de seguridad de una clave de un almacén de claves en una ubicación de Azure se pueden restaura tooa en otra ubicación de Azure, el almacén de claves, siempre que ambas condiciones son verdaderas:

- Ambos hello Azure ubicaciones pertenecen toohello misma ubicación geográfica
- Ambos almacenes de claves de hello pertenecen toohello misma suscripción de Azure

Por ejemplo, una copia de seguridad realizada por una suscripción determinada de una clave en un almacén de claves de la India occidental, solo puede ser restaurada tooanother el almacén de claves en hello misma suscripción y ubicación geográfica; India occidental, India Central o India sur.

## <a name="regions-and-products"></a>Productos y regiones

- [Regiones de Azure](https://azure.microsoft.com/regions/)
- [Productos de Microsoft por región](https://azure.microsoft.com/regions/services/)

Las regiones son mundos toosecurity asignado, se muestra como encabezados principales en tablas de hello:

En los productos de hello en el artículo de la región, por ejemplo, hello **Americas** ficha contiene este US, CENTRAL EE. UU., oeste de Estados Unidos todos los asignación toohello Americas región. 

>[!NOTE]
>Una excepción es que el Departamento de Defensa del este y del centro de Estados Unidos tienen sus propios ámbitos de seguridad. 

De forma similar, en hello **Europa** ficha, Europa del Norte y Europa occidental asignan toohello región de Europa. Hello mismo también es cierto en hello **Asia-Pacífico** ficha.



