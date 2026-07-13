# IaC

[Quick Start](Quick%20Start%2037cd84c6b72a80c5bf55de1d40ae7f3d.md)

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html

estrutura:

```jsx
AWSTemplateFormatVersion: "versiondate" Description:StringMetadata: templatemetadataParameters: setofparametersRules: set ofrulesMappings: setofmappingsConditions: setofconditionsTransform: set oftransformsResources: set ofresourcesOutputs: set ofoutputs
```

## Modelo Simples de uma Instancia EC2:

```json
{"Resources":{"Ec2Instance":{"Type":"AWS::EC2::Instance","Properties":{"ImageId":"ami-9d23aeea","InstanceType":"m3.medium","KeyName":{"Ref":"KeyPair}}},"Outputs":{"InstanceId":{"Description":"InstanceId","Value":{"Ref":"Ec2Instance"}}}}
```

![image.png](image%203.png)

![image.png](image%204.png)