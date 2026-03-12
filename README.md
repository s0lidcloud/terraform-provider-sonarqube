# terraform-provider-sonarqube (s0lidcloud fork)

[![release](https://github.com/s0lidcloud/terraform-provider-sonarqube/actions/workflows/release.yaml/badge.svg)](https://github.com/s0lidcloud/terraform-provider-sonarqube/actions/workflows/release.yaml)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=s0lidcloud_terraform-provider-sonarqube&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=s0lidcloud_terraform-provider-sonarqube)
[![Go Report Card](https://goreportcard.com/badge/github.com/s0lidcloud/terraform-provider-sonarqube)](https://goreportcard.com/report/github.com/s0lidcloud/terraform-provider-sonarqube)
[![codecov](https://codecov.io/gh/s0lidcloud/terraform-provider-sonarqube/branch/master/graph/badge.svg)](https://codecov.io/gh/s0lidcloud/terraform-provider-sonarqube)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)

Terraform provider for managing Sonarqube configuration.

This is a **fork** of the original [jdamata/terraform-provider-sonarqube](https://github.com/jdamata/terraform-provider-sonarqube).

## Why this fork?

This fork was created to address several issues found in the original provider:

1.  **Correct Resource Lifecycle:** The original provider often throws hard errors during the `Read` phase if a resource is missing or was deleted externally. This fork correctly handles missing resources (404s and search misses) by returning an empty state, allowing Terraform to plan a re-creation instead of halting with an error.
2.  **Community Branch Plugin Support:** This provider correctly handles environments using the SonarQube Community Branch Plugin. It avoids hard errors when the plugin modifies default branch behavior or when resources are managed in a way that the original provider didn't expect.

## Installation
This provider is published to the Terraform Registry. To use it, add the following to your `main.tf`:

```hcl
terraform {
  required_providers {
    sonarqube = {
      source  = "s0lidcloud/sonarqube"
    }
  }
}
```

Please visit the [Terraform Registry](https://registry.terraform.io/providers/s0lidcloud/sonarqube) for full documentation and installation instructions.

## Developing the Provider

Working on this provider requires the following:

* [Terraform](https://www.terraform.io/downloads.html)
* [Go](http://www.golang.org)
* [Docker Engine](https://docs.docker.com/engine/install/)

You will also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `${GOPATH}/bin` to your `$PATH`.

To compile the provider, run `make`. This will install the provider into your GOPATH.

In order to run the full suite of Acceptance tests, run `make -i testacc`. These tests require Docker to be installed on the machine that runs them, and do not create any remote resources.

```sh
$ make -i testacc
```

## Debugging the Provider

See [debugging.md](docs/debugging.md)
