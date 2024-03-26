# README
目录说明
- prometheus: 包含针对 [prometheus operator](https://github.com/prometheus-operator/prometheus-operator) 的定制 Values
- s3-config: 提供 Thanos 组件访问 S3 的相关配置信息，这些配置将会被创建成 kubernetes 的 secret
- thanos-values: 包含针对 [bitnami thanos chart](https://github.com/bitnami/charts/tree/main/bitnami/thanos) 的定制 Values 
- thanos-yaml: 包含自建 Thanos 使用的相关 Yaml 定义文件。更多模板参考 [link](https://github.com/thanos-io/kube-thanos)


# setup variable for your POC environment
为了方便部署，配置模板中预置了变量，使用下面脚本创建实验用的目录，并且针对你的实验环境替换相应的变量。配合本实验环境使用的 Terraform 脚本参见（[github](https://github.com/panlm/eks-blueprints-clusters/tree/main/multi-cluster-thanos)）。

```sh
DATE=$(TZ=EAT-8 date +%m%d)
CLUSTER_NAME_1=ekscluster1
CLUSTER_NAME_2=ekscluster2
CLUSTER_NAME_3=ekscluster3
DOMAIN_NAME=thanos.eks${DATE}.aws.panlm.xyz
THANOS_BUCKET_NAME=thanos-store-${DATE}-$RANDOM
AWS_DEFAULT_REGION=us-east-2
export CLUSTER_NAME_1 CLUSTER_NAME_2 CLUSTER_NAME_3 DOMAIN_NAME THANOS_BUCKET_NAME AWS_DEFAULT_REGION

mkdir POC
cd POC-template
find ./ -type d -name "[a-z]*" -exec mkdir ../POC/{} \;

find ./ -type f -name "*" |while read filename ; do
  cat $filename |envsubst '$CLUSTER_NAME_1 $CLUSTER_NAME_2 $CLUSTER_NAME_3 $DOMAIN_NAME $THANOS_BUCKET_NAME $AWS_DEFAULT_REGION' > ../POC/$filename
done
```

# refer
- https://panlm.github.io/EKS/solutions/monitor/POC-prometheus-ha-architect-with-thanos/


