---
title: aaaDelegating ofrece en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooput otras personas a encargar de crear ofertas y suscribirse a los usuarios."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a>Delegación de ofertas en Azure Stack

Como operador de nube de Azure pila hello, a menudo es conveniente tooput otras personas a encargar de crear ofertas y suscribirse a los usuarios. Por ejemplo, si es un proveedor de servicios y desea toosign de distribuidores de clientes y administrarlos en su nombre. También puede ocurrir en una empresa si forma parte de un grupo de TI central y desea divisiones o subsidiarias toosign configurar usuarios sin intervención del usuario.

La delegación ayuda a estas tareas, que ayudan a tooreach y administrar más usuarios sería capaz de toodo directamente. Hello en la ilustración siguiente se muestra un nivel de delegación, pero la pila de Azure es compatible con varios niveles. Proveedores de delegado a su vez pueden delegar tooother proveedores, los niveles de toofive.

![](media/azure-stack-delegated-provider/image1.png)

Los operadores de nube de Azure pila pueden delegar la creación de hello de usuarios tooother ofertas y los inquilinos mediante la funcionalidad de delegación de Hola.

## <a name="roles-and-steps-in-delegation"></a>Roles y pasos de la delegación
delegación de toounderstand, tenga en cuenta que hay tres roles implicados:

* Hola **operador nube** administra la infraestructura de la pila de Azure de hello, crea una plantilla de oferta y delegados de otros usuarios para ofrecer a los usuarios de tootheir.
* Hello en la nube delegados administradores se denomina **delegado proveedores**. Pertenezcan tooother organizaciones (por ejemplo, otros inquilinos de Azure Active Directory).
* **Los usuarios** suscribirse a ofertas de Hola y usarlas para administrar sus cargas de trabajo, crear máquinas virtuales, almacenamiento de datos, etcetera.

Como se muestra en el siguiente gráfico de hello, hay dos pasos para configurar la delegación.

1. **Identificar los proveedores de hello delegada** suscribiéndose a tooan oferta basado en un plan que contiene solo el servicio de suscripciones Hola.
   Los usuarios que se suscriben toothis oferta adquirir algunas de las capacidades del Administrador de la nube de hello, incluidos Hola capacidad tooextend ofertas y usuarios de inicio de sesión para disfrutar de ellos.
2. **Delegado una oferta toohello delegado proveedor**, esta oferta funciona como una plantilla para qué Hola proveedor delegado puede ofrecer. Hello proveedor delegado es ahora tootake capaz de hello oferta, elija un nombre para ella (pero no cambiar sus servicios y cuotas) y ofrecen toocustomers.

![](media/azure-stack-delegated-provider/image2.png)

tooact como proveedores de delegados, los usuarios necesitan tooestablish una relación con el proveedor principal de hello; en otras palabras, deben toocreate una suscripción. En este escenario, esta suscripción identifica los proveedores de delegado como si tuviera derecho toopresent ofrece en nombre de proveedor principal de Hola Hola.

Una vez establecida esta relación, operador de hello en la nube puede delegar un proveedor de la oferta de toohello delegados. Hello proveedor delegado es ahora tootake capaz de hello oferta, cámbiele el nombre (pero no cambiar su sustancia) y ofrecen tooits clientes.

Hola las secciones siguientes describe cómo delegar una oferta tooestablish un proveedor de delegados y compruebe que los usuarios pueden suscribirse para él.

## <a name="set-up-roles"></a>Configurar los roles

toosee un proveedor de delegado en el trabajo, necesita cuentas de Azure Active Directory adicionales en la cuenta de operador de suma tooyour en la nube. Si no los tiene, cree Hola dos cuentas. las cuentas de Hello pueden pertenecer a tooany inquilino de AAD. Nos referimos toothem como Hola había delegada proveedor (DP) y el usuario de Hola.

| **Rol** | **Derechos organizativos** |
| --- | --- |
| Proveedor delegado |Usuario |
| Usuario |Usuario |

## <a name="identify-hello-delegated-providers"></a>Identificar los proveedores de hello delegada
1. Inicie sesión como operador en la nube.
2. Crear una oferta de Hola que permite a los usuarios toobecome delegado proveedores. Esto requiere la creación de un plan y una oferta basada en este:
   
   a.  [Cree un plan](azure-stack-create-plan.md).
       Este plan debe incluir solo el servicio de suscripciones Hola. En este artículo, se usa un plan denominado PlanForDelegation.
   
   b.  [Cree una oferta](azure-stack-create-offer.md) en función de este plan. En este artículo, usamos una oferta denominada OfferToDP.
   
   c.  Una vez completada la creación de hello de oferta de hello, agregar proveedor delegados de hello como una oferta de toothis de suscriptor, haga clic en **suscripciones** &gt; **agregar** &gt; **nuevo Suscripción de inquilino**.
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> Como con todas las ofertas de pila de Azure, tiene la opción de Hola de hacer que la oferta de hello públicas y permitiéndole usuarios suscribirse a él o mantener privado y tienen operador en la nube de hello administrar Hola inicio de sesión. Proveedores de delegados suelen ser un pequeño grupo y desea toocontrol que se admitan tooit, por lo que mantener esta oferta privada tiene sentido en la mayoría de los casos.
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a>Operador de nube crea Hola delegados oferta

Ya ha establecido su proveedor delegado. paso siguiente Hola consiste en Crear plan de Hola y ofrecer que se van toodelegate y que utilizarán los clientes. Debe definir esta oferta exactamente como desea que los clientes toosee, porque Hola delegada proveedor no podrá cambiar los planes de Hola y las cuotas que incluye.

1. Como operador en la nube, [cree un plan](azure-stack-create-plan.md) y [una oferta](azure-stack-create-offer.md) basada en él. En este artículo, usamos una oferta denominada DelegatedOffer.
   
   > [!NOTE]
   > Esta oferta no tiene toobe público. Se pueda hacer público si elige pero, en la mayoría de los casos, solo desea delegados proveedores toohave acceso tooit. Una vez delegar una oferta privada como se describe en los pasos de hello, proveedor delegados hello tiene acceso tooit.
   > 
   > 
1. Oferta de Hola de delegado. TooDelegatedOffer y, en el panel de configuración de hello, haga clic en **delegado proveedores** &gt; **agregar**.
2. Seleccionar suscripción del proveedor de hello delegada de cuadro de lista desplegable de Hola y haga clic en **delegado**.

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a>Proveedor de delegado personaliza oferta Hola

Inicie sesión en toohello **portal del inquilino** como Hola delega el proveedor y crear una oferta nueva con hello delegados oferta como una plantilla.

1. Haga clic en **Nueva** &gt; **Ofertas + Planes de inquilinos** &gt; **Oferta**.

    ![](media/azure-stack-delegated-provider/image5.png)


1. Asignar una oferta de toohello nombre. Aquí elegiremos ResellerOffer. Seleccione Hola delegado toobase de oferta en y, a continuación, haga clic en **crear**.
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > Nota Hola diferencia en comparación con creación de toooffer igual que las experimentadas por el operador de hello en la nube. proveedor de delegados de Hello no construye Hola oferta de planes de base y complemento; solo pueden elegir de ofertas que se han delegado toothem y no se puede realizar cambios toothose ofertas.

1. Hacer Hola ofrecen público haciendo clic en **examinar** &gt; **ofrece**, seleccionar la oferta de Hola y haga clic en **cambio de estado**.
2. proveedor delegado Hello expone estas ofertas a través de su propio portal de dirección URL. Estas ofertas son visibles solo a través de portal de hello delegada. toofind y cambiar esta dirección URL:
   
    a.  Haga clic en **examinar** &gt; **más servicios** &gt; **suscripciones** &gt; Hola seleccione delegada suscripción del proveedor, en nuestro caso su *DPSubscription* &gt; **propiedades**.
   
    b.  Copie Hola portal URL tooa ubicación independiente, como el Bloc de notas.
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   Ahora ha completado la creación de hello de una oferta delegada como un proveedor de delegado. Cierre la sesión como Hola proveedor delegado. Cerrar la pestaña de explorador Hola que ha utilizado.

## <a name="sign-up-for-hello-offer"></a>Suscríbase a Hola oferta
1. En una nueva ventana del explorador, vaya portal delegados toohello dirección URL que guardó en el paso anterior de Hola. Inicie sesión en el portal de toohello como usuario. Nota: Hola Use delegados portal para este paso. oferta delegados de Hello no son visibles en caso contrario.
2. En el panel de hello, haga clic en **obtener una suscripción**. Verá que sólo proporciona Hola delegado creado por el proveedor de hello delegada se presenta toohello usuario:

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

Esto concluye el proceso de Hola de delegación de la oferta. usuario de Hello ahora puede registrarse en esta oferta obteniendo una suscripción para ella.

## <a name="multiple-tier-delegation"></a>Delegación de varios niveles

Delegación de varios niveles permite Hola delegada proveedor toodelegate las entidades de tooother de oferta. Esto permite, por ejemplo, creación de hello de canales de reseller un poco más, en el que hello proveedor administra Azure pila delega un distribuidor de tooa oferta, que a su vez delega tooreseller.
Pila de Azure es compatible con los niveles de toofive de delegación.

toocreate varios niveles de ofrecen la delegación, proveedor delegados Hola delega a su vez toohello siguiente proveedor de oferta de Hola. proceso Hello es Hola igual para proveedor delegados de Hola igual que con el operador de hello en la nube (consulte [operador en la nube crea Hola delegados oferta](#cloud-operator-creates-the-delegated-offer)).

## <a name="next-steps"></a>Pasos siguientes
[Aprovisionar una máquina virtual](azure-stack-provision-vm.md)

