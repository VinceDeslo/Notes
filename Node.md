# Node

## NPM (Packages):

```bash
# Installing and updating
npm i -g npm@latest

# Get info about install
npm config list

# List packages
npm list
npm list -g # Global
npm list -g --depth=0

# Start project (creates package.json)
npm init

# Add/remove dependency
npm install  # install everything from package.json
npm install [name]
npm install [name@version]
npm uninstall [name]
npm install [name] --save-dev # development dependency

# Check for outdated packages (Wanted avoids code break)
npm outdated

# Update package
npm update [name]

# Finding packages
npm search [name]

# Managing the cache (in .npm)
ls ~/.npm
npm cache clean --force

# Auditing
npm audit # lists vulnerabilities
npm audit fix # applies recommended version patches
npm audit fix --force # applies fixes without considering breaks

# Aliases
npm i # install
npm i -g # install global
npm un # uninstall
npm up # updates
npm t # run tests
npm ls # list modules
npm ll # additional information (la also)
```

## NVM (version management):

```bash
nvm ls-remote # view versions available
nvm ls # view local versions
nvm install node # install latest version of node
nvm install v11.14.0 # install specific version of node
nvm use node # use most recent version
nvm use v11.14.0 # use specific version of node
```

## Node modules:

```bash
assert # Set of assertion tests
buffer # Handle binary data
child_process # to run a child proc
cluster # Split a Node process into multiple
crypto # Handle OpenSSL crypto functions
dgram # UDP datagram sockets implementation
dns # DNS lookups and name resolution
events # Event handling
fs # File system
http # Node behave as an HTTP server
https # Node bejave as an HTTPS server
net # server and client creation
os # info about operating system
path # handle file paths
querystring # handle URL querystrings
readline # Handle readable streams
stream # Handle streaming data
string_decoder # Decode buffer objects into strings
timers # Execution after a certain milliseconds count
tls # TLS and SSL protocol implementation
tty # Classes for a text terminal
url # parse URL strings
util # Access utility functions
v8 # info about V8 engine
vm # compile JS in virtual machine
zlib # file compression 
```