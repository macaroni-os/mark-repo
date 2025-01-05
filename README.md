<p align="center">
  <img src="https://github.com/macaroni-os/macaroni-site/blob/master/site/static/images/logo.png">
</p>

# **M**.**A**.**R**.**K**. Anise Repository

The **M**acaroni **A**utomated **R**epositories **K**it is the Stack
of all softwares used by Macaroni to maintain and to generate `kits` together
with the tools used by Macaroni to convert Portage metadata to *anise* specs.

This repository wants to manage the binary of the core software used in the MARK stack
and speed up installation for CD/CI pipeline.

## Bump new packages

In order to update the selected packages we use the `anise-portage-converter`
tool. You need to have the *reposcan* JSON files aligned to the seed/mark-kits copy on `kit-cache` directory.

The *reposcan* JSON files could be generated manually with this command:

```bash
$> mark-devkit kit clone --concurrency 30 --generate-reposcan-files --kit-cache-dir ./kit-cache --specfile packages/seeds/mark-kits/kits-versions/kits.yaml
```

or using the package `reposcan/meta-mark-xl` of the `mark-repo`. Obviously, in this case,
the package must be bumped to updates kits to last available commit.

When the `kit-cache` directory is ready to update *anise* specs runs:

```bash
$> anise-portage-converter generate --rules portage-converter/tools.yaml  --ignore-missing-deps \
   --to . --enable-stage4 --ignore-wrong-packages
```

