# Short Description
This repo will collect ideas and examples on how structure your configuration management code to avoid forks from happening.

      _________ __                  ___________.__             ___________           __    
       /   _____//  |_  ____ ______   \__    ___/|  |__   ____   \_   _____/__________|  | __
        \_____  \\   __\/  _ \\____ \    |    |   |  |  \_/ __ \   |    __)/  _ \_  __ \  |/ /
         /        \|  | (  <_> )  |_> >   |    |   |   Y  \  ___/   |     \(  <_> )  | \/    < 
         /_______  /|__|  \____/|   __/    |____|   |___|  /\___  >  \___  / \____/|__|  |__|_ \
                 \/             |__|                     \/     \/       \/                   \/

# Longer Description
Unlike your parents telling you to use a fork for better manners, in software you should avoid it!

Now that infrastructure is code, we can start sharing our code on sites like github.
Far too often we see for a specific cookbook/manifests that forks are happening.

So let's document the reasons so we can argue people and have them unlearn this habbit!
Please consider adding your own thoughts, ideas whenever you feel like **forking**.

Ultimately I hope to detect the reasons with a tool similar to foodcritic or puppet-lint and point them out to people.

# Excuses to fork
## Learning

- Experimenting/Learning: maybe the only valid argument for running your own fork. But it's cool to integrate your learnings in others people projects. Unless you are the first of course .

## Hardcoding

- Paths, directories: not everyone like /opt or /usr/local
- Version control: often people just assumes latest, it's useful to version the software that will be installed (not only packages, also github checksums)
- URL: make all urls configurable, period
- Users/Groups: not everyone likes the same username you're installing under
- Root use: don't install things with root priviliges if you don't need it
- Different Os: only 1 OS platform targets, solved by added cases
- Username/Password: not everyone like dummy passwords you provide

## Different methods

- Install method: provide people with different options for installation: source, package, download
- Download method: to get certain software, make it configurable : copy, download,
- Services methods: Not everyone may use upstart, daemontools, standard init.d scripts

## Structure

- Confusing names: avoid the use of 'Path' use InstallDir and InstallFile (avoid using Path as it confuses people)
- Single file structure: Follow an easy structure for your code: separate download,install,config,service 
- Undocumented attributes: document all used parameters, attributes in your README

## Templates

- Templates: not everyone likes your templates, provide as many options as you can but also allow global override (chef using cook_book flag for templates, puppet using override param)

## Web virtualhosts

- Virtual hosts: avoid claiming default virtualhost, don't assume port 80
- Type of webserver: not everyone uses apache but maybe nginx

## Network/Connectivity

- Proxy: not everyone can download directly from the internet
- Binding: don't assume 0.0.0.0 or 127.0.0.1 make the IP address the service binds on configurable

## Other

- Multiple instances: sometimes you want to install the same software multiple times on the same OS

## Security

- SSL not used: not everyone toys with security , support SSL where possible
- Security ports: make sure they are documented
- Authenticate vs Anonymous:

# Thoughts/Suggestions

## Generic

- Use a 'infracode'-bundler tool like librarian-chef, berkshelf, librarian-puppet
- Make sure your code passes one of the lint tools: puppet-lint, food-critic
- Put a Rakefile in your project
- Put a Vagrant file in your project
- Provide tests for your code
- Fail if the code run if it is run on a non supported OS
- Standardize naming of things like http_port

## Puppet

- Use hiera to seperate configuration from code
- Avoid parametrized classes
- Favor definitions over Classes (multi-instance)

## Chef

- Use Databags to get your configuration from
- Use Databags for users/password/etc..
- Check for Chef::Solo and make your search code work for solo too
- Use Search:Roles to configure hostname
