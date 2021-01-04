# hassio-cloudflareipupdater

Dynamic IP Updater for Cloudflare in Home Assistant

### This Home Assistant Addon

This addon allows you to update your Cloudflare DNS with your current public IP addess. All the magic happens in a shell script and it is run when the add-on is started. Once the add-on has decided if the IP has changed it will update (if needed) and then exit. Errors and successes are logged to the log. You should add a section to your automations in Home Assistant to run this add-on at your desired frequency.

### How to get an API key from Cloudflare

Log in to your account and then head to your account settings. At the top click on "API Tokens". Next click the blue "Create token" button in the API Tokens section.

When asked if you wish to use a template click on the blue "Use template" option next to "Edit Zone DNS". You will need to then select the zone you wish to update a subdomain of in the "Zone Resources" section (in the right most dropdown).

Scroll to the bottom and click "Continue to summary" then on the summary page click "Create token". You will then be shown the token, copy this and paste it in to your config. It will only be shown this one time.



### Configuration

The available configuration options are as follows (this is filled in with some example data):

```
{
    "zone": "yourdomain.com",
    "host": "sub.yourdomain.com",
    "api": "YourAPITokenFromCloudflare"
}
```

An example to add to your automations.yaml:

```
- id: cloudflare-updater
  alias: "IP Cloudflare Updater"
  trigger:
  - platform: time_pattern
    # This will match every 1 minutes
    minutes: '/1'
  action:
  - service: hassio.addon_restart
    data:
      addon: local_hassio_cloudflareipupdater
```