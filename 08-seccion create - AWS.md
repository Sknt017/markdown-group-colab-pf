## seccion create - desplegar recurso AWS

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

_para hacer que la utilidad proceda se selecciona 'CREATE'_


### AWS S3 Bucket — Actualizar

Esta opcion es para realizar modifiacion en un bucket de S3 ya existente. Hace cambios en el versionado, la visibilidad e cifrado del bucket usando stack Terraform en un repo IaC. Al Hacer push, por medio de  GitHub Actions, aplica solo ese stack. 

#### paso 1: Origen del repositorio IaC

al continuar con el asistente, en el paso uno, se debe indicar la region donde esta ubicado el repositorio IaC en CodeCommit del stack de terraform

![vista paso 1 indicar origen stack](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-terraform-stack-location-image.png)

#### Paso 2: Bucket a actualizar

En este paso, se selacciona el bucket a modificar de la lista desplegable y se permite modificar los datos que se ven en el formulario (Nombre del bucket - editable, visibilidad activar versionado cifrado del bucket y algun identifcador unico en caso de ser necesario.)

![vista paso 2 actualizar bucket](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-update-bucket-view-image.png)

#### Paso 3: Review

Ya para confirmar los cambios, se muestra una vista previa de lo anotado en los pasos anteriores para realizar el cambio.

![vista paso 3 revision previa a aplicar](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-update-review-image.png)

### AWS S3 Bucket - Eliminar

#### Paso 1: Origen del repositorio IaC

Esta accion realiza una eliminacion de bucket en AWS y marca el stack en el repo IaC como eliminado. Los archivos Terraform se conservan como traza (`DELETED.md`).

![vista paso 1 - AWS S3 Bucket - Eliminar](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-delete-image.png)

#### Paso 2: Bucket a eliminar

En este paso, se selecciona el bucket de S3 de la lista que se encontro en la region indicada en el paso anterior. se solicita confirmar el nombre y el motivo es opcional.

![vista paso 2 - AWS S3 Bucket - Eliminar](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-delete-select-bucket-image.png)

#### Paso 3: review

Antes de proceder con la eliminacion, se genera una vista general de lo que se va a hacer por parte de IDP

![vista paso 3 - AWS S3 Bucket - Eliminar](assets/create/AWS-S3-bucket/create-AWS-S3-bucket-delete-review-image.png)

### Lambda Function 

En esta accion, se crea la función Lambda en AWS desde cero, esquema o imagen ECR. genera el stack Terraform en el repo IaC (GitHub o CodeCommit) y se seleccion como entregar el codigo: repo+pipeline, zip en S3 o manual (CLI/consola).

#### Paso 1: Origen de repositorios

En el paso 1, se solicita indicar la region en donde se necesita tener la Lambda function

![vista de paso 1: ubicacion del repositorio IaC](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-repo-source-image.png)

#### Paso 2: Informacion basica

En este paso, se debe seleccionar un metodo de creacion. se tienen tres formas:

![vista paso 2 - opciones de creacion](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-details-image.png)


- **crear desde cero:** Ejecucion en la consola AWS «Crear función»: desde cero (Hello World y runtime). Se debe indicar nombre de la funcion, Que version y lenguaje de programacioin de necesita usar (ver lista desplegable), el Handler. si se requiere configuracion adicional. La configuracion por defecto es:
  - memoria: 256 MB 
  - timeout 30s 
  - arquitectura x86_64
  - sin VPC
  - sin capas ni DLQ. 
  - Si se selecciona aplicar configuracion adicional, se mostrara las opciones a configurar:
  ![Vista paso 2 - configuracion avanzada de VM](assets/create/AWS-Lambda-Function/create-AWS-Lambda-function-details-advanced-config-image.png)

- **usar un esquema**: Es elige un blueprint, el runtime y la arquitectura quedan fijados por el esquema (la arquitectura se puede cambiar en configuración adicional).



![vista paso 2 seleccionar un esquema - lambda function](assets/create/AWS-Lambda-Function/create-AWS-lamda-function-details-sel-scheme-image.png)

- **imagen de contenedor**: crea un contenedor ECR (URI + examinar repositorios). 


Se debe indicar el origen del codigo (repo, S3 o manual) solo aplica a zip; con imagen ECR no hace falta.

![vista paso 2 imagen de contenedor - lambda function](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-details-container-image-image.png)

Se muestra para añadir una descripccion (opcional).

Se solicita donde se necesita el condigo despues de crear:

![vista paso 2 - ubicacion final del codigo](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-details-code-loc-demployment-image.png)

- **Repo fn-{nombre} + pipeline — push empaqueta zip y despliega:** Sube el codigo a un repo y genera su pipeline de empaquetado y despliegue

- **Artefacto zip en S3 — subir function.zip al bucket y desplegar:** se debie indicar bucket de S3 a donde se necesita subir, algun prefijo o carpeta que este o se necesite en el bucket y luego despliega. Solo se debe mencionar el nombre de carpeta o subcarpetas. la vista con esta seleccion indica el destino de la lambda 

![vista paso 2 - artefacto subir como ZIP a S3](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-details-zip-artifact-image.png)

- **Sin automatizacion — actualizar codigo por CLI o consola AWS**

Se indica la estrategia Git necesaria: 

- **Gitflow**: se crea en el ambiente necesario (se confirma mas adelante) separando .env
- **Trunk-based**: se genera un pipeline único sobre rama main con 3 stages para el deploy. 

En cada caso se confirma como se vera la estructura, sus prefijos y politicas.

Al finalizar este paso, se indica en que ambiente sea necesario: 

![vista paso 2 ambiete solicitado - crear lambda function](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-details-environment-required-image.png)

#### Paso 3: Review

Se muestra un resumen de lo que se recibio y lo que se va a realizar.

![Vista paso 3 - Lambda function](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-review-image.png)

### Lambda — Preview efímero por PR (existente)
#### paso 1: Origen de repositorios

![vista paso origen de repos - preview efimero por pr](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-ephemeral-code-source-image.png)

En esta seleccion se habilita una preview por PR en una Lambda ya desplegada (ya sea GitHub o CodeCommit). Al abrir/actualizar un Pull Request compila el código de la rama y despliega a `{fuente}-eph-{pr-id}`. 

Al cerrarse el pull request, se destruye la Lambda efímera. Requiere idp-code-source=repo-pipeline, s3-artifact o container-image (no manual).

#### paso 2: Lambda existente y preview por PR

![vista paso 2 lambda existete pr Lambda — Preview efímero por PR](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-ephemeral-details-image.png)

en este paso, se debe seleccionar la estrategia git del repo

**Requisitos:** Lambda creada por el IDP con tags idp-code-source (repo-pipeline, s3-artifact o container-image). Repo de código esperado: fn-{nombreBase} (ej. fuente miApi-dev → repo fn-miApi).

**Flujo habitual (repo+pipeline):** habilita pipelines → abre/actualiza PR → el pipeline compila la rama del PR (feature/xx) y despliega {fuente}-eph-pr-{n}. No eliges rama en el portal: la rama es la del PR.

**Opcional:**campo «Rama preview inmediato» compila esa rama sin PR (CodeCommit; build puntual tras habilitar).

El pipeline estable (fn-*-deploy) no se modifica.

Ya con esto, ubicara la lambda fuente ya extistente en la region. Y se ingresa el nombre de la rama preview (opcional). Tras habilitar pipelines, dispara un build con esa rama (CodeCommit). Para GitHub usa un PR: el pipeline toma la rama del PR automáticamente. Y ya al final, se debe indicar el tiempo que estara habilitada el entorno efimero

![Vista de paso 2 - rama efimera de lambda](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-ephemeral-preview-branch-image.png)


#### Paso 3: review

Se muestra un resumen de lo que se recibio y lo que se va a realizar.

![vista de paso 3 - rama efimera de lambda](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-ephemeral-review-image.png)

### Desplegar lambda (blue-green / Canary)

#### Paso 1: Función y estrategia

Esta accion despliega un artefacto que este comprimido en zip (o imagen ECR) publicando versiones Lambda y moviendo el alias live. Canary y Blue-Green piden aprobación en el IDP (bajo quien este en rol RBAC). Abortar o completar se ejecuta al momento. 

se debe llenar lo siguiente:
  - **la funcion lambda a desplegar**: muestra la lista de componentes disponibles en formato comprimido tecnologias y pipeline si tiene.
  - **API Gateway y ruta:** Elige el API/path que invoca esta Lambda. El deploy apuntará esa integración al alias live.
  - **Estrategia de despliegue:** se debe elgir la forma de paso de version de aplicacion en el ambiente necesitado. **Canary**: porcentaje en los que se van remplazando los entornos en el ambiente. **blue-green**: crea un ambinte similar al disponible los entornos verdes son para probar y desplegar y azul maneja el trafico real del ambiente.

Al seleccionar la estrategia de despliegue relacinada se habilitara la forma de ejecutar la accion

|Accion Canary| Accion Blue-green|
|-|-|
|iniciar canary (artefacto nuevo +%)|Manual 1/3 - preparar (alias green, sin tocar live)|
|promover canary (100% Live)|Automatico + switch|
|Abortar canary (quitar peso adicional)|Manual 2/3 - switch (live -> green)|
|...|Manual 3/3 - Completar (borrar alias green)|
|...|Abortar|

En la opcion de "Artefacto Zip (S3)", se solicita confirmacion de la version en concreto a desplegar:

|latest|buildID concreto|
|-|-|
|usa el ultimo que se debe contrar en `artifacts/latest/function`. _Solo Zip. Si no hay objetos en S3, publica un artefacto antes (pipeline o aws s3 cp)._|Se habilita un campo para especificar el BuildID de artefacto S3 para desplegar|

#### Paso 2: Review

Se muestra un resumen de lo que se recibio y lo que se va a realizar.

![vista 2 de lamda-desplegar - review](assets/create/AWS-Lambda-Function/create-AWS-lambda-function-deploy-review-image.png)

### Microservicio AWS — CI + EKS (Git strategy)

En este servicio, se hace una copia de trabajo del microservicio CI en EKS. Aquí se implementará la estrategia Git y ambientes efímeros. 

Ya con eso, crea ECR, repositorio (GitHub o CodeCommit), CodePipeline/CodeBuild y stacks Terraform en repos-microservices-cluster.

#### Paso 1: Origen de repositorios

En este paso se debe selecionar la region donde se encuentra los repositorios de codecommit, la plantilla de terraform y el destino de los Stack de EKS en forma de cluster.

![vista de paso 1 - creacion de microservicio en AWS](assets/create/AWS-microservice/create-AWS-microservice-code-loc-image.png)

#### Paso 2: Project Information (Informacion del proyecto)

![vista de paso 2 - informacion del proyecto - despliegue de microservicio de AWS](assets/create/AWS-microservice/create-AWS-microservice-project-info-image.png)

Para este paso, se debe llenar:

- **Estrategia de Git:** Uso de las estrategias ya mencionadas (trunk-based o GitFlow)
- **Puerto de contenedor:** Puerto HTTP que escucha la app dentro del contenedor (containerPort del Deployment EKS).
- **Tipo de Service (EKS):**  Tipo de Service (EKS) si es **ClusterIP** (de acceso interno (port-forward / Ingress aparte)). LoadBalancer: crea un NLB en AWS y expone hostname externo. El canary por % exacto sigue siendo por réplicas; pesos ALB Ingress serían un siguiente paso.
- **Tipo de loadbalancer:** NBL (Network Load Balancer)(recomendado - por defecto) o CLB (Classic Load Balancer)
- **Esquema del load balancer:** como se comunicara el microservicio. si es internet-facing para servicio publico o interno con VPC para ambientes bajos
- **nombre del proyecto:** Nombre base del proyecto CodeBuild (sin espacios). Se agrega sufijo por ambiente según IDP_GITFLOW_ENV_NAMES.
- **nombre del microservicio:** el nombre con el que se diferencia el microservicio
- **Tipo:** que clase de microservicio es. si se trata de frontend o backend
- **Descripccion:** descripccion corta para el pipeline 
- **lenguaje de programacion:** lenguaje del proyecto principal

_en esta vista se confirma los ambientes creara con sus ramas y pipelines. con politicas de creacion y aoturizacion de PRs. Ajusta el .env y reinicia el backend para cambiarlos._

_el nombre que tendra el repositorio sera asignado bajo el formato ms-NOMBRE_DEL_SERVICIO-front o ms-NOMBRE_DEL_SERVICIO-back segun indique su .env_

#### paso 3: Configuracion de pipeline

![vista paso 3 - configuracion de pipeline - despliegue de microservicio en AWS](assets/create/AWS-microservice/create-AWS-microservice-pipeline-configuration-image.png)

En este paso se elige el nivel de configuracion que necesita el pipeline.

|Nivel|Detalle|
|-|-|
|Instalar Dependencias|instala dependencias necesaria para el funcionamiento del microservicio|
|Ejecutar Test|Ejecucion de pruebas unitarias en el microservicio|
|Compilar aplicacion|pasos de ejecucion para la compilacion de la aplicacion|
|Escaneo de Seguridad|Revision de esquemas de seguridad que se tengan|
|Build Docker|construccion de la imagen docker|
|Publicar artefactos|subir artefactos de compilados o componente del microservicio|
|Generar terraform (EKS) + deploy en push|diseña la plantilla terraform para EKS y hace Deploy|


#### Paso 5: Review

Se muestra un resumen de lo que se recibio y lo que se va a realizar.

![vista de paso 5 - resumen - creacion de microservicio en AWS](assets/create/AWS-microservice/create-AWS-microservice-review-image.png)

