.DEFAULT_GOAL := list

PRODCONF = -f docker-compose.yml -f docker-compose.prod.yml

list:
	@printf "%-20s %s\n" "Target" "Description"
	@printf "%-20s %s\n" "------" "-----------"
	@make -pqR : 2>/dev/null \
			| awk -v RS= -F: '/^# File/,/^# Finished Make data base/ {if ($$1 !~ "^[#.]") {print $$1}}' \
			| sort \
			| egrep -v -e '^[^[:alnum:]]' -e '^$@$$' \
			| xargs -I _ sh -c 'printf "%-20s " _; make _ -nB | (grep -i "^# Help:" || echo "") | tail -1 | sed "s/^# Help: //g"'
inventory:
	@# Help: Show inventory
	@ansible-inventory --list -y

ping:
	@# Help: Ping servers
	@ansible all -m ping

uptime:
	@# Help: Ping servers
	@ ansible all -a "uptime"

install:
	@# Help: Install packages
	@ansible-playbook playbook.yml

galaxy:
	@# Help: Install roles and collections fron ansible galaxy
	@ansible-galaxy install -r requirements.yml


update:
	@# Help: Update packages
	@ansible-playbook update.yml