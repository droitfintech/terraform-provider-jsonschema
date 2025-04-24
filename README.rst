=============================
terraform-provider-jsonschema
=============================

.. contents::
    :local:
    :depth: 2


Abstract
========

A |terraform|_ provider for validating json files using |json-schema|_.

Installation
============

On |terraform|_ versions 0.13+ use:

.. code-block:: terraform

  terraform {
    required_providers {
      jsonschema = {
        source = "xxxbobrxxx/jsonschema"
        version = "0.1.0"
      }
    }
  }

For |terraform|_ versions 0.12 or lower use instructions: |terraform-install-plugin|_

Usage
=====

See |user-docs|_ for details.

Example:

.. code-block::

  #: Validate values file
  data "jsonschema_validator" "values" {
    document = file("/path/to/document.json")
    schema = file("/path/to/schema.json")
  }

  #: Install a helm release with the validated json
  resource "helm_release" "service_overview" {
    values = [
      data.jsonschema_validator.values.validated,
    ]
  }

Development
===========

This repository follows structure of |terraform-provider-scaffolding|_ template
recommended by |terraform|_ developers (see |terraform-publishing-provider|_).

For publishing it uses Github Actions.

To force a new version to build, push a semantic tag to the repository.

Environment requirements:

- |go|_ 1.15 (to build the provider plugin)

Running tests:

.. code-block:: bash

  make testacc


.. |terraform| replace:: Terraform
.. _terraform: https://www.terraform.io/

.. |terraform-install-plugin| replace:: install a terraform plugin
.. _terraform-install-plugin: https://www.terraform.io/docs/plugins/basics.html#installing-a-plugin

.. |user-docs| replace:: User Documentation
.. _user-docs: https://registry.terraform.io/providers/xxxbobrxxx/jsonschema/latest/docs

.. |json-schema| replace:: json-schema
.. _json-schema: https://json-schema.org/

.. |terraform-provider-scaffolding| replace:: terraform-provider-scaffolding
.. _terraform-provider-scaffolding: https://github.com/hashicorp/terraform-provider-scaffolding

.. |terraform-publishing-provider| replace:: Publishing Providers
.. _terraform-publishing-provider: https://www.terraform.io/docs/registry/providers/publishing.html

.. |go| replace:: Go
.. _go: https://golang.org/doc/install
