---
title: seguridad de Azure Security Center recomendaciones tooenhance aaaUse | Documentos de Microsoft
description: " Obtenga información acerca de cómo las directivas de seguridad toouse y las recomendaciones de Azure Security Center toohelp mitigar un ataque de seguridad. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Seguridad de tooenhance de recomendaciones de uso de Azure Security Center
Puede reducir las posibilidades de Hola de un evento de seguridad importantes configurando una directiva de seguridad y, a continuación, implementar las recomendaciones de hello proporcionadas por el centro de seguridad de Azure. Este artículo muestra cómo las directivas de seguridad toouse y las recomendaciones de centro de seguridad toohelp mitigar un ataque de seguridad.

> [!NOTE]
> En este artículo se basa en roles de Hola y los conceptos presentados en el centro de seguridad de hello [Guía de planeación y las operaciones de](security-center-planning-and-operations-guide.md). Es una guía de planificación de buena idea tooreview Hola antes de continuar.
>
>

## <a name="managing-security-recommendations"></a>Administración de recomendaciones de seguridad
Una directiva de seguridad define Hola conjunto de controles que se recomiendan para los recursos dentro de hello especificado suscripción o grupo de recursos. En el centro de seguridad, define directivas según los requisitos de seguridad de la compañía tooyour. más información, consulte toolearn [establecer directivas de seguridad en el centro de seguridad](security-center-policies.md).

Directivas de seguridad para grupos de recursos se heredan del nivel de suscripción de Hola.

![Herencia de directivas de seguridad][1]

Si necesita las directivas personalizadas en grupos de recursos específico, puede deshabilitar la herencia en el grupo de recursos de Hola. toodisable, establecer tooUnique de herencia en la hoja de directiva de seguridad de Hola y personalizar los controles de Hola que el centro de seguridad muestra recomendaciones para.

Por ejemplo, si tiene cargas de trabajo que no requieren la directiva de cifrado de datos transparente (TDE) de SQL base de datos de hello, desactiva la directiva de hello en nivel de suscripción de Hola y habilitar solo en los grupos de recursos de Hola donde se requiere SQL TDE.

> [!NOTE]
> Si hay un conflicto entre la directiva de nivel de suscripción y directiva de nivel de grupo de recursos, la directiva de nivel de grupo de recursos de hello tiene prioridad.
>
>

Centro de seguridad analiza el estado de seguridad de Hola de los recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, crea recomendaciones basadas en los controles de hello establecida en la directiva de seguridad de Hola. recomendaciones de Hello le guiará a través de proceso de Hola de configuración de controles de seguridad de Hola que sea necesitado.

Las recomendaciones de directiva actuales de Security Center se centran en las actualizaciones del sistema, la configuración del sistema operativo, los grupos de seguridad en subredes y máquinas virtuales, la auditoría de SQL Database, el TDE de Security Center, y los firewalls de aplicaciones web. Para la cobertura más actualizada de Hola de recomendaciones de centro de seguridad, consulte [administrar las recomendaciones de seguridad en el centro de seguridad](security-center-recommendations.md).

## <a name="scenario"></a>Escenario
Este escenario muestra cómo toouse centro de seguridad toohelp reducir posibilidades de Hola de un incidente de seguridad mediante la supervisión de las recomendaciones del centro de seguridad y llevar a cabo acción. Hello escenario utiliza la compañía ficticia hello, Contoso, y funciones que se presentan en Hola centro de seguridad [Guía de planeación y las operaciones de](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). los roles de Hello representan usuarios y equipos que pueden usar tareas relacionadas con la seguridad del centro de seguridad tooperform diferentes. Hola roles son:

![Roles de escenario][2]

Contoso había migrado recientemente algunos de su tooAzure de recursos locales. Contoso desea tooimplement y mantener protecciones que reducen su ataque de seguridad de tooa vulnerabilidad de sus recursos en nube Hola.

## <a name="recommended-solution"></a>Solución recomendada
Una solución es toouse tooprevent de centro de seguridad y detectar las vulnerabilidades de seguridad. Contoso tiene acceso tooSecurity Center a través de su suscripción de Azure. Hola [nivel gratuito](security-center-pricing.md) del centro de seguridad se habilita automáticamente en todas las suscripciones de Azure y recopilación de datos está habilitada en todas las máquinas virtuales en su suscripción.

David, del equipo de seguridad de TI de Contoso, configura una **directiva de seguridad** mediante Security Center. Centro de seguridad analiza el estado de seguridad de Hola de Contoso recursos de Azure. Cuando el centro de seguridad identifica posibles vulnerabilidades de seguridad, se crean **recomendaciones** basado en controles de hello establecida en la directiva de seguridad de Hola.

Juan, propietario de las cargas de trabajo en la nube, es el responsable de la implementación y el mantenimiento de las protecciones de acuerdo con las directivas de seguridad de Contoso. Juan puede supervisar las recomendaciones de hello creadas por protecciones de tooapply de centro de seguridad. recomendaciones de Hello guían a Jeff en proceso de Hola de configuración de controles de seguridad de Hola que sea necesitado.

En el criterio de Jeff tooimplement y mantienen protecciones y eliminar vulnerabilidades de seguridad, debe:

- Supervisar las recomendaciones de seguridad de Security Center
- Evaluar las recomendaciones de seguridad y decidir si deben aplicar o descartar
- Aplicar las recomendaciones de seguridad

Vamos a seguir toosee de pasos de Juan cómo utiliza tooguide de recomendaciones de centro de seguridad le en proceso de Hola de vulnerabilidades de seguridad de tooeliminate de controles de configuración.

## <a name="how-tooimplement-this-solution"></a>¿Cómo tooimplement esta solución
Juan inicia sesión demasiado[portal de Azure](https://azure.microsoft.com/features/azure-portal/) y abre Hola de la consola central de seguridad. Como parte de su diario actividades de supervisión, lo protege toosee si no hay recomendaciones de seguridad mediante la realización de hello pasos:

1. Juan selecciona hello **recomendaciones** icono tooopen hello **recomendaciones** hoja.
   ![Icono de recomendaciones de hello SELECT][3]
2. Juan revisa la lista Hola de recomendaciones. Ve que el centro de seguridad ha proporcionado lista Hola de recomendaciones en orden de prioridad, de prioridad toolowest de prioridad más alta. Decide tooaddress una recomendación de alta prioridad en la lista de Hola. Selecciona **instalar Endpoint Protection** en hello **recomendaciones** hoja.
3. Hola **instalar Endpoint Protection** hoja abrirá mostrando una lista de máquinas virtuales sin antimalware habilitado. Juan revisa la lista de Hola de máquinas virtuales, selecciona todas las máquinas virtuales y, a continuación, selecciona **instalar en máquinas 3 virtuales**.
   ![Instalar Endpoint Protection][4]
4. Hola **seleccione Endpoint Protection** hoja abre Jeff proporcionando con dos soluciones antimalware. Juan selecciona hello **Microsoft Antimalware** solución.
5. Se muestra información adicional sobre la solución antimalware de Hola. Juan selecciona **Crear**.
   ![Microsoft Antimalware][5]
6. Juan escribe Hola requerido configuración en hello **instalar** hoja y selecciona **Aceptar**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) está activo en hello selecciona las máquinas virtuales.

Juan sigue toomove a través de las principales prioridades de Hola y recomendaciones de prioridad Media, tomar decisiones sobre implementación. Juan hace referencia a hello [administrar las recomendaciones de seguridad](security-center-recommendations.md) artículo recomendaciones de hello toounderstand y lo que cada una de ellas hace si lo aplica.

Juan que aprende [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) realiza una supervisión de infraestructura y de red de Azure Hola seleccione seguridad y recibe las quejas de inteligencia y controlar el abuso de amenaza de terceros. Si Juan proporciona detalles de contacto de seguridad para la suscripción de Azure de Contoso, una entidad ilegal o no autorizada se ha accedido a los contactos de Microsoft Contoso si Hola MSRC detecta los datos del cliente de que Contoso. Vamos a seguir Juan como la aplica hello **proporcionar detalles de contacto de seguridad** recomendación (una recomendación con una gravedad Media en lista de Hola de recomendaciones anteriores).

1. Juan selecciona **proporcionar detalles de contacto de seguridad** en hello **recomendaciones** hoja, que abre hello **proporcionar detalles de contacto de seguridad** hoja.
2. Juan selecciona información de contacto de tooprovide de suscripción de Azure de hello en. Se abre una segunda hoja **Proporcionar datos de los contactos de seguridad** .
   ![Datos de los contactos de seguridad][6]
3. En hello segundo **proporcionar detalles de contacto de seguridad** hoja, Juan entra en:

  - direcciones de correo electrónico de contacto de seguridad Hola separadas por comas (no hay un toohello limitar el número de direcciones de correo electrónico puede escribir)
  - Un número de teléfono de contacto de seguridad

4. Juan vuelve a activar la opción de Hola **Enviarme correos electrónicos sobre alertas** tooreceive mensajes de correo electrónico acerca de las alertas de gravedad alta.
5. Juan selecciona **Aceptar** seguridad de hello tooapply póngase en contacto con suscripción de tooContoso de información.

Por último, Juan revisa la recomendación de baja prioridad hello **vulnerabilidades de sistema operativo corregir** y determina que esta recomendación no es aplicable. Quiere que la recomendación de hello toodismiss. Juan selecciona puntos Hola tres que aparecen toohello derecha y, a continuación, selecciona **descartar**.
   ![Descartar recomendación][7]

## <a name="conclusion"></a>Conclusión
Supervisar las recomendaciones de Security Center puede ayudarlo a eliminar vulnerabilidades de seguridad antes de que se produzca un ataque. Puede evitar que ocurra un incidente de seguridad implementando y manteniendo protecciones con las directivas de seguridad de Security Center.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
