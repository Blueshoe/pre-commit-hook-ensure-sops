# pre-commit-hook-ensure-sops
A pre-commit hook to ensures that files are sops encrypted.

Our main usage for SOPS is to directly encrypt Kubernetes Secrets. 
Out of this, this pre-commit hook has been developed. 

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
        # only run this hook on files with .sops.yaml extension
        files: \.sops\.yaml$
```