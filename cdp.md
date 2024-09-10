Compute Cluster enabled environments and Compute Clusters


# [Management Console - Registering environments (UI)](https://docs.cloudera.com/management-console/cloud/environments/topics/mc-environment-register-aws-ui.html)<a id="h.kxmqjb6b5te8"></a>

**Data Access and Data Lake Scaling**

1. Select **Enable Compute Clusters** checkbox to create a compute cluster enabled environment. 

Compute clusters enable you to deploy a containerized platform on Kubernetes for data services and shared services. For more information about Compute Clusters, see the _Management Console documentation_.

**Networking and Security**

1. Provide the necessary networking information for the **Kubernetes** cluster.

   1. If you need to create a Private Cluster, select the **Private Cluster** checkbox to create a private cluster that blocks all access to the API Server endpoint.\
      The following configurations must be set:

      1. (Azure Only) Select the **AKS Private DNS Zone ID** from the available drop-down list.

      2. (Azure Only) Select **Enable User Defined Routing** (UDR) checkbox.\
         In case you enable UDR, you must select the specific worker node subnet where the UDR is configured.

      3. Provide the CIDRs to the **Worker Node Subnets** field to specify subnets for the Kubernetes Nodes.\
         If subnets were provided in the previous **Network** configuration step, the **Worker Nodes Subnets** field is automatically filled out with the same subnets. You can remove the pre-filled subnets.

   2. If you do not need to create a Private Cluster, leave the **Private Cluster** checkbox unchecked.\
      The following configurations must be set:

      1. Provide the CIDRs to the **Kubernetes API Server Authorized IP Ranger** field to specify a set of IP ranges that will be allowed to access the Kubernetes API server.

      2. Provide the CIDRs to the **Worker Node Subnets** field to specify subnets for the Kubernetes Nodes.\
         If subnets were provided in the previous **Network** configuration step, the **Worker Nodes Subnets** field is automatically filled out with the same subnets. You can remove the pre-filled subnets.


# [Management Console - Registering environments (CLI)](https://docs.cloudera.com/management-console/cloud/environments/topics/mc-register_an_aws_environment_from_cdp_cli.html)<a id="h.s5x952fgju6o"></a>

**Steps**

Unlike in the CDP web interface, in CDP CLI environment creation is a three-step process with environment creation, setting IDBroker mappings and Data Lake creation being three separate steps. The easiest way to obtain the correct commands is to provide all parameters in CDP web interface and then generate the CDP CLI commands on the last page of the wizard. For detailed steps, refer to [Obtain CLI commands for registering an environment](https://docs.cloudera.com/management-console/cloud/environments/topics/mc-obtain_cli_commands_for_environment.html).

**Enabling Compute Cluster environments**

Compute clusters enable you to deploy a containerized platform on Kubernetes for data services and shared services. For more information about Compute Clusters, see the _Management Console documentation_.

**Before you begin**

To register an environment with a default Compute Cluster, you need to use the following CLI command:

AWS:

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

Azure:

```
cdp environments create-azure-environment \
--environment-name <value> \
--credential-name <value> \
--region <value> \
--public-key <value> \
--security-access <value> \
--use-public-ip | --no-use-public-ip \
--log-storage <value> \
--enable-compute-cluster
--compute-cluster-configuration
privateCluster=false, 
kubeApiAuthorizedIpRanges=<cidr1>,<cidr2>,
workerNodeSubnets=<subnet1>,<subnet2>
```

After the command runs, you can verify if the environment was successfully created with the Compute Cluster with the following command:

1. Describing the environment:

```
cdp environments describe-environment --environment-name {your created env CRN}

...
        "awsComputeClusterConfiguration": {
            "privateCluster": false,
            "kubeApiAuthorizedIpRanges": [
                "0.0.0.0/0"
            ]
        },
        "enableComputeCluster": "true"
...
```

2. Listing compute clusters:

```
cdp compute list-clusters --env-name-or-crn {your created env name or CRN}
```

**Note**\
In case the environment creation fails, the response will be empty. You need to wait for a functioning FreeIPA to start the Compute Cluster creation process.

\


You can use the following command to retry the environment creation with the default Compute Cluster:

- AWS

```
cdp environments initialize-aws-compute-cluster
```

- Azure

```
cdp environments initialize-azure-compute-cluster
```


# [Management Console](https://docs.cloudera.com/management-console/cloud/index.html) - Compute Clusters<a id="h.liub14thnqq4"></a>

## Overview<a id="h.gmj4mryffdug"></a>

Compute clusters enable you to deploy a containerized platform on Kubernetes for Data Services and shared services. The Compute Cluster architecture offers simplified management, enhanced efficiency, and centralized control that leads to faster deployments, reduced configuration errors and improved system reliability. As multiple Data Services can optionally share the same Compute Cluster, it also lowers the cost of ownership.

When registering a Compute Cluster enabled environment, a default Compute Cluster is created. This default Compute Cluster is tied to the environment, and is used for running critical applications. Therefore the default Compute Cluster cannot be stopped or deleted. The default Compute Cluster is labeled as **Default Cluster** in your environment to distinguish it from the other Compute Clusters.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd62ZyOjormb3lXp2vp-_VWYxE5BsY6QpKWVGSen3VejDtq41PcHi3r3JB5Pt2ZVIU9irFALvI8fnjzbBn_kbBe8hygV1MiHqhneIFvO5evJUzZTbV5uZdXxlwwCYVjtUm_OrH9rEQu4rvYZgY_Lp5IMLNk?key=OSI_VXIg5JPRMBrD4S-hEg)

You can create additional Compute Clusters that inherit the configuration of the default Compute Cluster. You can manage the lifecycle of the additional Compute Clusters as they are independent of the environment.

For more information about creating Compute Cluster enabled environments, see the _Registering environment_ documentation.


## Adding more Compute Clusters<a id="h.dusn0p6e1hrz"></a>

You can add as many Compute Clusters as required beside the default Compute Cluster. You can use the User Interface (UI) or CDP CLI to create the Compute Clusters.

**Required role:** _EnvironmentAdmin_


### Creating Compute Cluster with UI<a id="h.ek6x8g7khhei"></a>

You can create additional Compute Clusters beside the default Compute Cluster using Management Console.

1. Navigate to your environment.

2. Select **Compute Clusters** tab.

3. Click A**dd Compute Cluster**.

The **Add Compute Cluster** wizard appears.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdM5b-3AYCgOPgA7tOEVbaRL6YZTqbI3JXir51fQxGFfjFT2-7GbCCqJL1cMhJAJOI7J9QZsbs1zsi7jfEzJQESiCfDVNdNZRLRTG1ivIX9uam5G1HzZSwM6b7D6WkGuieZIz72aOhmRCz5EEIMND7sfaav?key=OSI_VXIg5JPRMBrD4S-hEg)

1. Provide a **Name** to the cluster, and optionally a **Description**.

4) Click **Add Cluster**.

You will be redirected to the **Compute Clusters** tab, where you can track the creation process of the Compute Cluster.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd3i6zVjq1e6eOlHU5HIK2ZOLO8-kpzpjBgT4UrQ4D9bDQT_SglhqkOpzHXRSKxGMTyTSQ3Zc-QMC0gdU105bkTLviXv9kfzB3A6VHeyPQBjNZnUxj9MWEOHo8-7UzUwuTE8axQ0CvwDw4DvlTUNgm45xk?key=OSI_VXIg5JPRMBrD4S-hEg)


### Creating Compute Clusters with CLI<a id="h.5xg64bsgbz86"></a>

You can use the following CDP CLI command to create additional Compute Clusters after the default Compute Cluster is created:

\


```
cdp compute create-cluster --cli-input-json '{"environment": "<envCrn>","name": "<clusterName>","description": "...","tags": {"key": "value"},"network": {"podCidr": "...","serviceCidr": "...","subnets": ["..."],"outboundType": "..."}}'
```

 

**Note**

Ensure that you have `COMPUTE_API_LIFTIE` and `COMPUTE_API_LIFTIE_BETA` entitlements granted to your account.

After the command runs, you can verify if the Compute Cluster creation was successful using the following command:

```
cdp compute list-clusters --env-name-or-crn {your created env CRN}
```

The Compute Cluster status should be `RUNNING`.


## Managing additional Compute Clusters<a id="h.5evpus2akpwq"></a>

After creating additional Compute Clusters, you can view the cluster details, manage the access of the clusters, download the Kubeconfig file, and delete the created clusters.

**Required role:** _EnvironmentAdmin_ or _Owner_

1. Click on the **Name** of the additional Compute Cluster.\
   You will be redirected to the **Cluster Details** page. On the Cluster Details page, you can view the Status, Creation Date, Created By, Description and CRN of the Compute Cluster.

2. Click **Actions** to open the drop-down menu.

   1. Click **Manage Access** to update the list of users who have access to manage the Compute Cluster and use it for installing Data Services.

      1. Click **Update roles** to update the **Resource Role** of a user or group.

You can assign the Owner resource role to a user or group to provide permission to manage the Compute Cluster and install services on it.

2. (Azure only) Click **Download Kubeconfig** to have the Kubeconfig file of the Compute Cluster downloaded to your computer.

3. Click **Kubeconfig** to grant access to download the Kubeconfig file.

   1. Provide the **Cloud User ID (ARN)** before downloading the Kubeconfig file.

   2. Click **Grant Access**.

   3. Click **Download Kubeconfig**.

4. Click **Delete Compute Cluster**, if you no longer need the additional Compute Cluster.

   1. Confirm the deletion of the additional Compute Cluster by clicking **Remove**.

3) Click **Networking** tab to view the subnet information of the Compute Cluster.

   1. Click \<icon> to update the **Kubernetes API Server Authorized IP Ranges**.

      1. Add or remove the CIDRs, and click **Save**.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPSSZi5ft5Grj3-dU2fQWexHXJXOxsft3XCWo6-M84tt036doU6dTLz9TVkoMK3N2FEoePjVPAO04D6qpHUIxo4UZqiVA5TIR9pbJgFSdnL2bhOrgTZN8SYNPUiigKb4RXv9tQ4NQ5R05p_KdLJ7Ko15o?key=OSI_VXIg5JPRMBrD4S-hEg)

4. Click **Encryption** tab to view the encryption key of the Compute Cluster.

5. Click **Node Groups** tab to have an illustrated overview of the resource utilization of the different services running on the Compute Cluster.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeV48jYsD0x-JS7vJv0WkH4yFsFEY-Tcwq0WnV9BkfV3ACXAtyjGP4XyGizAZo8OxSJYb3lZYGUHWM4MNhrESacIXXroXN6BLcaXfNXRA6RxL1oHgOIfha7K2hRWFKLRPnd3EXZ_65Ab-dMG23SVXSiHog?key=OSI_VXIg5JPRMBrD4S-hEg)

6. Click **Compute Cluster Version** to view the **Kubernetes** and **Infra Service** versions of the cluster.

7. Click **Logs** to check the different events of the Compute Cluster.

8. Click **Tags** to view the list of tags associated with the Compute Cluster.


## Enabling Compute Clusters for an existing environment<a id="h.29boo7uxmsvc"></a>

In case you already have an environment, but would like to have your services to run on the containerized platform enabled by Compute Clusters, you can add the default Compute Cluster to your existing environment.

**Required role:** _EnvironmentAdmin_

**Before you begin**

- Ensure that the environment has no default Compute Cluster provisioned.

- Ensure that the environment is started and available.


### Using CLI<a id="h.rfxvcs5xks7v"></a>

1. Run the following command to add the default Compute Cluster to the environment:

```
cdp environments initialize-aws-compute-cluster 
--environment-name <env_name>
--compute-cluster-configuration
privateCluster=false, 
kubeApiAuthorizedIpRanges=<cidr1>,<cidr2>,
workerNodeSubnets=<subnet1>,<subnet2>
```

The environment will have `COMPUTE_CLUSTER_CREATION_IN_PROGRESS` status. You can use the following command to check the status of the environment creation, the statusReason field will contain the information about the process:

```
cdp environments describe-environment --environment-name <env_name>
```

For more detailed status information about the cluster creation, you can use the following command:

cdp compute list-clusters --env-name-or-crn \<env\_name\_or\_crn>


### Using UI<a id="h.inxgrqr2nyfg"></a>

1. Navigate to your environment.

2. Click Compute Clusters.\
   The following message will indicate that Compute Cluster are not enabled for your environment:\
   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXddguin7C4rW5jb6fy4h3WEOQ99_eTSfvm_PBzRDkKU_m9ADR4o-Ezx7WR81CggIufUZ8XBbglD9TmiIKGfBTRceYUm0dcbMozLM0pe70iENnjghtYCxpfm7q9kj28xTnPJAsu0yTpaLrwH13_Yqd2ziYvj?key=OSI_VXIg5JPRMBrD4S-hEg)

3. Click **Enable Compute Clusters**.

4. Provide the necessary networking information for the **Kubernetes** cluster.

   1. If you need to create a Private Cluster, select the **Private Cluster** checkbox to create a private cluster that blocks all access to the API Server endpoint.\
      The following configurations must be set:

      1. (Azure Only) Select the **AKS Private DNS Zone ID** from the available drop-down list.

      2. (Azure Only) Select **Enable User Defined Routing** (UDR) checkbox.\
         In case you enable UDR, you must select the specific worker node subnet where the UDR is configured.

      3. Provide the CIDRs to the **Worker Node Subnets** field to specify subnets for the Kubernetes Nodes.\
         If subnets were provided in the previous **Network** configuration step, the **Worker Nodes Subnets** field is automatically filled out with the same subnets. You can remove the pre-filled subnets.

   2. If you do not need to create a Private Cluster, leave the **Private Cluster** checkbox unchecked.\
      The following configurations must be set:

      1. Provide the CIDRs to the **Kubernetes API Server Authorized IP Ranger** field to specify a set of IP ranges that will be allowed to access the Kubernetes API server.

      2. Provide the CIDRs to the **Worker Node Subnets** field to specify subnets for the Kubernetes Nodes.\
         If subnets were provided in the previous **Network** configuration step, the **Worker Nodes Subnets** field is automatically filled out with the same subnets. You can remove the pre-filled subnets.

5. Click **Upgrade Environment**.

You will be redirected to the **Compute Clusters** tab, where you can track the creation process of the default Compute Cluster.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpmD4jf7e-Tah067Hp3qlonafcR3xGmPjkZcMVXBBMMxEqJbvYDleoBx2Iru1bOUPQ2UnLO6WnkI3b45J0cAnBX15jPiJVgqXTEi2i5WH1F1MnaS7xxhlKI7cgLbumFV6i7bfirqC7EJImmTCCM9RmwFxr?key=OSI_VXIg5JPRMBrD4S-hEg)
