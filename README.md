Vision: To export configurations from a Cloudflare zone and import into another zone as part of IaC or in the event where or issue with the cloudflare admin console or etc.

Pre-requites/set up for the export process using cf-terraforming:

1. Ensure you have access to the Cloudflare accounts such as sandbox, UAT, production.
2. Install terraform.
3. Install the cf-terraforming command line utility from this link: https://github.com/cloudflare/cf-terraforming/releases
4. Create an API token with permissions granted in the zone, account and user. As best practice, create an API token for each different environment so that it is easier for troubleshooting purposes.
5. Ensure that the zone marked for export is an active zone as it will affect the cf-terraforming command.
6. Check the API key and Zone ID in the export/generate command belongs to the zone which you want to export configuration from.

Ensure that step 4 there is either Read or Edit permissions granted in the API token before moving on the step 5.
Below is a screenshot of all the permissions in the API token set up in order to run cf-terraforming.

Some of the resources that can be exported using cf-terraforming:
<html><body>
<!--StartFragment-->

Resource | Resource Scope
-- | --
cloudflare_access_application | Account
cloudflare_access_group | Account
cloudflare_access_identity_provider | Account
cloudflare_access_policy | Account
cloudflare_access_rule | Account
cloudflare_access_service_token | Account
cloudflare_account_member | Account
cloudflare_api_shield | Zone
cloudflare_argo | Zone
cloudflare_byo_ip_prefix | Account
cloudflare_certificate_pack | Zone
cloudflare_custom_hostname | Zone
cloudflare_custom_hostname_fallback_origin | Account
cloudflare_custom_pages | Account or Zone
cloudflare_custom_ssl | Zone
cloudflare_filter | Zone
cloudflare_firewall_rule | Zone
cloudflare_healthcheck | Zone
cloudflare_load_balancer | Zone
cloudflare_load_balancer_monitor | Account
cloudflare_load_balancer_pool | Account
cloudflare_logpush_job | Zone
cloudflare_origin_ca_certificate | Zone
cloudflare_page_rule | Zone
cloudflare_rate_limit | Zone
cloudflare_record | Zone
cloudflare_ruleset | Account or Zone
cloudflare_spectrum_application | Zone
cloudflare_tiered_cache | Zone
cloudflare_tunnel | Account
cloudflare_turnstile_widget | Account
cloudflare_url_normalization_settings | Zone
cloudflare_waf_override | Zone
cloudflare_waf_package | Zone
cloudflare_waiting_room | Zone
cloudflare_worker_route | Zone
cloudflare_workers_kv_namespace | Account
cloudflare_zone | Account
cloudflare_zone_lockdown | Zone
cloudflare_zone_settings_override | Zone

<!--EndFragment-->
</body>
</html>

The command below will help to create a .tf file which is the exported config file in the directory where terraform is installed.
sample export cf-terraforming to input in CMD:
cf-terraforming generate --email CLOUDFLARE_EMAIL --token CLOUDFLARE_API_TOKEN --zone cfzoneID -- resource-type "cloudflare_record" > [exporting-filename.tf](http://exporting-filename.tf/)

Sample .tf file output will look like this in notepad++


The following resources are not supported by terraform to generate or import configurations from CloudFlare:
<html><body>
<!--StartFragment-->

Resource | Resource Scope
-- | --
cloudflare_access_policy | Account
cloudflare_api_token | User
cloudflare_authenticated_origin_pulls | Zone
cloudflare_authenticated_origin_pulls_certificate | Zone
cloudflare_logpull_retention | Zone
cloudflare_logpush_ownership_challenge | Zone
cloudflare_magic_firewall_ruleset | Account
cloudflare_waf_group | Zone
cloudflare_waf_rule | Zone
cloudflare_worker_cron_trigger | Account
cloudflare_worker_script | Account
cloudflare_workers_kv | Account
cloudflare_zone_dnssec | Zone

<!--EndFragment-->
</body>
</html>


**Useful links:**

[[Troubleshooting · Cloudflare Fundamentals docs](https://developers.cloudflare.com/fundamentals/api/troubleshooting/)](https://developers.cloudflare.com/fundamentals/api/troubleshooting/)

[[Import Cloudflare resources · Cloudflare Terraform docs](https://developers.cloudflare.com/terraform/advanced-topics/import-cloudflare-resources/)](https://developers.cloudflare.com/terraform/advanced-topics/import-cloudflare-resources/)

[[GitHub - cloudflare/cf-terraforming: A command line utility to facilitate terraforming your existing Cloudflare resources.](https://github.com/cloudflare/cf-terraforming#supported-resources)](https://github.com/cloudflare/cf-terraforming#supported-resources)

https://developers.cloudflare.com/learning-paths/get-started/
