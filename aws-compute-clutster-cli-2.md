**What is the CLI command to register an CDP AWS environment with a default compute cluster?**

The CDP CLI command to register an CDP AWS environment with a default compute cluster is as follows-
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