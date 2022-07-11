+++
title = "Setup AWS credentials for your AWS account and create new user."
author = ["Anak Wannaphaschaiyong"]
tags = ["iam", "blog", "setup"]
draft = false
+++

## AWS credentials and configuration to your AWS account. {#aws-credentials-and-configuration-to-your-aws-account-dot}

AWS configuration file and credential file can be found at `~/.aws/config` and `~/.aws/credentials`.

Once that done, you can use the following to get your account information.

```sh
aws sts get-caller-identity
```

It will not show secret key `aws_access_key_id` and `aws_secret_access_key` which you have set. It will only show information of your account including: `UserId`, `AccountId`, `Arn`.


## AWS users {#aws-users}

Note that 1 account has 1 root and can have many `IAM user`.

Word of advice is to not NEVER use root account directly. ALWAYS create IAM users within your account. You can create user as followed

```sh
aws iam create-user --user-name <new-user-name>
```

Then you have to create password for the new user.

```sh
aws iam create-login-profile --user-name <new-user-name> --password <password>
```

If you are admin (root user) and have to create new user for other, says your co-worker. Using the below command, your coworker (or anyone) will be asked to create new password when you login to the new username for the first time.

```sh
aws iam create-login-profile --user-name <new-user-name> --password-reset-required --password <password-to-be-changed>
```

You can check that user is created using the following

```sh
aws iam list-users
```
