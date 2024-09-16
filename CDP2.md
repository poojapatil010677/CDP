**What are compute clusters?**

Compute clusters enable you to deploy a containerized platform on Kubernetes for Data Services and shared services. The Compute Cluster architecture offers simplified management, enhanced efficiency, and centralized control that leads to faster deployments, reduced configuration errors and improved system reliability. As multiple Data Services can optionally share the same Compute Cluster, it also lowers the cost of ownership.

When registering a Compute Cluster enabled environment, a default Compute Cluster is created. This default Compute Cluster is tied to the environment, and is used for running critical applications. The default Compute Cluster is labeled as **Default Cluster** in your environment to distinguish it from the other Compute Clusters.



**What are external compute clusters?**

Externalized and Shared Compute Clusters are the future of the CDP data service architecture. 

**External Compute Clusters** will standardize our containerized platform for all data services. 

Administrators will be able to deploy a standard, uniform Kubernetes platform that can host any data services (like CDE, CML, CDW, or CDF) and shared services (like Airflow, Notebooks, Data Catalog, Data Sharing Server, Iceberg REST Catalog etc). This change will remove all inconsistent terminologies (e.g., private network vs private cluster) and provide the same features (e.g., UDR support) across all services. It will also provide a central management console for all operations, monitoring, and troubleshooting. 

This architecture offers administrators simplified management, enhanced efficiency, and centralized control, leading to quicker deployments, reduced configuration errors, and improved system reliability. 

Cloudera will also greatly benefit from the Externalized Compute Cluster architecture. Support matrixes can be streamlined, as the DSP team doesn’t need to cater to an ala-carte platform where data services pick and choose what platform features to enable within their service. This will enable shorter QA times and faster feature delivery while increasing product quality. 

**External Compute Clusters** will enable multiple instances and types of data services to share Compute Clusters. This architecture maximizes resource efficiency, reduces operational costs, and streamlines management.



**Containerized Service** - A Cloudera Service that runs as a collection of container(s) inside a Kubernetes Cluster, This umbrella term can be used to refer to data services (DFX, CML, CDE, etc.) and metadata services alike (Containerized Data Lake, Data Catalog, etc.)

**Compute Cluster** - Cloudera’s abstraction of Kubernetes in Cloud (EKS, AKS). Containerized Services

run on a Compute Cluster, which can be - 

- **Embedded Compute Cluster** - A compute cluster whose lifecycle is managed by the hosted containerized service. An embedded compute cluster has no existence outside of the containerized service that manages it.

* **External Compute Cluster** - A compute cluster that is independent of any containerized service and exists independently as a first-class citizen. Its lifecycle is managed by the user instead of a containerized service. An External compute cluster can host one or more containerized service(s).



**What is an app factory?**

A unified framework that streamlines development by offering foundational components and essential infrastructure for data services. It comprises multiple microservices and/or modules.

A unified framework for the development of both new and existing services, known as the **App Factory**. This tool will streamline development by offering foundational components and essential infrastructure, supporting the following capabilities:

- Unified Experience for Service Administrators: Offering a consistent UI, API, and CLI interface.

- Seamless onboarding process for new containerized services within CDP. 

- Out of box support for standard admin operations

  - Installation/Uninstallation

  - Upgrades

  - Backup/Restore

  - Suspend/resume

- Flexibility to integrate custom logic tailored to specific services.

- In-built integration with other platform microservices and necessary cloud services. 

  - Integration with Liftie, Redbeams, Cloudbreak 

  - Integration with EFS, Azure Files, etc (until these interactions are abstracted out in a separate platform microservice)

**Why do we need app factory service and what is the purpose of it?**

- _Customer Benefit_

  - **_Customer Experience_**_: Consistent customer (administrator) experience across services, enhancing the overall customer experience._

  - **_Administrator Experience_**_: Consistent terminology for infrastructure capabilities across services, reducing deployment complexity, training burden, and feature gaps._

- _Business Benefit_

  - **_Accelerate Service Delivery_**_: By leveraging a unified platform, we can significantly speed up the delivery of new services and features, reducing time-to-market and allowing us to respond to business needs quickly._

  - **_Optimize Vendor Relationships_**_: By standardizing one technology stack for similar use cases, we position ourselves to potentially purchase a single, comprehensive service from a vendor in the future. This approach can lead to cost savings, simplified vendor management, and more cohesive service integration._

- _System Benefits_

  - **_Enhance Service Supportability_**_: A standardized approach improves the supportability of services, as common issues can be identified and resolved more efficiently across the board._

  - **_Minimize Threat Surface_**_: Utilizing a single technology stack for similar use cases across the company helps to minimize the threat surface. This consolidation reduces the complexity of security management and enhances our overall cybersecurity posture._

  - **_Interoperability_**_: Seamless integration with existing and upcoming platform tools (Redbeams, Liftie, Cloudbreak, etc)_

  - **_Maintainability_**_: Easier maintenance with modular design, clear documentation, well-defined interfaces, and streamlined processes, allowing for quick updates without causing regressions._ 

  - **_Centralized Gating_**_: Any new service additions can be gated against a common service readiness checklist. For example: making sure that services are added only with HA support (replicas > 1)._ 

**What is the CLI command to register an AWS environment with a default compute cluster?**


```
cdp environments create-aws-environment 
--environment-name <value> \
--credential-name <value> \
--region <value> \
--security-access <value> \
--authentication <value> \
--log-storage <value> \
--enable-compute-cluster
--compute-cluster-configuration
privateCluster=false, 
kubeApiAuthorizedIpRanges=<cidr1>,<cidr2>,
workerNodeSubnets=<subnet1>,<subnet2>
```
