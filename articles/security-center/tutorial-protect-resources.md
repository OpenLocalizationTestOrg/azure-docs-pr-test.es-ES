---
title: "Tutorial de Azure Security Center: protección de los recursos con Azure Security Center | Microsoft Docs"
description: "En este tutorial se muestra cómo configurar una directiva de acceso a VM Just-In-Time y una directiva de control de aplicaciones."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/08/2018
ms.author: terrylan
ms.openlocfilehash: f0a32f90e68101f805a52427fab2d5bb29b94939
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="tutorial-protect-your-resources-with-azure-security-center"></a>Tutorial: protección de los recursos con Azure Security Center
Security Center limita la exposición a amenazas mediante controles de acceso y aplicación para bloquear actividades malintencionadas. El acceso a máquinas virtuales (VM) Just-In-Time reduce la exposición a ataques mediante la posibilidad de denegar el acceso persistente a VM. En su lugar, se proporciona acceso controlado y auditado a VM solo cuando se necesita. Los controles de aplicación adaptables ayudan a proteger las VM frente a malware controlando qué aplicaciones se pueden ejecutar en dichas VM. Security Center usa el aprendizaje automático para analizar los procesos que se ejecutan en la máquina virtual y le ayuda a aplicar reglas de inclusión en listas de permitidos con esta inteligencia.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Configuración de una directiva de acceso a VM Just-In-Time
> * Configuración de una directiva de control de aplicación

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos
Para recorrer todas las características que se tratan en este tutorial, es preciso tener el plan de tarifa Estándar de Security Center. Dicho plan se puede probar de forma gratuita los primeros 60 días. En [Guía de inicio rápido de Azure Security Center](security-center-get-started.md) le explicamos cómo realizar la actualización al plan de tarifa Estándar.

## <a name="manage-vm-access"></a>Administración de acceso a VM
El acceso a VM Just-In-Time se puede usar para bloquear el tráfico entrante a las VM de Azure. Para ello, se reduce la exposición a ataques al mismo tiempo que se proporciona un acceso sencillo para conectarse a las VM cuando sea necesario.

El acceso a VM Just-In-Time se encuentra en versión preliminar.

No es necesario que los puertos de administración estén abiertos en todo momento. Solo deben estar abiertos mientras se está conectado a la máquina virtual, por ejemplo, para realizar tareas de administración o mantenimiento. Cuando se habilita Just-In-Time, Security Center usa las reglas del grupo de seguridad de red (NSG), que restringen el acceso a los puertos de administración para que no puedan ser objeto de ataques.

1. En el menú principal de Security Center, seleccione **Acceso a VM Just-In-Time** en **PROTECCIÓN EN LA NUBE AVANZADA**.

  ![Acceso a VM Just-In-Time][1]

  La hoja **Acceso a VM Just-In-Time** proporciona información sobre el estado de las máquinas virtuales:

  - **Configurado**: máquinas virtuales que se han configurado para admitir el acceso a máquina virtual Just-In-Time.
  - **Recomendado**: máquinas virtuales que pueden admitir el acceso a máquina virtual Just-In-Time pero que no se han configurado para ello.
  - **Ninguna recomendación**: una máquina virtual podría no recomendarse por diversas razones:

    - Falta el NSG: la solución Just-In-Time requiere que exista un NSG.
    - Máquina virtual clásica: en la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager.
    - Otros: se incluirá una máquina virtual en esta categoría si la solución Just-In-Time está desactivada en la directiva de seguridad de la suscripción o del grupo de recursos, o si la máquina virtual no tiene una IP pública y no existe un NSG.

2. Seleccione una VM recomendada y haga clic en **Enable JIT on 1 VM** (Habilitar JIT en 1 VM) para configurar una directiva Just-In-Time para esa VM:

  Puede guardar los puertos predeterminados que Security Center recomienda o puede agregar y configurar un puerto nuevo en el que desea habilitar la solución Just-In-Time. En este tutorial, vamos a agregar un puerto seleccionando **Agregar**.

  ![Adición de configuración de puerto][2]

3. En **Add port configuration** (Agregar configuración de puerto), se identifica:

  - El puerto
  - El tipo de protocolo
  - Las direcciones IP de origen permitidas (intervalos IP que pueden acceder una vez que se ha aprobado una solicitud)
  - El tiempo de solicitud máximo (el período de tiempo máximo durante el que puede estar abierto un puerto específico)

4. Seleccione **Aceptar** para guardar.

## <a name="harden-vms-against-malware"></a>Proteger VM frente a malware
Los controles de aplicación adaptables ayudan a definir un conjunto de aplicaciones que se pueden ejecutar en grupos de recursos configurados que, entre otras ventajas, le ayuda a proteger las VM frente a malware. Security Center usa el aprendizaje automático para analizar los procesos que se ejecutan en la máquina virtual y le ayuda a aplicar reglas de inclusión en listas de permitidos con esta inteligencia.

Los controles de aplicaciones adaptables se encuentran en versión preliminar. Esta característica solo está disponible para máquinas Windows.

1. Vuelva al menú principal de Security Center. En **PROTECCIÓN EN LA NUBE AVANZADA**, seleccione **Controles de aplicaciones adaptables**.

   ![Controles de aplicación adaptables][3]

  La sección **Grupos de recursos** contiene tres pestañas:

  - **Configurado**: lista de grupos de recursos con VM configuradas con control de aplicación.
  - **Recomendado**: lista de grupos de recursos para los que se recomienda el control de aplicación.
  - **No recommendation** (Ninguna recomendación): lista de grupos de recursos que contienen VM sin ninguna recomendación de control de aplicación. Por ejemplo, máquinas virtuales en las que las aplicaciones cambian constantemente y no han alcanzado un estado estable.

2. Seleccione la pestaña **Recomendado** para obtener una lista de grupos de recursos con las recomendaciones de control de aplicación.

  ![Recomendaciones de control de aplicación][4]

3. Seleccione un grupo de recursos para abrir la opción **Crear reglas de control de aplicaciones**. En **Seleccionar máquinas virtuales**, revise la lista de máquinas virtuales recomendadas y desactive cualquiera a la que no desee aplicar el control de aplicación. En **Seleccionar procesos para reglas de inclusión en lista blanca**, revise la lista de aplicaciones recomendadas y desactive aquellas a las que no desea que se apliquen. La lista incluye:

  - **NOMBRE**: la ruta de acceso completa de la aplicación
  - **PROCESOS**: el número de aplicaciones que residen dentro de cada ruta de acceso
  - **COMÚN**: "Sí" indica que estos procesos se han ejecutado en la mayoría de las máquinas virtuales de este grupo de recursos
  - **INFRINGIBLE**: un icono de advertencia indica si un atacante podría usar las aplicaciones para evitar las listas de aplicaciones permitidas. Se recomienda revisar estas aplicaciones antes de su aprobación.

4. Cuando haya terminado de realizar las selecciones, elija **Crear**.

## <a name="clean-up-resources"></a>Limpieza de recursos
Otras guías de inicio rápido y tutoriales de esta colección se basan en los valores de esta. Si planea continuar trabajando con las guías rápidas y tutoriales posteriores, debe seguir ejecutando el plan de tarifa Estándar y mantener el aprovisionamiento automático habilitado. Si no planea continuar o desea volver al nivel Gratis:

1. Vuelva al menú principal de Security Center y seleccione **Directiva de seguridad**.
2. Seleccione la suscripción o directiva que desea que vuelva al nivel Gratis. Se abre **Directiva de seguridad**.
3. En **COMPONENTES DE LA DIRECTIVAS**, seleccione **Plan de tarifa**.
4. Seleccione **Gratis** para cambiar la suscripción de Estándar a Gratis.
5. Seleccione **Guardar**.

Si desea deshabilitar el aprovisionamiento automático:

1. Vuelva al menú principal de Security Center y seleccione **Directiva de seguridad**.
2. Seleccione la suscripción en la que quiere deshabilitar el aprovisionamiento automático.
3. En **Directiva de seguridad: Colección de datos**, en **Incorporación**, seleccione **Desactivado** para deshabilitar el aprovisionamiento automático.
4. Seleccione **Guardar**.

>[!NOTE]
> La deshabilitación del aprovisionamiento automático no quita Microsoft Monitoring Agent de las máquinas virtuales de Azure en las que se ha aprovisionado el agente. La deshabilitación del aprovisionamiento automático limita la supervisión de seguridad de los recursos.
>

## <a name="next-steps"></a>pasos siguientes
En este tutorial, aprendió a limitar la exposición a amenazas mediante:

> [!div class="checklist"]
> * La configuración de un directiva de acceso a VM Just-In-Time para proporcionar acceso controlado y auditado a VM solo cuando se necesita
> * La configuración de una directiva de controles de aplicación adaptables para controlar qué aplicaciones se pueden ejecutar en las VM

Pase al siguiente tutorial para aprender a responder a incidentes relacionados con la seguridad.

> [!div class="nextstepaction"]
> [Tutorial: respuesta a incidentes relacionados con la seguridad](tutorial-security-incident.md)

<!--Image references-->
[1]: ./media/tutorial-protect-resources/just-in-time-vm-access.png
[2]: ./media/tutorial-protect-resources/add-port.png
[3]: ./media/tutorial-protect-resources/adaptive-application-control-options.png
[4]: ./media/tutorial-protect-resources/recommended-resource-groups.png
