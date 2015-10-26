NAME=asux/rails-phantomjs
VERSION=`git describe --tags`
CORE_VERSION=HEAD
PWD=`pwd`

all: version build tag_latest

version:
	git describe --tags

build:
	docker build -t $(NAME):$(VERSION) --rm .

tag_latest:
	docker tag -f $(NAME):$(VERSION) $(NAME):latest

push:
	docker push $(NAME)

pull:
	docker pull $(NAME)

run:
	docker run -P $(NAME)
