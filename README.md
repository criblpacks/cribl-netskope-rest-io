# Cribl Netskope Rest Collector
----
## About this Pack

This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the pack's context, eliminating the need to connect it to globally defined Sources and Destinations. 

This Pack is designed to collect, process, and output Netskope Alert and Event data using the [Netskope V2 REST API](https://docs.netskope.com/en/using-the-rest-api-v2-dataexport-iterator-endpoints). 

The Pack includes optional Splunk output processing that maps data to Splunk sourcetypes compatible with the [Netskope Add-on for Splunk](https://splunkbase.splunk.com/app/3808).

## Deployment

* This pack is configured by default to use the Worker Group's *Default Destination*.
* To use the *Default Destination*: No changes are required. The pack will route the data to the destination currently set as the Default on the Worker Group.
* To use a different Destination: You must update the pack's routes to specify your desired Destination.
* For immediate functionality without requiring Pack route filter expression modifications, every bundled Source within this pack adds a hidden field: `__packsource`. This field allows for seamless routing based on the Pack source.

### Configure the Collectors
* Obtain a `Netskope API Base URL` and `API Token` from your Netskope Administrator and update the Pack variables with this information (see below for details).
* Perform a Commit and Deploy - this ensures that Preview works correctly. 
* Perform a **Run > Preview** of each Collector to verify that they work correctly.
* Schedule the Collectors and adjust the schedule as needed. 

### Configure Output Format

Each data type can be configured to output data in either normalized JSON or Splunk (`_raw` + Splunk fields) format. Enable *only one* format for each of the following pipelines:
* `netskope_alerts`
* `netskope_events`

### Configure your Destination/Update Pack Routes
To ensure proper data routing, you must make a choice: retain the current setting to use the Default Destination defined by your Worker Group, or define a new Destination directly inside this pack and adjust the pack's routes accordingly.

### Commit and Deploy
Once everything is configured, perform a Commit & Deploy to enable data collection.

#### Variables

The Pack has the following variables:
* `netskope_tenant_url`: The full base URL to your Netskope deployment.
* `netskope_api_token`: Your V2 API Token (*must* be a V2 token!)
* `netskope_alerts_index`: The "index" name that Netskope will use for tracking state. See [here](https://docs.netskope.com/en/using-the-rest-api-v2-dataexport-iterator-endpoints) for information. In general, this does not need to be changed.
* `netskope_events_index`: As above but for Events. 
* `netskope_default_splunk_index`: Default index for the Splunk output.

## Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.

## Release Notes

### Version 1.0.0
- Initial release

## Contributing to the Pack

To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.

## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).