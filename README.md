# Vagrant-based JIRA and MySQL Deployment

## The Purpose

You need to do some development work with JIRA, but you don't have the time or patience to install JIRA by hand. 
This is where the JIRA-MySQL Vagrantfile comes in handy. 

## System Requirements

* Vagrant
* VirtualBox

## Usage

Since this is a git repo, it's best to pull it down via git:

```git clone https://github.com/jelyman2/vagrant-jira-mysql && vagrant up```

I've tested this deployment on both Windows and OS X. I expect Linux to be the same.

## The Ingredient List

The Vagrantfile included in this repo will:

- Download Atlassian JIRA `6.4.10 x64` for Linux (`.bin`)
- Install MySQL the latest branch of MySQL attached to the `mysql-server` tag in the pre-configured repo list.
- Auto-install JIRA using a varfile. Said file is included.

## The Technical Stuff

- JIRA: version `6.4.10 x64`
- MySQL: Latest
- Ports (internal/external): `8080:8080`
- The manual step of installing the JDBC driver for MySQL is included.
- Added VIM, curl, and some python to the mix to be safe.
- RAM: `2GB`

## Noteworthy

There is an issue surrounding Apache not starting up fast enough after the inital installation is complete which may cause the Vagrant output to display an error. This won't matter too much as we manually stop and re-start JIRA after copying over the MySQL driver.
If you find yourself not being able to get past that issue, file an issue in this repo and I'll take a look. 

I tried this setup with `1GB` and `1.5GB` allotments and there wasn't enough ram for Tomcat to run properly. 2GB seems to work well enough for 2000 issues across a half-dozen projects. Your mileage may vary.

## License

The MIT license is in effect here. Do with this repo whatever you wish. Fork the hell out of it and make it awesome!
