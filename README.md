# website for movement spaces network

## Contributing

For now, we're going to make changes directly on the WordPress server through the admin. But, eventually we would like changes made on Github to be automatically deployed to the server, so any changes made on the current server are just temporary.

Let's aim for next week to start adding data to the site to give plenty time to explore different plugins.

Please add any TODOs to the Issues in the issues tab.

## Github tips

Cassie and Libby made a Github workshop for AMC earlier this year -- if you want a safe place to mess around, that repository is a good place!  [Read the slides](https://slides.com/emhoracek/collaboration-with-github-and-git) and make issues, edits/commits, and pull requests on the [repo](https://github.com/amc-workshop/amc-workshop.github.io). We also compiled a lot of learning resources in the readme.

## Repo structure

`site` contains WordPress files and settings. It uses [Bedrock](https://roots.io/bedrock/) as a base.

`trellis` contains settings for the server itself. It uses [Trellis](https://roots.io/trellis/).

## ** Everything after this point is a Work in Progress!! **

## Using Trellis

## For development on your local machine

 * Create `movementspacesnetwork.com` directory
 * Inside directory, `git clone git@github.com:positiondev/mxlinche.git`
 * Run `vagrant up`

## For deployment to AWS server

 * Create a `.vault_pass` file in the trellis directory and put the Vault password in it
 * Put SSH key in `.ssh` and add new sub-domain and keys to `.ssh/config`:
```
 Host msn-staging.positiondevapp.com
  ForwardAgent yes
```

 * Run `ansible-playbook server.yml -e env=staging`
 * Run `./bin/deploy.sh staging movementspacesnetwork.com`
