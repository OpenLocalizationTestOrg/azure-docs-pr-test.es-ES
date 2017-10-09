


## <a name="tagging-a-virtual-machine-through-templates"></a>Etiquetado de una máquina virtual mediante plantillas
En primer lugar, veamos el etiquetado a través de plantillas. [Esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) coloca las etiquetas en hello recursos siguientes: proceso (Máquina Virtual), almacenamiento (cuenta de almacenamiento) y red (dirección IP pública, red Virtual e interfaz de red). Esta plantilla es para una máquina virtual Windows, pero se puede adaptar a máquinas virtuales Linux.

Haga clic en hello **implementar tooAzure** botón de hello [vínculo plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Esto le remitirá toohello [portal de Azure](https://portal.azure.com/) donde puede implementar esta plantilla.

![Implementación sencilla con etiquetas](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Esta plantilla incluye Hola siguientes etiquetas: *departamento*, *aplicación*, y *creado por*. Puede agregar o modificar estas etiquetas directamente en la plantilla de hello si desea que los nombres de etiqueta distinto.

![Etiquetas de Azure en una plantilla](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Como puede ver, etiquetas de Hola se definen como pares de clave/valor, separados por dos puntos (:). Hola etiquetas deben definirse en este formato:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Guarde el archivo de plantilla de hello cuando termine de editar con etiquetas de Hola de su elección.

Después, en hello **editar parámetros** sección, puede rellenar los valores de hello para las etiquetas.

![Editar etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Haga clic en **crear** toodeploy esta plantilla con los valores de etiqueta.

## <a name="tagging-through-hello-portal"></a>Etiquetado a través del Portal de Hola
Después de crear los recursos con etiquetas, puede ver, agregar y eliminar etiquetas en el portal de Hola.

Hola seleccione etiquetas icono tooview etiquetas:

![Icono de etiquetas en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Agrega una nueva etiqueta a través del portal de hello mediante la definición de su propio par clave/valor y guárdelo.

![Agregar etiqueta nueva en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

La nueva etiqueta debería aparecer ahora en la lista de Hola de etiquetas para el recurso.

![Etiqueta nueva guardada en el Portal de Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

