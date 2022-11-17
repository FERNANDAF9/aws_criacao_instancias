# Como listar, criar e excluir instâncias via AWS CLI :globe_with_meridians:
## Objetivos
Esse projeto visa um estudo acerca de conteúdos que englobam o DevOps, mais especificamente o estudos da criação, exclusão e listagem de instâncias por meio de um console CLI, isto é, por linha de comando. 
## Projeto
Para o estudo, foi utilizado uma máquina Linux, e criados servidores com SO Linux. Logo, para acessar remotamente esse servidor, visto que o SO Windows não consegue acessar diretamente um SO Linux, é necessário a utilização do Software Putty.
Para a criação de uma nova instância via linha de comando, primeiro precisamos configurar nossos dados da AWS. Para isso, digitamos no console:

`aws configure`
<h1 align=center>
<img width=600  src="https://user-images.githubusercontent.com/56310579/202342477-bc05f6b5-81cc-487f-bb57-bd5ea7b3c68f.png"> </>
</h1>


É solicitado ao usuário duas chaves de acesso (**Access Key ID e Secret Access Key**), referente ao usuário de login, também previamente criado na AWS. 
A parte da região não é necessária no momento, e no formato de saída (output) escolhemos json por ser um formato de mais fácil leitura, porém também é possível colocar no formato text.

## Listar Instâncias
Para listar instâncias, digitamos:


`aws ec2 describe-instances`

Assim, um json é criado listando todas as instâncias, e seus respectivos dados.
<h1 align=center>
<img width=500  src="https://user-images.githubusercontent.com/56310579/202344647-31823098-2462-4816-b7ee-51f2a520681a.png"> </>
</h1>

## Criar Instâncias

Para criar uma instância via AWS CLI, podem ser passados diversos parâmetros, mas para fins de estudo, colocamos alguns principais:

```
aws ec2  run-instances --image-id ami-0b0dcb5067f052a63 --count 1 --instance-type t2.micro --key-name ChavePrivadaAWS --security-group-ids sg-00b3a32c880028e4c --subnet-id subnet-0bae1f2b8b89405a4
```
A seguir um pouco da explicação sobre cada parâmetro.

**--image-id**: referente a AMI, cada AMI possui um ID . Essa informação pode ser obtida no console em EC2/Images/AMI’s Catalog.
Uma Imagem de máquina da Amazon (AMI) é um modelo que contém uma configuração de software (por exemplo, sistema operacional, servidor de aplicação e aplicações).
No exemplo em questão, utilizou-se a AMI Amazon Linux 2 AMI (HVM).
**--count**: Quantidade de instâncias a serem criadas.

**--instance-type**: A especificação que define a memória, a CPU, a capacidade de armazenamento e o custo por hora da instância. Essa informação pode ser obtida no console em EC2/Instance Types.
Nesse caso utilizou-se uma t2.micro, pois é elegível para “free-tier” e muito utilizada para fins de estudo.

**--key-name**: Chave previamente criada no console AWS, tem o objetivo de promover maior segurança, sendo um conjunto de credenciais de segurança que você usa para provar sua identidade ao se conectar a uma instância.

**--security-group**: Grupo previamente criado no console AWS Um grupo de segurança atua como firewall virtual para as instâncias do EC2 visando controlar o tráfego de entrada e de saída. 

**--subnet-id**: As subnets são espaços de rede menores que fazem parte da nuvem. Podem ser ou subnets privadas ou subnets públicas, dependendo da configuração desejada. Essa informação pode ser obtida no console em VCP/Virtual Private Cloud/Subnets.


## Excluir instâncias
Para excluir instâncias, primeiro precisamos saber os ID's das instâncias a serem deletadas.

O ID de instâncias pode ser verificado no console AWS, ou listando as instâncias na linha de comando, como visto anteriormente. A informação é mostrada em "InstanceID".
<h1 align=center>
<img width=500  src="https://user-images.githubusercontent.com/56310579/202346125-da1781ae-f415-4f56-9271-65135d0febda.png"> </>
</h1>
Para excluir instâncias, basta digitar:

`aws ec2 terminate-instances --instance-ids "id_da_instância"`

<h1 align=center>
<img width=700  src="https://user-images.githubusercontent.com/56310579/202346869-8a42c966-a19a-4fec-bd01-7a993e8f5d6d.png"> </>
</h1>

## Considerações finais
Obrigada por visitar!

