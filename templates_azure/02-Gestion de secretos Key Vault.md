# Plantilla: Gestión de Secretos Key Vault

## 1. Descripción general

La plantilla **Gestión de Secretos Key Vault** permite crear o listar secretos almacenados en un Azure Key Vault existente. Su objetivo es facilitar la gestión de información sensible desde el IDP, centralizando las operaciones sobre secretos sin necesidad de realizar manualmente cada acción desde el portal de Azure.

Los secretos pueden contener información confidencial utilizada por aplicaciones, servicios y procesos de automatización, como contraseñas, cadenas de conexión, tokens y claves de acceso.

La plantilla cuenta con dos etapas principales: **Configuración** y **Review**. Después de confirmar los datos, el IDP ejecuta la acción seleccionada y presenta el resultado de la operación.

### 2. Paso 1. Configuración
![2. Paso 1. Configuración](../assets/create_azure/keyvault3.png)


En esta primera pantalla se selecciona la operación que se desea realizar y se proporcionan los datos necesarios para identificar el Key Vault y el secreto.

### Campos disponibles

**Acción**

Campo obligatorio que permite seleccionar la operación que se ejecutará. En la interfaz se observa la opción `Crear secreto`. La plantilla contempla operaciones relacionadas con la creación y el listado de secretos. Los campos y las acciones que se ejecutan pueden variar según la opción seleccionada.

**Nombre del Key Vault**

Campo obligatorio donde se introduce el nombre del Azure Key Vault existente en el que se realizará la operación.

Ejemplo: `prueba-periferia30`.

Es importante indicar el nombre correcto del almacén de secretos y verificar que se encuentre disponible en la suscripción de Azure correspondiente.

**Nombre del Secreto**

Campo obligatorio que identifica el secreto que se desea crear o consultar.
Según la indicación de la interfaz, el nombre debe contener únicamente letras, números y guiones.
Ejemplo: `prueba`.
Se recomienda utilizar nombres descriptivos que permitan identificar la finalidad del secreto sin exponer información confidencial.

**Valor del Secreto**

Campo obligatorio para introducir el valor que se almacenará cuando se selecciona la acción de creación. Puede contener una contraseña, una cadena de conexión, un token u otro dato sensible requerido por una aplicación.


### Procedimiento

1. Selecciona la acción que deseas ejecutar.
2. Introduce el nombre del Key Vault existente.
3. Especifica el nombre del secreto.
4. Si la acción seleccionada es `Crear secreto`, introduce el valor que deseas almacenar.
5. Verifica que los datos sean correctos.
6. Selecciona **Review** para continuar.


### 3. Paso 2. Review
![3. Paso 2. Review](../assets/create_azure/keyvault1.png)


Después de completar la configuración, se presenta una pantalla de revisión con el resumen de los datos ingresados.

En el ejemplo de creación se muestran los siguientes campos:

- **Acción:** `Crear secreto`.
- **Nombre del Key Vault:** `prueba-periferia30`.
- **Nombre del Secreto:** `prueba`.
- **Valor del Secreto:** aparece enmascarado mediante asteriscos.

Esta pantalla permite verificar la información antes de ejecutar la operación. El enmascaramiento del valor ayuda a evitar su exposición visual durante la revisión.

### Procedimiento

1. Revisa la acción seleccionada.
2. Confirma el nombre del Key Vault.
3. Verifica el nombre del secreto.
4. Comprueba que el valor se haya ingresado correctamente, sin intentar exponerlo en pantalla.
5. Si necesitas modificar algún dato, selecciona **Back** para regresar a la configuración.
6. Si toda la información es correcta, selecciona **Create** para ejecutar la operación.

**Importante:** antes de crear el secreto, confirma que el Key Vault y el nombre seleccionado sean los correctos. Un error en estos datos puede provocar que la información se almacene en un lugar distinto al esperado.

### 4. Paso 3. Resultado de la ejecución
![4. Paso 3. Resultado de la ejecución4.](../assets/create_azure/keyvault.png)

Una vez seleccionada la opción **Create**, el IDP muestra la pantalla de ejecución de la plantilla.

Cuando la operación termina correctamente, se presenta el mensaje **Operación completada**, junto con información general de la ejecución:

- **Key Vault:** identifica el almacén sobre el que se realizó la operación.
- **Acción:** indica la operación ejecutada, por ejemplo, `crear`.
- **Flujo de ejecución:** muestra los pasos que se ejecutaron y su estado.
- **Logs:** permiten consultar los mensajes generados durante el proceso.


### 5. Consideraciones finales

La plantilla Gestión de Secretos Key Vault facilita la creación y consulta de secretos desde el IDP, integrando estas operaciones en un flujo guiado y con una pantalla de revisión previa.

Antes de utilizarla, es necesario verificar el almacén de destino, la acción seleccionada y los permisos requeridos. Después de ejecutarla, se debe comprobar el resultado mediante el estado de la operación, los logs y, cuando corresponda, la validación del secreto en Azure Key Vault.