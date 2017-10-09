---
title: conceptos de laboratorios de aaaDevTest | Documentos de Microsoft
description: "Obtenga información acerca de los conceptos básicos de Hola de laboratorios de desarrollo y pruebas y cómo puede que sea fácil toocreate, administrar y supervisar máquinas virtuales de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>Conceptos de DevTest Labs
## <a name="overview"></a>Información general
Hola lista siguiente contiene las definiciones y conceptos clave de laboratorios de desarrollo y pruebas:

## <a name="labs"></a>Laboratorios
Un laboratorio es la infraestructura de Hola que abarca el proceso de un grupo de recursos, como máquinas virtuales (VM), que permite una mejor administrar esos recursos especificando los límites y cuotas.

## <a name="virtual-machine"></a>Máquina virtual
Una máquina virtual de Azure es uno de los distintos tipos de [recursos informáticos a petición y escalables](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) que ofrece Azure. Dé de máquinas virtuales de Azure Hola flexibilidad de virtualización sin necesidad de toobuy y mantener el hardware físico de Hola que lo ejecuta, aunque todavía necesita toomaintain Hola VM mediante la realización de ciertas tareas, como configurar, aplicar revisiones e instalar software de Hola que se ejecuta en él.

[Información general sobre las máquinas virtuales Windows en Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) proporciona información sobre lo que se debe considerar antes de crear una máquina virtual, cómo crearla y cómo administrarla.

## <a name="claimable-vm"></a>Creación de máquinas virtuales reclamables
Una máquina virtual reclamable de Azure Claimable es una que está disponible para que pueda usarla cualquier usuario de laboratorio con permisos. Un administrador de laboratorio puede preparar las máquinas virtuales con los artefactos y las imágenes base específicas y guardarlas grupo tooa compartido. Un usuario de laboratorio, a continuación, puede solicitar una máquina virtual desde el grupo de hello en funcionamiento cuando necesiten uno con esa configuración concreta.

Una máquina virtual que está claimable no se asigna inicialmente tooany determinado usuario, pero se mostrará en la lista de todos los usuarios en "Máquinas virtuales Claimable". Después de una máquina virtual es reclamada por un usuario, es posible subir tootheir área de "Mis máquinas virtuales" y ya no está claimable por ningún otro usuario.

## <a name="environment"></a>Environment
En los laboratorios de desarrollo y pruebas, un entorno hace referencia tooa colección de recursos de Azure en un laboratorio. [Esta entrada de blog](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) explica cómo toocreate entornos de varias VM desde las plantillas de Azure Resource Manager.

## <a name="base-images"></a>Imágenes base
Las imágenes base son imágenes de máquina virtual con todas las herramientas de Hola y configuración preinstalado y configurado tooquickly crear una máquina virtual. Puede aprovisionar una máquina virtual seleccionando una base existente y agregar un artefacto tooinstall el agente de prueba. Puede, a continuación, guardar Hola aprovisionar máquinas virtuales como una base para que hello base se puede utilizar sin necesidad de agente de prueba de hello tooreinstall para cada aprovisionamiento de Hola máquina virtual.

## <a name="artifacts"></a>Artefactos
Artefactos son toodeploy usado y configurar la aplicación después de aprovisiona una máquina virtual. Los artefactos pueden ser:

* Herramientas que desea tooinstall en hello VM - como los agentes, Fiddler y Visual Studio.
* Acciones que desea toorun en hello VM - como la clonación de un repositorio.
* Aplicaciones que desea tootest.

Los artefactos son [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) archivos JSON que contienen la implementación de tooperform instrucciones y aplican la configuración.

## <a name="artifact-repositories"></a>Repositorios de artefacto
Los repositorios de artefactos son repositorios de Git donde se insertan los artefactos. Repositorios de artefacto pueden agregarse toomultiple laboratorios de su organización, lo cual permite reutilizar y compartir.

## <a name="formulas"></a>Fórmulas
Las fórmulas en las imágenes de toobase de adición, proporcionan un mecanismo para el aprovisionamiento rápido de máquina virtual. Una fórmula en los laboratorios de desarrollo y pruebas es una lista de toocreate utiliza los valores de propiedad predeterminado un laboratorio virtual.
Con las fórmulas, las máquinas virtuales con el mismo conjunto de propiedades, como la imagen base, tamaño de máquina virtual, red virtual y artefactos - de Hola se pueden crear sin necesidad de toospecify las propiedades de cada vez. Al crear una máquina virtual de una fórmula, los valores predeterminados de hello pueden usarse como-se o modifica.

## <a name="policies"></a>Directivas
Las directivas ayudan a controlar los costos en su laboratorio. Por ejemplo, puede crear un tooautomatically directiva apagar las máquinas virtuales según una programación definida.

## <a name="caps"></a>Límites
CAP es un desperdicio de toominimize mecanismo en el laboratorio. Por ejemplo, puede establecer un número de hello toorestrict cap de máquinas virtuales que se pueden crear por usuario, o en un laboratorio.

## <a name="security-levels"></a>Niveles de seguridad
La seguridad del acceso viene determinada por el Control de acceso basado en roles (RBAC) de Azure. toounderstand cómo tener acceso a works, ayuda a las diferencias de hello toounderstand entre un permiso, un rol y un ámbito tal como se define por RBAC.

* -Un permiso es una acción específica de tooa de acceso definida (máquinas virtuales de acceso de lectura, por ejemplo, tooall).
* Rol: un rol es un conjunto de permisos que se pueden agrupar y tooa usuario asignado. Por ejemplo, hello *propietario de la suscripción* rol tiene acceso a los recursos de tooall dentro de una suscripción.
* Ámbito: un ámbito es un nivel dentro de la jerarquía de Hola de un recurso de Azure, como un grupo de recursos, un único laboratorio o suscripción completa Hola.

En el ámbito de Hola de laboratorios de desarrollo y pruebas, hay dos tipos de permisos de usuario de roles toodefine: usuario de laboratorio y de propietario de laboratorio.

* Propietario de laboratorio: el propietario de un laboratorio tiene tooany acceder a los recursos de laboratorio Hola. Por lo tanto, un propietario de laboratorio puede modificar las directivas, leer y escribir todas las máquinas virtuales, cambiar la red virtual de hello y así sucesivamente.
* Usuario de laboratorio: un usuario de laboratorio puede ver todos los recursos de laboratorio, como máquinas virtuales, directivas y redes virtuales, pero no puede modificar las directivas ni las máquinas virtuales creadas por otros usuarios.

toosee cómo toocreate roles personalizados en los laboratorios de desarrollo y pruebas, consulte el artículo toohello, [conceder permisos de usuario en las directivas de laboratorio toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Puesto que los ámbitos son jerárquicos, cuando un usuario tiene permisos en un ámbito determinado, también se le conceden automáticamente en cada ámbito de nivel inferior que engloba. Por ejemplo, si se asigna a un usuario toohello rol de propietario de la suscripción, tienen acceso a los recursos del tooall en una suscripción, que incluyen todas las máquinas virtuales, todas las redes virtuales y todas las prácticas. Por lo tanto, un propietario de la suscripción hereda automáticamente el rol Hola del propietario de laboratorio. Sin embargo, no es cierto Hola opuesto. El propietario de un laboratorio tiene laboratorio tooa de acceso, que es un ámbito inferior al nivel de suscripción de Hola. Por lo tanto, el propietario de un laboratorio no será capaz de toosee las máquinas virtuales o redes virtuales o todos los recursos que se encuentran fuera del laboratorio de Hola.

## <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager
Todos Hola conceptos descritos en este artículo se pueden configurar mediante el uso de plantillas de Azure Resource Manager, que le permiten definen Hola/configuración de la infraestructura de la solución de Azure y lo implementación varias veces en un estado coherente.

[Comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) describe Hola estructura de un propiedades de hello y plantilla de Azure Resource Manager que están disponibles en las diferentes secciones de Hola de una plantilla.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Pasos siguientes
[Creación de un laboratorio en DevTest Labs](devtest-lab-create-lab.md)
