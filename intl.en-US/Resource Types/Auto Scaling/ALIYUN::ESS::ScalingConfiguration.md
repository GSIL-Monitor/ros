# ALIYUN::ESS::ScalingConfiguration {#concept_51203_zh .concept}

The ALIYUN::ESS::ScalingConfiguration type is used to create a scaling configuration.

## Syntax {#section_k4p_5d1_mfb .section}

```language-json
{
   "Type" : "ALIYUN::ESS::ScalingConfiguration",
   "Properties" : {
         "DiskMappings" : List,
         "InternetMaxBandwidthIn" : Integer,
         "InstanceId" : String,
         "SecurityGroupId" : String,
         "SystemDiskCategory" : String,
		 "SystemDiskSize" : Integer,
         "ImageId" : String,
         "InternetMaxBandwidthOut" : Integer,
         "IoOptimized" : String,
         "ScalingGroupId" : String,
         "InternetChargeType" : String,
         "InstanceType" : String,
         "ScalingConfigurationName" : String,
		 "InstanceTypes": List,
		 "KeyPairName": String,
		 "UserData": String,
		 "RamRoleName": String
   }
}

```

## Properties {#section_zvc_wd1_mfb .section}

|Name|Type|Required|Update allowed|Description|Constraint|
|ScalingGroupId|string|Yes|No|ID of the scaling group to which the scaling configuration belongs|N/A|
|DiskMappings|list|No|No|Disk you want to attach|Up to four disks can be attached|
|InternetChargeType|string|No|No|Bandwidth billing method for access over the Internet|Value options: PayByBandwidth and PayByTraffic. Default value: PayByTraffic|
|InternetMaxBandwidthIn|integer|No|No|Maximum Internet inbound bandwidth, in Mbps|Value range: \[1, 100\]. Default value: 100|
|InternetMaxBandwidthOut|integer|No|No|Maximum Internet outbound bandwidth,in Mbps|Value range in PayByBandwidth mode: \[0, 200\]; default value: 0. Value range in PayByTraffic mode: \[1, 200\]. This parameter must be specified in PayByTraffic mode|
|InstanceId|string|No|No|ID of the ECS instance whose attributes are used to create the scaling configuration|N/A|
|SystemDiskCategory|string|No|No|System disk type|Value options: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|ImageId|string|No|No|ID of the image used to start the ECS instance. The image can be a public image, custom image, or a marketplace image| [ECS public image list](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList) |
|InstanceType|string|No|No|ECS instance type|[Instance generations and type families](https://www.alibabacloud.com/help/doc-detail/25378.htm) |
|SecurityGroupId|string|No|No|ID of the security group to which the created instance belongs|N/A|
|IoOptimized|string|No|No|Whether to create an I/O optimized instance|Value options: none \(non-I/O optimized\) and optimized \(I/O optimized\). Default value: none|
|ScalingConfigurationName|string|No|No|Displayed name of the scaling configuration|The name is a string of 2 to 40 Chinese characters or English letters. It must start with a digit, an uppercase/lowercase letter, or a Chinese character and can contain English letters, Chinese characters, digits, underscores\(\_\), periods\(.\), and hyphens\(-\). The name must be unique in the same scaling group. If this parameter is not specified, the default value is ScalingConfigurationId|
|KeyPairName|string|No|No|Name of the key pair bound to the ECS instance|This parameter is ignored if the key pair is bound to a Windows ECS instance. Default value: null. If this parameter is set, the value of the Password parameter will be set to the instance. However, the password logon mode in the Linux operating system will be initialized to be disabled|
|RamRoleName|string|No|No|RAM role name|You can use the RAM API ListRoles to query instance RAM role names. For more information, see API [CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm) and [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm).|
|SystemDiskSize|string|No|Yes|System disk size|Value range: \[40, 500\]. If a custom image is used to create a system disk, make sure that the system disk size is greater than the image size.|
|UserData|string|No|No|User data that is input during ECS instance creation.|The user data size cannot exceed 16 KB.|
|InstanceTypes|list|No|No|Multiple ECS instance specifications|You can specify up to 10 ECS instance specifications. If InstanceType is specified, the value of InstanceType is ignored|

## DiskMappings syntax {#section_cvf_221_mfb .section}

```language-json
"DiskMappings" : [
    {
		"Category" : String,
		"DiskName" : String,
		"Description" : String,
		"Device" : String,
		"SnapshotId" : String,
		"Size" : String
	}
]

```

## DiskMappings properties { .section}

|Name|Type|Required|Update allowed|Description|Constraint|
|Size|string|Yes|No|Data disk size,in GB|N/A|
|Category|string|No|No|Data disk type|Value options: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssdDefault|
|DiskName|string|No|No|Data disk name|The data disk name can contain a maximum of 128 characters including Chinese characters and English letters , digits, underscores\(\_\), periods\(.\), and hyphens\(-\)|
|Description|string|No|No|Description|Value range: \[2, 256\]. Default value: null|
|Device|string|No|No|Device name of the data disk in the ECS instance|Example: /dev/xvd\[a-z\]|
|SnapshotId|string|No|No|ID of the snapshot used to create the data disk|N/A|

## Response value {#section_bsn_k21_mfb .section}

**Fn::GetAtt**

ScalingConfigurationId: ID of the scaling configuration, which is generated by the system and is globally unique.

## Example {#section_ozp_n21_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ImageId": "ubuntu1404_64_20G_aliaegis_20150325.vhd",
        "InstanceType": "ecs.t1.small",
        "InstanceId": "i-25xhhcqbu",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 1,
        "InternetMaxBandwidthOut": 20,
        "SystemDisk_Category": "cloud",
        "ScalingGroupId": "bwhtvpcBcKYac9fe3vd0kv7E",
        "SecurityGroupId": "sg-25zwc3se0",
        "DiskMappings": [
            {
                "Size": 10
            },
            {
                "Category": "cloud",
                "Size": 10
            }
        ]
      }
    }
  },
  "Outputs": {
    "ScalingConfiguration": {
         "Value" : {"get_attr": ["ScalingConfigurationId"]}
    }
  }
}

```

