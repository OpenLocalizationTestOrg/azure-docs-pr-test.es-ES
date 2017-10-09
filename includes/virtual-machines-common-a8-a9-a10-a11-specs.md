

## <a name="deployment-considerations"></a>Consideraciones de la implementación
* **Suscripción de Azure** – toodeploy más que algunas instancias de proceso intensivo, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra. Si usa una [cuenta gratuita de Azure](https://azure.microsoft.com/free/), solo puede usar un número limitado de núcleos de proceso de Azure.

* **Precio y disponibilidad** -tamaños de estas máquinas virtuales se ofrecen solo en nivel de precios estándar Hola. Compruebe [Productos disponibles por región] (https://azure.microsoft.com/regions/services/) para ver la disponibilidad en regiones de Azure. 
* **Cuota de núcleos** : tendrá que tooincrease cuota de núcleos de hello en su suscripción de Azure desde el valor predeterminado de Hola. La suscripción también puede limitar el número de Hola de núcleos que se puede implementar en ciertas familias de tamaño de máquina virtual, incluyendo Hola H-series. aumentar una cuota de toorequest, [abrir una solicitud de soporte al cliente en línea](../articles/azure-supportability/how-to-create-azure-support-request.md) sin cargo. (Los límites predeterminados pueden variar según la categoría de suscripción).
  
  > [!NOTE]
  > Si tiene necesidades de capacidad a gran escala, póngase en contacto con el soporte técnico de Azure. Las cuotas de Azure son límites de crédito, no garantías de capacidad. Independientemente de la cuota, solamente se le cobrarán los núcleos que use.
  > 
  > 
* **Red virtual** : Azure [red virtual](https://azure.microsoft.com/documentation/services/virtual-network/) es toouse no requiere instancias de proceso intensivo de Hola. Sin embargo, para muchas de las implementaciones también tiene al menos una red virtual Azure basada en la nube, o una conexión de sitio a sitio si necesita tooaccess recursos locales. Cuando sea necesario, cree una nueva red virtual instancias de hello toodeploy. No se admite la adición de red virtual de tooa de las máquinas virtuales de proceso intensivo en un grupo de afinidad.
* **Cambiar el tamaño de** – debido a su hardware especializado, solo se pueden cambiar las instancias de proceso intensivo en hello mismo tamaño familia (H-series o de proceso intensivo serie a). Por ejemplo, solo se puede cambiar una máquina virtual de serie H de una serie de H tamaño tooanother. Además, no se admite el cambio de tamaño de un tamaño de proceso intensivo de tooa de tamaño de proceso intensivo.  
