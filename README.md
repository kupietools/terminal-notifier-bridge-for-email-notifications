# terminal-notifier-bridge-for-email-notifications
This is a MacOS BASH script designed to receive information from Thunderbird plugins such as Mailbox Alerts or FiltaQuilla's "Run Application" action and use it to display custom notifications for incoming emails. The notification can be clicked to open the email directly if a working message URI is provided. 

This may well work with other email programs or plugins, it doesn't particularly care where the information is coming from. However, warning: it has only been tested with the above and support for anything else (or any support at all) may not be available. 

Clicking the alerts will open the email directly in Thunderbird. If you can pass it a message URI for a message in another email program, that should work fine, too, subject to the above warning. 

I previously used this to receive calls from TB's Mailbox Alert plugin and display clickable alerts in Terminal-Notifier.app for MacOS <https://github.com/julienXX/terminal-notifier>. It should still work for that purpose, but the plugin hasn't been updated to work with TB 115 as of this writing.

This bridge can be used with FiltaQuilla's "Run Application" filter action by specifying the following line as the application for the action to run:
/path/to/terminalNotifierBridgeForThunderbird.sh,-j,@SUBJECT@,-u,@MESSAGEURI@,-s,@AUTHOR@,-d,@date@

Just so you are aware, this script creates an invisible folder called .terminalNotifierForThunderbird in your home directory, for purpose of tracking dupes and keeping a lockfile to prevent simultaneously executing more than once at a time. You can safely delete this folder at any time, although if you choose to prohibit duplicate notifications in the settings below, you will reset the duplicate tracking by deleting it and the next appearance of any subsequent notification will never register as a dupe.
