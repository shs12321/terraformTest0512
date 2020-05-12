#1차 시험때는 terraform plan 및 apply가 안되었습니다.
#이번엔 모두 정상 완료되나 네트워크 문제로 생각되는 nginx page접속 확인을 못 하였습니다.
#네트워크 문제로 반복된 timeout으로 제대로 확인이 어려웠습니다.



# terraformTest0512
'''
push test
'''
# 명령 프롬프트
'''
# nano ~/.bashrc
PS1="\[\033[32m\] \[\033[34;1m\]\W \[\033[32m\]\[\033[m\]\[\e[91m\]\[\e[00m\]$ "
echo "
export TF_VAR_AWS_ACCESS_KEY="키삭제"
export TF_VAR_AWS_SECRET_KEY="키삭제"
export TF_VAR_AWS_REGION="ap-northeast-2"
">> ~/.bashrc
'''
#default VPC를 웹UI로 만들고 시작
'''
vpc 검색 후 작업 - 기본 VPC생성
'''

#시큐리티그룹 생성
default에 ssh, http, https 0.0.0.0/0 위치무관 추가


#vars.tf
'''
ap-northeast-1 일본 추가
ap-northeast-2 서울도..
'''

#인스턴스 생성과정
'''
sol1 $ terraform init

sol1 $ . ~/.bashrc
여기서 IAM 사용자 액세스 관리에서 key생성 한거 적용 및 리전 적용

sol1 $ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.


------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-00edfb46b107f643c"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = "mykey"
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

  # aws_key_pair.mykey will be created
  + resource "aws_key_pair" "mykey" {
      + fingerprint = (known after apply)
      + id          = (known after apply)
      + key_name    = "mykey"
      + key_pair_id = (known after apply)
      + public_key  = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDHwhiV6T7Pqzdlnm9JtR1ZlGaL8FviLTvr8N+MoFCLijuv4csmEpP2MO2MSmyuPrppVlwiMZgZy0o4FRth730r/pQGLhoc1jDgYb8rNtFlpqT+u0A1nzxn+1dHlRMl9Ts8imA33pGW/F4jtnY8fG0gM6Ap0UQX83r8q5L/W8NIvCqwSG0Zg1CfXZTTnviqzESHY+MfE58KPlqd3E1VNsTMihYt0mlBF0L9QSSeL5nEjL3nF/AK6A6EN9Ixsl6yIHK5nXR7rrL6wTAN/BTBEQdluA+Kt4Px9nLv2CKwi9G/N6CfPyxr/daMBC3/QpGJZ/PGurNUYZWgLmUjLEStWVYJ ubuntu@u1"
    }

Plan: 2 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

Note: You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.

sol1 $ ta

terraform destroy -auto-approve
terraform init
terraform apply -auto-approve
cat terraform.tfstate|grep public_ip|grep -v associate

aws_key_pair.mykey: Refreshing state... [id=mykey]
aws_instance.example: Refreshing state... [id=i-00657cc7e02a02143]
aws_instance.example: Destroying... [id=i-00657cc7e02a02143]
aws_instance.example: Still destroying... [id=i-00657cc7e02a02143, 10s elapsed]
aws_instance.example: Still destroying... [id=i-00657cc7e02a02143, 20s elapsed]
aws_instance.example: Still destroying... [id=i-00657cc7e02a02143, 30s elapsed]
aws_instance.example: Destruction complete after 30s
aws_key_pair.mykey: Destroying... [id=mykey]
aws_key_pair.mykey: Destruction complete after 0s

Destroy complete! Resources: 2 destroyed.

Initializing the backend...

Initializing provider plugins...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.aws: version = "~> 2.61"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
aws_key_pair.mykey: Creating...
aws_key_pair.mykey: Creation complete after 0s [id=mykey]
aws_instance.example: Creating...
aws_instance.example: Still creating... [10s elapsed]
aws_instance.example: Still creating... [20s elapsed]
aws_instance.example: Still creating... [30s elapsed]
aws_instance.example: Provisioning with 'file'...
aws_instance.example: Still creating... [40s elapsed]
aws_instance.example: Still creating... [50s elapsed]
aws_instance.example: Still creating... [1m0s elapsed]
aws_instance.example: Still creating... [1m10s elapsed]
aws_instance.example: Still creating... [1m20s elapsed]
aws_instance.example: Still creating... [1m30s elapsed]
aws_instance.example: Still creating... [1m40s elapsed]
aws_instance.example: Still creating... [1m50s elapsed]
aws_instance.example: Still creating... [2m0s elapsed]
aws_instance.example: Still creating... [2m10s elapsed]
aws_instance.example: Still creating... [2m20s elapsed]
aws_instance.example: Still creating... [2m30s elapsed]
aws_instance.example: Still creating... [2m40s elapsed]
aws_instance.example: Still creating... [2m50s elapsed]
aws_instance.example: Still creating... [3m0s elapsed]
aws_instance.example: Still creating... [3m10s elapsed]
aws_instance.example: Still creating... [3m20s elapsed]
aws_instance.example: Still creating... [3m30s elapsed]
aws_instance.example: Still creating... [3m40s elapsed]
aws_instance.example: Still creating... [3m50s elapsed]
aws_instance.example: Still creating... [4m0s elapsed]
aws_instance.example: Still creating... [4m10s elapsed]
aws_instance.example: Still creating... [4m20s elapsed]
aws_instance.example: Still creating... [4m30s elapsed]
aws_instance.example: Still creating... [4m40s elapsed]
aws_instance.example: Still creating... [4m50s elapsed]
aws_instance.example: Still creating... [5m0s elapsed]
aws_instance.example: Still creating... [5m10s elapsed]
aws_instance.example: Still creating... [5m20s elapsed]
aws_instance.example: Still creating... [5m30s elapsed]


Error: timeout - last error: SSH authentication failed (nginx@54.180.97.228:22): ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain


            "public_ip": "54.180.97.228",
 sol1 $



'''
#TEST과정 :
'''
webpage접속 : 인스턴스의 pulbic IP확인.

명령줄 : set|grep TF_VAR
'''
