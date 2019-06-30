# wordpress on elastic beanstalk

This repo represents that you will need in order to setup a wordpress instance on elasticbeanstalk.

Fork this repo and modify for your requirement. 

### Stack
- Wordpress
- MySQL
- Docker
- S3
- Amazon Linux
- Elastic Beanstalk


Once you setup the wordpress environment, add the following environment variables. 

- WORDPRESS_DB_HOST: mysql
- WORDPRESS_DB_NAME: db
- WORDPRESS_DB_PASSWORD: root
- WORDPRESS_DB_USER: example
- WORDPRESS_CONFIG_EXTRA: define('FS_METHOD', 'direct');


Beanstalk requires permission to the s3 bucket for asset syncing.

Sample policy json for s3 bucket.
```
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "beanstalk",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::1234567890:role/aws-elasticbeanstalk-ec2-role"
            },
            "Action": [
                "s3:Get*",
                "s3:List*",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucketname/*",
                "arn:aws:s3:::bucketname"
            ]
        }
    ]
}
```

replace my-s3-bucket in ```.ebextensions/wp.config``` with your bucket name.

### Notes:
- This is a single site setup. For multisite here's the things to know before 👉: http://codex.wordpress.org/Create_A_Network
- We recommend using Mysql. Here's why 👉 https://codex.wordpress.org/Using_Alternative_Databases





