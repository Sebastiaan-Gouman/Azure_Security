# AzureGoat: Attacking and defending a vulnerable Azure instance

AzureGoat is a vulnerable by design infrastructure on Azure featuring the latest released OWASP Top 10 web application security risks (2021) and other misconfiguration based on services such as App Functions, CosmosDB, Storage Accounts, Automation and Identities. AzureGoat mimics real-world infrastructure but with added vulnerabilities. It features multiple escalation paths and is focused on a black-box approach.

## Why?

Mainly this is just because I love doing these kind of projects to learn more about cyber security and gaining some hands on experience. It's a great to learn, tinker around, and just do some stuff without having to pay for it, or risking breaking some real life stuff. Besides that I'm putting all of this on GitHub just to show that I did it, how I did it, and what obstacles I faced doing it. 

## Vulnerabilities

This project contains all significant vulnerabilities including the OWASP TOP 10 2021, and popular cloud misconfigurations. Currently, the project contains the following vulnerabilities/misconfigurations.

- XSS 
- SQL Injection
- Insecure Direct Object reference
- Server Side Request Forgery on App Function Environment
- Sensitive Data Exposure and Password Reset
- Storage Account Misconfigurations
- Identity Misconfigurations

## Getting started

This should have been very easy, like everything, it wasn't for me!
Unfortunatly I kept getting the following error:

`This region has quota of 0 instances for your subscription. Try selecting different region or SKU.`

I have never worked with TerraForm, but that wasn't the hard part here. Getting the Azure App Service plan to run took some time. In the end, this is how I got it to work:

1. Created a new resource group via the Azure GUI, named it `azuregoat_app` and set it's location to `West Europe`
2. In the Azure Cloud Shell: `git clone https://github.com/ine-labs/AzureGoat`
3. `cd AzureGoat` to get into the folder
4. Edit the TerraForm file with `nano main.tf`
5. Find all `eastus` instances and replace them with `westeurope` by using ALT+R and choosing the ^A (all) option
6. Save the file with CTRL+X
7. Run `terrafom init`
8. Run `terraform apply --auto-approve`

## Credits

All credits for this project go to [AzureGoat GitHub](https://github.com/ine-labs/AzureGoat/tree/master)