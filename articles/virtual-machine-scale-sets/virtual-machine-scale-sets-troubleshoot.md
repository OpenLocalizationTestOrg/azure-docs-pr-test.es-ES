---
title: "escalado automático aaaTroubleshoot con conjuntos de escalas de máquina Virtual | Documentos de Microsoft"
description: "Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales. Comprender los problemas típicos que se producen y cómo tooresolve ellos."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales
**Problema** : se ha creado una infraestructura de escalado automático en Azure Resource Manager mediante conjuntos de escalas de VM: por ejemplo mediante la implementación de una plantilla similar al siguiente: https://github.com/Azure/azure-quickstart-templates/tree/master/201- vmss-bottle-escalado automático: dispone de las reglas de escala definidas y funciona bien, salvo que independientemente de cuánta carga, se coloca en hello las máquinas virtuales, no lo hará de escalado automático.

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas
Algunas cosas tooconsider incluyen:

* ¿El número de núcleos tiene cada máquina virtual y se carga cada núcleo? plantilla de inicio rápido de Azure de ejemplo de Hola anterior tiene una secuencia de comandos do_work.php, que carga un único núcleo. Si está usando una máquina virtual supera el tamaño de máquina virtual a un único núcleo como Standard_A1 o D1, a continuación, se necesitaría toorun esta carga varias veces. Compruebe el número de núcleos de las máquinas virtuales después de consultar [Tamaños de las máquinas virtuales Windows en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* ¿Cuántas máquinas virtuales en hello conjunto de escalado de máquinas virtuales, está realizando trabajo en cada uno de ellos?
  
    Un evento de ampliación sólo llevará a cabo cuando Hola promedio de CPU a través de **todos los** hello las máquinas virtuales en un conjunto de escala supera Hola valor de umbral con el tiempo de hello interno definido en las reglas de escalado automático de Hola.
* ¿Falta cualquier evento de escalado?
  
    Compruebe los registros de auditoría de Hola Hola portal de Azure para eventos de escala. Tal vez se haya producido un escalado o una reducción vertical que se ha perdido. Puede filtrar por “Escala”...
  
    ![Registros de auditoría][audit]
* ¿Son los umbrales de reducción y escalado horizontal suficientemente diferentes?
  
    Imagine que establece una regla tooscale cuando la CPU promedio es mayor que 50% más de 5 minutos y tooscale en cuando la CPU promedio es inferior al 50%. Esto provocaría que un problema "aleteo" cuando el uso de CPU es umbral toothis cerrar, con acciones de escalado Hola constantemente aumentar y disminuir el tamaño del conjunto de Hola. Por este motivo, servicio de escalado automático de hello intenta tooprevent "oscilante", que puede presentarse como no escalar. Por lo tanto, asegúrese de que la escalabilidad y umbrales de escala son lo suficientemente diferente tooallow libere espacio entre el ajuste de escala.
* ¿Escribió su propia plantilla JSON?
  
    Es fácil toomake errores, por lo que empezar con una plantilla como Hola uno por encima del cual se pueda demostrar toowork y realizar pequeños cambios incrementales. 
* ¿Puede escalar o reducir horizontalmente de forma manual?
  
    Intente volver a implementar Hola recurso de conjunto de escala de máquinas virtuales con un número de "capacidad" diferente configuración toochange Hola de máquinas virtuales manualmente. Un toodo de plantilla de ejemplo se trata aquí: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing: puede que necesite tooedit Hola plantilla toomake seguro tiene Hola mismo tamaño de la máquina como el conjunto de escala está usando. Si correctamente puede cambiar manualmente número Hola de máquinas virtuales, a continuación, se sabe que el problema de hello está aislado tooautoscale.
* Compruebe su Microsoft.Compute/virtualMachineScaleSet y los recursos de Microsoft.Insights Hola [Explorador de recursos de Azure](https://resources.azure.com/)
  
    Se trata de un indispensables Hola a solucionar problemas de herramienta que se muestra el estado de los recursos de Azure Resource Manager. Haga clic en la suscripción y examine Hola está solucionando el grupo de recursos. En el proveedor de recursos de proceso de hello, examine Hola conjunto de escalado de máquina virtual que creó y compruebe Hola vista de instancia, que se muestra hello estado de una implementación. Compruebe también la vista de instancia de Hola Hola conjunto de escalado de máquinas virtuales de máquinas virtuales. A continuación, pasa a proveedor de recursos de hello Microsoft.Insights y comprobar las reglas de escalado automático de hello muestren correctamente.
* ¿Hola extensión diagnóstico trabajando y emitir los datos de rendimiento?
  
    **Update:** escalado automático de Azure ha sido mejorada toouse canalización métricas que ya no requiere un toobe de extensión de diagnósticos instalado basado en un host. Esto significa Hola de los próximos párrafos dejará de aplicarse si crea una aplicación de escalado automático mediante Hola nueva canalización. Un ejemplo de plantillas de Azure que hayan sido canalización de host de hello toouse convertido es: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Usar las métricas de basada en host para el escalado automático es mejor para hello siguientes motivos:
  
  * Menos partes móviles como ninguna extensión de diagnóstico deben toobe instalado.
  * Plantillas más sencillas. Basta con Agregar conjunto de escalado de existente de tooan de reglas de escalado automático de visión de plantilla.
  * Informes más confiable e inicio rápido de nuevas máquinas virtuales.
    
    Hello solo razones por las que debería tookeep mediante una extensión de diagnóstico sería si necesita memoria diagnóstico reporting/ajuste de escala. Las métricas basadas en host no informan sobre memoria.
    
    Con esto en mente, siga sólo rest Hola de este artículo si todavía está usando extensiones de diagnóstico para el escalado automático.
    
    Escalado automático en el Administrador de recursos de Azure puede funcionar (pero ya no tiene que) por medio de una extensión de máquina virtual denominada Hola extensión de diagnósticos. Emite la cuenta de almacenamiento de rendimiento datos tooa que se define en la plantilla de Hola. Servicio de Monitor de Azure de hello, a continuación, agrega estos datos.
    
    Si Hola servicio visión no puede leer datos de hello las máquinas virtuales, se supone que toosend un correo electrónico: por ejemplo, si las máquinas virtuales de hello estuvieran inactivos, de ser así, comprobar el correo electrónico (Hola especificada al crear la cuenta de Azure hello).
    
    También puede ir y buscar datos Hola. Mire Hola cuenta de almacenamiento de Azure mediante un explorador en la nube. Por ejemplo si se usa hello [Explorador de Visual Studio en la nube](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), inicie sesión y seleccionar Hola suscripción de Azure que está usando y Hola cuenta de almacenamiento de diagnóstico hacer referencia al nombre en hello definición de extensión de diagnósticos en la implementación plantilla...
    
    ![Cloud Explorer][explorer]
    
    Aquí verá una serie de tablas donde se está almacenando datos Hola de cada máquina virtual. Llevar a cabo Linux y métrica de CPU como un ejemplo de Hola, mire filas más recientes de Hola. Explorador de Hello Visual Studio en la nube es compatible con un lenguaje de consulta para que pueda ejecutar una consulta como "marca de tiempo gt datetime'2016-02-02T21:20:00Z'" toomake seguro de obtener eventos más recientes de hello (se supone tiempo está en hora UTC). ¿Datos de Hola que se ven en se corresponden toohello escalar reglas que configurar? En el ejemplo de Hola siguiente, Hola CPU para la máquina 20 inicia ininterrumpidamente too100% durante el saludo últimos 5 minutos...
    
    ![Tablas de almacenamiento][tables]
    
    Si los datos de hello no la encuentra, a continuación, implica problema hello es con la extensión de diagnóstico de hello ejecuta en máquinas virtuales de Hola. Si hay datos de hello, implica que hay un problema con las reglas de escala o con el servicio de visión Hola. Compruebe el [estado de Azure](https://azure.microsoft.com/status/).
    
    Una vez que ha estado a través de estos pasos, si sigue teniendo problemas de escalado automático puede intentar foros de hello [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), o [desbordamiento de pila](http://stackoverflow.com/questions/tagged/azure), o iniciar una llamada de soporte técnico. Ser plantilla de hello tooshare preparada y una vista de datos de rendimiento de saludo.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
