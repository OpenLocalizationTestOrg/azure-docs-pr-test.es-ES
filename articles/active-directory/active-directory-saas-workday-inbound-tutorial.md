---
title: "Tutorial: configuración de Workday para aprovisionar automáticamente usuarios con Active Directory y Azure Active Directory locales | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse Workday como origen de datos de identidad de Active Directory y Azure Active Directory."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Tutorial: configuración de Workday para aprovisionar automáticamente usuarios con Active Directory y Azure Active Directory locales
objetivo de Hola de este tutorial es tooshow Hola pasos que debe tooperform tooimport personas desde Workday en Active Directory y Azure Active Directory, con la escritura diferida opcional de algunos tooWorkday de atributos. 



## <a name="overview"></a>Información general

Hola [aprovisionamiento del servicio de usuario de Azure Active Directory](active-directory-saas-app-provisioning.md) se integra con hello [API de recursos humanos Workday](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) en orden tooprovision cuentas de usuario. Azure AD usa este hello tooenable de conexión después de los flujos de trabajo de aprovisionamiento de usuario:

* **Aprovisionamiento de usuarios tooActive Directory** : sincronizar conjuntos seleccionados de los usuarios desde jornada laboral en uno o más bosques de Active Directory. 

* **Aprovisionamiento de usuarios solo en la nube tooAzure Active Directory** -usuarios híbrida que existen en Active Directory y Azure Active Directory se pueden aprovisionar en hello última utiliza [AAD Connect](connect/active-directory-aadconnect.md). Sin embargo, se pueden aprovisionar los usuarios que están solo en la nube directamente desde Workday tooAzure Active Directory utilizando Hola servicio de aprovisionamiento de usuarios de Azure AD.

* **Reescritura de correo electrónico direcciones tooWorkday** -servicio de aprovisionamiento de usuario de hello Azure AD puede escribir seleccionado Azure AD usuario atributos atrás tooWorkday, como la dirección de correo electrónico de Hola.

### <a name="scenarios-covered"></a>Escenarios descritos

los flujos de trabajo compatibles con el servicio de aprovisionamiento de usuarios de Azure AD Hola de aprovisionamiento de usuarios de jornada laboral de Hello habilita la automatización de Hola los escenarios de administración de ciclo de vida de recursos humanos y la identidad siguientes:

* **Contrata a nuevos empleados** : cuando un empleado nuevo se agrega tooWorkday, se creará automáticamente una cuenta de usuario en Active Directory, Azure Active Directory y, opcionalmente, Office 365 y [otras aplicaciones SaaS compatibles con Azure AD ](active-directory-saas-app-provisioning.md), con la escritura de tooWorkday de dirección de correo electrónico de Hola.

* **Actualizaciones de atributos y de perfil de los empleados**: si se actualiza un registro de empleado en Workday (por ejemplo, el nombre, el cargo o el administrador), su cuenta de usuario se actualizará automáticamente en Active Directory, Azure Active Directory y, opcionalmente, en Office 365 y en [otras aplicaciones SaaS compatibles con Azure AD](active-directory-saas-app-provisioning.md).

* **Ceses de empleados**: cuando se prescinde de un empleado en Workday, su cuenta de usuario se deshabilita automáticamente de Active Directory, Azure Active Directory y, opcionalmente, de Office 365 y de [otras aplicaciones SaaS compatibles con Azure AD](active-directory-saas-app-provisioning.md).

* **Volver a contrataciones empleado** : cuando un empleado se rehired en Workday, su cuenta anterior se puede reactivar automáticamente o vuelven a aprovisionar (función de sus preferencias) tooActive Directory, Azure Active Directory y, opcionalmente, Office 365 y [otras aplicaciones SaaS compatibles con Azure AD](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Planeamiento de la solución

Antes de comenzar la integración de Workday, comprobar requisitos previos de Hola a continuación y lectura hello después de obtener información sobre cómo toomatch la arquitectura actual de Active Directory y con los requisitos de aprovisionamiento de usuarios Hola o las soluciones proporcionadas por Azure Active Directorio.

### <a name="prerequisites"></a>Requisitos previos

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción válida a Azure AD Premium P1 con acceso de administrador global
* Un inquilino de implementación de Workday para fines de pruebas y de integración
* Permisos de administrador en Workday toocreate un usuario de integración del sistema y datos de empleados de hacer cambios tootest con fines de prueba
* Para aprovisionamiento tooActive directorio de usuarios, un servidor unido a un dominio con el servicio de Windows 2012 o superior es necesario toohost hello [agente de sincronización local](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) para la sincronización entre Active Directory y Azure AD.

> [!NOTE]
> Si se encuentra el inquilino de Azure AD en Europa, vea hello [problemas conocidos](#known-issues) sección más adelante.


### <a name="solution-architecture"></a>Arquitectura de la solución

Azure AD proporciona un amplio conjunto de toohelp conectores que resolver administración del ciclo de vida de aprovisionamiento y la identidad desde Workday tooActive Directory, Azure AD, aplicaciones de SaaS y más allá de aprovisionamiento. Qué características se va a usar y cómo configurar soluciones de hello variará según el entorno y los requisitos de su organización. Como primer paso, considere existencias de cuántos de los siguientes Hola están presentes e implementada en su organización:

* ¿Cuántos bosques de Active Directory están en uso?
* ¿Cuántos dominios de Active Directory están en uso?
* ¿Cuántas unidades organizativas (UO) de Active Directory están en uso?
* ¿Cuántos inquilinos de Azure Active Directory están en uso?
* ¿Hay usuarios que necesitan toobe aprovisionado tooboth Active Directory y Azure Active Directory (por ejemplo, los usuarios de "híbrido")?
* ¿Hay usuarios que necesitan toobe aprovisionado tooAzure Active Directory, pero no en Active Directory (por ejemplo, los usuarios de "solo en la nube")?
* ¿Tienen direcciones de correo electrónico del usuario toobe reescriben tooWorkday?

Una vez que tenga respuestas toothese preguntas, puede planear su jornada laboral aprovisionamiento implementación siguiente directriz de Hola a continuación.

#### <a name="using-provisioning-connector-apps"></a>Uso de aplicaciones de conectores de aprovisionamiento

Azure Active Directory admite los conectores de aprovisionamiento previamente integrados para Workday y muchas otras aplicaciones SaaS. 

Un solo conector aprovisionamiento interactúa con hello API de un sistema de origen único y ayuda a aprovisionar datos tooa destino único sistema. Mayoría de los conectores aprovisionamiento que admite Azure AD es para un único origen y el sistema de destino (por ejemplo, tooServiceNow de Azure AD) y puede ser el programa de instalación con solo Agregar aplicación hello en cuestión de galería de aplicaciones de Azure AD de hello (p. ej. ServiceNow). 

Hay una relación unívoca entre las instancias de los conectores de aprovisionamiento y las instancias de aplicación en Azure AD:

| Sistema de origen | Sistema de destino |
| ---------- | ---------- | 
| Inquilino de Azure AD | Aplicación SaaS |


Sin embargo, cuando se trabaja con Workday y Active Directory, hay varios toobe de sistemas de origen y de destino considerada:

| Sistema de origen | Sistema de destino | Notas |
| ---------- | ---------- | ---------- |
| Workday | Bosque de Active Directory | Cada bosque se trata como un sistema de destino distinto |
| Workday | Inquilino de Azure AD | Según sea necesario para los usuarios que solo están en la nube |
| Bosque de Active Directory | Inquilino de Azure AD | Actualmente, este flujo está controlado por AAD Connect |
| Inquilino de Azure AD | Workday | Para la reescritura de direcciones de correo electrónico |

toofacilitate estos varios flujos de trabajo toomultiple origen y destino sistemas, Azure AD proporciona varias aplicaciones de conector de aprovisionamiento que puede agregar desde la Galería de aplicaciones de hello Azure AD:

![Galería de aplicaciones de AAD](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **Día de trabajo tooActive el aprovisionamiento de directorio** -esta aplicación facilita el aprovisionamiento de cuentas de usuario Workday tooa único bosque de Active Directory. Si tiene varios bosques, puede agregar una instancia de esta aplicación desde la Galería de aplicaciones de Azure AD de Hola para cada bosque de Active Directory a que necesita tooprovision.

* **Día laborable tooAzure AD aprovisionamiento** -mientras AAD Connect es la herramienta de Hola que debería ser tooAzure a los usuarios de Active Directory toosynchronize usa Active Directory, esta aplicación puede ser usado toofacilitate el aprovisionamiento de usuarios solo en la nube desde Workday tooa único Inquilino de Azure Active Directory.

* **Reescritura WORKDAY** -esta aplicación facilita la reescritura de direcciones de correo electrónico del usuario de Azure Active Directory tooWorkday.

> [!TIP]
> Hola regular "Workday" aplicación se usa para configurar el inicio de sesión único entre los días laborables y Azure Active Directory. 

¿Cómo tooset una copia de seguridad y configurar estas opciones especiales aprovisionamiento de aplicaciones de conector es el asunto de Hola de hello restantes secciones de este tutorial. Qué aplicaciones elija tooconfigure dependerán de qué sistemas necesita tooprovision y cuántos bosques de Active Directory y Azure AD los inquilinos están en su entorno.

![Información general](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Configurar un usuario de integración de sistemas en Workday
Un requisito común de todos los conectores de aprovisionamiento de jornada laboral hello es requieren las credenciales para una cuenta tooconnect toohello API de recursos humanos Workday de jornada laboral sistema integración. Esta sección describe cómo cuenta toocreate integradores de sistemas de jornada laboral.

> [!NOTE]
> Es posible toobypass este procedimiento y en su lugar, use una cuenta de administrador global de jornada laboral como cuenta de sistema de integración de Hola. Puede funcionar correctamente en las demostraciones, pero no se recomienda en las implementaciones de producción.

### <a name="create-an-integration-system-user"></a>Creación de un usuario del sistema de integración

**toocreate un usuario del sistema de integración:**

1. Inicie sesión en su inquilino de Workday usando una cuenta de administrador. Hola **Workday Workbench**, escriba crear usuario en el cuadro de búsqueda de Hola y, a continuación, haga clic en **crear usuario del sistema de integración**. 
   
    ![Creación de usuarios](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Creación de usuarios")
2. Hola completa **crear usuario del sistema de integración** tarea proporcionando un nombre de usuario y una contraseña para un nuevo usuario de sistema de integración.  
 * Deje hello **solicitar una nueva contraseña en el siguiente inicio de sesión** opción no está activada, dado que este usuario iniciará sesión mediante programación. 
 * Deje hello **minutos de tiempo de espera de sesión** con su valor predeterminado de 0, que impide que las sesiones de usuario de hello agote antes de tiempo. 
   
    ![Crear usuario de sistema de integración](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Crear usuario de sistema de integración")

### <a name="create-a-security-group"></a>Creación de un grupo de seguridad
Es necesario toocreate un grupo de seguridad del sistema de integración sin restringir y asignar Hola tooit de usuario.

**toocreate un grupo de seguridad:**

1. Escriba crear grupo de seguridad en el cuadro de búsqueda de hello y, a continuación, haga clic en **crear grupo de seguridad**. 
   
    ![Crear grupo de seguridad](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "Crear grupo de seguridad")
2. Hola completa **crear grupo de seguridad** tarea.  
3. Seleccione un grupo de seguridad de sistema de integración: sin restricciones de hello **tipo de grupo de seguridad con inquilinos** lista desplegable.
4. Crear un toowhich de grupo de seguridad se agregan miembros explícitamente. 
   
    ![Crear grupo de seguridad](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "Crear grupo de seguridad")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Asignar a grupo toohello seguridad de usuario de sistema de integración Hola

**: el usuario del sistema de integración de hello tooassign**

1. Escriba Editar grupo de seguridad en el cuadro de búsqueda de hello y, a continuación, haga clic en **Editar grupo de seguridad**. 
   
    ![Editar grupo de seguridad](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Editar grupo de seguridad")
2. Busque y seleccione Nuevo grupo de seguridad de integración Hola por su nombre. 
   
    ![Editar grupo de seguridad](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Editar grupo de seguridad")
3. Agregar Hola nueva integración sistema usuario toohello nuevo grupo de seguridad. 
   
    ![Grupo de seguridad del sistema](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "Grupo de seguridad del sistema")  

### <a name="configure-security-group-options"></a>Configuración de las opciones del grupo de seguridad
En este paso, se concede toohello nuevo seguridad permisos de grupo para **obtener** y **colocar** operaciones en objetos de hello protegidos por hello siguiendo las directivas de seguridad de dominio:

* External Account Provisioning
* Worker Data: Public Worker Reports
* Worker Data: All Positions
* Worker Data: Current Staffing Information
* Worker Data: Business Title on Worker Profile

**Opciones de grupo de seguridad de tooconfigure:**

1. Escriba las directivas de seguridad de dominio en el cuadro de búsqueda de hello y, a continuación, haga clic en el vínculo de hello **directivas de seguridad de dominio para área funcional**.  
   
    ![Directivas de seguridad de dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Directivas de seguridad de dominio")  
2. La búsqueda de sistema y seleccione hello **System** área funcional.  Haga clic en **Aceptar**.  
   
    ![Directivas de seguridad de dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Directivas de seguridad de dominio")  
3. En la lista Hola de directivas de seguridad para hello área funcional del sistema, expanda **administración de la seguridad** y seleccione la directiva de seguridad de dominio de hello **el aprovisionamiento de cuentas externas**.  
   
    ![Directivas de seguridad de dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Directivas de seguridad de dominio")  
4. Haga clic en **Editar permisos**y, a continuación, en hello **Editar permisos**cuadro de diálogo página, agregue Hola nueva seguridad grupo toohello lista de grupos de seguridad con **obtener** y **Colocar** permisos de integración. 
   
    ![Editar permiso](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Editar permiso")  
5. Repita el paso 1 anterior tooreturn toohello pantalla para seleccionar las áreas funcionales, y en esta ocasión, busque personal, seleccione hello **área funcional de personal** y haga clic en **Aceptar**.
   
    ![Directivas de seguridad de dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Directivas de seguridad de dominio")  
6. En la lista Hola de directivas de seguridad para hello área funcional de personal, expanda **datos del trabajador: personal** y repita el paso 4 anterior para cada una de estas directivas de seguridad restantes:

   * Worker Data: Public Worker Reports
   * Worker Data: All Positions
   * Worker Data: Current Staffing Information
   * Worker Data: Business Title on Worker Profile
   
7. Repita el paso 1, anteriormente, tooreturn toohello pantalla para seleccionar las áreas funcionales y esta vez, busque **información de contacto**, seleccione el área funcional de personal de Hola y haga clic en **Aceptar**.

8.  En la lista Hola de directivas de seguridad para hello área funcional de personal, expanda **datos del trabajador: información de contacto de trabajo**y repita el paso 4 anterior para las directivas de seguridad de Hola a continuación:

    * Worker Data: Work Email (Datos de trabajadores: Correo electrónico de trabajo)

    ![Directivas de seguridad de dominio](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Directivas de seguridad de dominio")  
    
### <a name="activate-security-policy-changes"></a>Activación de cambios en directivas de seguridad

**cambios de directiva de seguridad de tooactivate:**

1. Escriba activar en el cuadro de búsqueda de hello y, a continuación, haga clic en el vínculo de hello **activar cambios de la directiva de seguridad pendientes**. 
   
    ![Activar](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activar") 
2. BEGIN Hola activar cambios de la directiva de seguridad pendientes de tareas, escriba un comentario con fines de auditoría y, a continuación, haga clic en **Aceptar**. 
   
    ![Activar seguridad pendiente](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activar seguridad pendiente")   
3. Tarea de hello completa en la siguiente pantalla de bienvenida activando la casilla de verificación de hello **confirmar**y, a continuación, haga clic en **Aceptar**. 
   
    ![Activar seguridad pendiente](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activar seguridad pendiente")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Configuración de aprovisionamiento de usuarios desde jornada laboral tooActive Directory
Siga estos cuenta de usuario de tooconfigure instrucciones de aprovisionamiento de jornada laboral tooeach bosque de Active Directory que necesite para el aprovisionamiento.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Agregar aplicación de conector de aprovisionamiento de hello y la creación de hello conexión tooWorkday

**tooconfigure Workday tooActive el aprovisionamiento de directorio:**

1.  Vaya demasiado<https://portal.azure.com>

2.  En la barra de navegación izquierda de hello, seleccione **Azure Active Directory**

3.  Seleccione **Enterprise Applications** (Aplicaciones empresariales) y **All Applications** (Todas las aplicaciones).

4.  Seleccione **agregar una aplicación**, seleccione hello y **todos los** categoría.

5.  Busque **tooActive Workday aprovisionamiento directorio**y agregar esa aplicación de galería de Hola.

6.  Después de hello aplicación se ha agregado y se muestra la pantalla de detalles de la aplicación de bienvenida, seleccione **aprovisionamiento**

7.  Hola de cambio **Provisioning** **modo** demasiado**automática**

8.  Hola completa **las credenciales de administrador** sección como sigue:

   * **Administración Username** : escriba el nombre de usuario de Hola de hello cuenta de sistema de integración de Workday, anexado el nombre de dominio de inquilino de Hola. **Debe tener un aspecto similar al siguiente: username@contoso4**

   * **Contraseña de administrador:** escriba una contraseña de cuenta de sistema de integración de Workday Hola Hola

   * **Dirección URL: del inquilino** escriba el extremo de servicios web de hello URL toohello Workday para su inquilino. Esto debería ser similar: https://wd3-impl-services1.workday.com/ccx/service/contoso4, donde contoso4 se sustituye por el nombre del inquilino correcto y wd3 impl se reemplaza con la cadena de entorno correcto de Hola.

   * **Bosques de Active Directory -** Hola "Name" de su bosque de Active Directory, tal como lo devuelve Hola Get-ADForest powershell commandlet. Suele ser una cadena tipo *contoso.com*.

   * **Contenedor de Active Directory -** escriba Hola contenedor cadena que contiene todos los usuarios en el bosque de AD. Ejemplo: *OU=Standard Users,OU=Users,DC=contoso,DC=test*

   * **Correo electrónico de notificación**: escriba su dirección de correo electrónico y marque la casilla "Enviar una notificación por correo electrónico cuando se produzca un error".

   * Haga clic en hello **Probar conexión** botón. Si la prueba de conexión de Hola se realiza correctamente, haga clic en hello **guardar** situado en la parte superior de Hola. Si se produce un error, compruebe que las credenciales de Workday Hola sean válidas en Workday. 

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Parte 2: configuración de las asignaciones de atributos 

En esta sección configurará cómo fluyen los datos de los usuarios de Workday a Active Directory.

1.  En la pestaña de aprovisionamiento de hello en **asignaciones**, haga clic en **tooOnPremises de sincronizar los trabajadores de jornada laboral**.

2.  Hola **el ámbito del objeto de origen** campo, puede seleccionar qué conjuntos de usuarios en Workday deben estar en el ámbito para definir un conjunto de filtros basados en el atributo tooAD, el aprovisionamiento. ámbito de Hello predeterminado es "todos los usuarios en Workday". Filtros de ejemplo:

   * Ejemplo: Scope toousers con Id. de trabajo entre 1000000 y 2000000

      * Atributo: WorkerID

      * Operador: REGEX.COINCIDIR

      * Valor: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Ejemplo: solo los empleados, no los trabajadores temporales 

      * Atributo: EmployeeID

      * Operador: NO ES NULO

3.  Hola **acciones de objeto de destino** campo, todo el mundo puede filtrar qué acciones están permitidas toobe realizada en Active Directory. **Crear** y **Actualizar** son las más habituales.

4.  Hola **asignaciones de atributo** sección, puede definir el modo en que cada día laborable atributos asignan atributos de directorio tooActive.

5. Haga clic en un tooupdate de asignación de atributo existente, o haga clic en **agregar nueva asignación** final Hola de tooadd nuevas asignaciones de pantalla de Hola. Las asignaciones de atributos admiten estas propiedades:

      * **Tipo de asignación**

         * **Direct** : escribe el valor Hola Hola Workday toohello AD atributo, sin cambios

         * **Constante** -escribir un valor de cadena de constantes y estáticas al atributo Hola AD

         * **Expresión** – le permite toowrite un valor personalizado al atributo Hola AD, en función de uno o más atributos de jornada laboral. [Para obtener más información, consulte este artículo sobre las expresiones](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Atributo de origen** -atributo de usuario de Hola desde jornada laboral.

      * **Valor predeterminado**: opcional. Si el atributo de origen de hello tiene un valor vacío, asignación de hello escribirá en su lugar, este valor.
            Configuración más común es tooleave este en blanco.

      * **Atributo de destino** : atributo de usuario de hello en Active Directory.

      * **Coincide con los objetos mediante este atributo** : si no se debe usar esta asignación toouniquely identificar a los usuarios entre los días laborables y Active Directory. Normalmente esto se establece en el campo Id. de trabajo para Workday, que normalmente se asigna a uno de los atributos de identificador de empleado de hello en Active Directory.

      * **Precedencia de coincidencia**: se pueden establecer varios atributos coincidentes. Si hay varios, se evalúan en el orden definido por este campo. En el momento en que se encuentre una coincidencia, no se evaluarán más atributos coincidentes.

      * **Aplicar esta asignación**
       
         * **Siempre**: esta asignación se aplica a las acciones de creación y actualización de usuarios

         * **Solo durante la creación**: esta asignación se aplica solo a las acciones de creación de usuarios

6. Haga clic en las asignaciones de toosave **guardar** en la parte superior de saludo de la sección asignación de atributos.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**A continuación se muestran algunos ejemplos de asignaciones de atributos entre Workday y Active Directory, con algunas expresiones comunes**

-   expresión de Hola que asigna toohello parentDistinguishedName AD atributo puede ser usado tooprovision un tooa usuario OU específica en función de uno o más atributos de origen de jornada laboral. En este ejemplo se coloca a los usuarios en unidades organizativas diferentes en función de los datos de Workday relacionados con sus ciudades.

-   expresión de Hola que se asigna el atributo userPrincipalName AD de toohello crear un UPN de firstName.LastName@contoso.com. También reemplaza los caracteres especiales no válidos.

-   [Aquí encontrará documentación sobre cómo escribir expresiones.](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| ATRIBUTO DE WORKDAY | ATRIBUTO DE ACTIVE DIRECTORY |  ¿IDENTIFICADOR COINCIDENTE? | CREAR / ACTUALIZAR |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **Sí** | Escrito únicamente en Crear | 
|  **Municipality**   |   l   |     | Crear y Actualizar |
|  **Company**         | company   |     |  Crear y Actualizar |
|  **CountryReferenceTwoLetter**      |   co |     |   Crear y Actualizar |
| **CountryReferenceTwoLetter**    |  c  |     |         Crear y Actualizar |
| **SupervisoryOrganization**  | department  |     |  Crear y Actualizar |
|  **PreferredNameData**  |  DisplayName |     |   Crear y Actualizar |
| **EmployeeID**    |  cn    |   |   Escrito únicamente en Crear |
| **Fax**      | facsimileTelephoneNumber     |     |    Crear y Actualizar |
| **Nombre**   | givenName       |     |    Crear y Actualizar |
| **Switch(\[Active\], , "0", "True", "1",)** |  accountDisabled      |     | Crear y Actualizar |
| **Mobile**  |    mobile       |     |       Escrito únicamente en Crear |
| **EmailAddress**    | mail    |     |     Crear y Actualizar |
| **ManagerReference**   | manager  |     |  Crear y Actualizar |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Crear y Actualizar |
| **PostalCode**  |   postalCode  |     | Crear y Actualizar |
| **LocalReference** |  preferredLanguage  |     |  Crear y Actualizar |
| **Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**      |    sAMAccountName            |     |         Escrito únicamente en Crear |
| **Apellidos**   |   sn   |     |  Crear y Actualizar |
| **CountryRegionReference** |  st     |     | Crear y Actualizar |
| **AddressLineData**    |  streetAddress  |     |   Crear y Actualizar |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Escrito únicamente en Crear |
| **BusinessTitle**   |  título     |     |  Crear y Actualizar |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | Crear y Actualizar                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  Crear y Actualizar |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Parte 3: Configurar el agente de sincronización de hello local

En orden tooprovision tooActive directorio local, debe instalarse un agente en un servidor unido a un dominio en el deseo de hello bosque de Active Directory. Administrador de dominio (o administrador empresarial) las credenciales son necesarias para completar el procedimiento de Hola.

**[Puede descargar el agente de sincronización de local de hello aquí](https://go.microsoft.com/fwlink/?linkid=847801)**

Después de instalar el agente, ejecute los comandos de Powershell de hello debajo de agente de hello tooconfigure para su entorno.

**Comando n.º 1**

> cd C:\\Archivos de programa\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent

> import-module AADSyncAgent.psd1

**Comando n.º 2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* Entrada: Como "Nombre de directorio", escriba nombre de bosque de AD de hello, tal y como se especificó parcialmente \#2
* Entrada: nombre y contraseña del usuario administrador del bosque de Active Directory

**Comando n.º 3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* Entrada: nombre y contraseña del usuario administrador global de su inquilino de Azure AD

**Comando n.º 4**

> Get-AdSyncAgentProvisioningTasks

* Acción: se devuelven los datos de confirmación. Este comando detecta automáticamente las aplicaciones de aprovisionamiento de Workday en su inquilino de Azure AD. Salida de ejemplo:

> Nombre: Mi bosque de AD
>
> Habilitado: True
>
> DirectoryName : mydomain.contoso.com
>
> Credenciales: False
>
> Identificador: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Comando n.º 5**

> Start-AdSyncAgentSynchronization -Automatic

**Comando n.º 6**

> net stop aadsyncagent

**Comando n.º 7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Parte 4: Iniciar servicio de Hola
Una vez que se hayan completado las partes 1 a 3, puede iniciar Hola aprovisionamiento del servicio en hello Portal de administración de Azure.

1.  Hola **Provisioning** ficha, conjunto hello **estado de aprovisionamiento** a **en**.

2. Haga clic en **Guardar**.

3. Se iniciará la sincronización inicial hello, que puede tomar un número variable de horas, según el número de usuarios que se encuentran en la jornada laboral.

4. Eventos de sincronización individuales, como los que los usuarios se leen de jornada laboral y, a continuación, se pueden ver posteriormente agregado o actualizado tooActive directorio, en hello **los registros de auditoría** ficha. **[Vea Hola aprovisionamiento a Guía de informes para obtener instrucciones detalladas sobre cómo los registros de auditoría de hello tooread](active-directory-saas-provisioning-reporting.md)**

5.  registro de aplicación de Windows Hello en el equipo del agente de hello mostrará todas las operaciones realizadas a través de agente de Hola.

6. Una vez finalizada la operación, se escribe un informe resumido de auditoría en la pestaña **Aprovisionamiento**, tal y como se muestra a continuación.

![Azure Portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Configurar tooAzure Active Directory de aprovisionamiento de usuarios
Cómo configurar el aprovisionamiento tooAzure Active Directory dependerá de los requisitos de aprovisionamiento, como se detalla en la siguiente tabla se Hola.

| Escenario | Solución |
| -------- | -------- |
| **Los usuarios necesitan toobe aprovisionado tooActive Directory y Azure AD** | Use **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Los usuarios necesidad toobe aprovisionado tooActive directorio solo** | Use **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Los usuarios necesitan toobe aprovisionado tooAzure AD solo (solo en la nube)** | Hola de uso **aprovisionamiento de Active Directory de jornada laboral tooAzure** aplicación en Galería de aplicaciones de Hola |

Para obtener instrucciones sobre cómo configurar Azure AD Connect, consulte hello [documentación de Azure AD Connect](connect/active-directory-aadconnect.md).

Hola las secciones siguientes describe cómo configurar una conexión entre los días laborables y Azure AD tooprovision solo en la nube a los usuarios.

> [!IMPORTANT]
> Siga solo Hola procedimiento si tiene usuarios solo en la nube que necesitan toobe aprovisionado tooAzure AD y no en Active Directory local.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Agregar aplicación de conector de aprovisionamiento de hello Azure AD y la creación de hello conexión tooWorkday

**tooconfigure aprovisionamiento de Active Directory de tooAzure Workday para los usuarios solo en la nube:**

1.  Vaya demasiado<https://portal.azure.com>.

2.  En la barra de navegación izquierda de hello, seleccione **Azure Active Directory**

3.  Seleccione **Enterprise Applications** (Aplicaciones empresariales) y **All Applications** (Todas las aplicaciones).

4.  Seleccione **agregar una aplicación**y, a continuación, seleccione hello **todos los** categoría.

5.  Busque **Workday tooAzure AD aprovisionamiento**y agregar esa aplicación de galería de Hola.

6.  Después de hello aplicación se ha agregado y se muestra la pantalla de detalles de la aplicación de bienvenida, seleccione **aprovisionamiento**

7.  Hola de cambio **Provisioning** **modo** demasiado**automática**

8.  Hola completa **las credenciales de administrador** sección como sigue:

   * **Administración Username** : escriba el nombre de usuario de Hola de hello cuenta de sistema de integración de Workday, anexado el nombre de dominio de inquilino de Hola. Debe tener un aspecto similar al siguiente: username@contoso4

   * **Contraseña de administrador:** escriba una contraseña de cuenta de sistema de integración de Workday Hola Hola

   * **Dirección URL: del inquilino** escriba el extremo de servicios web de hello URL toohello Workday para su inquilino. Esto debería ser similar: https://wd3-impl-services1.workday.com/ccx/service/contoso4, donde contoso4 se sustituye por el nombre del inquilino correcto y wd3 impl se reemplaza con la cadena de entorno correcto de hello (si es necesario).

   * **Correo electrónico de notificación**: escriba su dirección de correo electrónico y marque la casilla "Enviar una notificación por correo electrónico cuando se produzca un error".

   * Haga clic en hello **Probar conexión** botón.

   * Si la prueba de conexión de Hola se realiza correctamente, haga clic en hello **guardar** situado en la parte superior de Hola. Si se produce un error, comprueba que Hola URL Workday y las credenciales son válidas en la jornada laboral.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: configuración de las asignaciones de atributos 

En esta sección configurará cómo fluyen los datos de los usuarios de Workday a Azure Active Directory para los usuarios que solo están en la nube.

1.  En la pestaña de aprovisionamiento de hello en **asignaciones**, haga clic en **tooAzure trabajadores sincronizar AD**.

2.   Hola **el ámbito del objeto de origen** campo, puede seleccionar qué conjuntos de usuarios en Workday deben estar en el ámbito para definir un conjunto de filtros basadas en atributos tooAzure AD, el aprovisionamiento. ámbito de Hello predeterminado es "todos los usuarios en Workday". Filtros de ejemplo:

   * Ejemplo: Scope toousers con Id. de trabajo entre 1000000 y 2000000

      * Atributo: WorkerID

      * Operador: REGEX.COINCIDIR

      * Valor: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Ejemplo: solo los trabajadores temporales, no los empleados habituales

      * Atributo: ContingentID

      * Operador: NO ES NULO

3.  Hola **acciones de objeto de destino** campo, todo el mundo puede filtrar qué acciones están permitidas toobe realizada en Azure AD. **Crear** y **Actualizar** son las más habituales.

4.  Hola **asignaciones de atributo** sección, puede definir el modo en que cada día laborable atributos asignan atributos de directorio tooActive.

5. Haga clic en un tooupdate de asignación de atributo existente, o haga clic en **agregar nueva asignación** final Hola de tooadd nuevas asignaciones de pantalla de Hola. Las asignaciones de atributos admiten estas propiedades:

   * **Tipo de asignación**

      * **Direct** : escribe el valor Hola Hola Workday toohello AD atributo, sin cambios

      * **Constante** -escribir un valor de cadena de constantes y estáticas al atributo Hola AD

      * **Expresión** – le permite toowrite un valor personalizado al atributo Hola AD, en función de uno o más atributos de jornada laboral. [Para obtener más información, consulte este artículo sobre las expresiones](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Atributo de origen** -atributo de usuario de Hola desde jornada laboral.

   * **Valor predeterminado**: opcional. Si el atributo de origen de hello tiene un valor vacío, asignación de hello escribirá en su lugar, este valor.
            Configuración más común es tooleave este en blanco.

   * **Atributo de destino** : atributo de usuario de hello en Azure AD.

   * **Coincide con los objetos mediante este atributo** : si no se debe usar esta asignación toouniquely identificar a los usuarios entre los días laborables y Azure AD. Normalmente esto se establece en el campo Id. de trabajo para Workday, que normalmente se asigna al atributo de Id. de empleado de hello (nuevo) o un atributo de extensión en Azure AD.

   * **Precedencia de coincidencia**: se pueden establecer varios atributos coincidentes. Si hay varios, se evalúan en el orden definido por este campo. En el momento en que se encuentre una coincidencia, no se evaluarán más atributos coincidentes.

   * **Aplicar esta asignación**

     * **Siempre**: esta asignación se aplica a las acciones de creación y actualización de usuarios

     * **Solo durante la creación**: esta asignación se aplica solo a las acciones de creación de usuarios

6. Haga clic en las asignaciones de toosave **guardar** en la parte superior de saludo de la sección asignación de atributos.

### <a name="part-3-start-hello-service"></a>Parte 3: Iniciar servicio de Hola
Una vez que se hayan completado las partes 1 y 2, puede iniciar Hola aprovisionamiento del servicio.

1.  Hola **Provisioning** ficha, conjunto hello **estado de aprovisionamiento** a **en**.

2. Haga clic en **Guardar**.

3. Se iniciará la sincronización inicial hello, que puede tomar un número variable de horas, según el número de usuarios que se encuentran en la jornada laboral.

4. Eventos de sincronización individuales pueden verse en hello **los registros de auditoría** ficha. **[Vea Hola aprovisionamiento a Guía de informes para obtener instrucciones detalladas sobre cómo los registros de auditoría de hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Una vez finalizada la operación, se escribe un informe resumido de auditoría en la pestaña **Aprovisionamiento**, tal y como se muestra a continuación.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Configurar la escritura diferida de tooWorkday de direcciones de correo electrónico
Siga estos reescritura de tooconfigure instrucciones de direcciones de correo electrónico del usuario de Azure Active Directory tooWorkday.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Agregar aplicación de conector de aprovisionamiento de hello y la creación de hello conexión tooWorkday

**tooconfigure Workday tooActive el aprovisionamiento de directorio:**

1.  Vaya demasiado<https://portal.azure.com>

2.  En la barra de navegación izquierda de hello, seleccione **Azure Active Directory**

3.  Seleccione **Enterprise Applications** (Aplicaciones empresariales) y **All Applications** (Todas las aplicaciones).

4.  Seleccione **agregar una aplicación**, a continuación, seleccione hello **todos los** categoría.

5.  Busque **Workday reescritura**y agregar esa aplicación de galería de Hola.

6.  Después de hello aplicación se ha agregado y se muestra la pantalla de detalles de la aplicación de bienvenida, seleccione **aprovisionamiento**

7.  Hola de cambio **Provisioning** **modo** demasiado**automática**

8.  Hola completa **las credenciales de administrador** sección como sigue:

   * **Administración Username** : escriba el nombre de usuario de Hola de hello cuenta de sistema de integración de Workday, anexado el nombre de dominio de inquilino de Hola. Debe tener un aspecto similar al siguiente: username@contoso4

   * **Contraseña de administrador:** escriba una contraseña de cuenta de sistema de integración de Workday Hola Hola

   * **Dirección URL: del inquilino** escriba el extremo de servicios web de hello URL toohello Workday para su inquilino. Esto debería ser similar: https://wd3-impl-services1.workday.com/ccx/service/contoso4, donde contoso4 se sustituye por el nombre del inquilino correcto y wd3 impl se reemplaza con la cadena de entorno correcto de hello (si es necesario).

   * **Correo electrónico de notificación**: escriba su dirección de correo electrónico y marque la casilla "Enviar una notificación por correo electrónico cuando se produzca un error".

   * Haga clic en hello **Probar conexión** botón. Si la prueba de conexión de Hola se realiza correctamente, haga clic en hello **guardar** situado en la parte superior de Hola. Si se produce un error, comprueba que Hola URL Workday y las credenciales son válidas en la jornada laboral.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: configuración de las asignaciones de atributos 


En esta sección configurará cómo fluyen los datos de los usuarios de Workday a Active Directory.

1.  En la pestaña de aprovisionamiento de hello en **asignaciones**, haga clic en **tooWorkday de usuarios de Azure sincronizar AD**.

2.  Hola **el ámbito del objeto de origen** campo, opcionalmente puede filtrar los conjuntos de usuarios de Azure Active Directory deben se sus direcciones de correo electrónico reescrito tooWorkday. ámbito de Hello predeterminado es "todos los usuarios de Azure AD". 

3.  Hola **asignaciones de atributo** sección, puede definir el modo en que cada día laborable atributos asignan atributos de directorio tooActive. Hay una asignación de dirección de correo electrónico de Hola de forma predeterminada. Sin embargo, Hola coincidencia de identificador debe ser toomatch actualizada a los usuarios en Azure AD con sus entradas correspondientes en la jornada laboral. Un método popular coincidente es Id. de trabajo de jornada laboral de toosynchronize Hola o employee ID tooextensionAttribute1-15 en Azure AD y, a continuación, utilice este atributo en usuarios de Azure AD toomatch en Workday.

4.  Haga clic en las asignaciones de toosave **guardar** princip Hola de hello sección asignación de atributos.

### <a name="part-3-start-hello-service"></a>Parte 3: Iniciar servicio de Hola
Una vez que se hayan completado las partes 1 y 2, puede iniciar Hola aprovisionamiento del servicio.

1.  Hola **Provisioning** ficha, conjunto hello **estado de aprovisionamiento** a **en**.

2. Haga clic en **Guardar**.

3. Se iniciará la sincronización inicial hello, que puede tomar un número variable de horas, según el número de usuarios que se encuentran en la jornada laboral.

4. Eventos de sincronización individuales pueden verse en hello **los registros de auditoría** ficha. **[Vea Hola aprovisionamiento a Guía de informes para obtener instrucciones detalladas sobre cómo los registros de auditoría de hello tooread](active-directory-saas-provisioning-reporting.md)**

5. Una vez finalizada la operación, se escribe un informe resumido de auditoría en la pestaña **Aprovisionamiento**, tal y como se muestra a continuación.

## <a name="known-issues"></a>Problemas conocidos

* **Registros en configuraciones regionales europeas de auditoría** : como de versión de Hola de esta versión technical preview, hay un problema conocido con hello [registros de auditoría](active-directory-saas-provisioning-reporting.md) para las aplicaciones de conector de jornada laboral hello no aparecen en hello [deportaldeAzure](https://portal.azure.com) si el inquilino de Azure AD Hola reside en un centro de datos Europea. Próximamente habrá disponible una corrección para este problema. Compruebe si este espacio de nuevo al cabo de hello próximas actualizaciones. 

## <a name="additional-resources"></a>Recursos adicionales
* [Tutorial: configuración del inicio de sesión único entre Workday y Azure Active Directory](active-directory-saas-workday-tutorial.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Pasos siguientes

* [Obtenga información acerca de cómo se registra tooreview y obtener informes sobre el aprovisionamiento de actividad](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
