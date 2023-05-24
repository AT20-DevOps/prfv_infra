
#################
DevOps1
## Create the VM ci_server
cd vagrant
vagrant up
## Clone project
https://github.com/AT20-DevOps/AT_20_GRAPHQL_SERVICE.git
## Acces to VM via SSH
vagrant ssh ci_server

## Apply permissions changes
vagrant provision ci_server
