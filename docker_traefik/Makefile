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
up:
	@# Help: (dev) Run 
	@docker compose up -d

down:
	@# Help: (dev) Stop
	@docker compose down

restart:
	@# Help: (dev) Restart
	@docker compose restart

build:
	@# Help: (dev) Build
	@docker compose build

prune:
	@# Help: (dev) Complete cleanup
	@docker system prune -a --volumes

rebuild: down build up
	@# Help: (dev) Re-build

logs:
	@# Help: (dev) Show logs
	@docker compose logs -f

ps:
	@# Help: (dev) Show running containers
	@docker compose ps

rm:
	@# Help: (dev) Remove containers
	@docker compose rm

prod-up:
	@# Help: (prod) Run 
	@docker compose $(PRODCONF) up -d

prod-down:
	@# Help: (prod) Stop
	@docker compose $(PRODCONF) down

prod-restart:
	@# Help: (prod) Restart
	@docker compose $(PRODCONF) restart

prod-build:
	@# Help: (prod) Build
	@docker compose $(PRODCONF) build

prod-rebuild: down build up
	@# Help: (prod) Re-build

prod-logs:
	@# Help: (prod) Show logs
	@docker compose $(PRODCONF) logs -f

prod-ps:
	@# Help: (prod) Show running containers
	@docker compose $(PRODCONF) ps	