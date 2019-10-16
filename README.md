# bucket-access-bucket

You have a bucket with a `private` ACL, and you want to share access with only a password. Well,
now you can.

Try it out at https://drfk89hh94pbd.cloudfront.net

The password is `hunter2`.

## How does it work?

* Send a link and password to your friend / colleague / lover / apprentice / chef.

* They enter the password, and click the nice big button.

* Access is granted!

## No really, how does it work?

The bucket is fronted with a CloudFront distribution. The S3 bucket only allows access from the
distribution.

The button / form sends off to a Lambda function that verifies the password and then produces a
signed cookie. This cookie is retrieved by the form, set in the browser and then you can view the
bucket unimpeded! Magic.

## Amazeballs! How do I use it?

Using Terraform? See `terraform_example` for a quick-start. You'll need to create a CloudFront key
pair and choose a password and then encrypt them both separately with the KMS key the module
generates. These form the variables in the terraform.tfvars file (see terraform.tfvars.example).

See: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-trusted-signers.html#private-content-creating-cloudfront-key-pairs

Not using Terraform? That's a shame! I'd love you to contribute a CloudFormation template or
instructions.

## For multple aws config:

alias aws='docker run --rm -t $(tty &>/dev/null && echo "-i") -e "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}" -e "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}" -e "AWS_DEFAULT_REGION=${AWS_DEFAULT_REGION}" -v "$(pwd):/project" mesosphere/aws-cli'
