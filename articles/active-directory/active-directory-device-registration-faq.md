---
title: "aaaAzure registro automático de dispositivos de Active Directory preguntas más frecuentes | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre el registro automático de dispositivos con Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a>Preguntas más frecuentes sobre el registro automático de dispositivos de Azure Active Directory

**P: ¿puedo registrar dispositivo Hola recientemente. ¿Por qué no puedo ver dispositivo hello en mi información de usuario en hello portal de Azure?**

**R:** dispositivos Windows 10 que están unidos al dominio con el registro automático de dispositivos no se muestran en la información de usuario de Hola.
Debe toouse PowerShell toosee todos los dispositivos. 

Solo hello dispositivos siguientes aparecen en información de usuario de hello:

- Todos los dispositivos personales que no están unidos a una empresa 
- Todos los dispositivos que no tengan Windows 10 / Windows Server 2016 
- Todos los dispositivos que no son de Windows 

---

**P: ¿por qué no puedo ver todos los dispositivos de hello registrados en Azure Active Directory en hello portal de Azure?** 

**R:** actualmente no hay ninguna manera toosee todos los dispositivos registrados en hello portal de Azure. Puede usar Azure PowerShell toofind todos los dispositivos. Para obtener más información, vea hello [MsolDevice Get](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.

--- 

**P: ¿Cómo puedo saber qué estado de registro del dispositivo de Hola de cliente hello es?**

**R:** depende de estado de registro del dispositivo de hello:

- ¿Qué dispositivo Hola
- Cómo se ha registrado 
- Los detalles relacionados con tooit. 
 

---

**P: ¿por qué es un dispositivo que he eliminado en hello Azure portal o mediante Windows PowerShell siguen apareciendo como está registrado?**

**R:** Se debe al diseño. dispositivo de Hello no tendrá acceso tooresources en la nube de Hola. Si desea tooremove Hola dispositivo y vuelva a registrar, una acción manual debe ser toobe realizada en los dispositivos de Hola. 

Para dispositivos Windows 10 y Windows Server 2016 unidos a un dominio AD local:

1.  Abra el símbolo del sistema de hello como administrador.

2.  Escriba `dsregcmd.exe /debug /leave`

3.  Cierre la sesión e inicie sesión tarea programada de tootrigger Hola que registra el dispositivo de Hola de nuevo. 

Para otras plataformas de Windows unidas a un dominio AD local:

1.  Abra el símbolo del sistema de hello como administrador.
2.  Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**P: ¿Por qué veo entradas duplicadas del dispositivo en Azure Portal?**

**R:**

-   Para Windows 10 y Windows Server 2016, si son varios intentos toounjoin y vuelva a unir hello mismo dispositivo, puede haber entradas duplicadas. 

-   Si ha usado Agregar cuenta profesional o educativa, cada usuario de windows que usa Agregar cuenta profesional o educativa creará un nuevo registro de dispositivo con hello mismo nombre de dispositivo.

-   Otras plataformas de Windows que están en las instalaciones con el registro automático unido a un dominio de AD creará un nuevo registro de dispositivo con hello mismo nombre de dispositivo para cada usuario de dominio que inicie sesión en el dispositivo de Hola. 

-   Una máquina AADJ que se borró, volver a instalar y volver a unirse con hello mismo nombre, se mostrarán como otro registro con hello mismo nombre de dispositivo.

---

**P: ¿por qué puede un usuario tener acceso a recursos desde un dispositivo que he deshabilitado en hello portal de Azure?**

**R:** puede tardar hasta hora tooan para un toobe revoke aplicado.

>[!Note] 
>Para dispositivos perdidos, se recomienda borrar Hola dispositivo tooensure que los usuarios no pueden tener acceso a dispositivo Hola. Para más información, vea [Inscribir dispositivos para administrarlos en Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**P: ¿Por qué mis usuarios ven un mensaje que indica que no pueden acceder desde aquí?**

**R:** si ha configurado determinado toorequire de reglas de acceso condicional un estado de dispositivo específico y Hola dispositivo no cumple los criterios de hello, los usuarios están bloqueados y verá este mensaje. Por favor, evaluar reglas de Hola y asegúrese de que el dispositivo hello es capaz de toomeet Hola criterios tooavoid este mensaje.

---


**P: ¿puedo ver registro de dispositivo de hello en información de usuario de Hola Hola portal de Azure y puede ver el estado de hello como está registrado en el cliente de Hola. ¿He establecido la configuración correctamente para utilizar el acceso condicional?**

**R:** registro hello de dispositivo (deviceID) y el estado en el portal de Azure Hola deben coincidir con el cliente de Hola y se cumplen los criterios de evaluación de acceso condicional. Para más información, vea [Introducción al Registro de dispositivos de Azure Active Directory](active-directory-device-registration.md).

---

**P: ¿por qué obtengo un mensaje de "nombre de usuario o contraseña es incorrecta" para un dispositivo recién he unido tooAzure AD?**

**R:** Las razones comunes para este escenario son:

- Las credenciales de usuario ya no son válidas.

- El equipo es no se puede toocommunicate con Azure Active Directory. Compruebe si existen errores de conectividad de red.

- no se cumplieron los requisitos previos de Azure AD Join Hola. Asegúrese de que ha seguido los pasos de Hola para [extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md).  

- Los inicios de sesión federados requiere su toosupport de servidor de federación un punto de conexión activo de WS-Trust. 

---

**P: ¿por qué veo un saludo "¡vaya!... se produjo un error!" cuando intento del cuadro de diálogo unir su PC?**

**R:** Es el resultado de configurar la inscripción de Azure Active Directory con Intune. Para más información, vea [Configurar la administración de dispositivos Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**P: ¿por qué mi toojoin intento producirá un error en un equipo aunque no aparece ninguna información de errores?**

**R:** una causa probable es que ese usuario Hola se registra en el dispositivo toohello con cuenta de administrador integrada de Hola. Cree una cuenta local diferente antes de usar el programa de instalación de Azure Active Directory Join toocomplete Hola. 

---

**P: ¿dónde puedo encontrar instrucciones para el programa de instalación de Hola de registro automático de dispositivos?**

**R:** para obtener instrucciones detalladas, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**P: ¿dónde puedo encontrar solución de problemas de información sobre el registro de hello automático de dispositivos?**

**R:** Para consultar información sobre solución de problemas, vea:

- [Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

