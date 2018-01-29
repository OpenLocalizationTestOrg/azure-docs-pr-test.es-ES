---
title: "Telemetría de Azure Stack | Microsoft Docs"
description: "Describe cómo configurar los valores de telemetría de Azure Stack mediante PowerShell."
services: azure-stack
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/08/2017
ms.author: jeffgilb
ms.reviewer: comartin
ms.openlocfilehash: 5cd8d4045764b753c5fdd81ade98d69c72709881
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2017
---
# <a name="azure-stack-telemetry"></a>Telemetría de Azure Stack

*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*

Los datos del sistema, o telemetría, de Azure Stack se cargan automáticamente en Microsoft mediante la Experiencia del usuario asociada. Los datos que se recopilan de la telemetría de Azure Stack los usan principalmente los equipos de Microsoft para mejorar las experiencias de nuestros clientes y de cara a los análisis de seguridad, mantenimiento, calidad y rendimiento.

Como operador de Azure Stack, la telemetría puede proporcionar información valiosa sobre las implementaciones empresariales y le ofrece una opción que ayuda a modelar las versiones futuras de Azure Stack.

> [!NOTE]
> Azure Stack se puede configurar también para reenviar la información de uso a Azure con fines de facturación. Esta información es necesaria para los clientes de Azure Stack de varios nodos que eligen la facturación de pago por uso. Los informes de uso se controlan de forma independiente de la telemetría y no son necesarios para los clientes de varios nodos que eligen el modelo de capacidad o para los usuarios del kit de desarrollo de Azure Stack. En estos escenarios, los informes de uso se pueden desactivar [mediante el script de registro](https://docs.microsoft.com/azure/azure-stack/azure-stack-usage-reporting). 

La telemetría de Azure Stack se basa en el componente Experiencia del usuario y telemetría asociadas de Windows Server 2016, que usa la tecnología de registro de seguimientos [ETW (Seguimiento de eventos para Windows)](https://msdn.microsoft.com/library/dn904632(v=vs.85).aspx) para recopilar y almacenar eventos y datos de telemetría. Los componentes de Azure Stack usan la misma tecnología de registro para publicar eventos y datos que se recopilan mediante las API de seguimiento y registro de eventos del sistema operativo. Ejemplos de componentes de Azure Stack son Proveedor de recursos de red, Proveedor de recursos de almacenamiento, Proveedor de recursos de supervisión y Proveedor de recursos de actualización. El componente Experiencia del usuario y telemetría asociadas cifra los datos mediante SSL y usa la asignación de certificados para transmitir datos de telemetría al servicio Microsoft Data Management a través de HTTPS.

> [!NOTE]
> Para admitir el flujo de datos de telemetría, el puerto 443 (HTTPS) debe estar abierto en la red. El componente Experiencia del usuario y telemetría asociadas se conecta al servicio Microsoft Data Management en https://v10.vortex-win.data.microsoft.com. El componente Experiencia del usuario y telemetría asociadas también se conecta a https://settings-win.data.microsoft.com para descargar información de configuración.

## <a name="privacy-considerations"></a>Consideraciones sobre privacidad
El servicio ETW enruta los datos de telemetría de vuelta al almacenamiento de nube protegido. El acceso a los datos de telemetría se rige por el principio de menores privilegios. Solo el personal de Microsoft con una necesidad empresarial válida tiene permiso de acceso a los datos de telemetría. Microsoft no comparte los datos personales de nuestros clientes con terceros, excepto si así lo decide el cliente o con las finalidades limitadas que se describe en la [declaración de privacidad de Azure Stack](http://windows.microsoft.com/windows/preview-privacy-statement). Se comparten informes empresariales con OEM y asociados que incluyen información de telemetría acumulada y anónima. Las decisiones de compartir los datos las realiza un equipo interno de Microsoft entre los que se cuentan las partes interesadas de privacidad, aspectos legales y administración de datos.

Microsoft cree en la minimización de la información, y la practica. Nos esforzamos por recopilar solo la información necesaria y la almacenamos solo mientras la necesitamos para proporcionar un servicio o realizar un análisis. Gran parte de la información sobre cómo funcionan el sistema de Azure Stack y los servicios de Azure se elimina al cabo de seis meses. Los datos acumulados o resumidos se mantienen durante más tiempo.

Sabemos que la privacidad y la seguridad de la información de nuestros clientes son muy importantes.  Por este motivo, hemos adoptado un enfoque serio y completo hacia la privacidad del cliente y la protección de sus datos con Azure Stack. Los administradores de TI disponen de controles para personalizar características y configuraciones de privacidad en cualquier momento. Nuestro compromiso a la transparencia y la confianza es claro:
- No escondemos a nuestros clientes los tipos de datos que recopilamos.
- Ponemos a los clientes de empresa al mando: ellos pueden personalizar su propia configuración de privacidad.
- Colocamos la seguridad y la privacidad del cliente en primer lugar.
- Somos transparentes sobre el modo en que se usa la telemetría.
- Usamos la telemetría para mejorar las experiencias del cliente.

La intención de Microsoft no es recopilar información confidencial, como números de tarjeta de crédito, nombres de usuario y contraseñas, direcciones de correo electrónico u otra información igualmente confidencial. Si determinamos que, por accidente, se ha recibido información confidencial, la eliminamos.

## <a name="examples-of-how-microsoft-uses-the-telemetry-data"></a>Ejemplos de cómo Microsoft usa los datos de telemetría
La telemetría desempeña un importante papel a la hora de ayudarnos a identificar y corregir rápidamente problemas críticos de confiabilidad en las implementaciones y configuraciones de nuestros clientes. La información que extraemos de los datos de telemetría que recopilamos nos ayuda a identificar rápidamente problemas con servicios o configuraciones de hardware. La posibilidad que tiene Microsoft de obtener estos datos de los clientes y de impulsar las mejoras en el ecosistema ayuda a elevar el estándar de calidad de nuestras soluciones integradas de Azure Stack. 

La telemetría también ayuda a Microsoft a entender mejor cómo los clientes implementan componentes y usan características y servicios para lograr sus objetivos empresariales. Al extraer información de los datos es posible destinar nuestras inversiones de ingeniería de manera prioritaria a áreas que pueden tener una repercusión directa sobre las experiencias y las cargas de trabajo de nuestros clientes.

Algunos ejemplos incluyen el uso de contenedores por parte del cliente, el almacenamiento y las configuraciones de redes que están asociadas con roles de Azure Stack. También usamos la información para impulsar mejoras e inteligencia en algunas de nuestras soluciones de administración y supervisión.  De esta forma, los clientes pueden diagnosticar problemas de calidad y ahorrar dinero, ya que realizan menos llamadas de soporte técnico a Microsoft.

## <a name="manage-telemetry-collection"></a>Administración de la recopilación de telemetría
No se recomienda desactivar la telemetría en su organización, ya que proporciona datos que controlan la funcionalidad y la estabilidad mejorada del producto. Sin embargo, reconocemos que en algunos casos puede ser necesario. 

En estos casos, puede configurar el nivel de telemetría que se envía a Microsoft mediante la implementación previa de la configuración del Registro o mediante la implementación posterior de los puntos de conexión de telemetría.

### <a name="asdk-set-telemetry-level-in-the-windows-registry"></a>ASDK: establecimiento del nivel de telemetría en el Registro de Windows
El Editor del Registro de Windows se usa para establecer manualmente el nivel de telemetría en el equipo host físico antes de implementar Azure Stack. Si ya existe una directiva de administración, como la directiva de grupo, reemplazará a este valor del Registro. 

Antes de implementar Azure Stack en el host del kit de desarrollo, inicie CloudBuilder.vhdx y ejecute el siguiente script en una ventana de PowerShell con privilegios elevados:

```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0' # Set this value to 0,1,2,or3.  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

Los niveles de telemetría son acumulativos y se clasifican en cuatro niveles (0-3):

**0 (Seguridad)**. Solo datos de seguridad. Información que es necesaria para ayudar a proteger el sistema operativo, lo que incluye datos sobre la configuración del componente Experiencia del usuario y telemetría asociadas y Windows Defender. En este nivel no se emite ninguna telemetría específica de Azure Stack.

**1 (Básico)**. Datos de seguridad y datos básicos de mantenimiento y calidad. Información básica del dispositivo, lo que incluye datos relacionados con la calidad, compatibilidad con aplicaciones, datos de uso de aplicaciones y datos del nivel Seguridad. Al establecer el nivel de telemetría en Básico se habilita la telemetría de Azure Stack. Los datos recopilados en este nivel incluyen:

- **Información básica del dispositivo** que ayuda a comprender los tipos y las configuraciones de instancias de Windows Server 2016 nativas y virtualizadas del ecosistema, como por ejemplo:
 - Atributos de la máquina, como OEM, modelo 
 - Atributos de red, como número y velocidad de los adaptadores de red
 - Atributos de procesador y memoria, como número de núcleos, tamaño de memoria 
 - Atributos de almacenamiento, como número de unidades, tipo y tamaño
- **Funcionalidad de telemetría**, que incluye el porcentaje de eventos cargados, eventos descartados y hora de última carga.
- **Información relacionada con la calidad** que ayuda a Microsoft a desarrollar una comprensión básica de cómo funciona Azure Stack. Un ejemplo es el número de alertas críticas en una configuración de hardware determinada.
- **Datos de compatibilidad** que ayudan a comprender qué proveedores de recursos están instalados en un sistema y en una máquina virtual y a identifican posibles problemas de compatibilidad.

**2 (Mejorado)**. Información adicional, que incluye cómo se usan el sistema operativo y otros servicios de Azure Stack, cuál es su rendimiento, datos avanzados de confiabilidad y datos de los niveles Básico y Seguridad. 

**3 (Completo)**. Todos los datos necesarios para identificar problemas y ayudar a su solución, además de los datos de los niveles **Seguridad**, **Básico** y **Mejorado**.

> [!NOTE]
> El valor de nivel de telemetría predeterminado es 2 (mejorado).

Tenga en cuenta que al desactivar la telemetría de Windows y de Azure Stack también se deshabilita la telemetría de SQL. Para información adicional sobre las implicaciones de la configuración de telemetría de Windows Server, use como referencia las [notas del producto de la telemetría de Windows](https://aka.ms/winservtelemetry). 

> [!IMPORTANT]
> Estos niveles de telemetría solo se aplican a los componentes de Microsoft Azure Stack. Los componentes y servicios de software que no sean de Microsoft que se ejecutan en el host de ciclo de vida de hardware de los asociados de hardware de Azure Stack se pueden comunicar con sus servicios en la nube fuera de estos niveles de telemetría. Acuda a su proveedor de soluciones de hardware de Azure Stack para que le informe de su directiva de telemetría y cómo puede usarla o no. 

### <a name="asdk-and-multinode-enable-or-disable-telemetry-after-deployment"></a>ASDK y varios nodos: habilitación o deshabilitación de la telemetría después de la implementación

Para habilitar o deshabilitar la telemetría después de la implementación, debe tener acceso al punto de conexión con privilegios (PEP) que se expone en las máquinas virtuales de ERCS.
1.  Para habilitar: `Set-Telemetry -Enable`
2.  Para deshabilitar: `Set-Telemetry -Disable`

Detalle del PARÁMETRO: 
> .PARÁMETRO Enable: activa la carga de telemetría 

> .PARÁMETRO Disable: desactiva la carga de datos de telemetría  

**Script para habilitar la telemetría:**
```powershell
$ip = "<IP ADDRESS OF THE PEP VM>" # You can also use the machine name instead of IP here.
$pwd= ConvertTo-SecureString "<CLOUD ADMIN PASSWORD>" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("<DOMAIN NAME>\CloudAdmin", $pwd)
$psSession = New-PSSession -ComputerName $ip -ConfigurationName PrivilegedEndpoint -Credential $cred
Invoke-Command -Session $psSession {Set-Telemetry -Enable}
if($psSession)
{
    Remove-PSSession $psSession
}
```

**Script para deshabilitar la telemetría:**
```powershell
$ip = "<IP ADDRESS OF THE PEP VM>" # You can also use the machine name instead of IP here.
$pwd= ConvertTo-SecureString "<CLOUD ADMIN PASSWORD>" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("<DOMAIN NAME>\CloudAdmin", $pwd)
$psSession = New-PSSession -ComputerName $ip -ConfigurationName PrivilegedEndpoint -Credential $cred
Invoke-Command -Session $psSession {Set-Telemetry -Disable}
if($psSession)
{
    Remove-PSSession $psSession
}
```

## <a name="next-steps"></a>Pasos siguientes
[Descarga del paquete de implementación de Azure Stack Development Kit](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[Implementación de Azure Stack Development Kit](azure-stack-run-powershell-script.md)

