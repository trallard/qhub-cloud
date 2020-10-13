# QHub

Is a tool for initializing and maintaining the state of QHub
deployments on Digital Ocean, Amazon Web Services, and Google Cloud
Platform.

## Installation:

```bash
pip install qhub
```

## Configuration

QHub is entirely controlled from a configuration file. 

To generate a configuration file follow these instructions.

```
mkdir <repository-name>
cd <repository-name>
qhub init <platform-name> # platform-name can be do, aws or gcp.
```

This generates a configuration file. Now modify the configuration according to your needs.
See documentation on modifying your configuration file for all of the cloud providers: [Configuration File](https://github.com/Quansight/qhub/blob/master/docs/docs/aws/configuration.md) 

## Initializing the Provider Template

The exact naming of the configuration file is needed to trigger the CI
actions when the configuration is changed.

```bash
qhub render -c qhub-config.yaml -o ./ --force
```

After initialising the provider templates, follow the instructions in
docs on deploying the infrastructure at
`<repository-name>/docs/installation.md`. At this current moment some
bootstrapping is required before github-actions can manage the
infrastructure as code. All of these instructions are automated in
`scripts/00-guided-install.sh`. Note that you will need to set the
environment variables in `intallation.md` for this script to
succeed. You will be prompted several times for use actions such as
setting oauth provider and dns.

```bash
./scripts/00-guided-install.sh
```

## Terraform Module Dependencies

This project depends on the terraform modules repository:
https://github.com/Quansight/qhub-terraform-modules

## Architecture

The architecture diagrams for each cloud provider is in `architecture` folder.
To generate them, just run the following command:

```bash
python <diagram_file>.py
```

# License

QHub is BSD3 licensed


# Release

Creating a release:

1. Increment the version number in `qhub/VERSION`
2. Ensure that the version number in `qhub/VERSION` is used in pinning qhub in the github actions `qhub/template/{{ cookiecutter.repo_directory }}/.github/workflows/qhub-config.yaml`
