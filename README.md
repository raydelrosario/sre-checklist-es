<p align="center">
<img src="images/sre_checklist.png"/>
</p>

:dart: **Propósito del respositorio**: Proporcionar a equipos e individuos una idea general sobre lo que hay que tener en cuanta y lo que hay que aspirar en el campo y trabajo del SRE.

**Nota**: Estos checklist son **opiniones**. Se basan en mi propia opinión y experiencia, no son verdades universales  (duh! :smile:).
Así que no deberías dudar de lo que leas aquí y eres más que bienvenido a añadir tu propia opinión sobre el asunto, iniciando un debate o proponiendo un cambio en el [proyecto](https://github.com/bregman-arie/sre-checklist).

**Nota del traductor**: Este trabajo le corresponde a [Arie Bregman](https://github.com/bregman-arie) del [proyecto en inglés](https://github.com/bregman-arie/sre-checklist). Cualquier asunto con la traducción, no dudes crear un Issue o Pull request.

:construction: Se puede decir que este repositorio está todavía en progreso. Yo no lo trataría algo totalmente completo en este momento ni nada que se le parezca. ¡Las contribuciones son más que bienvenidas!

- [Team :couple:](#team-couple)
  - [Responsabilidades](#responsibilities)
  - [Skills](#skills)
    - [Must](#must)
    - [Opcional](#opcional)
  - [Processes](#processes)
  - [SRE Team Goals](#sre-team-goals)
  - [SRE Lead](#sre-lead)
  - [New SRE Team Member](#new-sre-team-member)
- [Producción](#producción)
  - [Requerimientos](#requirements)
  - [Aprovisionamiento](#provisioning)
  - [Instalación](#installation)
  - [Despliegue](#deployment)
  - [Configuración](#configuration)
  - [Resilencia](#resiliency)
- [Tecnologías :computer:](#technologies-computer)
  - [Repositorios Git](#git-repositories)
    - [CI](#ci)
    - [Seguridad](#security)
    - [Automatización](#automation)
  - [Cloud](#cloud)
    - [Aprovisionamiento](#provisioning-1)
    - [Tracking and Monitoring](#tracking-and-monitoring)
    - [Accounts](#accounts)
    - [Recursos](#resources)
    - [Reliability](#reliability)
  - [Kubernetes](#kubernetes)
    - [Resource Management](#resource-management)
    - [CI/CD](#cicd)
    - [Cluster Management](#cluster-management)
  - [GitOps - ArgoCD](#gitops---argocd)
    - [Git Repositories](#git-repositories-1)
    - [GitOps Management](#gitops-management)
    - [Sync Strategy](#sync-strategy)
  - [Monitoreo](#monitoring)
  - [Ingeniería del caos](#chaos-engineering)
  - [IaC](#iac)
    - [The Chosen One](#the-chosen-one)
    - [Implementación](#implementation)
  - [Terraform](#terraform)
    - [Desarrollo y CI/CD](#development-and-cicd)
    - [State](#state)
    - [Estructura de los archivos de Terraform](#terraform-projects-file-structure)
    - [Terraform Code](#terraform-code)
      - [Módulos](#modules)
    - [Git](#git)
    - [Cloud](#cloud-1)
    - [Secretos](#secrets)

## Team :couple:

### Responsabilidades

- [ ] **Decide on responsibilities**
  - Common
    - [ ] Infrastructure management
    - [ ] Monitoreo
    - [ ] Manejo de incidentes
    - [ ] Infra and Reliability related automation
  - [ ] Arguable
    - [ ] App Performance - Arguable because some organizations treat it as dev responsibility
- [ ] **Documented/Written**
  - Make sure to write down the responsibilities of the team somewhere. That will be useful for many things like new members joining, recruiting, clarity for the organization and more.

### Skills

#### Must

- [ ] Coding
  - It doesn't matter what language! it seems market right now leaning towards Go mostly, for SRE and Devops, but Python is also quite common and eventually whatever works best for the team is what matters
- [ ] Monitoring
  - To achieve good reliability and improve it, monitoring should be performed continuously. This makes it to quite critical skill to own
- [ ] CI/CD
  - CI/CD today is integrated in every development process, whether it's of the application itself or the automation and infra managed by SRE and DevOps teams
- [ ] IaC, CM
  - IaC and CM is how you manage infra and operations through code. If you do your work as SRE manually and using ad-hoc commands or UI, you probably want to reconsider your approach and obtain some IaC (Infrastructure as Code) and CM (configuration management) skills and knowledge


#### Opcional

Algunos argumentarán que las siguientes habilidades y temas no deberían ser opcionales y que son 100 % obligatorios, pero en mi opinión personal dependen mucho de tus responsabilidades como SRE y de tu entorno de trabajo. Si tu entorno consiste principalmente en servidores físicos, por ejemplo, y no hay contenedores, entonces ¿por qué los contenedores son una necesidad para ti?

- [ ] Contenedores
- [ ] Kubernetes
- [ ] Cloud
- [ ] Virtualización

### Processes

- [ ] Incident Management
  - There must be a well defined process to how incidents are managed. Some thoughts:
    - Where incidents are reported/raised?
    - Who monitors the alerts at any given point of time?
    - Do you need 100% time coverage?
    - Is there any team that gets the alerts before the SRE team and tries to handle the issue?
  - Is the process automated?
    - [ ] Do you need to manually open a ticket?
    - [ ] Do you need to go to incidents platform/page or do you get an alert?
    - [ ] Do you schedule a meeting to talk about

### SRE Team Goals

- [ ] Set goals
  - [ ] Define SLO (Service Level Objective)
  - 100% reliability is not a good goal! (not sustainable + not feasible. One example: maybe you can drive 100% reliability for the service you own, but most of the time not for its dependencies)

### SRE Lead

- [ ] Is there an onboarding page for SREs joining the team?
- [ ] Schedule 1:1 meeting with team (probably...manager or lead? TBD)
- [ ] Identify Possible Gaps. Few things to watch our for:
  - Does development team waits on SRE for infra related operations?
  - Basically going over other check lists in this page :)
- [ ] Identify SRE team maturity and work on improving it
  - [ ] Step 1: Operations: SRE is focused on resolving issues, dealing with requests
    - At this step you'll be mainly focused on making sure you and the team are able to respond to any issue raised
    - Slowly you'll automated processes, fixes and move towards step 2
  - [ ] Step 2: Automation: SRE is moving towards automation and self-service. Providing tooling, documentation, etc.
    - In this step you focus on building the mindset of automating fixes, documenting what the team and others parties in the organization should be aware of
    - This step is probably the most long one. Don't expect to achieve it in short time, just make sure you have consistent progress towards next step
  - [ ] Step 3: Product: SRE is focused on improving the product itself - reliability, performances, etc.
    - Congratulations. Processes are automated, you respond quickly to issue, .., you are living the dream. Now you can go deeper and focus on the product itself
    - This not for everyone but definitely a feasible step and one to aspire for
- [ ] Keep learning ALL THE TIME
  - [ ] Learn how others are doing it!
    - https://github.com/upgundecha/howtheysre - so many good examples!

### New SRE Team Member

* Welcome :)
* Have a mentor? Great. If not, ask for one
* [ ] Do the onboarding
  * [ ] No onboarding? maybe you can be the first to add one
* [ ] Learn about the product
  * What it does?
  * Is it SaaS? On-Premise? ...
  * How it's delivered and deployed?
* [ ] Time to deep dive into operations
  * TODO: add some items :)

## Producción

### Requerimientos

- [ ] ¿Cuáles son los requisitos para pasar a producción?

### Aprovisionamiento

- [ ] ¿Cómo se aprovisiona la infraestructura necesaria para desplegar la aplicación? (Terraform, Pulumi, CloudFormation, ...)

### Instalación

- [ ] ¿Cómo instalar la aplicación y sus dependencias? (Contenedor, Bash Script, Ansible, ...)

### Despliegue

- [ ] ¿Cómo desplegar la aplicación o el servicio de aplicación? (k8s, cloud instances)

### Configuración

- [ ] ¿Cómo configurar la aplicación? (k8s, Ansible, ...)

### Resilencia

- [ ] Tu aplicación es capaz de soportar interrupciones (generalmente implementando arquitecturas multirregión o multicloud)
- [ ] Tu aplicación aumentará y disminuirá en respuesta a los cambios de carga.

## Tecnologías :computer:

### Repositorios Git

#### CI

- [ ] Is there CI for every project?
  - [ ] Linting and Styling
  - [ ] Unit tests
  - [ ] E2E testing

#### Seguridad

- [ ] Privilegios mínimos y política Zero Trust
  - [ ] Asegúrate que solo las personas del equipo/compañía tengan accesos a los repositorios

#### Automatización

  - [ ] Esto es bastante avanzado, pero aún así, puede que quieras considerar automatizar la creación de repositorios y el control de acceso (usando tecnologías como Terraform o lenguajes de programación, puedes llegar a automatizar completamente el proceso de gestión de repositorios).

### Cloud

#### Aprovisionamiento

- [ ] Recursos manejados mediante Infraestructura como código como Terraform, Pulumi, etc.
  - Si en algún momento necesitas restaurar toda tu infraestructura, tiene el código para hacerlo y puedes hacerlo con bastante rapidez.

#### Seguimiento y control

  - [ ] Los recursos deben tener tags
    - [ ] Env (e.g. staging, prod, dev)
    - [ ] Owner (e.g. team)

#### Accounts

- [ ] Separate **accounts** for dev, staging, production, ...
  - Why? better isolation, granular and accurate authentication and authorization, reporting per env, ...

#### Resources

- [ ] Resources Quotas are set (no one wants to hit high bills)

#### Reliability

- [ ] No single point of failure
  - [ ] Resources deployed across availability zones, regions, etc.

### Kubernetes

#### Resource Management

- [ ] Apply/Add labels for every type of resources. You may use this [page](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels) as a suggestion to which labels you should be adding

#### CI/CD
  - [ ] CI/CD for Cluster bootstraping
  - [ ] CD process for manifests/configurations (using something like Flux, ArgoCD)
    - [ ] Make sure cluster bootstraping (the process of preparing the cluster) is managed fully using GitOps

#### Cluster Management

- [ ] ¿Cluster por cada ambiente? Dev, QA, Staging, Production
  - [ ] Por región? Por nube? ¿Cómo de distribuido debe estar tu entorno?
- [ ] Cluster Policy Management
  - [ ] Networking Policies
  - [ ] Storage Policies

### GitOps - ArgoCD

#### Repositorios Git

- [ ] Infra code (Manifests, Configurations, etc.) is in a separate repository (and not in application repository)

#### GitOps Management

- [ ] **GitOps adopted for GitOps agents themselves and not only for app related code and infra**
  
- [ ] DON'T install ArgoCD with kubectl commands
- [ ] Helm chart not recommended as it lags behind official releases of new ArgoCD releases
- [ ] Consider:
  - [ ] Hosted Argo CD instance (pros: maintenance is on others. cons: make sure you have some money in the wallet)
  - [ ] ArgoCD for managing ArgoCD (pros: easy DR, rollbacks, ... and full audit and changelog. cons: maintenance)
    - [ ] Consider using [Argo CD Pilot](https://argocd-autopilot.readthedocs.io/en/stable) for that which is "opinionated way of installing Argo-CD and managing GitOps repositories"
- [ ] Think about:
  - [ ] One ArgoCD to control multiple clusters (why not: single point of failure)
  - [ ] Argo CD per cluster (why not: a lot of maintenance and basically over complexity)

#### Sync Strategy

- [ ] Auto Prune (resources deleted when files/content deleted)
- [ ] Self-heal (cluster state corrected based on Git state and when manual changes done to the cluster)

### Monitoreo

- [ ] Choose monitoring solution
  - If you can afford it, go for ready monitoring solutions like DataDog, NewRelic, ...
  - Be aware of maintenance and how much time you are willing to invest in maintaining monitoring solution

### Ingeniería del caos

The interesting topic of ensuring your environment can withstand unexpected disruptions

TODO: insert a list of steps to go towards the process of establishing and integrating chaos engineering in your environments

### IaC

#### The Chosen One

- Aspectos a tener en consideración a la hora de elegir la herramienta IaC:
  - Madurez (nuevo vs. establecido y conocido)
  - Comunidad y soporte
  - Número de integraciones, plugins, proveedores, módulos, ...

#### Implementación

- [ ] Follow DRY (Don't Repeat Yourself) principle as in make sure there are no code duplication so when you change parameter's value for example, you don't need to change it in two different place
- [ ] Readable code - use naming conventions, formatting, ... make sure anyone can read the code and doesn't suffer much in doing so :)

### Terraform

#### Desarrollo y CI/CD

  - [ ] CI pipeline to test Terraform changes (syntax, lint, ...)
    - Consider inserting cost considerations (e.g. test whether a change will raise the bill significantly if you are using a public cloud)
  - [ ] CD pipeline to deploy/apply Terraform changes after the change is merged
  - To apply changes as part of a pull request (without merging a change) you can use something like [Atlantis](https://www.runatlantis.io)
    - This way you can avoid using local configurations and credentials
  - Needless to say, but once you started to use Terraform in your org, you should use only that and not allow users to make changes manually in the providers you are using (that will lead to errors when running `terraform apply`)

#### State

- [ ] Stored in a private secured location
  - [ ] Encrypted
  - [ ] Public access blocked
- [ ] Stored in a shared location as it may be updated by different team members
- [ ] Backed up (e.g. by having versioning)
- [ ] Never edited directly/manually (as it should be managed and updated by Terraform itself as part of the Terraform lifecycle)

#### Terraform Projects File Structure

- [ ] Directorios separados por cada ambiente de desarrollo (staging, production, ...)
- [ ] Separate backend for each environment (as you don't want share the same authentication and access controls for all environments)
- [ ] Separate directory in each environment for each component and application

  ```
  staging/
    networking/
    applications/
    databases/

  production/
    networking/
    applications/
      web-app-1/
      web-app-2/
    databases/
      mongo/
      mysql/

  global/
    user_access_management/

  modules/
    applications/
      web-app-1/...
  ```

- [ ] You don't put everything in main.tf
  -  Terraform configuration files themselves can be organized in many ways
  - Possible files:
    - main.tf
    - outputs.tf
    - variables.tf
    - providers.tf
    - dependencies.tf
  - Files can be further divided (avoid managing very long files)

#### Terraform Code

- [ ] Variables have description (to document what they are used for)
- [ ] Set lifecycle "prevent_destroy" on resources that should never be deleted (e.g. Terraform state source like S3 bucket)
- [ ] Try not including shell scripts inline (some tend to grow quite a lot over time). Use instead templatefile function to render a script from a file
- [ ] No hardcoded repeated values (common examples are ports, CIDR blocks, etc.). Instead use the concept of `locals`
- [ ] Prefer using `for_each` instead of `count`. `count` is very limited in modifying lists as it uses list position/index to rely on while `for_each` is map, set based so it based on specific keys
- [ ] Consistent naming, code style conventions and formatting
- [ ] Set tagging standards
  - [ ] Decide on which tags to use. Some ideas:
    - owner (team, department, ...)
    - generted_by/managed_by/... = "terraform"
  - [ ] Rather than specifying tags for each resources, consider setting them at provder level with `default_tags`. This will help you manage tags at scale

##### Modules

- [ ] Evita la duplicación de código o configuración en Terraform usando módulos
- [ ] Trata de crear módulos lo más reusables posibles
  - [ ] Don't include provider code in a reusable module. Different teams and organizations can use different provider versions and constraints (e.g. different default tags)
- [ ] Avoid hardcoding values, especially in the case reusable modules. To make them reusable, values will have to come from input variables
- [ ] Consider using only separate resources in a module and not inline blocks as they may limit you at some point or another when reusing the module
- [ ] Don't use relative paths! use `path references` (e.g. `path.module`, `path.root`)
- [ ] Try avoiding using latest version of a module. Instead stick for example to tags.
  - [ ] Branches can be also used, but since anyone can introduce a change to them, they considered less stable than tags

#### Git

- Recommended repositories layout:
  - [ ] Separate Repository for modules
  - [ ] Separate Repository for environments (this repository makes use of the modules repository mentioned above)
- [ ] Consider using Git tags
  - [ ] They can be used for specifying specific versions of modules

#### Cloud

- [ ] Don't hardcode image IDs (it's hard to maintain long term). Instead use filters

```

data "cloud_image" "image_data" {
  provider = ...
  filter {
    name = "name"
    values = ["some-image-you-would-like-to-use"]
}

resource "some_instance" "instance" {
  image = data.cloud_image.image_data.id
}
```

#### Secrets

- [ ] **Básico!**
  - [ ] DON'T store credentials in Terraform configuration as it's highly insecure
  - [ ] Eventually sensitive data will end up in your state file, for this reason make sure it's encrypted and only visible to those who should be able to access it
    - [ ] Same applies for plan files
- [ ] **Provider Credentials**
  - [ ] For local Terraform work/development, you can use generic secret-management tools/CLIs like 1Password or provider-specific options like aws-vault
  - [ ] For CI/CD that's highly depends on the CI/CD solution/service you are using:
     - GitHub Actions: Use Open ID Connect (OIDC) to establish connection with your provider. You then can specify in your GitHub Actions workflow the following:

  ```
  - uses: aws-actions/configure-aws-credentials@v1
    with:
      role-to-assume: arn:aws:iam::someIamRole
      aws-region: ...
  ```


    - Jenkins: If Jenkins runs on the provider, you can use the provider access entities (like roles, policies, ...) to grant the instance, on which Jenkins is running, access control
    - CircleCI: you can use `CircleCI Context` and then specify it in your CircleCI config file

  ```
  context:
    - some-context
  ```
- [ ] Secretos en configuraciones de Terraform
  - [ ] Consider how you would like to manage secrets inside Terraform configuration files
    - **Variables de entorno** - you define Terraform variables (with `sensitive = true`) and pass values with environment variables
      - pros: simple to use, no need to store sensitive data inside Terraform code
      - cons: managed outside of Terraform so tracking, enforcing, managing for different environments, ... is challenging or not feasible
    - **Archivos encriptados** - encrypting the secret and storing the encrypted secrets in Terraform configurations
      - pros: secrets are encrypted and are of Terraform code and part of the version control system
      - cons: working this way can be cumbersome (to modify, you first have to decrypt, makes the changes and then encrypt it again). Still holds security risk if someone gets their hands on the decryption key
    - **Secret Store** - centralized secret store
      - pros: no plain text secrets in Terraform configurations. Easy to standardize practices and policies around secrets if they are all in the same place
      - cons: not managed as part of the repository, version control, ... makes it easier to makes mistakes in regards to different environments. Costs $$$
