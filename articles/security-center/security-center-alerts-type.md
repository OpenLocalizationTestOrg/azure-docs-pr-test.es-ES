---
title: aaaSecurity alertas por tipo en el centro de seguridad de Azure | Documentos de Microsoft
description: "En este artículo se describe diferentes tipos de Hola de alertas de seguridad disponibles en el centro de seguridad de Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Comprensión de las alertas de seguridad en Azure Security Center
En este artículo le ayuda a tipos diferentes de hello toounderstand de alertas de seguridad e información relacionados que están disponibles en el centro de seguridad de Azure. Para obtener más información sobre cómo ver las alertas de toomanage e incidentes, [toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset seguridad avanzadas detecciones, tooAzure actualización estándar de centro de seguridad. Hay disponible una versión de evaluación gratuita de 60 días. tooupgrade, seleccione **tarifa** en hello [directiva de seguridad](security-center-policies.md). toolearn más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>¿Qué tipo de alertas está disponible?
Centro de seguridad de Azure usa una variedad de [las capacidades de detección](security-center-detection-capabilities.md) tooalert clientes toopotential ataques sus entornos de destino. Estas alertas contienen información valiosa acerca de Hola qué desencadena Hola alerta, recursos de Hola de destino y Hola origen del ataque Hola. información de Hello incluida en una alerta varía según tipo hello de análisis usa toodetect Hola amenaza. Los incidentes también pueden contener información contextual adicional que puede resultar útil para la investigación de la amenaza.  Este artículo proporciona información acerca de hello siguientes tipos de alerta:

* Análisis del comportamiento de la máquina virtual (VMBA)
* Análisis de red
* Análisis de recursos
* Información contextual

## <a name="virtual-machine-behavioral-analysis"></a>Análisis del comportamiento de la máquina virtual
Centro de seguridad de Azure puede usar recursos de tooidentify en peligro de análisis de comportamiento basados en el análisis de registros de eventos de máquina virtual. Por ejemplo, eventos de creación de proceso y eventos de inicio de sesión. Además, hay una correlación con los otro toocheck de señales para admitir la evidencia de una campaña generalizada.

> [!NOTE]
> Para más información acerca de cómo actúan las funcionalidades de detección de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Análisis de bloqueos
Análisis de memoria de volcado de bloqueo es un método que se utiliza toodetect malware sofisticado que es capaz de tooevade soluciones de seguridad tradicionales. Diversas formas de malware intente oportunidad de hello tooreduce de productos antivirus detectando escribiendo nunca toodisk o mediante el cifrado de los componentes de software que se han escrito toodisk. Esto hace Hola malware difícil toodetect mediante métodos tradicionales de antimalware. Sin embargo, este tipo de malware se puede detectar mediante el análisis de memoria, debido a que malware debe dejar seguimientos en memoria, en orden toofunction.

Cuando se bloquea el software, un volcado de memoria captura una parte de la memoria en tiempo de Hola de fallo de Hola. bloqueo de Hello puede deberse a malware, generales de la aplicación o problemas del sistema. Mediante el análisis de memoria de hello en el volcado de memoria hello, centro de seguridad puede detectar técnicas empleadas tooexploit vulnerabilidades de software, obtener acceso a datos confidenciales y conservar escondidas dentro de una máquina en peligro. Esto se logra con rendimiento mínimo impacto toohosts como Hola el análisis se realiza por hello finalizar el nuevo centro de seguridad.

Hola después campos es toohello bloqueo volcado alerta ejemplos comunes que aparecen más adelante en este artículo:

* Archivo de volcado: El nombre del archivo de volcado Hola.
* PROCESSNAME: Nombre de hello bloquea el proceso.
* PROCESSVERSION: Versión de Hola bloquea el proceso.

### <a name="shellcode-discovered"></a>Detectado shellcode
Código shell es carga Hola que se ejecuta una vez malware aprovecha una vulnerabilidad de software. Esta alerta indica que el análisis del volcado de memoria ha detectado código ejecutable que muestra un comportamiento normalmente realizado mediante cargas malintencionadas. Aunque el software no malintencionado puede tener este comportamiento, no es típico en las prácticas de desarrollo de software normal.

ejemplo de Hola código shell alerta proporciona Hola siguiente campo adicional:

* DIRECCIÓN: la ubicación de hello en la memoria de código de hello Shell.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta de shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Detectado secuestro de módulo
Windows utiliza la funcionalidad de sistema de bibliotecas de vínculos dinámicos (DLL) tooallow software tooutilize común Windows. Cambiando la configuración de archivo DLL se produce cuando malware cargas malintencionados tooload del orden de carga de hello DLL en la memoria, donde se puede ejecutar código arbitrario. Esta alerta indica que el análisis de volcado de bloqueo de hello detectan un módulo con el mismo nombre que se carga desde dos rutas de acceso diferentes. Una de las rutas de acceso de carga de Hola procede de una ubicación binaria de sistema común de Windows.

Los desarrolladores de software legítimo en ocasiones, cambiar el orden de carga DLL de Hola por razones no malintencionado, como la instrumentación, extender el sistema operativo Windows hello o extender una aplicación de Windows. toohelp diferenciar cambios malintencionado y potencialmente benigno toohello orden de carga DLL, centro de seguridad de Azure comprueba si un módulo cargado ajusta tooa sospechosa perfil. resultado de Hello de esta comprobación se indica mediante el campo de "Firma" hello de alerta de Hola y se refleja en la gravedad de Hola de alerta de hello, descripción de la alerta y pasos de corrección de alerta. tooresearch si el módulo de hello es legítimo o malintencionados, analizar hello en copia de disco de hello cambiando la configuración de módulo. Por ejemplo, puede comprobar la firma digital del archivo de Hola o ejecutar un análisis antivirus.

Además toohello campos comunes que se describe en la sección anterior "código shell detectados" de hello, esta alerta proporciona Hola siguientes campos:

* FIRMA: Indica si Hola cambiando la configuración de módulo ajusta tooa perfil de comportamiento sospechoso.
* HIJACKEDMODULE: nombre de Hola de hello secuestradas módulo de sistema de Windows.
* HIJACKEDMODULEPATH: ruta de acceso de Hola de hello secuestradas módulo de sistema de Windows.
* HIJACKINGMODULEPATH: ruta de acceso Hola del módulo de secuestro de Hola.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta de secuestro de módulos](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Detectado módulo de Windows enmascarado
Software malintencionado puede usar nombres comunes de los archivos binarios del sistema de Windows (por ejemplo, SVCHOST. (EXE) o módulos (por ejemplo, NTDLL. DLL) demasiado*blend* y ocultar la naturaleza de Hola de software malintencionado de Hola de los administradores del sistema. Esta alerta indica que el análisis de volcado de bloqueo de hello ha detectado que ese archivo de volcado hello contiene módulos que utilizan nombres de módulo de sistema de Windows, pero no cumplen otros criterios que son típicos de módulos de Windows. Analizar hello en copia de disco de módulo enmascarado Hola puede proporcionar más información acerca de la naturaleza de hello legítimo o malintencionados de este módulo. El análisis puede incluir:

* Confirmar que ese archivo de hello en cuestión se incluye como parte de un paquete de software legítimo.
* Comprobar la firma digital del archivo Hola.
* Ejecute un análisis antivirus en el archivo hello.

Además toohello campos comunes que se ha descrito anteriormente en la sección de "Código de shell detectado" Hola, esta alerta proporciona Hola siguientes campos adicionales:

* Detalles: Describe si los metadatos del módulo de hello son válido y si se cargó el módulo de Hola desde una ruta de acceso del sistema.
* NOMBRE: nombre de hello del módulo de Windows enmascarado Hola.
* Ruta de acceso: Hola ruta de acceso toohello enmascarado módulo de Windows.

Esta alerta también extrae y muestra algunos de los campos de encabezado de PE del módulo de hello, como "CHECKSUM" y "TIMESTAMP". Estos campos solo se muestran si están presentes en el módulo de hello campos Hola. Vea hello [especificación Microsoft PE y COFF](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) para obtener más información sobre estos campos.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta de Windows enmascarado](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Detectados archivos binarios del sistema modificados
Malware puede modificar los archivos binarios del sistema principal en datos de access de orden toocovertly o escondidas se conservan en un sistema en peligro. Esta alerta indica que los análisis de volcado de bloqueo de Hola ha detectado que los archivos binarios del núcleo del sistema operativo Windows se han modificado en la memoria o en disco.

Los desarrolladores de software legítimo modifican ocasionalmente módulos del sistema en la memoria por razones no malintencionados, como desvíos o compatibilidad de aplicaciones. toohelp diferenciar entre módulos malintencionados y potencialmente legítimos, centro de seguridad de Azure comprueba si Hola modificado módulo ajusta tooa sospechosa perfil. resultado de Hello de esta comprobación se indica por gravedad Hola de alerta de hello, descripción de la alerta y pasos de corrección de alerta.

Además toohello campos comunes que se ha descrito anteriormente en la sección de "Código de shell detectado" Hola, esta alerta proporciona Hola siguientes campos adicionales:

* MODULENAME: Nombre de hello modifica binario del sistema.
* MODULEVERSION: Versión de Hola modifica binario del sistema.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta binaria del sistema](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Proceso sospechoso ejecutado
Centro de seguridad identifica un proceso sospechoso que se ejecuta en la máquina virtual de destino de hello y, a continuación, genera una alerta. detección de Hello no busque el nombre específico de hello, pero busque el parámetro del archivo ejecutable de Hola. Por lo tanto, incluso si el atacante Hola cambia el nombre de ejecutable hello, centro de seguridad todavía puede detectar proceso sospechosa Hola.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta de proceso sospechoso](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Múltiples cuentas de dominio consultadas
Centro de seguridad puede detectar varios intentos tooquery cuentas de dominio de Active Directory, que es algo normalmente realizadas por los atacantes durante el reconocimiento de red. Los atacantes pueden aprovechar esta técnica tooquery Hola dominio tooidentify Hola a los usuarios, identificar las cuentas de administrador de dominio de hello, identificar los equipos de Hola que son controladores de dominio así como identifican la relación de confianza de dominio potencial de hello con otros dominios.

A continuación se muestra un ejemplo de este tipo de alerta:

![Alerta de cuenta con múltiples dominios](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Se enumeraron los miembros del grupo Administradores locales

Centro de seguridad se va tootrigger una alerta cuando se desencadenar eventos de seguridad de hello 4798, en Windows Server 2016 y Windows 10. Esto sucede cuando se enumeran los grupos de administradores locales, que es algo que los atacantes suelen hacer durante el reconocimiento de la red. Los atacantes pueden aprovechar esta identidad de hello tooquery técnica de los usuarios con privilegios administrativos.

A continuación se muestra un ejemplo de este tipo de alerta:

![Administrador local](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Mezcla anómala de mayúsculas y minúsculas

Centro de seguridad se desencadenará una alerta cuando detecta el uso de Hola de una combinación de mayúsculas y minúsculas en línea de comandos de Hola. Algunos los atacantes pueden utilizar esta toohide técnica de mayúsculas y minúsculas o hash según la regla de la máquina.

A continuación se muestra un ejemplo de este tipo de alerta:

![Mezcla anómala](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Sospecha de ataque de golden ticket de Kerberos

Una en peligro [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) clave puede utilizarse por un toocreate atacante Kerberos "Dorada vales", que permite Hola atacante tooimpersonate cualquier usuario que desean. Centro de seguridad se va tootrigger una alerta cuando detecta este tipo de actividad.

> [!NOTE] 
> Para más información sobre el golden ticket de Kerberos, consulte [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx) (Guía de mitigación del robo de credenciales de Windows 10).

A continuación se muestra un ejemplo de este tipo de alerta:

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Cuenta sospechosa creada

Security Center desencadenará una alerta cuando se cree una cuenta que se parezca mucho a una cuenta integrada existente con privilegios administrativos. Esta técnica puede usarse por toocreate los atacantes tooavoid que se detecte por comprobación de usuario de la cuenta no fiable.
 
A continuación se muestra un ejemplo de este tipo de alerta:

![Cuenta sospechosa](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Regla de firewall sospechosa creada

Los atacantes pueden intentar toocircumvent host seguridad mediante la creación de firewall personalizadas reglas tooallow aplicaciones malintencionadas toocommunicate con el comando y control, o ataques toolaunch a través de la red de Hola a través de hello en peligro host. Security Center desencadenará una alerta cuando detecte que se ha creado una regla de firewall a partir de un archivo ejecutable en una ubicación sospechosa.
 
A continuación se muestra un ejemplo de este tipo de alerta:

![Regla de firewall](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Combinación sospechosa de HTA y PowerShell

Security Center desencadenará una alerta cuando detecte que un host de aplicación HTML (HTA) de Microsoft esté iniciando comandos de PowerShell. Se trata de una técnica utilizada por los scripts de PowerShell de los atacantes toolaunch malintencionados.
 
A continuación se muestra un ejemplo de este tipo de alerta:

![HTA y PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Análisis de red
La detección de amenazas de Security Center recopila automáticamente información de seguridad de su tráfico (exportación de la información de flujo del protocolo de Internet) de IPFIX de Azure. Analiza esta información, a menudo correlacionar información procedente de varios orígenes, tooidentify amenazas.

### <a name="suspicious-outgoing-traffic-detected"></a>Suspicious outgoing traffic detected (Tráfico saliente sospechoso detectado)
Pueden detectar dispositivos de red y generar perfiles en cantidad Hola igual que otros tipos de sistemas. Los atacantes suelen comenzar con la exploración de puertos o con el barrido de puertos. En el siguiente ejemplo de Hola, tiene tráfico sospechoso de Shell seguro (SSH) de una máquina virtual. En este escenario, es posible un ataque por fuerza bruta SSH o por ataque circular contra un recurso externo.

![Alerta de tráfico saliente sospechoso](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Esta alerta proporciona información que puede usar recursos de hello tooidentify que estaba tooinitiate usa este tipo de ataque. Esta alerta también proporciona información en peligro tooidentify Hola máquina, hora de detección de hello, además de protocolo de Hola y puerto que se utilizó. Esta hoja también proporciona una lista de pasos de corrección que pueden ser utilizado toomitigate este problema.

### <a name="network-communication-with-a-malicious-machine"></a>Network communication with a malicious machine (Comunicación de red con una máquina malintencionada)
Mediante el aprovechamiento de las fuentes de inteligencia de amenazas de Microsoft, Azure Security Center puede detectar equipos en peligro que se comunican con direcciones IP malintencionadas. En muchos casos, dirección malintencionada hello es un centro de comando y control. En este caso, el centro de seguridad ha detectado que se efectúan comunicación hello mediante ponis cargador malware (también conocido como [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![alerta de comunicación de red](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Esta alerta proporciona información que permite los recursos de hello tooidentify que estaba tooinitiate usado este ataque, Hola atacadas recursos, IP de la víctima de hello, Hola atacante IP y hora de detección de Hola.

> [!NOTE]
> Las direcciones IP activas se quitaron de esta captura de pantalla por privacidad.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Posible ataque de denegación de servicio de salida detectado
Anómala tráfico de red que se origina en una máquina virtual puede provocar tootrigger de centro de seguridad un tipo de denegación de servicio posible de ataque.

A continuación se muestra un ejemplo de este tipo de alerta:

![Denegación de servicio saliente](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Análisis de recursos
Análisis de recursos del centro de seguridad se centra en la plataforma como los servicios de servicio (PaaS), como la integración de hello con hello [detección de amenazas de base de datos de SQL Azure](../sql-database/sql-database-threat-detection.md) característica. Basándose en los resultados del análisis de Hola de estas áreas, centro de seguridad genera una alerta relacionada con el recurso.

### <a name="potential-sql-injection"></a>Posible inyección de código SQL
Inyección de código SQL es un ataque donde se inserta código malintencionado en las cadenas que posteriormente se pasan tooan instancia de SQL Server para su análisis y ejecución. Como el servidor SQL Server ejecuta todas las consultas sintácticamente válidas que recibe, deben revisarse todos los procedimientos que crean instrucciones SQL en busca de vulnerabilidades por inyección de código. Detección de amenazas de SQL usa el aprendizaje automático, análisis del comportamiento y anomalías detección toodetermine eventos sospechosos que podrían ser teniendo lugar en las bases de datos de SQL Azure. Por ejemplo:

* Un antiguo empleado ha intentado acceder a la base de datos
* Ataques de inyección de código SQL
* Base de datos de access inusual tooa producción de un usuario en casa

![Alerta de posible inyección de código SQL](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

información de Hello en esta alerta puede ser usado tooidentify Hola atacada recursos, tiempo de detección de Hola y el estado de Hola de ataque de Hola. También proporciona un vínculo toofurther pasos de investigación.

### <a name="vulnerability-toosql-injection"></a>TooSQL vulnerabilidades por inyección de código
Esta alerta se desencadena cuando se detecta un error de aplicación en una base de datos. Esta alerta puede indicar que una inyección de código de tooSQL vulnerabilidad posibles ataques.

![Alerta de posible inyección de código SQL](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Acceso inusual desde una ubicación desconocida
Esta alerta se desencadena cuando se detecta un evento de acceso desde una dirección IP familiarizado en servidor de hello, que no se ha visto en hello último período.

![Alerta de acceso inusual](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Información contextual
Durante una investigación, los analistas necesitan contexto adicional tooreach un veredicto sobre la naturaleza de Hola de amenaza de Hola y cómo toomitigate lo.  Por ejemplo, se ha detectado una anomalía de red, pero sin saber qué otras cosas sucede en red de Hola o con el recurso de destino de toohello tener en cuenta es cada disco duro toounderstand qué tootake acciones a continuación. tooaid con eso, puede incluir un incidente de seguridad artefactos, eventos e información relacionados que puede ayudar a los investigadores de Hola. Hello disponibilidad de información adicional varían en función Hola tipo de amenaza detectada y Hola una configuración del entorno y no estará disponible para todos los incidentes de seguridad.

Si hay disponible información adicional, se mostrará en hello incidentes de seguridad por debajo de la lista de Hola de alertas. Podría contener datos como:

- Eventos de registro borrados
- Dispositivos Plug and Play desconocidos
- Alertas que no se pueden activar 

![Alerta de acceso inusual](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Otras referencias
En este artículo, ha aprendido acerca de los tipos diferentes de hello de alertas de seguridad en el centro de seguridad. toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Control de incidentes de seguridad en Azure Security Center](security-center-incident.md)
* [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md)
* [Guía de planeamiento y operaciones de Azure Security Center](security-center-planning-and-operations-guide.md)
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md): preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.
