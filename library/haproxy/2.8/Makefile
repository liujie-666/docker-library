# This file is generated by the template.

REGISTRY?=lcr.loongnix.cn
ORGANIZATION?=library
REPOSITORY?=haproxy
TAG?=2.8

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)


default: image

image:
	docker build \
		-t $(IMAGE) \
		-t $(IMAGE)-buster \
		.

push:
	docker push $(IMAGE)
	docker push $(IMAGE)-buster
