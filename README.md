
# env0 OPA Plugin

  

This env0 OPA Plugin will allow you to run `opa eval` on a bundle directory as a part of your custom flow. To use this plugin, you will need to use version 2 of `env0.yml`.

  

We are using OPA version `0.46.1`

  

## Inputs

  

The OPA plugin accepts the following inputs:

* path (required) - the path to your bundle directory (the root folder is your project's root folder)

* query (required) - a query to eval with `opa eval`

* flags - a string containing additional flags as one string


If you are used to using `--input` or `--data` you can bundle those into a bundle directory and use it. Read more about it [here](https://www.openpolicyagent.org/docs/latest/management-bundles/#bundle-build).


## Example Usage

  

In this example we will run `opa eval` with our own bundle file after the "Terraform Plan" step of a deploy. We will call that step "My Step Name":

```yaml
version: 2
deploy:
  steps:
    terraformPlan:
      after:
        - name: My Step Name # The name that will be presented in the UI for this step
          use: https://github.com/env0/env0-opa-plugin
          input:
            path: bundle-file-path
            flags: --fail --format=raw
            query: data.example.violation[x]

```

  

## Further Reading

You can read more about the `eval` command and the available flags [here](https://www.openpolicyagent.org/docs/latest/#2-try-opa-eval).
