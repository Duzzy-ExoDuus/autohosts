# Auto Update Ad-blocking Hosts file on Linux and Mac

Automate the hosts file process with cronjobs.

### Purpose of Hosts Files
Hosts files will reroute unwanted traffic to a blackhole; routing to 0.0.0.0 or 127.0.0.1 (localhost; your PC) when a request is made to a URL on the blacklist.

Which means any traffic that would have left your system for that destination, is sent inward, to your localhost and then abandoned.

Despite what some may suggest, hosts files are not "1980s technology" and still very useful today, as an additional *layer* of security.

Hosts file are a useful redundancy when coupled with ad blockers like [uBlock Origin](https://github.com/gorhill/uBlock) and [uMatrix](https://github.com/gorhill/uMatrix) - while debugging or 'Temporarily Allow All on this Site' with [Noscript](https://noscript.net/) can open you up to underlying attacks or privacy intrusions.

If you have an up-to-date hosts file, the risk is severely lessened.

**Auto Hosts** will automate the setup process for maintaining an up to date hosts file, by:
 - Installing a weekly cronjob to pull a copy of [Steven Black's Host file](https://github.com/StevenBlack/hosts) (default is every Sunday at 7:22pm)
 - Appends Facebook trackers, Linkedin ads, Google fonts and other harvester sites that curated lists for whatever reason, have not added to their blacklists
 - Refreshes DNS to instantiate the re-routed changes (Mac Only)
 - If [Devdom](https://notabug.org/angela/devdom) is installed, append all local virtualhosts

## To Install
```bash
git clone https://github.com/angela-d/autohosts.git && sudo ./autohosts
```

The script will take care of the rest!

### Adjust the cron time
If your computer is not powered on when the cron is scheduled, you'll miss the update.  Ensure the cronjob is set for a time when you're most likely to have it on.  You can adjust it by running:
```bash
crontab -e
```
and modifying the dates to suit.

Cron legend:
```html
* * * * * = minute, hour, day of month, month
```
(`*` = *every*, so 5 straight stars is equal to every minute of every hour of every day and every month.. which you should never run while pulling 3rd party content!)

**Note:** Because this script has to modify `/etc/hosts` - it needs elevated privileges (running as root or a sudo user).  Scripts that require elevated privilenges should be read an analyzed so you know what's being done to your system!  Read the source code of this script (and any others requiring such permissions) before you install.

### Alternative uses with Hosts files
- If you're running DD-WRT, you can add a cron to pull a [hosts file for your entire network](https://github.com/angela-d/configs/blob/master/dd-wrt.md).

- Android users can utilize [DNS66](https://f-droid.org/en/packages/org.jak_linux.dns66/) for hosts-based adblocking on mobile devices, without needing a rooted device (useful for gaining back privacy and blocking analytics tracking from being sent all over the place)
