_Manual de uso comercial y para uso interno de comprension para los colaboradores_

se realizara recorrido de seccion por seccion de la vista general del IDP y se anota paso a paso de como funciona cada seccion (si se requiere)

## seccion HOME

![vista principal - Home](assets/home/home-image.png)

Es una seccion de vista general del IDP. en este, se pueden ver novedades que se tengan de los. En este se pude observar un resumen de las secciones. Se tiene aprobaciones para que se enlace directamente desde acaa por si las microservicios la


## seccion Catalog

![Vista principal - Catalog](assets/catalog/catalog-image.png)

En esta seccion se enlista todos los componentes ya creados. se ve propiedades de NAME SYSTEM OWNER TYPE LIFECYCLE DESCRIPTION 

### NAME
#### Overview

![Vista General de componente - Catalog](assets/catalog/overview-component-image.png)


Al seleccionar 'NAME', muestra una vista general del componente/servicio seleccionado. En sus propiedades muestra la opcion para ir al origen y ver documentacion.

#### CI/CD

![seccion CI/CD - Catalog](assets/catalog/catalog-CICD-view-image.png)

En el apartado de CI/CD se visualiza las ejecuciones de pipelines dentro de la plataforma en la que se encuentre el componente. Es necesario tener una anotacion del componente si se quiere habilitar CI/CD en el componente

#### DORA

![seccion DORA - Catalog](assets/catalog/catalog-DORA-view-image.png)

Este Apartado muestra las metricas DORA que se tiene en el monitoreo de este proyecto. separado en las 4 metricas principales (_Deployment Frequency_, _Lead Time for Changes_, _Change Failure Rate_, _Time to Restore Service_)

#### API

![Vista de APIs - Catalog](assets/catalog/catalog-API-view-image.png)

En esta seccion muestra un resumen de consumos de API por parte del componente. Se encuentra separado por dos resumenes. APIs aprovisionadas y APIs Consumidas

Seleccionar una API mostrara los detalles (OVERVIEW) de la misma.

##### Overview de API - Catalog

![Overview de API - Catalog](assets/catalog/catalog-API-view-selecion-API-image.png)

En esta vista se ven las propiedades de la API y a componente esta conectada en **Relations**

##### Definition de API - Catalog

![Definition de API - Catalog](assets/catalog/catalog-API-view-definition-API-image.png)

En la seccion 'DEFINITION' de la vista API dentro de catalog, se muestra la salud de la API relacionada a el componente seleccionado en Catalog. Se muestra tanto la vitsa de OpenAPI y RAW: 

![Definition de API - RAW - Catalog](assets/catalog/catalog-API-view-definition-API-RAW-image.png)


### ACTIONS

En 'ACTIONS' IDP permite ser redirigido a el recurso en si de forma directa ya sea que este en Azure o AWS

Seleccionar un elemento que se tenga en el catalog dara una vista avanzada con propiedades del mismo. en esta vista tambien se tienen las acciones que redirigen a el recurso en si en la plataforma que se encuentre:

![Vista propiedades catalog](assets/catalog/properties-view-catalog-item-image.png)

## seccion APIs

![Vista principal - APIs](assets/APIs/main-view-APIs-image.png)

La seccion de APIs es una vista general que se tiene de las APIs que se tengan activas. se puede ver en que plataforma esta, quien es el dueño, su tipo, de que ambiente consiste o que parte de SDLC pertenece, tags y en la columna ACTIONS es para ver o editar la API ya de forma directa en la plataforma que se encuentra

Seleccionar un elemento que se tenga en el catalog dara una vista avanzada con propiedades del mismo. en esta vista tambien se tienen las acciones que redirigen a el recurso en si en la plataforma que se encuentre:


![Vista propiedades APIs](assets/APIs/properties-view-APIs-item-image.png)

## seccion Docs



## seccion Resources

## seccion aprobaciones

![Vista pricipal aprobaciones](assets/approvals/main-view-approvals-image.png)

## section notificaciones

## seccion create

![vista incial seccion create](assets/create/AWS-S3-bucket/create-image1.png)

En esta seccion se tienen los templates disponibles para la aplciacion de infraestructura que ofrece IDP. En azure se puede observar cada recuso que puede desplegar en cada template y se visualiza en cada una de las tarjetas de esta vista: 

![vista tarjetas de servicios azure](assets/create/AWS-S3-bucket/create-azure-image.png)


Para AWS se tiene centralizado todos los servicios que puede instanciar IDP en una sola tarjeta:

![vista tarjetas de servicios AWS](assets/create/AWS-S3-bucket/create-AWS-image.png)

seleccionando es opcion se pide seleccionar el tipo de recurso y este lo redirija a el asistente correspondiente: 

### AWS S3 Bucket

Esta opcion genera el bucket en AWS, su stack de Terraform en el repo IaC (GitHub o AWS CodeCommit, dev/qa/prod) y hace push. Cada bucket tiene carpeta y state propios.

#### paso 1: Origen de repositorios
##### Repositorio IaC en CodeCommit

En el primer paso se solicita relacionar la region de ubicacion del Repositorio IaC dentro de CodeCommit

![Repositorio IaC en CodeCommit](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-CodeCommit-Repo-Loc-image.png)

##### Plantillas Terraform en CodeCommit

Ademas, se debe indicar la region donde se encuentra ubicado el repositorio con el template terraform dentro de AWS:

![Plantillas Terraform en CodeCommit](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-terraform-template-CodeCommit-Repo-Loc-image.png)

_para pasar al siguiente paso, selecionar 'next'_

#### paso 2: Configuracion general

En este paso se indica propiedades adicionales al bucket. Se relzaiona un nombre el ambiente que se requere. Dependiendo del ambiente, IDP asignara de forma automatica un prefijo dependiendo de que ambiete se haya seleccionado 




![vista Configuracion general](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-general-configuration-image.png)

para pasar al siguiente paso, selecionar 'PREVIEW'

#### paso 3: Review

En esta vista, es un resumen de lo indicado en pasos anteriores y que mas propiedades va a tener el bucket a crear

![vista resumen creacion bucket](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-preview-image.png)

_para hacer que la utilidad proceda se selecciona 'CREATE'


### AWS S3 Bucket — Actualizar

Esta opcion es para realizar modifiacion en un bucket de S3 ya existente. Hace cambios en el versionado, la visibilidad e cifrado del bucket usando stack Terraform en un repo IaC. Al Hacer push, por medio de  GitHub Actions, aplica solo ese stack. 

#### paso 1: Origen del repositorio IaC

en el paso uno se debe indicar la region donde esta ubicado el repositorio IaC en CodeCommit del stack de terraform

![vista paso 1 indicar origen stack](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-terraform-stack-location-image.png)

#### Paso 2: Bucket a actualizar

En este paso, se selacciona el bucket a modificar de la lista desplegable y se permite modificar los datos que se ven en el formulario (Nombre del bucket - editable, visibilidad activar versionado cifrado del bucket y algun identifcador unico en caso de ser necesario.)

![vista paso 2 actualizar bucket](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-update-bucket-view-image.png)





## section tech radar