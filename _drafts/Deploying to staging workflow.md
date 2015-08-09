#Deploying to staging workflow

##Rules to deploy to staging:

a branch:

- can only be deploy if the current deployment is master or itself
- on branch approval, PR to merge, merge to master, and deploy master to staging

master:

- can be deployed always overwriting any branch
- cap staging deploy:check_branch before deployment
- if there is a branch, arrange with branch owner before deployment

##How to push a branch to staging for live testing

code working on my-branch

update repo

    git push origin my-branch

deploy to staging server (it takes 10 min aprox)

    BRANCH=my-branch cap staging deploy

Deployed commit reference can be displayed at route

    /version

##How to see remote logs

    cap staging logs:tail_rails
    cap staging logs:tail_thin

##How to connect to staging server

    ssh deployer@67.205.57.114

##Where are the logs

    /var/www/shk/current/log/staging.log
    /var/www/log/thin.log

##Where is the web app

    /var/www/shk/current

##Where is the thin configuration file

    /etc/thin/shk.yml

##How stop/start/restart shk thin server instance

Remotely

    cap staging deploy:restart

Or connecting to server

    ssh deployer@67.205.57.114
    thin restart -C /etc/thin/shk.yml

##How to know if there is some branch being tested in staging (and who did it)

    cap staging deploy:check_branch

        DEBUG [f48ca6b3] Command: cat /var/www/shk/current/BRANCH
        DEBUG [f48ca6b3]     master:alfredo
        DEBUG [f48ca6b3]    
        DEBUG [f48ca6b3] Finished in 0.299 seconds with exit status 0 (successful).

Deployed commit reference can be displayed at route

    /version