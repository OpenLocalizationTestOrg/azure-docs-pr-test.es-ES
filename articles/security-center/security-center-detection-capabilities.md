---
title: capacidades de aaaDetection en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento le ayuda a toounderstand cómo funcionan las capacidades de detección de centro de seguridad de Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Funcionalidades de detección de Azure Security Center
Este documento describen las capacidades de detección avanzada del centro de seguridad de Azure, que ayuda a identificar amenazas activas que se dirige a los recursos de Microsoft Azure y se proporcionan que con visión Hola había toorespond rápidamente.

> [!NOTE]
> Detecciones avanzadas están disponibles en hello nivel estándar de centro de seguridad de Azure. Hay disponible una versión de evaluación gratuita de 60 días. Puede actualizar desde la selección de nivel de precios en Hola Hola [directiva de seguridad](security-center-policies.md). Visite [página del centro de seguridad](https://azure.microsoft.com/pricing/details/security-center/) toolearn más sobre los precios. 
> 
> 

## <a name="responding-tootodays-threats"></a>Responder a amenazas de tootoday
Ha habido cambios significativos en el panorama de amenazas de hello sobre hello en los últimos 20 años. Hola anteriores, las empresas normalmente solo tenían tooworry acerca de la destrucción del sitio web por los atacantes individuales que principalmente se pretendía ver "lo que podían hacer". Hoy en día, los atacantes son mucho más sofisticados y están más organizados. Normalmente, se mueven por un fin económico o estratégico. También tienen más recursos toothem disponibles, tal y como puede financió por Estados de la nación o crime organizado.

Este enfoque ha suscitado un nivel sin precedentes de tooan de profesionalidad en hello atacante rangos. Ya no les interesa alterar los sitios web. Únicamente son ahora está interesado en robar información, cuentas financieras y datos privados: todos los cuales puede usar toogenerate efectivo en hello open market o tooleverage un empresarial determinado, la posición política o militar. Incluso más relativas a que los atacantes con un objetivo de financiero son los atacantes de Hola que incumplen las personas y redes toodo daños tooinfrastructure.

En respuesta, las organizaciones a menudo implementación varias soluciones de punto, que se centran en defensa perimetral de empresa de Hola o puntos de conexión mediante la búsqueda de firmas de ataques conocidos. Estas soluciones suelen toogenerate un gran volumen de alertas de fidelidad baja, que requieren un tootriage de analistas de seguridad e investigar. Mayoría de las organizaciones no tienen tiempo de Hola y experiencia necesarios toorespond toothese alertas: por lo que muchas vaya sin destinatario.  Mientras tanto, los atacantes han evolucionado a su métodos toosubvert muchas defensas basadas en la firma y [adaptar entornos toocloud](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Nuevos enfoques son necesario toomore rápidamente identificar nuevas amenazas y acelerar la detección y respuesta. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Cómo Azure Security Center detecta y responde toothreats
Los investigadores de seguridad de Microsoft están constantemente en lookout hello en busca de amenazas. Tienen acceso tooan amplio conjunto de telemetría adquirida de la presencia global de Microsoft en la nube de Hola y local. Esta colección de gran alcance y distintas de conjuntos de datos permite que Microsoft toodiscover nuevos ataques patrones y tendencias en sus productos locales de consumidor y empresa, así como a sus servicios en línea. Como resultado, Security Center es capaz de actualizar rápidamente los algoritmos de detección a medida que los atacantes idean nuevas y más sofisticadas vulnerabilidades de seguridad. Este enfoque le ayuda a mantenerse al día en entornos llenos de amenazas que cambian continuamente. 

Detección de amenazas de centro de seguridad funciona mediante la recopilación automáticamente información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados. Analiza esta información, a menudo correlacionar información procedente de varios orígenes, tooidentify amenazas. En el centro de seguridad se priorizan las alertas de seguridad junto con recomendaciones sobre cómo tooremediate Hola amenaza.

![Recopilación y presentación de datos de Security Center](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Security Center utiliza análisis avanzados que superan con creces los enfoques basados en firmas. Avances en grandes cantidades de datos y [aprendizaje automático](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologías son tooevaluate aprovechado eventos a través de tejido de nube todo hello: detectar amenazas que serían imposible tooidentify usar métodos manuales y predecir Hola evolución de los ataques. Estas técnicas de análisis son: 

* **Integra inteligencia sobre amenazas**: parece para conocidos actores no válidos mediante el aprovechamiento de inteligencia de amenazas mundiales de productos y servicios, Microsoft Hola Microsoft Digital crímenes unidad (DCU), Hola Microsoft Security Response Center (MSRC) y external fuentes de distribución.
* **Análisis de comportamiento**: se aplica un comportamiento malintencionado toodiscover patrones conocidos. 
* **Detección de anomalías**: utiliza estadística de generación de perfiles toobuild una línea de base histórica. Le avisa sobre desviaciones respecto a las líneas de base establecidas que se ajustan tooa vector de ataque potencial.

### <a name="threat-intelligence"></a>Información sobre amenazas
Microsoft dispone de una ingente cantidad de información sobre amenazas globales. Telemetría flujos en desde varios orígenes, como Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, Hola unidad de crímenes digitales (DCU) de Microsoft y Microsoft Security Response Center (MSRC). Los investigadores de recibirán información de inteligencia de amenazas que se comparte entre los proveedores de servicios de nube principales y se suscribe toothreat intelligence fuentes de terceros. Centro de seguridad de Azure puede usar este tooalert de información que toothreats de conocidos actores no válidos. Estos son algunos ejemplos:

* **Dirección IP malintencionada de comunicación de salida tooa**: tooa el tráfico saliente sabe botnet o darknet probablemente indica que el recurso está en peligro y que un atacante intenta tooexecute de comandos en los datos exfiltrate o del sistema. Centro de seguridad de Azure compara la base de datos de amenaza global del tooMicrosoft del tráfico de red y le avisa si detecta dirección IP de comunicación tooa malintencionada.

## <a name="behavioral-analytics"></a>Análisis del comportamiento
Análisis de comportamiento es una técnica que analiza y compara la recopilación de datos de tooa de patrones conocidos. No obstante, estos patrones no son simples firmas, Están determinados a través de algoritmos de aprendizaje de máquina complejas que son conjuntos de datos de toomassive aplicado. También se determinan por medio de un análisis cuidadoso, llevado a cabo por analistas expertos, de los comportamientos malintencionados. Centro de seguridad de Azure puede usar recursos de tooidentify en peligro de análisis de comportamiento basados en el análisis de registros de la máquina virtual, registros de dispositivo de red virtual, registros de tejido, volcados de memoria y otros orígenes. 

Además, hay una correlación con los otro toocheck de señales para admitir la evidencia de una campaña generalizada. Esta correlación ayuda tooidentify eventos que son coherentes con los establecidos indicadores de riesgo. Estos son algunos ejemplos:

* **Ejecución de procesos sospechosos**: los atacantes emplean varias software malintencionado en tooexecute de técnicas sin que se detecte. Por ejemplo, un atacante podría dar malware Hola mismos nombres que los archivos del sistema legítimo pero coloque estos archivos en una ubicación alternativa, utilice un nombre que es muy similar archivo supone un riesgo de tooa o extensión real del archivo de máscara Hola. Monitores y los comportamientos de los procesos de modelos de centro de seguridad procesan a valores atípicos de toodetect ejecuciones como los siguientes.  
* **Oculta los intentos de malware y explotación**: malware sofisticado es capaz de tooevade antimalware tradicional productos nunca escribir toodisk o cifrar los componentes de software que se almacenan en el disco.  Sin embargo, dicho código mal intencionado se puede detectar mediante análisis de memoria, Hola malware debe dejar los seguimientos en memoria, en orden toofunction. Cuando se bloquea el software, un volcado de memoria captura una parte de la memoria en tiempo de Hola de fallo de Hola.  Mediante el análisis de memoria de hello en el volcado de memoria hello, Azure Security Center puede detectar técnicas empleadas tooexploit vulnerabilidades de software, obtener acceso a datos confidenciales y conservar escondidas con de una máquina en peligro sin afectar al rendimiento de Hola de su equipo.
* **Lateral movimiento y reconocimiento interno**: toopersist en un datos valiosos en peligro de red y busque/cosecha, los atacantes a menudo tratar toomove lateralmente de hello en peligro tooothers máquina dentro de Hola la misma red. Centro de seguridad supervisa el proceso y las actividades de inicio de sesión en orden toodiscover intenta tooexpand establecerse de un atacante dentro de la red de hello, como comando remoto sondeos de red de ejecución y la enumeración de cuentas.
* **Los Scripts de PowerShell malintencionados**: PowerShell está siendo utilizado por código malintencionado de los atacantes tooexecute en máquinas virtuales de destino para una variedad de propósitos. Security Center analiza la actividad de PowerShell en busca de evidencias de actividad sospechosa. 
* **Ataques de salida**: los atacantes a menudo los recursos de nube con el objetivo de hello del uso de dichos ataques adicionales de toomount de recursos de destino. En peligro las máquinas virtuales, por ejemplo, podría ser usado toolaunch ataques de fuerza bruta con otras máquinas virtuales, enviar SPAM o examinar puertos abiertos y otros dispositivos de Hola a internet. Aplicando máquina toonetwork tráfico de aprendizaje, el centro de seguridad puede detectar cuándo las comunicaciones de red saliente superan norm Hola. En caso de hello de correo no deseado, el centro de seguridad también correlaciona tráfico inusual de correo electrónico con inteligencia de Office 365 toodetermine si es probable que correo electrónico de hello malintencionadas u Hola resultado de una campaña de correo electrónico legítima.  

### <a name="anomaly-detection"></a>Detección de anomalías
Centro de seguridad de Azure también utiliza las amenazas de tooidentify de detección de anomalías. En análisis de toobehavioral de contraste (que depende de patrones conocidos que se deriva de grandes conjuntos de datos), detección de anomalías más "personalizada" y se centra en las líneas de base que son implementaciones de tooyour específico. Aprendizaje automático es toodetermine aplicada la actividad normal para las implementaciones y, a continuación, las reglas son las condiciones de valores atípicos de toodefine generado que pudieron representar un evento de seguridad. Veamos un ejemplo:

* **Ataques por fuerza bruta de RDP/SSH entrantes**: es posible que las implementaciones integren máquinas virtuales con mucha actividad que tengan multitud de inicios de sesión al día y otras máquinas virtuales que tengan pocos o ningún inicio de sesión. Centro de seguridad de Azure puede determinar la actividad de inicio de sesión de línea de base para estas máquinas virtuales y usar toodefine de aprendizaje de máquina lo que está fuera de la actividad de inicio de sesión normal. Si el número de Hola de inicios de sesión o el tiempo de hello del día de inicios de sesión de Hola o ubicación Hola desde qué Hola se solicitan los inicios de sesión u otras características relacionadas con el inicio de sesión es significativamente diferentes de línea de base de hello, puede generarse una alerta. Una vez más, es el aprendizaje automático el que se encarga de determinar qué es significativo.

## <a name="continuous-threat-intelligence-monitoring"></a>Supervisión continuada de la información sobre amenazas
Centro de seguridad de Azure funciona seguridad datos ciencia equipos de investigación y que supervise continuamente los cambios en el panorama de amenazas de Hola. Esto incluye Hola siguiendo las iniciativas:

* **Supervisión de la información sobre amenazas**: la información sobre amenazas incluye mecanismos, indicadores, implicaciones y notificaciones que tienen relación con amenazas nuevas o existentes. Esta información se comparte en la Comunidad de seguridad de Hola y Microsoft supervisa continuamente las fuentes de inteligencia de amenazas desde fuentes internas y externas.
* **Uso compartido de señales**: la información que recopilan los equipos de Microsoft a partir de la amplia cartera de servicios en la nube y locales, de servidores y de dispositivos cliente de punto de conexión de Microsoft se comparte y se analiza. 
* **Especialistas en seguridad de Microsoft**: colaboración continua con equipos de Microsoft que trabajan en ámbitos de seguridad especializados, como análisis forense y detección de ataques web.
* **Ajuste de detección**: algoritmos se ejecutarán en conjuntos de datos reales de los clientes y los investigadores de seguridad trabajar con resultados de los clientes toovalidate Hola. Positivos true y false son algoritmos de aprendizaje automático de toorefine usado.

Estos esfuerzos combinados culminan en detecciones nuevas y mejoradas, que puede beneficiarse de forma instantánea: no hay ninguna acción para tootake.

## <a name="see-also"></a>Otras referencias
En este documento, aprendió cómo funcionan las capacidades de detección de tooAzure centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md)
* [Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md)
* [Alertas de seguridad por tipo en Azure Security Center](security-center-alerts-type.md)
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.

