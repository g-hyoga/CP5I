DBNAME:=cookpad
TESTDB:=cookpad_dev
ENV:=development

setup:
	go get github.com/rubenv/sql-migrate/...
	go get github.com/tools/godep
	godep get

build:
	godep go build -o cmd/main cmd/main.go

run:
	./cmd/main

test:
	godep go test -v ./... | grep --color=auto -A 3 -e FAIL || echo "PASS ALL TEST"

migrate/init:
	#sudo service mysql restart
	sudo mysql.server restart
	mysql -u root -h localhost --protocol tcp -e "create database \`$(DBNAME)\`" -p

migrate/up:
	sql-migrate up -env="production"

migrate/down:
	sql-migrate down -env="production"

migrate/status:
	sql-migrate status

post/test:
	curl -X POST localhost:8080/api/recipe -H "Content-Type: application/json" -d "@public/sample.json"
	curl -X POST localhost:8080/api/recipe -H "Content-Type: application/json" -d "@public/sample2.json"
	curl -X POST localhost:8080/api/recipe -H "Content-Type: application/json" -d "@public/sample3.json"

post:
	curl -X POST http://noticeweb.net/api/recipe -H "Content-Type: application/json" -d "@public/sample2.json"
	curl -X POST http://noticeweb.net/api/recipe -H "Content-Type: application/json" -d "@public/sample3.json"
	curl -X POST http://noticeweb.net/api/recipe -H "Content-Type: application/json" -d "@public/sample4.json"
	curl -X POST http://noticeweb.net/api/recipe -H "Content-Type: application/json" -d "@public/sample5.json"
	curl -X POST http://noticeweb.net/api/recipe -H "Content-Type: application/json" -d "@public/sample6.json"
