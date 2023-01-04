!#/bin/bash/
AWSTemplateFormatVersion: 2010-09-09
Description: Create my first EC2 instance using cloudformation and installing apache.
Parameters:
  Imageid: 
    Default: ami-0b0dcb5067f052a63
    Description: This is baseline Linux instance
    Type: String
Resources:
  WebAppInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref Imageid # ImageID valid only in us-east-1 region
      InstanceType: t2.micro
      KeyName: geetha123
      SecurityGroupIds:
        - !Ref WebAppSecurityGroup
      UserData: 
        Fn::Base64: |
          #!/bin/bash -xe
          yum update -y # good practice to update existing packages
          yum install -y httpd # install web server 
          systemctl start httpd
          systemctl enable httpd
          echo "Hello Geetha!" > /var/www/html/index.html

  WebAppSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupName: JenkinsGroup
      GroupDescription: "Allow HTTP/HTTPS and SSH inbound and outbound traffic"
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 443
          ToPort: 443
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: -1
          CidrIp: 0.0.0.0/0
