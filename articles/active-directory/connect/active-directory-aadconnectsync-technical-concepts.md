---
title: "Sincronización de Azure AD Connect: conceptos técnicos | Microsoft Docs"
description: "Explica los conceptos técnicos de Hola de sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect Sync: conceptos técnicos
En este artículo es un resumen de tema de hello [descripción de la arquitectura](active-directory-aadconnectsync-technical-concepts.md).

Sincronización de Azure AD Connect se basa en una sólida plataforma de sincronización de metadirectorios.
Hola las secciones siguientes presentan los conceptos de Hola la sincronización de metadirectorios.
Basándose en MIIS, ILM y FIM, servicios de sincronización de Active Directory de hello Azure proporciona Hola siguiente plataforma para conectar los orígenes toodata, sincronizar datos entre orígenes de datos, así como Hola aprovisionar y desaprovisionar entidades.

![Conceptos técnicos](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Hola las secciones siguientes proporciona más detalles acerca de hello siguientes aspectos del servicio de sincronización de FIM de hello:

* Conector
* Flujo del atributo
* Espacio del conector
* Metaverso
* Aprovisionamiento

## <a name="connector"></a>Conector
los módulos de código de Hello que son utilizado toocommunicate con un directorio conectado se llaman conectores (anteriormente conocidos como agentes de administración (MAs)).

Están instalados en el equipo de Hola que se ejecuta la sincronización de Azure AD Connect. conectores de Hello proporcionan Hola capacidad sin agente tooconverse mediante protocolos del sistema remoto en lugar de confiar en la implementación de Hola de agentes especializados. Esto significa menor riesgo y el tiempo de implementación, especialmente al tratar con sistemas y aplicaciones críticas.

En la imagen anterior de hello, conector hello es sinónimo del espacio de conector de hello pero engloba todas las comunicaciones con el sistema externo de Hola.

Hello conector es responsable de todas las importación y exportación sistema toohello de funcionalidad y evita que los desarrolladores que necesitan toounderstand cómo tooconnect tooeach sistema forma nativa cuando se usa transformaciones de datos de toocustomize aprovisionamiento declarativo.

Importaciones y exportaciones solo se producen cuando programadas, lo que permite más aislamiento respecto a los cambios que se producen en el sistema de hello, ya que los cambios no propagan automáticamente toohello origen de datos conectado. Además, los desarrolladores pueden crear sus propios conectores para conectar toovirtually cualquier origen de datos.

## <a name="attribute-flow"></a>Flujo del atributo
Hola metaverso es la vista de hello consolidada de todas las identidades unidas de los espacios conectores colindantes. En la ilustración anterior de hello, se muestra el flujo de atributo mediante líneas con puntas de flecha para el flujo de entrada y salido. Flujo de atributo es el proceso de Hola de copiar o transformar datos desde un sistema tooanother y todos los atributos flujos (entrantes o salientes).

Flujo de atributo se produce entre el espacio del conector de Hola y Hola metaverso bidireccional cuando las operaciones de sincronización (completa o diferencial) están toorun programada.

El flujo de atributos solo se produce cuando se ejecutan estas sincronizaciones. Los flujos de atributos se definen en las reglas de sincronización. Puede tratarse de entrada (ISR en figura Hola anterior) o salida (OSR en figura Hola anterior).

## <a name="connected-system"></a>Sistema conectado
Sistema conectado (también conocido como directorio conectado) hace referencia a sistema remoto toohello Azure AD Connect sync ha conectado tooand lectura y escritura tooand de datos de identidad de.

## <a name="connector-space"></a>Espacio del conector
Cada origen de datos conectado se representa como un subconjunto filtrado de hello objetos y atributos en el espacio del conector de Hola.
Esto permite toooperate de servicio de sincronización de hello localmente sin sistema remoto de hello necesidad toocontact hello cuando sincroniza objetos de Hola y restringe la interacción tooimports y exportaciones.

Al origen de datos de Hola y el conector de hello tienen Hola capacidad tooprovide una lista de cambios (una importación diferencial), a continuación, Hola eficiencia operativa aumenta drásticamente como ciclo sólo los cambios desde el último sondeo de Hola se intercambia. espacio de conector de Hello aísla el origen de datos conectado Hola de cambios se propaguen automáticamente por requerir que dicha programación de conector de hello importa y exporta. Este seguro adicional le ofrece también tranquilidad durante la prueba, obtener una vista previa o bien al confirmar Hola siguiente actualización.

## <a name="metaverse"></a>Metaverso
Hola metaverso es la vista de hello consolidada de todas las identidades unidas de los espacios conectores colindantes.

Cuando las identidades se vinculan y la autoridad se asigna para varios atributos mediante asignaciones del flujo de importación, objeto de metaverso central Hola comienza tooaggregate información de varios sistemas. De este flujo de atributo de objeto, las asignaciones transportan los sistemas de toooutbound de información.

Los objetos se crean cuando un sistema autoritativo los proyecta en hello metaverso. En cuanto se quitan todas las conexiones, se elimina el objeto de metaverso Hola.

Objetos de metaverso de hello no pueden editarse directamente. Todos los datos Hola objeto deben aportarse mediante el flujo de atributo. Hola metaverso mantiene conectores persistentes con cada espacio de conector. Estos conectores no requieren una nueva evaluación en cada ejecución de la sincronización. Esto significa que sincronización de Azure AD Connect no tiene toolocate Hola coincidente remoto objeto cada vez. Esto evita la necesidad de Hola de utilizar agentes costosos tooprevent cambios tooattributes que normalmente serían responsables de correlacionar Hola objetos.

Cuando descubre nuevos orígenes de datos que pueden tener objetos preexistentes que habría toobe administrado, usos de la sincronización de Azure AD Connect un proceso denomina una combinación regla tooevaluate posibles candidatos con qué tooestablish vínculo.
Una vez que se ha establecido el vínculo de hello, esta evaluación no se vuelve a producir y puede producirse un flujo de atributo normal entre el origen de datos conectado remoto de Hola y Hola metaverso.

## <a name="provisioning"></a>Aprovisionamiento
Cuando un origen autoritativo proyecta un nuevo objeto en el metaverso de hello un nuevo objeto de espacio de conector puede crearse en otro conector que represente un origen de datos conectado de nivel inferior.

Esto establece intrínsecamente un vínculo y el flujo de atributos puede continuar de manera bidireccional.

Cuando una regla determine que un objeto de espacio conector nuevo necesita toobe creado, se habla de aprovisionamiento. Sin embargo, dado que esta operación solo tiene lugar en el espacio de conector de hello, lo no se mantienen en origen de datos conectado Hola hasta que se realiza una exportación.

## <a name="additional-resources"></a>Recursos adicionales
* [Sincronización de Azure AD Connect: personalización de las opciones de sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
