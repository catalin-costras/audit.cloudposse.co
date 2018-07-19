<!-- This file was automatically generated by the `build-harness`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

[![Cloud Posse](https://cloudposse.com/logo-300x69.svg)](https://cloudposse.com)

# audit.cloudposse.co [![Codefresh Build Status](https://g.codefresh.io/api/badges/build?repoOwner=cloudposse&repoName=audit.cloudposse.co&branch=master&pipelineName=audit.cloudposse.co&accountName=cloudposse&type=cf-1)](https://g.codefresh.io/pipelines/audit.cloudposse.co/builds) [![Latest Release](https://img.shields.io/github/release/cloudposse/audit.cloudposse.co.svg)](https://github.com/cloudposse/audit.cloudposse.co/releases) [![Slack Community](https://slack.cloudposse.com/badge.svg)](https://slack.cloudposse.com)


Terraform/Kubernetes Reference Infrastructure for Cloud Posse Audit Organization in AWS. 

This account is suitable for receiving all CloudTrail logs from other accounts. 

__NOTE:__ Before creating the Audit infrastructure, you need to provision the [Parent ("Root") Organization](https://github.com/cloudposse/root.cloudposse.co) in AWS (because it creates resources needed for all other accounts). Follow the steps in [README](https://github.com/cloudposse/root.cloudposse.co) first. You need to do it only once.


---

This project is part of our comprehensive ["SweetOps"](https://docs.cloudposse.com) approach towards DevOps. 


It's 100% Open Source and licensed under the [APACHE2](LICENSE).









## Introduction

We use [geodesic](https://github.com/cloudposse/geodesic) to define and build world-class cloud infrastructures backed by AWS and powered by Kubernetes.

`geodesic` exposes many tools that can be used to define and provision AWS and Kubernetes resources.

Here is the list of tools we use to provision the `audit.cloudposse.co` infrastructure:

* [aws-vault](https://github.com/99designs/aws-vault)
* [chamber](https://github.com/segmentio/chamber)
* [terraform](https://www.terraform.io/)


## Quick Start


### Setup AWS Role

__NOTE:__ You need to do it only once.

Configure AWS profile in `~/.aws/config`. Make sure to change username (username@cloudposse.co) to your own.

```bash
[profile cpco-audit-admin]
region=us-west-2
role_arn=arn:aws:iam::205035139483:role/OrganizationAccountAccessRole
mfa_serial=arn:aws:iam::323330167063:mfa/username@cloudposse.co
source_profile=cpco
```

### Install and setup aws-vault

__NOTE:__ You need to do it only once.

We use [aws-vault](https://docs.cloudposse.com/tools/aws-vault/) to store IAM credentials in your operating system's secure keystore and then generates temporary credentials from those to expose to your shell and applications.

Install [aws-vault](https://docs.cloudposse.com/tools/aws-vault/) on your local computer first.

On MacOS, you may use `homebrew cask`

```bash
brew cask install aws-vault
```

Then setup your secret credentials for AWS in `aws-vault`
```bash
aws-vault add --backend file cpco
```

__NOTE:__ You should set `AWS_VAULT_BACKEND=file` in your shell rc config (e.g. `~/.bashrc`) so it persists.

For more info, see [aws-vault](https://docs.cloudposse.com/tools/aws-vault/)


## Examples

### Build Docker Image

```
# Initialize the project's build-harness
make init

# Build docker image
make docker/build
```

### Install the wrapper shell
```bash
make install
```

### Run the shell
```bash
audit.cloudposse.co
```

### Login to AWS with your MFA device
```bash
assume-role
```

__NOTE:__ Before provisioning AWS resources with Terraform, you need to create `tfstate-backend` first (S3 bucket to store Terraform state and DynamoDB table for state locking).

Follow the steps in this [README](https://github.com/cloudposse/terraform-root-modules/blob/master/aws/tfstate-backend/). You need to do it only once.

After `tfstate-backend` has been provisioned, follow the rest of the instructions in the order shown below.


### Provision `dns` with Terraform

Change directory to `dns` folder
```bash
cd /conf/dns
```

Run Terraform
```bash
init-terraform
terraform plan
terraform apply
```

For more info, see [geodesic-with-terraform](https://docs.cloudposse.com/geodesic/module/with-terraform/)

### Provision `cloudtrail` with Terraform

```bash
cd /conf/cloudtrail
init-terraform
terraform plan
terraform apply
```




## Makefile Targets
```
Available targets:

  all                                 Initialize build-harness, install deps, build docker container, install wrapper script and run shell
  build                               Build docker image
  deps                                Install dependencies (if any)
  help                                This help screen
  help/all                            Display help for all targets
  install                             Install wrapper script from geodesic container
  push                                Push docker image to registry
  run                                 Start the geodesic shell by calling wrapper script

```



## Related Projects

Check out these related projects.

- [Packages](https://github.com/cloudposse/packages) - Cloud Posse installer and distribution of native apps
- [Build Harness](https://github.com/cloudposse/dev) - Collection of Makefiles to facilitate building Golang projects, Dockerfiles, Helm charts, and more
- [terraform-root-modules](https://github.com/cloudposse/terraform-root-modules) - Collection of Terraform "root module" invocations for provisioning reference architectures
- [root.cloudposse.co](https://github.com/cloudposse/root.cloudposse.co) - Example Terraform Reference Architecture of a Geodesic Module for a Parent ("Root") Organization in AWS.
- [prod.cloudposse.co](https://github.com/cloudposse/prod.cloudposse.co) - Example Terraform Reference Architecture of a Geodesic Module for a Production Organization in AWS.
- [staging.cloudposse.co](https://github.com/cloudposse/staging.cloudposse.co) - Example Terraform Reference Architecture of a Geodesic Module for a Staging Organization in AWS.
- [dev.cloudposse.co](https://github.com/cloudposse/dev.cloudposse.co) - Example Terraform Reference Architecture of a Geodesic Module for a Development Sandbox Organization in AWS.
- [testing.cloudposse.co](https://github.com/cloudposse/testing.cloudposse.co) - Example Terraform Reference Architecture that implements a Geodesic Module for an Automated Testing Organization in AWS




## References

For additional context, refer to some of these links. 

- [Cloud Posse Documentation](https://docs.cloudposse.com) - Complete documentation for the Cloud Posse solution


## Help

**Got a question?**

File a GitHub [issue](https://github.com/cloudposse/audit.cloudposse.co/issues), send us an [email][email] or join our [Slack Community][slack].

## Commerical Support

Work directly with our team of DevOps experts via email, slack, and video conferencing. 

We provide *commercial support* for all of our [Open Source][github] projects. As a *Dedicated Support* customer, you have access to our team of subject matter experts at a fraction of the cost of a fulltime engineer. 

[![E-Mail](https://img.shields.io/badge/email-hello@cloudposse.com-blue.svg)](mailto:hello@cloudposse.com)

- **Questions.** We'll use a Shared Slack channel between your team and ours.
- **Troubleshooting.** We'll help you triage why things aren't working.
- **Code Reviews.** We'll review your Pull Requests and provide constructive feedback.
- **Bug Fixes.** We'll rapidly work to fix any bugs in our projects.
- **Build New Terraform Modules.** We'll develop original modules to provision infrastructure.
- **Cloud Architecture.** We'll assist with your cloud strategy and design.
- **Implementation.** We'll provide hands on support to implement our reference architectures. 


## Community Forum

Get access to our [Open Source Community Forum][slack] on Slack. It's **FREE** to join for everyone! Our "SweetOps" community is where you get to talk with others who share a similar vision for how to rollout and manage infrastructure. This is the best place to talk shop, ask questions, solicit feedback, and work together as a community to build *sweet* infrastructure.

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/audit.cloudposse.co/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://github.com/orgs/cloudposse/projects/3) with our other projects, we would love to hear from you! Shoot us an [email](mailto:hello@cloudposse.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!


## Copyright

Copyright © 2017-2018 [Cloud Posse, LLC](https://cloudposse.com)



## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.









## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

This project is maintained and funded by [Cloud Posse, LLC][website]. Like it? Please let us know at <hello@cloudposse.com>

[![Cloud Posse](https://cloudposse.com/logo-300x69.svg)](https://cloudposse.com)

We're a [DevOps Professional Services][hire] company based in Los Angeles, CA. We love [Open Source Software](https://github.com/cloudposse/)!

We offer paid support on all of our projects.  

Check out [our other projects][github], [apply for a job][jobs], or [hire us][hire] to help with your cloud strategy and implementation.

  [docs]: https://docs.cloudposse.com/
  [website]: https://cloudposse.com/
  [github]: https://github.com/cloudposse/
  [jobs]: https://cloudposse.com/jobs/
  [hire]: https://cloudposse.com/contact/
  [slack]: https://slack.cloudposse.com/
  [linkedin]: https://www.linkedin.com/company/cloudposse
  [twitter]: https://twitter.com/cloudposse/
  [email]: mailto:hello@cloudposse.com


