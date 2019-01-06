chmod:
	sudo chown -R ${USER}:www-data bootstrap/cache
	sudo chown -R ${USER}:www-data storage
	sudo chown -R ${USER}:users public
	sudo chmod -R 0777 storage
    sudo chmod -R 0777 public
    sudo chmod -R 0777 bootstrap/cache
	sudo chmod +x artisan
cupd:
	docker-compose run --rm php-cli composer update
cinst:
	docker-compose run --rm php-cli composer install
redis:
	docker-compose exec redis redis-cli
nodeinit:
	docker-compose run --rm node yarn install
noderun:
	docker-compose run --rm node yarn run dev
nodeprod:
	docker-compose run --rm node yarn run prod
nodehot:
	docker-compose run --rm node yarn run hot
nodelive:
	docker-compose run --rm node yarn run watch
cli:
	docker-compose exec php-cli bash
tink:
	docker-compose exec php-cli php artisan tinker
migrate:
	docker-compose run --rm php-cli php artisan migrate
test-migrate:
	docker-compose run --rm php-cli php artisan migrate --database testdb
queue:
	docker-compose exec php-cli php artisan queue:work --timeout=1000 --tries=3
init:
	chmod cinst migrate nodeinit

