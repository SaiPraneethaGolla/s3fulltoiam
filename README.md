# s3fulltoiam
AWSTemplateFormatVersion: '2010-09-09'
Description: Provision a simple Amazon Linux Instance and allow SSH  
Resources:
  IAMRoleS3fullaccess:
    Type: AWS::IAM::Role
    Properties: 
      AssumeRolePolicyDocument: 
          Version: "2012-10-17"
          Statement:
            - Effect: Allow
              Principal:
                Service:
                  - ec2.amazonaws.com
              Action:
                - 'sts:AssumeRole'
      Path: /
      Policies:
        - PolicyName: S3fullaccess
          PolicyDocument:
            Version: "2012-10-17"
            Statement:
              - Effect: Allow
                Action: 's3:*'
                Resource: '*'
  RootInstanceProfile:
    Type: 'AWS::IAM::InstanceProfile'
    Properties:
      Path: /
      Roles:
        - !Ref IAMRoleS3fullaccess   
