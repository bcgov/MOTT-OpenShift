# Uptime Monitoring
This helm chart is designed to quickly deploy/update an instance of Uptime-Kuma
More information can be found here: https://github.com/louislam/uptime-kuma

This helm chart also includes features such as
- Openshift oAuth Proxy so only people with access to the namespace can connect to admin pages (status pages are available to anyone)
- IP Filtering to Gov IP's by default
- Prometheus endpoint to

## Installation
### Helm Install
To install the first time using Helm
1. Copy this repo to your PC
1. Navigate to the `uptime-monitoring` folder in your CLI
1. Create a values.yaml file with the values you want to change from the defaults. You should set:
    - `fullNameOverride`
    - `nameOverride`
    - `namespace`
    - `route: host:`
1. Login to `oc` in your CLI
1. Confirm you are on the namespace you want to deploy to with `oc project`
1. To verify output before deploying you can run `helm template CUSTOM-monitoring -f ./values.yaml -f ./values-CUSTOM.yaml ./` (replacing CUSTOM)
1. Run `helm install CUSTOM-monitoring -f ./values.yaml -f ./values-CUSTOM.yaml ./` (replacing CUSTOM)

### Configuration
Once Uptime-Kuma is deployed to OpenShift, follow these steps to get started
1. Navigate to the route you created (Ensure you are on gov network)
1. Login using the oAuth Proxy using same credentials as you use to login to the namespace
1. Enter some credentials (temporary as we will disable after since we have oAuth enabled)
1. Click the drop down in the top left
1. Click `Settings`
1. Click `Security`
1. Click `Disable Auth`

Now you can setup monitors, notifications, etc. See the uptime-kuma documentation for more information.

### Helm Upgrades
Essentiall the same as the original install, except you run `helm upgrade` instead of `helm install`

# Sysdig Integration
Uptime Kuma has a `/metrics` endpoint which Sysdig can scrape.
Instead of having Uptime Kuma push notifications, you can set them up in Sysdig to limit the amount of places you have notifications.