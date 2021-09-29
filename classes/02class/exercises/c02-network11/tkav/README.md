# c02-network11

## Commands Execution Output

For the exercises below, you should use all the custom created network resources. NOT THE DEFAULT ONES.

- Commands for launching an EC2 instance on public subnet with public SG attached

```
aws ec2 run-instances \
		--image-id ami-0210560cedcb09f07 \
		--key-name tk-contino-dev \
		--instance-type t2.micro \
    --subnet-id subnet-035eecc54395ab403 \
    --security-group-ids sg-040506fdcfbbaf676 \
    --associate-public-ip-address \
    --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=tk-dojo-public}]"

#Attach your private SG to your public instance

aws ec2 modify-instance-attribute \
	--instance-id i-01aeeebf7b0caaad0 \
	--groups sg-0ede42a137608a804

```

- Commands for launching an EC2 instance on private subnet using custom ENI and private SG attached

```
aws ec2 run-instances \
		--image-id ami-0210560cedcb09f07 \
		--key-name tk-contino-dev \
		--instance-type t2.micro \
		--network-interfaces "[{\"NetworkInterfaceId\": \"eni-05456976fb2ae934a\",\"DeviceIndex\":0}]" \
    --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=tk-dojo-private}]"
```

- Commands for accessing your public instance using ssh

```
`ssh 13.236.36.82 -l ec2-user`
```
(key has already been added)

- Commands for accessing your private instance from public one

```
ssh -J ec2-user@13.236.36.82 ec2-user@10.128.20.10
```

- Commands for testing ping to `8.8.8.8` from private instance

```
[ec2-user@ip-10-128-20-10 ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=109 time=1.88 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=109 time=1.43 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=109 time=1.55 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=109 time=1.48 ms
```

- Any extra challenges faced?


<!-- Don't change anything below this point-->
***
Answer for exercise [c02-network11](https://github.com/devopsacademyau/academy/blob/893381c6f0b69434d9e8597d3d4b1c17f9bc1371/classes/02class/exercises/c02-network11/README.md)