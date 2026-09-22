# iOS Live Activities for Home Assistant

Home Assistant automations that show Samsung washer and dryer progress as iOS Live Activities.

Uses [LocalThings](https://github.com/mbillow/localthings) for appliance data and the Home Assistant iOS Companion App for Live Activity notifications.

## Features

* Current cycle stage
* Progress percentage
* Estimated time remaining
* Updates at 5% progress intervals
* Updates on stage changes
* Silent progress updates
* 100% / Done state when finished
* Automatically clears 15 minutes after completion

Files included:

```text id="2jxz8j"
samsung-washer.yaml
samsung-dryer.yaml
```

## Requirements

* Home Assistant
* Home Assistant Companion App for iOS
* iOS Live Activities enabled
* Samsung washer/dryer exposed through LocalThings

## Setup

Copy the relevant YAML into Home Assistant and replace:

```text id="5fxjxn"
notify.mobile_app_iphone
```

with your own entity IDs and iPhone notification service.

You can also change:

```yaml id="3fp4a4"
url: /lovelace/0
```

to point to your preferred dashboard.

## Update logic

```text id="b0v2fc"
Cycle starts
    ↓
Live Activity created

Stage changes
    ↓
Live Activity updated

Progress changes
    ↓
5% boundary?
 ├─ No → Ignore
 └─ Yes → Silent update

Cycle finishes
    ↓
Show 100% / Done
    ↓
Wait 15 minutes
    ↓
Clear Live Activity
```

ETA changes by themselves do not trigger an update. The latest ETA is included the next time a stage or 5% progress update occurs.

## Notes

Entity names and cycle stages may differ between Samsung models, so some adjustment may be required.

## License

See [LICENSE](LICENSE).
