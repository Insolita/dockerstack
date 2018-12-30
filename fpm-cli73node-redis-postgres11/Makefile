chmod:
	sudo chown -R ${USER}:www-data bootstrap/cache
	sudo chown -R ${USER}:www-data storage
	sudo chmod +x artisan
cupd:
	docker-compose exec php-cli composer update
cinst:
	docker-compose exec php-cli composer install
redis:
	docker-compose exec redis redis-cli
nodeinit:
	docker-compose run node yarn install
noderun:
	docker-compose run node yarn run dev
nodeprod:
	docker-compose run node yarn run prod
nodehot:
	docker-compose run node yarn run hot
nodelive:
	docker-compose run node yarn run watch
cli:
	docker-compose exec php-cli bash
migrate:
	docker-compose exec php-cli php artisan migrate
init:
	chmod cinst migrate nodeinit