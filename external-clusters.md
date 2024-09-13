Externalized Compute Cluster

Product Requirement Document


### Overview

Externalized and Shared Compute Clusters are the future of the CDP data service architecture. 

**External Compute Clusters** will standardize our containerized platform for all data services. 

Administrators will be able to deploy a standard, uniform Kubernetes platform that can host any data services (like CDE, CML, CDW, or CDF) and shared services (like Airflow, Notebooks, Data Catalog, Data Sharing Server, Iceberg REST Catalog etc). This change will remove all inconsistent terminologies (e.g., private network vs private cluster) and provide the same features (e.g., UDR support) across all services. It will also provide a central management console for all operations, monitoring, and troubleshooting. 

This architecture offers administrators simplified management, enhanced efficiency, and centralized control, leading to quicker deployments, reduced configuration errors, and improved system reliability. 

Cloudera will also greatly benefit from the Externalized Compute Cluster architecture. Support matrixes can be streamlined, as the DSP team doesn’t need to cater to an ala-carte platform where data services pick and choose what platform features to enable within their service. This will enable shorter QA times and faster feature delivery while increasing product quality. 


**External Compute Clusters** will enable multiple instances and types of data services to share Compute Clusters. This architecture maximizes resource efficiency, reduces operational costs, and streamlines management.

With the streamlined operations and reduced costs of Shared Compute Clusters, Cloudera can claim lower TCO, increasing our competitiveness in the market. 

—----------------------------------------


### Proposed Solution

_Describe the solution in detail. Explain clearly how the feature will resolve the problem for our customers.  Outline the value and benefit customers get if we solve this problem._

Managing the lifecycle of an embedded compute cluster with various a la carte options used by current data services (CML, CDE, CDF) has been a fractured experience for our customers. Since each data service can today select different platform components a la carte, it becomes extremely complex to support deployment and upgrade of various cluster shapes and bloating up the support matrix. Simply put, the [Paradox of Choice](https://en.wikipedia.org/wiki/The_Paradox_of_Choice) applies aptly here.  

From a time-to-market perspective, Cloudera spends 4x the time to deliver a platform feature across all data services than it should otherwise take for each data service to integrate with a standard platform feature. This disjointed delivery prevents customers from adopting a unified architecture across their stacks, and data service management opex increases linearly with the breadth of service adoption.

Moreover, in the embedded mode, the lines between a Platform Admin role and a Data Practitioner role are blurred because the same persona needs to have expertise in Infrastructure requirements (Compute, Storage, Scale, Networking, Security) as well as Data Service Capabilities (Service features, Service How-to). 

All data services have an opinionated product page for deployment, management, and monitoring, which further increases the operational complexity of our platform. These pages are spread across the platform, providing an inconsistent, fragmented experience. Also, each service requires a different entitlement on the customer tenant to enable, in principle, the same feature. All of these contribute to the prolonged deployment times of the first containerized workload and lead to an elevated overall TCO due to the burdensome management involved.

Hence, a move away from embedded mode and the centralization of service operations and monitoring has become necessary and can be addressed by  “Data services **_supporting deployment_** on a **_standard_** (capabilities, parameters, upgrade process) **_external_** (separate lifecycle from data service) compute cluster using a central, uniform management interface”.

With externalized compute clusters, an Environment/PlatformAdmin installs and manages the Compute Cluster and authorizes a WorkloadAdmin to provision a data service on it within the same administration experience.

Further, **_default parameters are inferred from the Environment, enabling practically a “single-click” provisioning of both the externalized compute cluster and data service_** (with optional overrides). Most importantly, **_platform features are developed and released at the Compute Cluster level and are, therefore, available synchronously across each data service._** 

 


### Glossary

**The following is a subset copied from ..**

**Containerized Service** - A Cloudera Service that runs as a collection of container(s) inside a Kubernetes Cluster, This umbrella term can be used to refer to data services (DFX, CML, CDE, etc.) and metadata services alike (Containerized Data Lake, Data Catalog, etc.)

**Compute Cluster** - Cloudera’s abstraction of Kubernetes in Cloud (EKS, AKS). Containerized Services

run on a Compute Cluster, which can be - 

- **Embedded Compute Cluster** - A compute cluster whose lifecycle is managed by the hosted containerized service. An embedded compute cluster has no existence outside of the containerized service that manages it.

* **External Compute Cluster** - A compute cluster that is independent of any containerized service and exists independently as a first-class citizen. Its lifecycle is managed by the user instead of a containerized service. An External compute cluster can host one or more containerized service(s).

_Note:_ **_Compute Cluster in this PRD implies External Compute_** _unless explicitly specified otherwise. Embedded isn’t covered as a part of this doc._ **_Therefore, the term External will be omitted henceforth._**

**Environment “v2”** - The environment attribute to enable support for External Compute Clusters. See this [section](https://docs.google.com/document/d/1gHJHjOUZw7i3DxHm-LvJbFZO_EKCy_QRm0FkyDgnEXc/edit#heading=h.o7h7tl721osj) for a detailed description. **__**

**_Note -_** _This naming may change depending on feedback from peer Product Managers / Product Marketing. Concerns about using v2 and implying a versioning of Environment are enumerated at_ [_https://jira.cloudera.com/browse/CB-25498_](https://jira.cloudera.com/browse/CB-25498?page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel\&focusedCommentId=6638522#comment-6638522)_. A more precise and functional term such as_ **_container-ready_** _may take its place._ 

**Default Compute Cluster** - The **_first_** _compute cluster_ which is created implicitly upon setting Environment v2. This is a special cluster whose lifecycle is tied to the Environment, and can’t be stopped/ deleted ad-hoc. 

This cluster is meant for running critical applications such as Containerized Data Lake.

**Add-on Compute Cluster** - An **_optional, explicit, user-requested_** compute cluster that inherits configuration from the default compute cluster. This cluster may be stopped/resumed/deleted independent of Environment.




### Go-to-Market  _(Tier 1 Only)_


The Externalized Compute Cluster represents Operational Innovation in hosting and managing data services, enabling organizations to embrace the power of containerization for their data infrastructure. Built on Cloudera's legacy of reliability and innovation, this solution eases the operational overhead, reduces the total cost of ownership, provides for synchronized feature availability and standardizes the platform for all data services.

Key Advantages of Cloudera's Externalized Compute Cluster:

1.Scalability Beyond Limits: Organizations can now dynamically install a compute cluster with no-to-minimal inputs and share them between data services.

2.Accelerated feature delivery: There is a significant reduction in time-to-market for platform features as they’re now developed and tested at a unified layer.

3.Resource Efficiency: Shared mode maximizes resource utilization, allowing businesses to do more with less while minimizing operational overhead.

4.Rapid Deployment: Quick provisioning of compute clusters and ease of deploying data applications (practically a single-click), reduces time-to-insight in data-driven decision-making.

5.Seamless Integration: The Externalized Compute Cluster seamlessly integrates with Cloudera's comprehensive ecosystem with guaranteed compatibility with all data services, enabling users to leverage the full suite of data management and analytics tools.

6.Enhanced Security: Benefit from Cloudera's robust security and compliance features, ensuring that best security practices are followed by containerized applications..

"Cloudera is committed to pushing the boundaries of data management, and the launch of our Externalized Compute Cluster is a testament to that commitment," said Dipto Chakravarty, Chief Product Officer at Cloudera. "This solution makes it easier for organizations to deploy and manage containerized applications that can scale limitlessly while maintaining the reliability and security Cloudera is renowned for."

The Externalized Compute Cluster is poised to unlock new opportunities for organizations seeking to harness the power of their data. With containerization, Cloudera enables customers to achieve unprecedented agility and scalability in managing their data resources, and with externalized compute clusters, it makes managing containerized workloads just as easy as intuitive.

About Cloudera:

Cloudera is a leading global provider of data management and analytics solutions, empowering organizations to transform complex data into clear and actionable insights. Our platform provides the tools, capabilities, and expertise to drive innovation and achieve superior business outcomes.



**_All actions below require an EnvironmentAdmin role._**

|                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Item**                                                      | **CLI** **(Some parameters may only be exposed via Beta/Internal CLI - This is TBD)**                                                                                                                                                                                                                                                                                                                                |
| _Create a v2 environment_                                     | `cdp environments create-aws-environment``––environmentVersion v2``--compute-cluster-configuration=node-subnet-ids=<Inferred>,``--load-balancer-subnet-ids=<Inferred>,``kube-api-authorized-ip-ranges=<inferred>,``private-cluster=<optional>,``enable-public-endpoint-access=<optional>,``encryption-key-arn=<inferred>,``user-defined-routing=<optional>,``load-balancer-authorized-ip-ranges=<optional-inferred>` |
|                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| _Delete a v2 environment_                                     | `cdp environments delete-environment…`                                                                                                                                                                                                                                                                                                                                                                               |
| _Convert an existing Non v2 environment to v2 Environment_ __ | `cdp environments update-configuration``--environmentVersion v2``--compute-cluster-configuration=node-subnet-ids=<Inferred>,load-balancer-subnet-ids=<Inferred>,kube-api-authorized-ip-ranges=<inferred>,private-cluster=<optional>,aks-private-dns-zone-id=<optional>,enable-public-endpoint-access=<optional>,encryption-key-arn=<inferred>,user-defined-routing=<optional>`                                       |
| _Convert an existing v2 to Non v2 Environment_                | `cdp environments update-configuration --environmentVersion null`                                                                                                                                                                                                                                                                                                                                                    |



**The default compute cluster should also be returned in the response for List Compute Clusters. We need to decide whether other API commands of this Compute Cluster service should apply to it. Ideally, this default compute cluster should not be required to be user managed (automated updates, autoscaling, etc should eventually be supported).**

CLI examples:

**_All POST/UPDATE/DELETE actions below require an EnvironmentAdmin role._**

|                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Item**                                                                         | **CLI** **(Beta/Internal CLI only options are highlighted in Blue - these won’t be available in public external CLI unless customers explicitly ask for it)**                                                                                                                                                                                                                                                                              |
| _List Compute Clusters for a CDP Environment_                                    | `cdp compute list-clusters --environment-crn <env_crn>``    # Lists the default compute cluster as the first one here``    <...>`                                                                                                                                                                                                                                                                                                          |
| _Add a Compute Cluster to a CDP Environment_                                     | `cdp compute create-cluster ``--environment <env_crn>``--node-subnet-ids <optional - inferred from environment by default>``--load-balancer-subnet-ids <optional - inferred> ``--private-cluster <optional> ``--aks-private-dns-zone-id <optional>``--enable-public-endpoint-access <optional> ``--encryption-key-arn <optional-inferred> ``--user-defined-routing <optional>  ``—-load-balancer-authorized-ip-ranges <optional-inferred>` |
| _Describe a Compute Cluster_                                                     | `cdp compute describe-cluster –compute-cluster-crn <compute_cluster_crn>`                                                                                                                                                                                                                                                                                                                                                                  |
| _Suspend a Compute cluster_                                                      | `cdp compute suspend-cluster –compute-cluster-crn <compute_cluster_crn> `                                                                                                                                                                                                                                                                                                                                                                  |
| _Resume a Compute Cluster_                                                       | `cdp compute resume-cluster –compute-cluster-crn <compute_cluster_crn>`                                                                                                                                                                                                                                                                                                                                                                    |
| _Remove a compute cluster_                                                       | `cdp compute delete-cluster –compute-cluster-crn <compute_cluster_crn> –force <optional>`                                                                                                                                                                                                                                                                                                                                                  |
| _List applications running on a compute cluster_                                 | `cdp compute list-deployed-applications –compute-cluster-crn <compute_cluster_crn>`                                                                                                                                                                                                                                                                                                                                                        |
| _Allow Remote Cloud User Access to Compute Cluster Kubernetes Server_            | `cdp compute grant-user-kubernetes-access –compute-cluster-crn <compute_cluster_crn> –cloud-user-id <cloud_user_id> –namespace <optional>`                                                                                                                                                                                                                                                                                                 |
| _Authorize a WorkloadAdmin to manage a data/shared service on a compute cluster_ | `cdp compute grant-cluster-access –compute-cluster-crn <compute_cluster_crn> --user-crn\|--user-group-crn <user_group_crn>`                                                                                                                                                                                                                                                                                                                |
| _Download KUBECONFIG of a compute cluster_                                       | `cdp compute get-kubeconfig –compute-cluster-crn <compute_cluster_crn> `                                                                                                                                                                                                                                                                                                                                                                   |




**_Note:_** _The CLI examples listed here are only illustrative. The final command, subcommand and parameter names will be decided by Engineering._ 



CLI examples:

**_All  POST/UPDATE/DELETE actions below require a WorkloadAdmin role._**

|                                                                           |                                                                                                                                   |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Item**                                                                  | **CLI**                                                                                                                           |
| _List externalized compute clusters available for workload provisioning_  | `cdp <workload_placeholder> list-available-compute-clusters –env-crn <env_crn> `                                                  |
| _Select an externalized compute cluster when deploying a data service_    | `cdp <workload_placeholder> deploy-instance –compute-cluster-crn <compute_cluster_crn> --min-k8s-node-count --max-k8s-node-count` |



## References

[Moving to externalized compute for all new workloads (CML Serving, COD, CDL etc)](https://docs.google.com/document/d/1vunxGy3QFmOjJg5mrjW3wZqbUI543ttoc9KGMBwx84c/edit#heading=h.nbxu4acfu2il)

[Externalized Cluster Decision Points Dump](https://docs.google.com/document/d/1uUWVzDZqGgKVoArjQntNYCF_ltqCWVaTpN8YG2wLs1k/edit)

[Externalized Cluster Upgrade - Use Cases](https://docs.google.com/document/d/19sPSaR7EVDsERatj0GENgOwgXluL8tBqgxXo4YhDm5Y/edit)

[k8s Cluster setup and Life Cycle Management](https://docs.google.com/document/d/1LlNbAnacLc91XyxcTqlHu_AfVZTNvgWOnwPp20yBg3Y/edit)

[Miro](https://miro.com/app/board/uXjVOs207Ps=/)
