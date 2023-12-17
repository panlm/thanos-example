# setup variable for your POC environment

```sh
CLUSTER_NAME_1=ekscluster1
CLUSTER_NAME_2=ekscluster2
CLUSTER_NAME_3=ekscluster3
DOMAIN_NAME=thanos.eks1217.aws.panlm.xyz
THANOS_BUCKET_NAME=thanos-store-123456
AWS_DEFAULT_REGION=us-east-2
export CLUSTER_NAME_1 CLUSTER_NAME_2 CLUSTER_NAME_3 DOMAIN_NAME THANOS_BUCKET_NAME AWS_DEFAULT_REGION

mkdir POC
cd POC-template
find ./ -type d -name "[a-z]*" -exec mkdir ../POC/{} \;

find ./ -type f -name "*" |while read filename ; do
  cat $filename |envsubst > ../POC/$filename
done

cd ../POC/
```