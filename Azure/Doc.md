# Doc

## Install Azure CLI
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli
`curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`
`az extension add --name azure-devops`

## Login

Generate Personal Access Token (User Settings -> Personal Access Tokens -> New Token)
`az devops login --organization https://dev.azure.com/assysteme/`

## CMake Generation
Generates cmake cache and files
`cmake -B .`

## Publishing
Publishes package defined by CMake-File to Azure Devops
`cmake --build . --target publish`

## Downloading
Downloads Artifact with given Version and Name
`az artifacts universal download --organization https://dev.azure.com/assysteme/ --project "Weinig" --scope project --feed test-feed --name test-package --version 0.0.1 --path TestPackage`