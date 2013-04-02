# Short Description
This repo will collect ideas and examples on how structure your configuration management code to avoid forks from happening.

> " Stop the Fork, before it eats you "

# Longer Description
Unlike your parents telling you to use a fork for better manners, in software you should avoid it!

Now that infrastructure is code, we can start sharing our code on sites like github.
Far too often we see for a specific cookbook/manifests that forks are happening.
This not only is a waste of energy as two people are working on the same problem.
Whenever you start your fork, your maintenance of that code will fall on you.

A good way to think is :

> " If I can't share it, I'm probably doing it wrong"

So let's document the reasons so we can argue with people and have them unlearn this habit!
Please consider adding your own thoughts, ideas whenever you feel like **forking**.

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

- User/group method: sometimes users/groups are created by another mechanism, so make creation optional
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
- Avoid parametrized classes just for passing configuration options globally for the manifest
- Favor definitions over Classes (multi-instance)
- Make sure to use the anchor-pattern if you do require on classes


## Chef

- Use Databags to get your configuration from
- Use Databags for users/password/etc..
- Check for Chef::Solo and make your search code work for solo too
- Use Search:Roles to configure hostname

Also see Peter Donald's post : Re-usable chef cookbooks <http://realityforge.org/code/2012/05/12/evolving-towards-cookbook-reusability-in-chef.html>
## CFEngine 3

- Use hard classes where possible (sys.fqhost, sys.ipv4, etc)
- Nest soft classes where you can to make inputs/bundles shorter yut still afford flexibility
- Declare variables as overridable where possible
- Pass paramaters to your usebundles as this decouples specifics from the bundle itself
- Run cf-serverd with appropriate security controls on all cf-agents
- Design your bundles to work with a upstream, production cf-serverd or with local, temporal cf-serverd

# Future

Ultimately I hope to detect the reasons with a tool similar to foodcritic or puppet-lint and point them out to people.
