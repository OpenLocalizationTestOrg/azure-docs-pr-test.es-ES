## <a name="deployment-considerations"></a>Consideraciones de la implementación

* Para ver la disponibilidad de máquinas virtuales de la serie N, consulte [Productos disponibles por región](https://azure.microsoft.com/en-us/regions/services/).

* Máquinas virtuales de serie N solo pueden implementarse en el modelo de implementación del Administrador de recursos de Hola.

* Al crear una máquina virtual de N-series mediante Hola portal de Azure, en hello **Fundamentos** hoja, seleccione un **tipo de disco de máquina virtual** de **HDD**. tamaño de toochoose una serie de N disponible, en hello **tamaño** hoja, haga clic en **todas las ver**.

* Las máquinas virtuales de la serie N no admiten discos de máquina virtual que estén respaldados por Azure Premium Storage.

* Si desea toodeploy máquinas virtuales una cantidad mayor de N-series, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra. Si usa una [cuenta gratuita de Azure](https://azure.microsoft.com/free/), solo puede usar un número limitado de núcleos de proceso de Azure.

* Podría necesita cuota de núcleos de hello tooincrease (por región) en su suscripción de Azure y aumentar la cuota independiente de Hola para NC o NV núcleos. aumentar una cuota de toorequest, [abrir una solicitud de soporte al cliente en línea](../articles/azure-supportability/how-to-create-azure-support-request.md) sin cargo. Los límites predeterminados pueden variar según la categoría de suscripción.

* Una imagen de máquina virtual que se puede implementar en máquinas virtuales de serie de N es hello [Azure Data Science Virtual Machine](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Hola Data Science Virtual Machine preinstala y configura muchas ciencia de datos muy popular y profunda herramientas de aprendizaje. También preinstala controladores de GPU de NVIDIA Tesla para instancias de NC.





