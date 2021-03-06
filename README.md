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

 * Create a `.vault_pass` file in the trellis directory and put the Vault password in it
 * Put SSH key in `.ssh` and add new sub-domain and keys to `.ssh/config`:
```
 Host grafnyc-staging.positiondevapp.com
  ForwardAgent yes
```

## For development on your local machine

 * Create a directory for development
 * Inside directory, `git clone git@github.com:positiondev/grafnyc.git`
 * Install the dependencies for Trellis: [instructions on root.io](https://roots.io/trellis/docs/installing-trellis/).
 * You'll also need passlib: `sudo pip install passlib`
 * Make sure you have a `.vault_pass` in the Trellis directory.
 * Run `vagrant up`
 * (If there's an error or you make changes, you may have to run `vagrant provision`.)

## For deployment to AWS server

 * Create a `.vault_pass` file in the trellis directory and put the Vault password in it
 * Put SSH key in `.ssh` and add new sub-domain and keys to `.ssh/config`:
```
 Host grafnyc-staging.positiondevapp.com
  ForwardAgent yes
```

* Back up the DB:
  * `ssh ubuntu@grafnyc-staging.positiondevapp.com`
  * If permissions are wrong: `chmod 600 aws-eb.pem`
  * `sudo su web` to become web user
  * `cd /srv/www/grafnyc.org/current`
  * `wp db export --add-drop-table`
  * Disconnect
  * `scp ubuntu@grafnyc-staging.positiondevapp.com:/srv/www/grafnyc.org/current/grafnyc_org_staging.sql .` 
   


 * Run `ansible-playbook server.yml -e env=staging`
 * Run `./bin/deploy.sh staging movementspacesnetwork.com`
