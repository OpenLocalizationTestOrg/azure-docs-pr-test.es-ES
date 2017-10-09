---
title: un dispositivo de StorSimple implementado aaaTroubleshoot | Documentos de Microsoft
description: "Describe cómo toodiagnose y corrección de errores que se producen en un dispositivo de StorSimple que está actualmente implementada y en funcionamiento."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Solución de problemas de un dispositivo de StorSimple operativo
## <a name="overview"></a>Información general
En este artículo se proporcionan instrucciones útiles para solucionar problemas de configuración que se pueden encontrar una vez que el dispositivo de StorSimple está implementado y operativo. Describe los problemas comunes, causas posibles y toohelp pasos recomendados que resolver problemas que pueden experimentar al ejecutar Microsoft Azure StorSimple. Esta información aplica tooboth dispositivo físico de hello StorSimple local y el dispositivo virtual StorSimple Hola.

Al final de Hola de este artículo, puede encontrar una lista de códigos de error que pueden surgir durante la operación de StorSimple de Microsoft Azure, así como pasos puede tardar errores de hello tooresolve. 

## <a name="setup-wizard-process-for-operational-devices"></a>Proceso del Asistente de instalación para dispositivos operativos
Usar el Asistente para la instalación de hello ([Invoke-HcsSetupWizard][1]) toocheck Hola configuración del dispositivo y tomar medidas correctivas si es necesario.

Al ejecutar el Asistente para la instalación de hello en un dispositivo previamente configurado y en funcionamiento, el flujo del proceso de hello es diferente. Puede cambiar solo Hola siguientes entradas:

* Dirección IP, máscara de subred y puerta de enlace
* Servidor DNS principal
* Servidor NTP principal
* Configuración de proxy web opcional

Asistente para la instalación de Hello no lleva a cabo Hola operaciones relacionadas toopassword recopilación y el registro de dispositivos.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Errores que se producen durante las ejecuciones posteriores del Asistente para instalación de Hola
Hello en la tabla siguiente describe los errores de Hola que pueden surgir al ejecutar el Asistente para la instalación de hello en un dispositivo operativo, las posibles causas de errores de Hola y las acciones recomendadas tooresolve ellos. 

| No. | Mensaje o condición de error | Causas posibles | Acción recomendada |
|:--- |:--- |:--- |:--- |
| 1 |Error 350032: El dispositivo ya se ha desactivado. |Verá este error si ejecuta el Asistente para la instalación de hello en un dispositivo que está desactivado. |[Póngase en contacto con el servicio de soporte técnico de Microsoft](storsimple-contact-microsoft-support.md) para conocer los pasos siguientes. No se puede poner en servicio un dispositivo desactivado. Antes de que puede volver a activarse dispositivo hello, puede ser necesario un restablecimiento de fábrica. |
| 2 |Invoke-HcsSetupWizard: ERROR_INVALID_FUNCTION (excepción de HRESULT: 0x80070001) |Error en Hello actualización del servidor DNS. Configuración de DNS es global y se aplica a todas las interfaces de red de hello habilitado. |Habilitar la interfaz de Hola y vuelva a aplicar la configuración de DNS de Hola. Esto puede afectar a la conectividad de Hola para otras interfaces habilitadas porque esta configuración es global. |
| 3 |dispositivo de Hello aparece toobe en línea en el portal del servicio de hello StorSimple Manager, pero al intentar la instalación mínima de toocomplete hello y guardar configuración de hello, se produce un error en la operación de Hola. |Durante la instalación inicial, no se configuró proxy web de hello, aunque había un servidor proxy real en su lugar. |Hola de uso [cmdlet Test-HcsmConnection] [ 2] toolocate error de Hola. [Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) si es un problema de hello toocorrect no se puede. |
| 4 |Invoke-HcsSetupWizard: Valor no está en el intervalo de espera de Hola. |Este error se debe a una máscara de subred incorrecta. Las posibles causas son:  <ul><li> máscara de subred de Hello falta o está vacío.</li><li>formato de prefijo Ipv6 de Hello es incorrecto.</li><li>interfaz de Hello está habilitada para la nube, pero la puerta de enlace de hello falta o es incorrecto.</li></ul>Tenga en cuenta que DATA 0 está en la nube-habilita automáticamente si ha configurado mediante el Asistente para la instalación de Hola. |problema de hello toodetermine, utilice subredes 0.0.0.0 o 256.256.256.256 y, a continuación, busque en la salida de hello. Escriba los valores correctos para la máscara de subred de hello, puerta de enlace y prefijo de Ipv6, según sea necesario. |

## <a name="error-codes"></a>Códigos de error
Los errores se muestran en orden numérico.

| Número de error | Texto o descripción del error | Acción del usuario recomendada |
|:--- |:--- |:--- |
| 10502 |Se encontró un error al obtener acceso a la cuenta de almacenamiento. |Espere unos minutos y vuelva a intentarlo. Si Hola error persiste, ponte en contacto con soporte técnico de Microsoft para los pasos siguientes. |
| 40017 |Error en operación de copia de seguridad de Hello como no se encontró un volumen especificado en la directiva de copia de seguridad de hello en dispositivo Hola. |Vuelva a intentar la operación de copia de seguridad de hello, si hello error persiste, póngase en contacto con Microsoft Support. Pasos siguientes |
| 40018 |Error en operación de copia de seguridad de Hello como ninguno de los volúmenes de hello especificados en la directiva de copia de seguridad de hello encontrado en dispositivos de Hola. |Vuelva a intentar la operación de copia de seguridad de hello, si hello error persiste, póngase en contacto con Microsoft Support. Pasos siguientes |
| 390061 |sistema de Hello está ocupado o no está disponible. |Espere unos minutos y vuelva a intentarlo. Si Hola error persiste, ponte en contacto con soporte técnico de Microsoft para los pasos siguientes. |
| 390143 |Se produjo un error con el código de error 390143. (Error desconocido). |Si Hola error persiste, póngase en contacto con Microsoft Support para los pasos siguientes. |

## <a name="next-steps"></a>Pasos siguientes
Si es un problema de hello tooresolve no se puede, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para obtener ayuda. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
