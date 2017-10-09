---
title: "entornos de prueba de aaaUse laboratorios de desarrollo y pruebas de Azure para máquinas virtuales y PaaS | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse laboratorios de desarrollo y pruebas de Azure para máquinas virtuales y PaaS probar escenarios de entorno."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>Usar Azure DevTest Labs para entornos de prueba de máquina virtual y PaaS

Puede usar muchos escenarios claves tooimplement de laboratorios de desarrollo y pruebas de Azure, pero un escenario principal implica el uso de máquinas de toohost de laboratorios de desarrollo y pruebas para los evaluadores. 

En este escenario, DevTest Labs ofrece estas ventajas:

- Evaluadores pueden probar la versión más reciente de Hola de su aplicación mediante el aprovisionamiento rápidamente entornos Windows y Linux mediante plantillas reutilizables y artefactos.
- Los evaluadores pueden escalar verticalmente la prueba de carga aprovisionando varios agentes de prueba.
- Los administradores pueden controlar los costos garantizando que:
  - Los evaluadores no puedan obtener más máquinas virtuales de las que necesitan.
  - Las máquinas virtuales se apaguen cuando no estén en uso.

![Uso de DevTest Labs para entrenamiento](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

En este artículo, obtenga información sobre distintos de los requisitos de evaluador laboratorios de desarrollo y pruebas de Azure características que se utilizan toomeet y Hola pasos detallados toofollow tooset un laboratorio.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Implementación de entornos de prueba con Azure DevTest Labs
1. **Cree el laboratorio de Hola** 
   
    Laboratorios son Hola punto inicial en los laboratorios de desarrollo y pruebas de Azure. Una vez que cree un laboratorio, puede realizar tareas como agregar laboratorio toohello de usuarios (evaluadores), los costos de toocontrol de directivas de configuración, definir imágenes de máquina virtual que pueden crear rápidamente y mucho más.  
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de un laboratorio con Laboratorios de desarrollo y pruebas de Azure](devtest-lab-create-lab.md) |Obtenga información acerca de cómo toocreate un laboratorio de prácticas de desarrollo y pruebas de Azure de Hola portal de Azure. |
2. **Creación de máquinas virtuales en cuestión de minutos mediante imágenes listas para usar de Marketplace e imágenes personalizadas** 
   
    Puede elegir imágenes prediseñadas desde una gran variedad de imágenes en hello Azure Marketplace y que estén disponibles en el laboratorio de Hola. Si imágenes prediseñadas hello no satisfacen sus necesidades, puede crear una imagen personalizada mediante la creación de un máquina virtual con una imagen listos para su uso desde hello guardar máquina virtual y Azure Marketplace, instalar todo el software de Hola que necesita, como una imagen personalizada en el laboratorio de Hola de laboratorio.

    Si va a utilizar imágenes personalizadas, considere el uso de un toocreate de fábrica de imagen y distribuir las imágenes. Un generador de imágenes es una solución de configuración como código que crea y distribuye periódicamente las imágenes configuradas de forma automática. Esta toomanually de tiempo necesario de hello guarda configurar sistema Hola una vez creada una máquina virtual con hello base OS.
  
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Configuración de imágenes de Azure Marketplace](devtest-lab-configure-marketplace-images.md) |Obtenga información acerca de cómo puede imágenes de Azure Marketplace de lista blanca, pasa a estar disponible para selección sólo hello las imágenes que desee para evaluadores Hola.|
   | [Creación de una imagen personalizada](devtest-lab-create-template.md) |Crear una imagen personalizada previamente instalando software de Hola que necesita para que los evaluadores pueden crear rápidamente una máquina virtual con una imagen personalizada hello.|
   | [Información acerca del generador de imágenes](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Vea un vídeo que describe cómo tooset una copia de seguridad y utilizar un generador de imágenes.|

3. **Creación de plantillas reutilizables para las máquinas de prueba** 
   
    Una fórmula de laboratorios de desarrollo y pruebas de Azure es que una lista de valores de propiedad predeterminados utiliza toocreate una máquina virtual. Puede crear una fórmula en el laboratorio de hello escogiendo una imagen, un tamaño de memoria virtual (una combinación de CPU y RAM) y una red virtual. Cada evaluador puede ver fórmula hello en el laboratorio de Hola y usarlo toocreate una máquina virtual. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Administrar las fórmulas de laboratorios de desarrollo y pruebas toocreate máquinas virtuales](devtest-lab-manage-formulas.md) |Aprenda cómo crear una fórmula en el laboratorio seleccionando una imagen, un tamaño de máquina virtual (una combinación de CPU y RAM) y una red virtual.|

3. **Crear entornos de prueba de varias máquinas virtuales** 
   
    Puede usar la infraestructura de Azure Resource Manager plantillas toodefine hello y la configuración de la solución de Azure e implementar repetidamente prueba varias máquinas virtuales en un estado coherente.

    Los recursos de PaaS de Azure se pueden aprovisionar en un entorno a partir de una plantilla de Resource Manager, de modo que aparezcan en el seguimiento de costos, Sin embargo, cierre automático de máquina virtual no aplica tooPaaS recursos.

    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de entornos de varias máquinas virtuales y recursos de PaaS con plantillas de Azure Resource Manager](devtest-lab-create-environment-from-arm.md) |Obtenga información sobre cómo puede implementar varias máquinas virtuales en un estado coherente para el entorno de prueba.|

4. **Crear artefactos tooenable flexible VM personalización**

   Artefactos son toodeploy usado y configurar la aplicación después de aprovisiona una máquina virtual. Los artefactos pueden ser:

   - Herramientas que desea tooinstall en hello VM - como los agentes, Fiddler y Visual Studio.
   - Acciones que desea toorun en hello VM - como la clonación de un repositorio.
   - Aplicaciones que desea tootest.

   Hay numerosos artefactos disponibles de serie. Puede crear sus propios artefactos personalizados si quiere obtener una mayor personalización para sus necesidades específicas.

   Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de artefactos personalizados para la máquina virtual de DevTest Labs](devtest-lab-artifact-author.md) |Cree sus propios artefactos personalizados para las máquinas virtuales de hello en el laboratorio.|
   | [Agregar un artefactos de Git repositorio toostore personalizados y plantillas del Administrador de recursos de Azure para su uso en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-add-artifact-repo.md) |Obtenga información acerca de cómo toostore los artefactos personalizados en su propio repositorio Git privado.|

5. **Control de los costos**
   
    Azure laboratorios de desarrollo y pruebas permite tooset una directiva de hello laboratorio toospecify Hola número máximo de máquinas virtuales que se pueden crear mediante un evaluador en laboratorio Hola. 
   
    Si el equipo de prueba tiene un conjunto de programación del trabajo y que desee toostop todas las máquinas virtuales de hello en un momento determinado del día de hello y, a continuación, automáticamente reiniciarlas Hola siguiente día, puede conseguirse fácilmente mediante directivas de apagado automático y el inicio automático de configuración en el laboratorio de Hola. 
   
    Por último, una vez completado el desarrollo de aplicaciones, puede eliminar todas las máquinas virtuales de Hola de a la vez mediante la ejecución de una única secuencia de comandos de PowerShell. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md) |Controlar los costos mediante el establecimiento de directivas en el laboratorio de Hola. |
   | [Eliminar el laboratorio de hello todas las máquinas virtuales con un script de PowerShell](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Eliminar todas las prácticas de hello en una sola operación cuando se completa la prueba.|

1. **Agregar un tooa de red virtual Lab** 
   
    DevTest Labs crea una red virtual (VNET) cada vez que se crea un laboratorio. Si ha configurado su propia red virtual, por ejemplo, mediante el uso de VPN de sitio a sitio o ExpressRoute: puede agregar configuración de red virtual de este laboratorio tooyour de red virtual para que esté disponible al crear máquinas virtuales.

    Además, hay un Azure Active Directory dominio combinación artefacto disponible que se une a un dominio de tooa VM cuando Hola máquina virtual se está creando. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Configuración de una red virtual en Azure DevTest Labs](devtest-lab-configure-vnet.md) |Obtenga información acerca de cómo tooconfigure una red virtual en los laboratorios de desarrollo y pruebas de Azure utilizando Hola portal de Azure.|

6. **Compartir laboratorio Hola con cada evaluador**
   
    Se puede obtener acceso directo a los laboratorios mediante un vínculo que puede compartir con los evaluadores. No incluso tienen toohave una cuenta de Azure, con tal de tienen un [cuenta de Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account). Los evaluadores no pueden ver las máquinas virtuales creadas por otros evaluadores.  
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Agregar un laboratorio de tooa evaluador en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-add-devtest-user.md) |Use hello tooadd portal Azure evaluadores tooyour laboratorio.|
   | [Agregar el laboratorio de toohello evaluadores mediante un script de PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Utilice tooautomate PowerShell agregar laboratorio tooyour de evaluadores. |
   | [Obtener un laboratorio de toohello de vínculo](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Aprenda cómo pueden los evaluadores obtener acceso directo a un laboratorio a través de un hipervínculo.|

7. **Automatización de la creación de un laboratorio para más equipos** 
   
    Puede automatizar la creación de laboratorio, incluida la configuración personalizada, crear una plantilla de administrador de recursos y utilizándolo laboratorios idénticos toocreate una y otra vez. 
   
    Más información, haga clic en vínculos de hello en hello en la tabla siguiente:
   
   | Tarea | Conocimientos que adquirirá |
   | --- | --- |
   | [Creación de un laboratorio mediante una plantilla de Resource Manager](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Cree laboratorios en Azure DevTest Labs mediante plantillas de Resource Manager. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

