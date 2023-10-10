# terminal-notifier-bridge-for-thunderbird

This is a MacOS BASH script designed to receive information from Thunderbird plugins such as Mailbox Alert <https://addons.thunderbird.net/en-US/thunderbird/addon/mailbox-alert/> or FiltaQuilla's "Run Application" action <https://addons.thunderbird.net/de/thunderbird/addon/filtaquilla/> and use it to display custom clickable alerts for incoming emails using Terminal-Notifier.app <https://github.com/julienXX/terminal-notifier>.

The notification this creates can be clicked to open the email directly if a working message URI is provided, which, if you follow these instructions, it should be. 

I previously used this to receive calls from TB's Mailbox Alert plugin. It should still work for that purpose, but that plugin hasn't been updated to work with TB 115 as of this writing.

This bridge can be used with FiltaQuilla's "Run Application" filter action by specifying the following line as the application for the action to run:
`/path/to/terminalNotifierBridgeForThunderbird.sh,-j,@SUBJECT@,-u,@MESSAGEURI@,-s,@AUTHOR@,-d,@date@`

# Requirements

To install, you will first need to download Terminal-Notifier.app from the above link, then you will need simply download this script, fill in the variables in the "USER CONFIGURATION" section to point it to your copies of Terminal-Notifier and Thunderbird. Then either create your alert in Mailbox Alert, or set up a "Run Application" filter action in FiltaQuilla as described above.

Due to MacOS's totally fun and not at all overly cumbersome security requirements, you may need to set the script as unquarantined and executable before you can run it. On MacOS X 10.14.6, you can do that by opening Terminal.app and typing the following commands, filling in your correct local path to the script:

```
xattr -d com.apple.quarantine /path/to/terminalNotifierBridgeForThunderbird.sh 
chmod +x /path/to/terminalNotifierBridgeForThunderbird.sh 
```
If you're on a different version of MacOS, you may need to find the commands for your particular system.

You will also need to set up your system to allow notifications from Terminal-Notifier. I have assumed some competency on your part in these instructions, if any of this is unclear you maybe aren't at a level where you should be messing with this kind of customization. 

# Compatibility

Only tested on Thunderbird, with Mailbox Alert prior to TB v115 and FiltaQuilla since then. This script may possibly work with, either directly or with minor modifications, with other email programs or plugins besides Thunderbird, as for most of what it does it doesn't particularly care where the information is coming from. However, warning: it has only been tested with the above, and support for anything else (or any support at all) may not be available.

# FYI

Just so you are aware, this script creates an invisible folder called `.terminalNotifierForThunderbird` in your home directory, for purpose of tracking dupes and keeping a lockfile to prevent simultaneously trying to execute more than one instance of Terminal-Notifier at a time. You can safely delete this folder at any time, although if you choose to prohibit duplicate notifications in the settings below, deleting it will reset the duplicate tracking and the next appearance of any subsequent notification will never register as a dupe. The folder will be recreated every time the script runs. 
