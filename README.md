# pre-commit-hook-ensure-sops
A pre-commit hook to ensures that files are sops encrypted.

Our main usage for SOPS is to directly encrypt Kubernetes Secrets. 
Out of this, this pre-commit hook has been developed. 

We SOPS-encrypt the K8s secrets with following settings: `unencrypted_regex: "^(apiVersion|metadata|kind|type)$"`.
This hook checks, whether the file has a top-level key called `sops:`.

## Example usage
Just add the following to your projects `.pre-commit-config.yaml`, to check whether all files that end in `.sops.yaml` are sops encrypted:

```yaml
# [...]
repos:
  # [...]
  - repo: https://github.com/Blueshoe/pre-commit-hook-ensure-sops
    rev: v1.0.0
    hooks:
      - id: forbid-unencrypted-sops
        # only run this hook on files with .sops.yaml extension (excluding the actual .sops.yaml file)
        files: .\.sops\.yaml$
```

Keep in mind, that the files to run it against need to be staged, i.e. run `git add .` (or something more specific) before running pre-commit.