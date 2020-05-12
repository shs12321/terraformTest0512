# terraformTest0512
'''
push test
'''
#1차 시험때와 동일합니다.
#아래 eu-west-1만 수정하였습니다.

# 명령 프롬프트
'''
# nano ~/.bashrc
PS1="\[\033[32m\] \[\033[34;1m\]\W \[\033[32m\]\[\033[m\]\[\e[91m\]\[\e[00m\]$ "
echo "
export TF_VAR_AWS_ACCESS_KEY="키삭제"
export TF_VAR_AWS_SECRET_KEY="키삭제"
export TF_VAR_AWS_REGION="eu-west-1"
">> ~/.bashrc
'''

# 멀티인스턴스 적용 instance.tf
'''
esource "aws_instance" "example" {
  count         = var.instance_count
'''

#vars
'''
variable "instance_count" {
  default = "4"
}

#test방법
'''
aws에서 instance 정보 확인
'''
