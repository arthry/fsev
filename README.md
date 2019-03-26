## FSEV

Fsev is a OSX file event watcher and command triggerer under 50 lines.

### Installation

```
sudo curl https://raw.githubusercontent.com/arthry/fsev/master/fsev -o /usr/local/bin/fsev
sudo chmod +x /usr/local/bin/fsev
```

### Usage

```
$ fsev <command>
```

This will run the given command when a file change event occurs in the current directory or subdirectories. *Ctrl-C* to exit.

### Example

In a new directory:

```
$ fsev say something changed 
<open a new terminal tab>
$ mkdir -p test/dir/
$ touch test/dir/test.txt
$ rm -rf test/
```

### How it works
It does so by creating a temporary `plist` xml file that use `WatchPaths`, and loads it using `launchctl`. Command given is also extended to have a log file at with same uuid under `/tmp/`. Upon quit, plist gets unloaded, and both files are deleted. While consequent changes don't pop immediately, it might need few more seconds to catch up. 

### Troubleshooting

If you accidentaly close the terminal, current `plist` might remain loaded. First, find out /tmp/<id> log exists, remove it and make sure to unload plist by following command:

```
$ launchctl unload ~/Library/LaunchAgents/<id>.plist
```

### License
GPLv2
 
