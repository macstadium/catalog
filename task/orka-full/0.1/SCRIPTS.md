# Install & Configure `orka-full` with Scripts

For easier install and configuration of the `orka-full` `Task`, you can use the provided scripts.

## TL;DR;

### Install the task

```sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/install.sh && chmod 755 install.sh

NAMESPACE=<namespace> ORKA_API=<endpoint> ./install.sh --apply
```

### Store the Orka environment credentials

```sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/add-orka-creds.sh && chmod 755 add-orka-creds.sh

NAMESPACE=<namespace> EMAIL=<email> PASSWORD=<password> ./add-orka-creds.sh --apply
```

### Store the SSH credentials for the base image

```sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/add-ssh-creds.sh && chmod 755 add-ssh-creds.sh

NAMESPACE=<namespace> SSH_USERNAME=<username> SSH_PASSWORD=<password> ./add-ssh-creds.sh --apply
```

## Install the task

Before you can use this `Task` in Tekton pipelines, you need to install it and the Orka configuration in your Kubernetes cluster.

### Get install.sh

```sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/install.sh && chmod 755 install.sh
```

### Default namespace installation

To install in your Kubernetes cluster's `default` namespace, run the following command against your actual Orka API endpoint.

```sh
ORKA_API=http://10.221.188.100 ./install.sh --apply
```

To uninstall from the `default` namespace, run the script with the `-d` or `--delete` flag:

```sh
./install.sh --delete
```

### Custom namespace installation**

To install in a custom namespace, run the following command against your preferred namespace and your actual Orka API endpoint:

```sh
NAMESPACE=tekton-orka ORKA_API=http://10.221.188.100 ./install.sh --apply
```

To uninstall from a selected namespace, run the script with the `-d` or `--delete` flag against the namespace:

```sh
NAMESPACE=tekton-orka ./install.sh --delete
```

## Storing your credentials

The provided `Task` looks for two Kubernetes secrets that store your credentials: `orka-creds` for the Orka user and `orka-ssh-creds` for the SSH credentials.
  * `orka-creds` has the following keys: `email` and `password`
  * `orka-ssh-creds` has the following keys: `username` and `password`

You need to create Kubernetes secrets to store the Orka user credentials and the base image's SSH credentials.

### Get the credentials scripts

```sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/add-orka-creds.sh && chmod 755 add-orka-creds.sh
curl -LO https://raw.githubusercontent.com/tektoncd/catalog/master/task/orka-full/0.1/add-ssh-creds.sh && chmod 755 add-ssh-creds.sh
```

### Store in the default namespace

To create a Kubernetes secret in the `default` namespace of your cluster, run the following commands:

```sh
EMAIL=<email> PASSWORD=<password> ./add-orka-creds.sh --apply
SSH_USERNAME=<username> SSH_PASSWORD=<password> ./add-ssh-creds.sh --apply
```

To remove the secrets from the `default` namespace, run:

```sh
./add-orka-creds.sh --delete
./add-ssh-creds.sh --delete
```

### Store in a custom namespace

To create a Kubernetes secret in a custom namespace, run the following commands against your preferred namespace:

```sh
NAMESPACE=tekton-orka EMAIL=<email> PASSWORD=<password> ./add-orka-creds.sh --apply
NAMESPACE=tekton-orka SSH_USERNAME=<username> SSH_PASSWORD=<password> ./add-ssh-creds.sh --apply
```

To remove the secrets from the custom specify, run the following commands against the namespace:

```sh
NAMESPACE=tekton-orka ./add-orka-creds.sh --delete
NAMESPACE=tekton-orka ./add-ssh-creds.sh --delete
```