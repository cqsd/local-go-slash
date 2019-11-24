## local-go-slash
local link shortener

## Usage
```
$ slash -h
usage: go-slash [-h] [-f PATHS_FILE] {list,ls,add,rm,mv,run} ...

Local go/ server admin tool

optional arguments:
  -h, --help            show this help message and exit
  -f PATHS_FILE, --paths-file PATHS_FILE
                        specific sqlite db to list from

subcommands:
  {list,ls,add,rm,mv,run}
    list (ls)           List available links
    add                 Add a link
    rm                  Remove a link
    mv                  Rename a link
    run                 Run the server
```

#### Example: add a link and run
Clone this repository and add [`./slash`]('./slash') to your `PATH`. Create
the link db with `sqlite3 links.db < schema.sql`. Then add a link and run:

```
$ slash add tweet https://twitter.com
Added tweet --> https://twitter.com
$ slash run 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

Add an `/etc/hosts` entry (e.g., `127.0.0.1 go`). `http://go/tweet` will now
redirect to `https://twitter.com`.


#### Example OS X installation
Put this in `~/Library/LaunchAgents/`, replacing the necessary values
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.bovineReligion.agent</string>
    <key>LimitLoadToSessionType</key>
    <string>Aqua</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/python3</string>
        <string>/path/to/local-go-slash/slash</string>
        <string>-f</string>
        <string>/path/to/local-go-slash/links.db</string>
        <string>run</string>
        <string>80</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <dict>
        <key>Crashed</key>
        <false/>
    </dict>
</dict>
</plist>
```

Log out and in, or start it immediately `launchctl start
~/Library/LaunchAgents/whatever`.
