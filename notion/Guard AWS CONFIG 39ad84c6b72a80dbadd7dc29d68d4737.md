# Guard AWS CONFIG

```bash
let ipv4 = '0.0.0.0/0'
let ipv6 = '::/0'

    rule conferir when 
        resourceType == "AWS::EC2::SecurityGroup" {
            configuration.ipPermissions[*].ipv6Ranges[*].cidrIpv6 != %ipv6
            configuration.ipPermissions[*].ipv4Ranges[*].cidrIp != %ipv4
        }
        
        #correto abaixo
        
let ipv4 = '0.0.0.0/0'
let ipv6 = '::/0'

rule conferir when
    resourceType == "AWS::EC2::SecurityGroup" {
    configuration.ipPermissions empty or
    configuration.ipPermissions[*] {
        ipv6Ranges empty or ipv6Ranges[*].cidrIpv6 != %ipv6
        ipv4Ranges empty or ipv4Ranges[*].cidrIp != %ipv4
    }
}        
```