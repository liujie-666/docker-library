  
REGISTRY        ?=lcr.loongnix.cn
ORGANIZATION    ?=kubeedge
REPOSITORY      ?=cloudcore
TAG             ?=v1.31.1
LATEST		?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest

default: image


image: 
	docker build \
                --build-arg http_proxy=$(http_proxy) \
                --build-arg https_proxy=$(https_proxy) \
                -t $(IMAGE) \
                .

push:
	docker push $(IMAGE)
	#latest image
	@if [ $(LATEST) = "true" ]; \
		then \
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi
