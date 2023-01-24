# [`infra-repos-shishifubing`][repo-url]

[![terraform][terraform-workflow-shield]][terraform-workflow-url]

This terraform module manages [shishifubing][owner-url] organization:

- It manages repositories
- It manages branch protection rules
- It manages organization settings
- It manages organization membership
- It mirrors all repositories in [shishifubing][owner-url] to [Gitlab][owner-gitlab-url]

# Usage

> **Note**
>
> GitHub's servers are "eventually consistent", not "immediately consistent",
>
> if you encounter errors (especially code 422), retry the operation
>
> 404 errors probably mean invalid token, check it

## CI

- Commit
- Make PR
- Merge

## Manual

```bash
# export auth variables
. ./variables.sh
# update the infrastructure
terraform apply
```

## Mirroring

> **Note**
>
> Pull mirroring is a premium Gitlab feature,
> so all Gitlab repositories are destroyed and then imported once every day to
> "_mirror_" them

## Regenerate module documentation

```bash
terraform-docs markdown table --recursive --output-file README.md .
```

# Getting started

[Setup an s3 bucket, setup terraform][setup-url]

```bash
# export auth variables
. ./variables.sh
# initialize the backend
terraform init -reconfigure -backend-config="main.s3.tfbackend"
# import existing repositories (if you need to)
./import.sh
# update the infrastructure
terraform apply
```

<!-- internal links -->

[branch_protection]: ./modules/branch_protection/
[repository]: ./modules/repository/

<!-- shield links -->

[terraform-workflow-shield]: https://img.shields.io/github/actions/workflow/status/shishifubing/infra-repos/terraform.yml?label=Terraform&style=for-the-badge

<!-- external links -->

[owner-url]: https://github.com/shishifubing
[owner-gitlab-url]: https://gitlab.com/shishifubing
[repo-url]: https://github.com/shishifubing/infra-repos-shishifubing
[setup-url]: https://github.com/shishifubing/infra-cloud-shishifubing.com/tree/main/cloud/yandex#setup-terraform-backend-and-local-environment
[terraform-workflow-url]: https://github.com/shishifubing/infra-repos-shishifubing/actions/workflows/terraform_main.yml

# Module documentation

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_github"></a> [github](#requirement\_github) | 5.14.0 |
| <a name="requirement_gitlab"></a> [gitlab](#requirement\_gitlab) | 15.7.1 |
| <a name="requirement_time"></a> [time](#requirement\_time) | 0.9.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_github"></a> [github](#provider\_github) | 5.14.0 |
| <a name="provider_gitlab"></a> [gitlab](#provider\_gitlab) | 15.7.1 |
| <a name="provider_time"></a> [time](#provider\_time) | 0.9.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_branch_protections"></a> [branch\_protections](#module\_branch\_protections) | ./modules/branch_protection | n/a |
| <a name="module_repositories"></a> [repositories](#module\_repositories) | ./modules/repository | n/a |

## Resources

| Name | Type |
|------|------|
| [github_membership.bot](https://registry.terraform.io/providers/integrations/github/5.14.0/docs/resources/membership) | resource |
| [github_organization_settings.organization](https://registry.terraform.io/providers/integrations/github/5.14.0/docs/resources/organization_settings) | resource |
| [gitlab_project.repository](https://registry.terraform.io/providers/gitlabhq/gitlab/15.7.1/docs/resources/project) | resource |
| [time_rotating.day](https://registry.terraform.io/providers/hashicorp/time/0.9.1/docs/resources/rotating) | resource |
| [gitlab_group.group](https://registry.terraform.io/providers/gitlabhq/gitlab/15.7.1/docs/data-sources/group) | data source |

## Inputs

No inputs.

## Outputs

No outputs.
<!-- END_TF_DOCS -->
